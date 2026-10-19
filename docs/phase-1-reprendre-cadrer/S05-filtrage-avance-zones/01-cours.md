# Cours – Filtrage avancé et zones réseau

*BTS SIO SISR 2e année – Bloc 3 – S05*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

En première année, tu as vu qu'un pare-feu refuse par défaut. Cette séance va plus loin : **découper le réseau en zones**, décider **quels flux** passent d'une zone à l'autre, l'écrire en règles, puis **prouver** qu'elles font ce qu'on croit.

---

## 1. Pourquoi des zones ?

Un réseau « à plat » (tout le monde voit tout) transforme **un poste compromis** en **point d'entrée vers tout le reste** (voir le scénario S1 de la séance S02). On découpe donc en **zones** de confiance différente :

| Zone | Contenu | Confiance |
|---|---|---|
| **Utilisateurs (LAN)** | Postes des salariés | Moyenne : un poste peut être infecté |
| **DMZ** (zone démilitarisée) | Serveurs **exposés** à Internet (web, relais de messagerie) | Faible : ils sont attaqués en premier |
| **Serveurs internes** | Fichiers, annuaire, bases de données | Haute |
| **Administration** | Postes et outils d'administration | Haute, très restreinte |
| **Internet** | Le reste du monde | Aucune |

Règle d'or : **un flux n'existe que s'il est écrit.** Une compromission d'une zone doit se **limiter à cette zone**.

---

## 2. La matrice de flux

Avant d'écrire une règle, on écrit la **matrice de flux** : qui peut joindre qui, sur quel service, pour quelle raison.

| Source ↓ / Destination → | LAN | DMZ | Internet |
|---|---|---|---|
| **LAN** | — | web (80, 443) ; administration (22) depuis le poste d'administration | web (80, 443), DNS (53) |
| **DMZ** | **rien** | — | mises à jour (443), DNS (53) |
| **Internet** | **rien** | HTTPS (443) | — |

On la lit **ligne par ligne** : chaque case non vide devient une ou plusieurs règles ; **chaque case vide devient un refus**. Elle est aussi un **document à joindre au dossier** : elle montre ce qui est autorisé, et pourquoi.

> [!WARNING]
> **Le flux « de la DMZ vers le LAN » est le plus dangereux à ouvrir.** Un serveur de la DMZ compromis qui peut joindre le réseau interne annule l'intérêt de la DMZ. Si un serveur de la DMZ doit joindre une base de données interne, on ouvre **un seul flux précis** (une adresse, un port), jamais un réseau entier.

---

## 3. Filtrer avec nftables

### La structure

```text
table inet filtre          # une table : un ensemble de chaînes (inet = IPv4 et IPv6)
  chain entrant            # une chaîne : un ensemble de règles, accrochée à un point du noyau
    type filter hook input priority 0; policy drop;    # point d'accroche et politique par défaut
    règle 1
    règle 2
```

| Point d'accroche (*hook*) | Paquets concernés |
|---|---|
| `input` | Destinés **au pare-feu lui-même** (son administration, son DNS…) |
| `forward` | Qui **traversent** le pare-feu, d'une zone à l'autre |
| `output` | Émis **par** le pare-feu |

Un pare-feu entre deux zones écrit surtout dans la chaîne **`forward`**. La **politique par défaut** (`policy drop`) s'applique à tout paquet qui ne correspond à aucune règle.

### Lire une règle

```text
iifname "fwlan" oifname "fwdmz" ip saddr 192.168.10.0/24 tcp dport { 80, 443 } accept
```

« Un paquet **entré** par `fwlan`, **sortant** par `fwdmz`, de source dans `192.168.10.0/24`, en TCP vers le port 80 ou 443 : **accepté**. »

- Les règles sont lues **dans l'ordre** ; la **première qui correspond** s'applique (pour un verdict comme `accept` ou `drop`).
- **Spécifique avant général.** Une règle large placée trop tôt masque les suivantes.
- `ct state established,related accept` (suivi de connexion) laisse passer **les réponses** aux connexions autorisées, au lieu d'ouvrir les ports dans les deux sens.
- `ct state invalid drop` jette les paquets incohérents.

### `drop` ou `reject` ?

| Verdict | Effet | Quand |
|---|---|---|
| `drop` | Le paquet est **jeté en silence** : l'émetteur attend puis abandonne | Vers Internet : on ne renseigne pas un attaquant |
| `reject` | Une **réponse de refus** est renvoyée : l'émetteur échoue tout de suite | À l'intérieur : plus pratique pour diagnostiquer |

### Journaliser et compter

```text
counter limit rate 5/minute log prefix "REFUS-TRANSIT "
```

- `counter` compte les paquets qui arrivent à cette règle : une **mesure** de ce qui est refusé.
- `log` écrit dans le journal du noyau ; la limite de débit (`limit rate`) évite qu'un attaquant **remplisse les journaux**.
- Une règle de journalisation placée **en dernier**, avant la politique par défaut, enregistre **ce qui a été refusé** : la matière première de la détection (S11).

### Ce qui ne se filtre pas bien avec des règles seules

Un filtrage par **adresses et ports** ne voit pas le **contenu**. Il n'empêche pas un message piégé de passer par un port 443 autorisé. Il **cloisonne** et **réduit la surface d'attaque** ; il ne remplace ni l'antivirus, ni la détection d'intrusion, ni les correctifs.

---

## 4. Vérifier : un filtrage non testé est une hypothèse

Pour chaque case de la matrice, on teste **deux choses** : ce qui **doit passer** passe, et ce qui **doit être refusé** l'est.

| Test | Outil |
|---|---|
| Un service web répond | `curl` |
| Un port TCP est ouvert ou fermé | `nc -z` (netcat) |
| Les règles sont chargées | `nft list ruleset` |
| Combien de paquets ont été refusés | les **compteurs** des règles |

> [!NOTE]
> **Un test négatif vaut un test positif.** « Je peux joindre le serveur web » ne prouve rien sur la sécurité ; « je ne peux **pas** joindre le port 22 depuis Internet » oui.

**Test flash.** Une règle `iifname "fwext" oifname "fwdmz" tcp dport 443 accept` est écrite **après** `iifname "fwext" accept`. Que se passe-t-il ?

<details markdown="1">
<summary>Voir la réponse</summary>

La règle large `iifname "fwext" accept`, lue **la première**, accepte **tout** ce qui vient d'Internet : la règle précise ne sert plus à rien, et le pare-feu est **ouvert**. Il faut toujours placer le **précis** avant le **général**, et éviter de telles règles larges.

</details>
