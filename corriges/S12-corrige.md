# Corrigé – S12 : Détection d'intrusion

*Réservé à l'enseignant.*

## Vérification

Exécuté dans un laboratoire Ubuntu 24.04 de l'auteur (**Suricata 7.0.3**, deux espaces de noms réseau reliés par un pont, la sonde écoutant le pont ; cible : serveur HTTP Python ; attaquant : `curl`, `nmap` 7.94) :

| Test | Résultat constaté |
|---|---|
| `suricata -T` avec le fichier de règles et `HOME_NET` | Configuration chargée |
| Action 1 (`sqlmap`) | Alerte `1000001` |
| Action 2 avec `http.uri` | **Aucune alerte**, alors que `eve.json` montre `/../../etc/passwd` |
| Action 2 avec `http.uri.raw` | Alerte `1000002` |
| Action 3 (légitime, `?select=rouge`) avec la règle large | **Faux positif** `1000004` |
| Actions 3 et 4 avec la règle `union` puis `select` | Pas d'alerte sur 3 ; alerte `1000005` sur 4 (y compris `+union+select+` et `UnIoN/**/SeLeCt`) |
| Action 5 (navigation normale) | Aucune alerte |
| Action 6 (`nmap -sS -p 1-200 -T4`) | Alerte `1000003` (une seule : `type both`) |
| Changement de `User-Agent` | Règle 1 muette ; règle 5 toujours déclenchée |
| `OR` booléen `' OR '1'='1` avec la règle 6 de la solution | Alerte `1000006` |
| `suppress` pour `10.40.0.10`, sid `1000005` | Plus d'alerte `1000005`, la règle 1 déclenche toujours |
| `imfile` sur `fast.log` | Les lignes d'alerte arrivent dans le journal du système sous l'étiquette `suricata` |

**Observation non expliquée** : lors de mes essais, **certaines premières requêtes d'une série n'ont pas été vues** (absentes d'`eve.json`) quand elles étaient envoyées dans la même seconde ; une série de six requêtes espacées a été vue **six fois sur six**, avec et sans désactivation du contrôle des sommes de contrôle (`-k none`). Je n'ai pas déterminé la cause. **Conseil** : attendre quelques secondes après `Engine started`, **rejouer** une action qui semble muette avant de conclure, et lire `eve.json` pour savoir si la sonde l'a **vue**.

**Non vérifié** : **Debian 12**, dont le paquet `suricata` est de la série **6.0** (testé en 7.0.3) : la syntaxe des tampons (`http.uri.raw`, `http.user_agent`) en 6.0 n'a pas pu être vérifiée (documentation de l'éditeur inaccessible depuis mon environnement) : à tester avant la séance ; le nom d'interface en machine virtuelle ; `suricata-update` et les jeux de règles publiés (réseau non disponible) ; le mode IPS ; l'effet de `distance:0` face à des charges plus complexes ; la règle 6 **non** rejouée **sans** la règle 5 (l'absence d'alerte sur le `OR` avant la règle 6 découle du contenu des règles et de l'essai avec `AND 1=1`, qui ne déclenche rien).

## Partie A

- Une **sonde en écoute** est un **IDS** (elle alerte, ne bloque pas). Placée derrière un reverse proxy qui **déchiffre** le HTTPS, elle voit le **contenu** des requêtes : oui, bien plus qu'en amont.
- Exemples de trafic non analysable : HTTPS sans déchiffrement, VPN, DNS chiffré, tout trafic qui ne passe pas devant la sonde.

## Partie C

| # | Alerte ? | Verdict |
|---|---|---|
| 1 | Oui, `1000001` | Vrai positif |
| 2 | **Non** (avant correction) | **Attaque manquée** : la règle cherche dans le mauvais tampon |
| 3 | Oui, `1000004` | **Faux positif** |
| 4 | Oui, `1000004` | Vrai positif |
| 5 | Non | Vrai négatif |
| 6 | Oui, `1000003` | Vrai positif |

L'adresse affichée par `jq` est `/../../etc/passwd` : la sonde **la voit**. La règle ne la reconnaît pas parce que `http.uri` est **normalisé** : à comparer avec `http.uri.raw`.

## Partie D

- D1 : après `http.uri.raw`, alerte `1000002`.
- D2 : `distance:0` : chercher `select` **après** `union`. Une adresse qui ne contient pas `union` ne correspond plus.
- D3 : la première (`OR`) est **manquée** (aucune règle ne la connaît), la seconde est **vue** par la règle 5 malgré l'obscurcissement par commentaires.
  **Règle 6 attendue** (exemple) :

  ```text
  alert http any any -> $HOME_NET any (msg:"LAB injection SQL (OR booleen)"; http.uri; content:"' or '"; nocase; classtype:web-application-attack; sid:1000006; rev:1;)
  ```

  Toute règle **testée** sur les actions 3 et 5 sans alerte, et qui déclenche sur le `OR`, est acceptée. Valeur d'une règle fondée sur le **nom de l'outil** : **faible** : l'attaquant change le `User-Agent` ; elle sert à repérer les attaquants **peu soigneux**, pas les autres.
- D4 : fiche d'exception : règle `1000005` ; adresse `10.40.0.10` (scanneur interne) ; raison : scans nocturnes planifiés ; responsable nommé ; date de revue. **Risque** : si `10.40.0.10` est compromis, ses injections SQL **ne sont plus signalées** par cette règle : seules les autres règles (comme `sqlmap`) restent actives. Il faut surveiller ailleurs (journaux, autres règles) et **limiter** l'exception (adresse précise, une règle).

## Partie E

- E1 : l'alerte arrive dans le dossier de la machine sous le nom du programme `suricata`.
- E2 : la **même adresse** fait du balayage puis essaie des mots de passe : **reconnaissance puis tentative d'accès**, donc **escalade** ; règle de corrélation : « même adresse dans une alerte de balayage **et** au moins N échecs de connexion dans les M minutes » ; à traiter en priorité haute.

## Partie F

Barème indicatif :

| Règle | Attendu |
|---|---|
| 1 | VP : 1 ; limite : contournable |
| 2 | Avant : 0 VP, 1 attaque manquée ; après : 1 VP |
| 4 large / 5 | Large : 1 VP, **1 FP** ; corrigée : 1 VP, 0 FP |
| 3 | 1 VP (alerte unique) |
| 6 | 1 VP sur le `OR`, 0 FP sur 3 et 5 |

**Passer en blocage** : une règle **précise**, sans faux positif constaté, dont le blocage ne coupe aucun usage légitime (par exemple la remontée de répertoire sur `http.uri.raw`) ; **garder en alerte** : le balayage de ports (un scanneur légitime existe), et toute règle large ou fondée sur un nom d'outil.

## Pièges fréquents

- **Mauvais tampon** : la règle ne se déclenche jamais et rien ne le signale.
- Mettre une règle **en blocage** avant de l'avoir réglée.
- Exception **trop large** (un réseau entier) ou **sans date de revue**.
- Conclure qu'une attaque n'a pas eu lieu parce que la sonde est **muette** (elle a pu ne pas la voir, ou ne pas la reconnaître).
- Oublier `-S` et se noyer sous des règles publiées, ou au contraire l'utiliser en production et **perdre** les règles publiées.
- Lancer une attaque **hors du laboratoire**.
