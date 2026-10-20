# S10 – Durcissement, conformité et gestion des correctifs

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 2e année – bloc 3 |
| **Séance** | S10 (séance 10 sur 19) – Phase 2 |
| **Durée** | 4 heures |
| **Parcours** | **Cœur** – Durcissement et conformité : prérequis de S11 et S13. Voir le [parcours cœur et complément](../../ressources/parcours-coeur-complement.md). |
| **Prérequis** | S03 · S05 |
| **Matériel** | VirtualBox : un serveur Debian |
| **Compétences travaillées** | B3.3 · B3.4 · B3.5A (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Comment savoir, preuves à l'appui, qu'un serveur est configuré comme prévu ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. Appliquer un guide de durcissement sur un serveur Linux ;
2. Mesurer la conformité avec un outil d'audit local et interpréter le rapport ;
3. Décrire un processus de gestion des correctifs (inventaire, test, déploiement, retour arrière) ;
4. Documenter les écarts acceptés et leur justification.

## Contenu de la séance

| Document | Rôle |
|---|---|
| [Cours – Durcissement, conformité et gestion des correctifs](01-cours.md) | Cours |
| [TP – Auditer, corriger, prouver](02-tp.md) | TP |
| [Aide-mémoire – Durcissement, conformité et correctifs](03-aide-memoire.md) | Aide-mémoire |

## Déroulé conseillé (4 h)

| Durée | Activité | Format |
|---|---|---|
| 0 h 00 – 0 h 20 | **Accroche : « Le serveur est installé depuis deux ans : est-il toujours comme on l'a décidé ? »** | Oral |
| 0 h 20 – 1 h 10 | **Cours** | Cours et questions |
| 1 h 10 – 4 h 00 | **TP**, puis bilan | Binôme puis individuel |

## Retour en entreprise

Si ta situation le permet : **observer** comment ton entreprise traite le sujet de la séance, **documenter** en une demi-page l'écart avec le TP, ou **réaliser** une partie après accord de ton tuteur. Voir [Transfert en entreprise](../../ressources/transfert-entreprise.md).

## Évaluation

- Compte rendu avec captures d'écran datées, nommé `RENDU-B3A2-S10-NOM.pdf`.
- Bilan de compétences rempli en fin de séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)) ; le choix des compétences pour cette séance est une proposition à valider.
- Reprend le durcissement vu en S14 de la première année : ici on mesure et on documente, on ne se contente plus d'appliquer. Choix de l'outil d'audit (Lynis ou OpenSCAP) à valider.
- Choix de l'outil d'audit : **Lynis** (OpenSCAP écarté, plus lourd à mettre en place). À valider. Les chiffres du corrigé sont propres à la machine de l'auteur. Reprend le durcissement vu en S14 de la première année : ici on mesure et on documente.

</details>
