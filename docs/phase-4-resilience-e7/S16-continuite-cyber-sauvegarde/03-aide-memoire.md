# Aide-mémoire – Continuité et sauvegarde

*BTS SIO SISR 2e année – Bloc 3 – S16*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## Objectifs

| Sigle | Sens | Décidé par |
|---|---|---|
| **DMIA** | Durée maximale d'interruption **admissible** | Direction (limite métier) |
| **PDMA** | Perte de données maximale **admissible** | Direction (limite métier) |
| **RTO** | Temps de reprise **visé** | Technique, **sous** la DMIA |
| **RPO** | Point de reprise **visé** (données perdues) | Technique, **sous** la PDMA |

Un RPO de 24 h = une sauvegarde par nuit = jusqu'à une journée perdue.

**PCA** : continuer **pendant** l'incident (mode dégradé). **PRA** : redémarrer **après**.

## Règle 3-2-1, version rançongiciel

| Chiffre | Sens |
|---|---|
| **3** | Trois copies |
| **2** | Deux supports ou technologies |
| **1** | Une copie **hors site** |
| **+ 1** | Une copie **hors ligne ou non modifiable** |
| **0** | **Zéro erreur** : restauration **testée** |

## Rendre la sauvegarde inatteignable

| Moyen | Limite |
|---|---|
| Compte séparé | Si l'attaquant est administrateur de la machine de sauvegarde : perdu |
| Sauvegarde **tirée** (la sauvegarde va chercher) | Le serveur de sauvegarde doit être durci et isolé |
| Administration **hors annuaire** de production | Procédures plus lourdes |
| Copie **hors ligne** | Rotation, rigueur |
| Stockage **non modifiable** | Coût, configuration |
| **Rétention** supérieure au temps de présence de l'attaquant | Espace disque |

## Commandes (outil `restic`)

| Besoin | Commande |
|---|---|
| Créer un dépôt | `restic init -r /chemin/depot` |
| Sauvegarder | `restic backup -r /chemin/depot /srv/donnees` |
| Lister les versions | `restic snapshots -r /chemin/depot` |
| Vérifier | `restic check -r /chemin/depot` |
| Restaurer la dernière version | `restic restore latest -r /chemin/depot --target /dossier` |
| Simuler une purge des anciennes versions | `restic forget -r /chemin/depot --keep-last 1 --dry-run` |
| Mot de passe du dépôt | Variable `RESTIC_PASSWORD` (laboratoire seulement) |

**Perdre le mot de passe du dépôt = perdre la sauvegarde** : à conserver séparément.

## Prouver une restauration

```bash
find /srv/donnees -type f | sort | xargs sha256sum > manifeste.sha256   # avant le sinistre
sha256sum -c manifeste.sha256                                            # après
```

## Estimer le temps de reprise

`durée ≈ volume ÷ débit mesuré` **+** reconstruction **+** éradication **+** vérifications **+** remise en service.

Un essai sur un petit volume est **optimiste**.

## Restaurer proprement

1. **Éradiquer** d'abord (S15)
2. Restaurer dans un **réseau isolé**
3. **Vérifier** (empreintes, échantillon)
4. Respecter l'**ordre de dépendance** (annuaire et noms avant les serveurs qui en dépendent)
5. **Changer** les secrets présents dans les données

## Tester

| Test | Fréquence usuelle |
|---|---|
| Intégrité | À chaque sauvegarde |
| Un fichier | Régulièrement |
| **Restauration complète chronométrée** | Au moins une fois par an |
| Exercice de crise | Annuel |
