# Aide-mémoire – Durcissement, conformité et correctifs

*BTS SIO SISR 2e année – Bloc 3 – S10*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## La boucle de conformité

**Référence** → **audit** → **tri** → **correction ou écart accepté par écrit** → **nouvel audit**.

## Lynis

| Besoin | Commande |
|---|---|
| Installer | `sudo apt install -y lynis` |
| Auditer (local, sans modification) | `sudo lynis audit system --quick --no-colors` |
| Indice | `sudo grep '^hardening_index' /var/log/lynis-report.dat` |
| Avertissements | `sudo grep '^warning\[\]' /var/log/lynis-report.dat` |
| Suggestions | `sudo grep '^suggestion\[\]' /var/log/lynis-report.dat` |
| Détail d'un test | `sudo lynis show details IDENTIFIANT` |

`show details` lit le journal de l'audit : ne pas lancer l'audit avec `--no-log`.

## Lire un rapport

| Élément | À faire |
|---|---|
| Avertissement | Traiter en priorité |
| Suggestion | **Trier** : gravité, effort, effet de bord |
| Indice | Indicateur de suivi, **pas un objectif** ni une certification |
| Identifiant (`AUTH-9328`) | Suivre le point d'un audit à l'autre |

## Quelques corrections courantes

| Point | Fichier ou commande |
|---|---|
| Droits des nouveaux fichiers | `UMASK 027` dans `/etc/login.defs` (nouvelles sessions) |
| Âge des mots de passe | `PASS_MAX_DAYS`, `PASS_MIN_DAYS` dans `/etc/login.defs` (nouveaux comptes) ; `chage -M … -m … compte` pour un compte existant |
| Intégrité des paquets | `debsums -s` (n'affiche que les fichiers modifiés) |
| Versions à suivre | `apt-show-versions` |

## Registre des écarts acceptés

Identifiant · raison · risque accepté · mesure compensatoire · responsable · **date de revue**.

## Gestion des correctifs

| Étape | Rappel |
|---|---|
| 1 | Inventorier |
| 2 | Sources d'alerte (éditeur, CERT-FR, distribution) |
| 3 | Évaluer : concerné ? exposé ? exploité ? |
| 4 | Tester sur une machine pilote |
| 5 | Déployer par vagues, avec instantané ou sauvegarde |
| 6 | Vérifier (correctif actif, service fonctionnel, redémarrage du noyau si besoin) |
| 7 | Tracer |
| 8 | Prévoir le retour arrière |

| Commande (Debian) | Effet |
|---|---|
| `sudo apt update` | Met à jour la liste des paquets |
| `apt list --upgradable` | Liste les mises à jour, avec le dépôt d'origine |
| `sudo apt-get -s upgrade` | **Simule** sans rien installer |
| `sudo apt upgrade` | Applique |
| `[ -f /var/run/reboot-required ] && echo oui` | Un redémarrage est-il demandé ? |

## Fin de support

Plus de correctifs : **migrer**, ou **isoler** en attendant (zone dédiée, flux minimaux, séance S05) et **documenter** le risque accepté.
