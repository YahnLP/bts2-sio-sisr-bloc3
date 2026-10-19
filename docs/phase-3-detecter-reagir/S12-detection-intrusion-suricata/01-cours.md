# Cours – Détection d'intrusion : règles, réglage et faux positifs

*BTS SIO SISR 2e année – Bloc 3 – S12*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

La séance S11 a appris à **rassembler** les journaux. Une sonde de détection d'intrusion ajoute une source : elle **observe le trafic réseau** et signale ce qui ressemble à une attaque. Le sujet de la séance n'est pas « installer la sonde » mais **la rendre utile** : une sonde qui crie à tout propos est éteinte au bout d'une semaine.

---

## 1. Ce que fait une sonde

| | IDS (détection) | IPS (prévention) |
|---|---|---|
| **Position** | Observe une **copie** du trafic (miroir, écoute) | Placée **en coupure** : le trafic la traverse |
| **Action** | **Alerte** | Alerte **et bloque** |
| **Risque** | Rien ne casse, mais l'attaque passe | Un **faux positif** coupe un trafic légitime |
| **Cas d'usage** | Commencer, apprendre, mesurer | Quand les règles sont **mûres** et la disponibilité maîtrisée |

> [!NOTE]
> On **commence par détecter**. Passer en blocage sans avoir réglé les règles revient à laisser un détecteur de fumée décider de couper l'électricité de l'immeuble.

### Où la placer

| Emplacement | Voit | Limite |
|---|---|---|
| **Entre Internet et le pare-feu** | Tout ce qui arrive, y compris ce que le pare-feu bloque | Beaucoup de bruit |
| **Derrière le pare-feu, devant la DMZ** | Ce qui a **passé** le filtrage vers les serveurs exposés (séance S05) | Ne voit pas le trafic interne |
| **Sur le réseau interne** | Les déplacements d'un attaquant déjà entré | Demande des miroirs sur les commutateurs |

### Ce qu'une sonde ne voit pas

- Le trafic **chiffré** (HTTPS) : elle voit les adresses, les volumes, certains éléments de la négociation TLS, pas le contenu des requêtes web. Une sonde réseau est **aveugle** à une injection envoyée en HTTPS, sauf à déchiffrer en amont (ce que fait, par exemple, un reverse proxy, séance S08) ;
- Ce qui ne passe **pas** devant elle (un autre segment, une clé USB) ;
- Les attaques **sans motif réseau** reconnaissable.

---

## 2. Deux façons de détecter

| | Par **signature** | Par **comportement** |
|---|---|---|
| **Principe** | « Cette chaîne ou ce motif est connu comme malveillant » | « Cette activité est inhabituelle » (volume, fréquence, horaire) |
| **Forces** | Précis, explicable | Peut repérer ce qui est **nouveau** |
| **Faiblesses** | Rate ce qui est **inconnu** ou légèrement modifié | Beaucoup de **faux positifs** |

Les deux se combinent. Dans ce TP : des **signatures** (outil `sqlmap`, remontée de répertoire, injection SQL) et une règle de **seuil** (balayage de ports).

---

## 3. Lire une règle Suricata

```text
alert http any any -> $HOME_NET any (msg:"LAB outil sqlmap (User-Agent)"; http.user_agent; content:"sqlmap"; nocase; classtype:web-application-attack; sid:1000001; rev:1;)
```

| Partie | Sens |
|---|---|
| `alert` | Action : alerter (`drop` bloquerait, en mode prévention) |
| `http` | Protocole analysé |
| `any any -> $HOME_NET any` | De n'importe quelle source vers **mon** réseau, n'importe quel port |
| `msg` | Texte de l'alerte |
| `http.user_agent;` | **Où** chercher : ici l'en-tête `User-Agent` |
| `content:"sqlmap"; nocase;` | **Quoi** chercher, sans tenir compte de la casse |
| `classtype` | Catégorie, qui donne la **priorité** |
| `sid` | Identifiant unique de la règle (les règles **locales** utilisent des numéros à partir de 1 000 000) |
| `rev` | Révision : on l'incrémente à chaque modification |

> [!WARNING]
> **Où chercher compte autant que quoi chercher.** Le tampon `http.uri` est l'adresse **normalisée** : le moteur y a déjà nettoyé les `../`. Pour voir une tentative de remontée de répertoire, il faut le tampon **brut**, `http.uri.raw`. Une règle écrite sur le mauvais tampon **ne se déclenche jamais**, et rien ne l'indique : on la **teste** toujours avec une attaque réelle de laboratoire.

### Règles de seuil

```text
alert tcp any any -> $HOME_NET any (msg:"LAB balayage de ports"; flags:S; threshold:type both, track by_src, count 20, seconds 5; sid:1000003; rev:1;)
```

`flags:S` : paquets de demande de connexion. `threshold` : n'alerter que si **20** demandes depuis la même source en **5 secondes**, et **une seule fois** (`type both`).

---

## 4. Le réglage : vrai ou faux, positif ou négatif

| | Il y a une attaque | Il n'y a pas d'attaque |
|---|---|---|
| **La sonde alerte** | **Vrai positif** : c'est le but | **Faux positif** : du bruit |
| **La sonde se tait** | **Faux négatif** : l'attaque **manquée**, le plus dangereux | **Vrai négatif** : normal |

Les deux erreurs s'**opposent** : élargir une règle réduit les attaques manquées mais augmente le bruit ; la resserrer fait l'inverse.

### Les leviers de réglage

| Levier | Exemple |
|---|---|
| **Préciser** la règle | Chercher `union` **suivi de** `select`, plutôt que le seul mot `select` (qui se trouve dans des adresses légitimes) |
| **Choisir le bon tampon** | `http.uri.raw` plutôt que `http.uri` pour les remontées de répertoire |
| **Seuiller** | N'alerter qu'après N événements |
| **Supprimer pour une source connue** | Une liste d'exceptions (`threshold.config`) pour le **scanneur interne** de la séance S13 : il fait exactement ce que les règles surveillent |
| **Désactiver** | Une règle qui ne concerne aucun service de l'organisation |

> [!NOTE]
> Une **exception** est une **décision de sécurité** : elle se documente (qui, quoi, pourquoi, date de revue), comme les écarts de la séance S10. Une adresse exclue **par commodité** est une porte laissée ouverte.

### Des règles toutes faites

On ne réécrit pas tout. Des **jeux de règles publiés** (communautaires ou commerciaux) s'installent et se mettent à jour avec un outil dédié (pour Suricata, `suricata-update`). Mais ils sont écrits pour **tout le monde**, donc **bruyants** pour toi : le réglage reste ton travail.

---

## 5. Relier la sonde au reste

Une alerte isolée est une **piste**. Elle prend du sens avec les journaux de la séance S11 :

| Alerte de la sonde | Journaux à croiser |
|---|---|
| Balayage de ports depuis `203.0.113.50` | Échecs SSH depuis la même adresse (collecteur) |
| Injection SQL vers le serveur web | Journaux du **reverse proxy** et de l'application (séance S08) ; **code de réponse** : l'application a-t-elle répondu normalement ? |
| Alerte sur un poste interne | Journaux de l'annuaire à la même heure (séance S06) |

On envoie donc les alertes **vers le collecteur central** et on y **corrèle**.

**Test flash.** La sonde émet 400 alertes par jour. L'équipe en lit trois. Quelle est la bonne réaction ?

<details markdown="1">
<summary>Voir la réponse</summary>

**Régler**, pas ignorer et pas éteindre : trier les 400 alertes par règle, repérer les quelques règles qui produisent presque tout le bruit, les préciser ou documenter une exception, et recompter. Une sonde non lue est une sonde **inutile**, et les vraies alertes sont noyées dans le bruit.

</details>
