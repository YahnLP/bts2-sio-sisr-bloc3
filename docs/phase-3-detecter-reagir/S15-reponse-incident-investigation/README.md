# S15 – Réponse à incident et investigation

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 2e année – bloc 3 |
| **Séance** | S15 (séance 15 sur 19) – Phase 3 |
| **Durée** | 4 heures |
| **Prérequis** | S04 · S11 |
| **Matériel** | VirtualBox : un jeu de machines et de journaux fournis, simulant une compromission |
| **Compétences travaillées** | B3.4 · B3.5A · B3.1 (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Une machine est chiffrée un lundi matin : que fait-on dans les premières heures, et que garde-t-on comme preuve ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. Dérouler les étapes de la réponse à incident (préparation, détection, contenance, éradication, reprise, retour d'expérience) ;
2. Collecter des éléments dans l'ordre de volatilité et préserver la chaîne de preuve ;
3. Reconstituer la chronologie d'une attaque à partir de journaux ;
4. Rédiger un compte rendu d'incident et une communication à la direction.

## Contenu de la séance

| Document | Rôle |
|---|---|
| [Cours – Réponse à incident et investigation](01-cours.md) | Cours |
| [TP – Un lundi matin : enquêter sur un rançongiciel](02-tp.md) | TP |
| [Aide-mémoire – Le premier quart d'heure et l'investigation](03-aide-memoire.md) | Aide-mémoire |

## Déroulé conseillé (4 h)

| Durée | Activité | Format |
|---|---|---|
| 0 h 00 – 0 h 20 | **Accroche : « Lundi 7 h 45, les fichiers du serveur ne s'ouvrent plus : que fait-on dans le premier quart d'heure ? »** | Oral |
| 0 h 20 – 1 h 10 | **Cours** | Cours et questions |
| 1 h 10 – 4 h 00 | **TP**, puis bilan | Binôme puis individuel |

## Retour en entreprise

Si ta situation le permet : **observer** comment ton entreprise traite le sujet de la séance, **documenter** en une demi-page l'écart avec le TP, ou **réaliser** une partie après accord de ton tuteur. Voir [Transfert en entreprise](../../ressources/transfert-entreprise.md).

## Évaluation

- Compte rendu avec captures d'écran datées, nommé `RENDU-B3A2-S15-NOM.pdf`.
- Bilan de compétences rempli en fin de séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)) ; le choix des compétences pour cette séance est une proposition à valider.
- **Corrigé :** dans `corriges/` à la racine du dépôt (hors du site publié).
- Les journaux fournis sont fictifs. Prolonge S17 de la première année (incident et preuves) : ici on travaille sur un scénario complet, avec la notification (S04).
- Les journaux fournis (dossier `journaux-fictifs`) sont **fictifs**, générés par l'auteur ; commandes d'analyse et de hachage vérifiées. Prolonge S17 de la première année. Voir le corrigé.

</details>
