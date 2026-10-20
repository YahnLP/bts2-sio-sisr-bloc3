# Corrigé – S11 : Journaux centralisés

*Réservé à l'enseignant.*

## Vérification

Exécuté dans un laboratoire Ubuntu 24.04 de l'auteur (rsyslog 8.2312, espaces de noms réseau pour ​simuler les machines, `logger` pour les événements) :

| Test | Résultat constaté |
|---|---|
| `rsyslogd -N1` sur les deux fichiers de configuration | Syntaxe valide |
| Réception TCP 514 avec la configuration Debian/Ubuntu par défaut + `10-collecteur.conf` | Un dossier par machine (`srv1/sshd.log`, `srv1/sudo.log`), `echecs-connexion.log` créé ; les messages distants **n'apparaissent pas** dans `auth.log` local (effet du `stop`) |
| Dossier de stockage ​appartenant à `root` | `open error: Permission denied` : rien n'est écrit. Corrigé par `install -d -o syslog -g adm` |
| Deux sources, trois échecs chacune | Six lignes dans `echecs-connexion.log`, le message `Accepted` n'y figure pas |
| `correle.sh 5` / `correle.sh 10` | `ALERTE: 203.0.113.50 : 6 echecs sur 2 serveur(s)` / aucune alerte |
| Collecteur arrêté, un message envoyé, collecteur relancé | Le message arrive **après ​environ 30 secondes** (délai de reprise par défaut) |
| `logrotate -d` sur la configuration du TP | Aucune erreur (l'option est `notifempty`, pas `notempty`) ; rotation forcée vérifiée |

**Non vérifié** : le comportement sur **Debian** (testé sous ​Ubuntu) ; les vraies connexions SSH échouées (le TP les **simule** avec `logger`) ; la file d'attente **sur disque** après un redémarrage de la source (la directive est acceptée par `rsyslogd -N1`, mais son effet n'a pas été rejoué) ; `chrony` (non ​demandé) ; le script `rsyslog-rotate` en `postrotate` sur Debian (présent sous Ubuntu) ; Wazuh (décrit dans le cours, jamais installé).

## Partie A

- La ligne apparaît dans `auth.log` parce que la **catégorie** (`authpriv`) est celle de l'authentification : c'est la règle de ​routage de la configuration par défaut.
- **Qui** : l'utilisateur tenté (`test`) ; **quoi** : échec de mot de passe ; **quand** : l'horodatage ; **d'où** : l'adresse indiquée dans le message. Ce qui manque : le **résultat final** et l'**identité de la machine** si le journal est lu hors contexte (d'où l'intérêt du nom de machine ajouté par le collecteur).

## Partie B

- B1 : sans la bonne appartenance, `Permission denied` : rsyslog tourne sous `syslog`.
- B2 : réception (`imtcp`) ; modèle de chemin par machine et ​programme ; modèle de ligne d'alerte ; copie des échecs ; rangement du reste puis **arrêt** du traitement. `stop` évite que les messages **distants** se mélangent aux journaux **locaux** du collecteur.

## Partie C

- UDP est à écarter pour la sécurité : perte **silencieuse** possible. `resumeRetryCount="-1"` : réessayer sans limite ; `queue.*` : garder les messages en attente tant que le collecteur est injoignable ; `saveOnShutdown` : les ​sauver sur disque à l'arrêt.
- C2 : au moins **trois** fichiers par source (par programme) selon les événements envoyés, plus `echecs-connexion.log`. Le message `Accepted` est dans `srv1/sshd.log` mais **pas** dans `echecs-connexion.log`.

## Partie D

| Seuil | Alertes | Fausse alerte ? | Attaque manquée ? |
|---|---|---|---|
| 2 | `192.0.2.10` (2 échecs), `203.0.113.50`, `198.51.100.7` | **Oui** : `192.0.2.10`, une simple ​erreur de frappe | Non |
| 5 | `203.0.113.50` (6), `198.51.100.7` (8) | Non | Non |
| 10 | Aucune | Non | **Oui** : les deux attaques passent sous le seuil |

Seuil retenu : **5 dans ce jeu de données**, avec cette limite : un seuil **sans fenêtre de temps** compte les échecs de plusieurs jours et se déclenche pour un utilisateur oublieux. Une règle ​réelle compte sur une **fenêtre** (par exemple « 5 échecs en 10 minutes »). À un responsable qui veut « une alerte dès le premier échec » : des centaines d'alertes quotidiennes, ignorées en pratique (**fatigue d'alerte**).

**D3** : règle de séquence : il faut les événements d'échec **et** de succès, avec la **même adresse** et l'**ordre horaire** ; on la calcule sur le **collecteur** parce que seul lui voit **toutes** les machines (et suppose des ​horloges synchronisées).

## Partie E

- E1 : la ligne arrive après environ **30 secondes** de reprise une fois le collecteur relancé. Limite d'une file en mémoire : perdue si la **source** redémarre ; ​atténuée par `queue.filename` et `queue.saveOnShutdown`.
- E2 : la copie **centrale** conserve les événements d'avant l'effacement : preuve (S15). Un attaquant avisé **coupe l'envoi** (arrêt de l'agent, règle de pare-feu) **avant** d'effacer : d'où la surveillance de l'**absence** de journaux.
- E3 : en laboratoire, les horloges de machines virtuelles dérivent peu mais ne sont pas garanties. Sans heure commune, la ​chronologie de plusieurs machines est **faussée** ; installer `chrony` avec une source commune sur toutes.

## Partie F

- F1 : 180 jours de rotation quotidienne, soit **environ six mois**, le bas de la fourchette recommandée par la CNIL pour la journalisation ​courante (délibération n° 2021-122 du 14 octobre 2021). C'est un **choix** documenté, pas une obligation générale ; une durée plus longue demande de justifier le besoin.
- F2 : attendre sources (authentification, annuaire, pare-feu, services exposés), ​durée **justifiée**, accès restreint, **information** du personnel, surveillance de l'absence de journaux, synchronisation du temps, rappel des données personnelles.

## Pièges fréquents

- Dossier de stockage mal **possédé** : aucune écriture, aucun message d'erreur côté source.
- **UDP** par habitude.
- Seuil **sans ​fenêtre de temps**.
- Oublier que la centralisation ne protège que ce qui est **envoyé**.
- Journaliser des **mots de passe** par accident (par exemple saisis à la place de l'identifiant).
- Conserver « tout, pour toujours » ou, à l'inverse, **trop peu**.
