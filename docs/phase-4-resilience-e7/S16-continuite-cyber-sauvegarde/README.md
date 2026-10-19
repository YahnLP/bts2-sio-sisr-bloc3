# S16 – Continuité d'activité face à une cyberattaque

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 2e année – bloc 3 |
| **Séance** | S16 (séance 16 sur 19) – Phase 4 |
| **Durée** | 4 heures |
| **Prérequis** | S02 · S15 ; bloc 2 S05 |
| **Matériel** | Une machine virtuelle Debian (ou Ubuntu) avec le paquet restic |
| **Compétences travaillées** | B3.4 · B3.5A (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Si tout est chiffré ou détruit, en combien de temps et avec quoi redémarre-t-on ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. Distinguer plan de continuité et plan de reprise, et définir des objectifs de reprise ;
2. Concevoir une sauvegarde résistante à un rançongiciel (copie isolée ou non modifiable) ;
3. Tester une restauration complète et mesurer le temps réel ;
4. Relier le plan de reprise aux résultats de l'analyse de risques.

## Contenu de la séance

| Document | Rôle |
|---|---|
| [Cours – Continuité d'activité face à une cyberattaque](01-cours.md) | Cours |
| [TP – Sauvegarder, subir un sinistre, restaurer en chronométrant](02-tp.md) | TP |
| [Aide-mémoire – Continuité et sauvegarde](03-aide-memoire.md) | Aide-mémoire |

## Déroulé conseillé (4 h)

| Durée | Activité | Format |
|---|---|---|
| 0 h 00 – 0 h 20 | **Accroche : « Tout le serveur est chiffré, y compris la sauvegarde : qu'aurait-il fallu faire autrement ? »** | Oral |
| 0 h 20 – 1 h 10 | **Cours** | Cours et questions |
| 1 h 10 – 4 h 00 | **TP**, puis bilan | Selon le TP |

## Retour en entreprise

Si ta situation le permet : **observer** comment ton entreprise traite le sujet de la séance, **documenter** en une demi-page l'écart avec le TP, ou **réaliser** une partie après accord de ton tuteur. Voir [Transfert en entreprise](../../ressources/transfert-entreprise.md).

## Évaluation

- Compte rendu nommé `RENDU-B3A2-S16-NOM.pdf`.
- Bilan de compétences rempli en fin de séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)) ; le choix des compétences pour cette séance est une proposition à valider.
- **Corrigé :** dans `corriges/` à la racine du dépôt (hors du site publié).
- Le TP a été **rejoué par l'auteur sur Ubuntu 24.04** avec restic 0.16.4, sur **une seule machine virtuelle** (deux comptes). **Non vérifié** : Debian 12 (restic plus ancien), une vraie machine de sauvegarde distincte, un serveur en mode ajout seul et le verrouillage d'objets. Les durées mesurées ne se généralisent pas. Voir le corrigé.

</details>
