# Corrigé – S13 : Gestion des vulnérabilités

*Réservé à l'enseignant.*

## Vérification

Exécuté dans un laboratoire Ubuntu 24.04 de l'auteur (nmap 7.94, **Nikto 2.1.5**, nginx 1.24, OpenSSH 9.6 ; deux espaces de noms ​réseau) :

| Test | Résultat constaté |
|---|---|
| `nmap -sV -p 1-1000` | Ports **22** (OpenSSH 9.6p1 Ubuntu) et **80** (nginx 1.24.0 Ubuntu) |
| `nmap --script http-enum` | `/backup/ : Backup folder w/ directory listing` |
| `nmap --script ssh2-enum-algos` | Liste des algorithmes (dont `hmac-sha1` côté MAC) |
| `nikto` sur la cible initiale | Version du serveur ; **fuite des inodes via ETag** ; absence de `X-Frame-Options` ; `/backup/` : liste de répertoire |
| Après correction (suppression de `backup`, `autoindex off`, `server_tokens off`, deux en-têtes) | `/backup/` et la version ont **disparu** ; `X-Frame-Options` et `X-Content-Type-Options` **présents** ; **la fuite d'inodes par ETag subsiste** |
| ​Calculateur CVSS 3.1 de la partie C | `10.0`, `7.5`, `8.8`, `8.1`, `7.8`, `5.4`, `0.0` pour sept vecteurs connus : conforme aux notes publiques de ces vulnérabilités ; autres notes du TP : `9.8`, `8.1`, `7.8`, `4.2`, `5.3`, `6.1` |

**Non vérifié** : le TP avec **Debian 12** (testé sous Ubuntu 24.04) : la version de **Nikto** diffère (le paquet Debian est plus récent que la 2.1.5 utilisée ici, la **sortie change**), de même que ​celle de nmap ; les autres scripts de nmap ; les **scanneurs complets** (OpenVAS / Greenbone, Nessus) : **non installés** (bases à télécharger, installation lourde, réseau limité), seulement décrits dans le cours ; les **scores CVSS publiés** par la NVD pour les exemples cités : à contrôler sur la NVD, la note de base d'une CVE pouvant différer selon la source ; les ​notes du **tableau fictif** de la partie D : calculées avec l'outil, mais les vecteurs sont **inventés** pour l'exercice.

## Partie A

- Risque d'un scan non autorisé : **infraction** (S04), possible **perturbation** du service, **fausse alerte** déclenchée chez le responsable ou la sonde (S12), blocage de l'adresse.
- Les **horaires** évitent de perturber la production et permettent de **distinguer** le scan autorisé d'une attaque ; le **contact** permet d'arrêter vite en cas d'incident.

## Partie B

Constats attendus (au ​moins quatre) :

| Constat | Outil | Nature |
|---|---|---|
| Ports 22 et 80 ouverts, versions annoncées | `nmap -sV` | Exposition |
| `/backup/` : liste de répertoire | `http-enum`, `nikto` | **Configuration** |
| Version du serveur dans l'en-tête | `nikto` | Configuration |
| `X-Frame-Options` absent | `nikto` | Configuration |
| Fuite d'inodes par ETag | `nikto` | Configuration |
| Algorithme `hmac-sha1` proposé | `ssh2-enum-algos` | Configuration (à relativiser) |

Le ​constat **grave sans note** : la **sauvegarde de configuration lisible** (`/backup/config.bak`), qui contient un mot de passe. Un scanneur ne la note pas parce que ce n'est **pas une vulnérabilité de logiciel** (pas de CVE) mais une **erreur d'exploitation** : le scanneur la **signale** (liste de répertoire) sans en **lire le contenu** ni ​mesurer son importance. C'est l'humain qui qualifie.

## Partie C

Qualifications : 1. `7.5` **élevée** (lecture à distance sans compte, confidentialité seule) ; 2. `7.8` **élevée** (local, mais impact total) ; 3. `6.1` **moyenne** (interaction requise, impact limité mais portée changée).

Réponse à « quel critère fait le plus ​varier la note » : en général **AV** (réseau contre local), **PR** et les impacts C/I/A ; l'important est que l'élève le **constate** par essai.

## Partie D

| Id | Priorité | Action | Délai |
|---|---|---|---|
| V01 | **P1** | **Fermer** la redirection 3389 ; remplacer par un accès via VPN avec authentification forte (séances S06, S07) | 48 h |
| V03 | **P1** | **Changer** les identifiants du NAS, restreindre l'interface d'administration, **déconnecter** la ​copie du réseau (séance S10 / continuité) | 48 h |
| V04 | **P1** | **Désactiver** SMBv1 (réglage) après test des usages | 48 h |
| V02 | **P1** (actif de production, exploitée, **pas de correctif**) | **Isoler** dans une zone dédiée aux flux minimaux (S05), sans accès à Internet ; **planifier** la migration ; acceptation écrite du risque résiduel | 48 h pour l'isolement, migration à planifier |
| V05 | P2 | Mettre à jour le lecteur sur les 8 ​postes, déploiement par vagues | 2 semaines |
| V06 | P2 | Mise à jour du serveur (note ≥ 7 sur actif essentiel) | 2 semaines |
| V07 | P3 | Désactiver TLS 1.0 | 2 mois |
| V08 | P4 | Mettre à jour le micrologiciel à l'occasion | Au fil de l'eau |

L'ordre **V01 en premier**, puis V03 et V04, est à discuter : V01 est exposée à Internet. **V02** peut aussi être classée P2 par un élève qui ne retient pas « machines de production » comme actif essentiel : accepter si **argumenté**.

Réponses aux questions :

1. **V01 et V03** (9,8 ​chacune) : V01 est **exposée à Internet**, V03 n'est atteignable que depuis le réseau interne ; V03 vise cependant la **sauvegarde**, dernier recours contre un rançongiciel (S02). V01 passe donc en **premier**, V03 immédiatement après.
2. **V02** : **isoler** (S05), **compenser** (désactiver ce qui n'est pas nécessaire, interdire l'accès à Internet), **migrer** à terme, **accepter par écrit** le ​risque résiduel avec **date de revue** (S10).
3. **Oui** : une faille à 4,2 **exploitée activement** et exposée, ou sur l'actif le plus critique, passe avant une faille à 7,8 **sans exploit connu** et sur un poste non essentiel : la note mesure la gravité **technique**, pas l'urgence.
4. **Réglages immédiats et gratuits** : V01 (fermer la redirection), V03 (changer le mot de passe), V04 (désactiver SMBv1), V07 (désactiver TLS 1.0).

## Partie E

- E1 : `rm` supprime la **faille réelle** (le fichier lisible) : **indispensable**. `autoindex off` empêche de ​lister les répertoires : **indispensable** avec la suppression. `server_tokens off` cache la **version** : du **durcissement** (réduit les informations offertes, ne corrige rien). Les en-têtes `X-Frame-Options` (contre l'inclusion de la page dans un cadre, détournement de clic) et `X-Content-Type-Options` : **durcissement** (séance S08).
- E2 : `/backup/` corrigé (preuve : `http-enum` ne le liste plus) ; version **masquée** (`nmap -sV` affiche `nginx` sans numéro) ; en-têtes **présents** ; **fuite d'inodes par ETag subsiste** : décision au choix et argumentée (**corriger** avec la directive `etag off;`, **compenser**, ou **accepter** : risque faible, information peu ​exploitable). `etag off;` n'a pas été rejoué dans mon laboratoire : à tester.

## Partie F

F1 : P1 : 4 (V01, V02, V03, V04), P2 : 2 (V05, V06), P3 : 1 (V07), P4 : 1 (V08) ; réglages : 4 (V01, V03, V04, V07) ; sans correctif : 1 (V02). Pour la cible de laboratoire : avant, quatre à cinq constats ; après, un seul ​subsiste (selon le choix en E2).

F2 : critères de la note : **trois actions** concrètes et compréhensibles (fermer l'accès à distance, changer le mot de passe de la sauvegarde, isoler les PC sous Windows 7), **pas de sigle** non expliqué, ce qu'on **repousse** et pourquoi, **vérification** par un ​nouveau scan ; ton adapté à un dirigeant.

## Pièges fréquents

- **Trier par la note** seule.
- **Corriger sans prouver** : pas de nouveau scan.
- Oublier que le scanneur ne **qualifie pas** une erreur de configuration comme la sauvegarde exposée.
- Scanner **sans autorisation** ou hors périmètre.
- **Faux positifs** non vérifiés à la main.
- Laisser une faille sans ​correctif **sans mesure compensatoire** ni acceptation écrite.
