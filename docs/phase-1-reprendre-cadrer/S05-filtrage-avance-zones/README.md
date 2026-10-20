# S05 – Filtrage avancé et zones réseau

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 2e année – bloc 3 |
| **Séance** | S05 (séance 5 sur 19) – Phase 1 |
| **Durée** | 4 heures |
| **Parcours** | **Cœur** – Filtrage et zones : prérequis de S07 à S11. Voir le [parcours cœur et complément](../../ressources/parcours-coeur-complement.md). |
| **Prérequis** | S01 ; bloc 2 : adressage et pare-feu |
| **Matériel** | VirtualBox, trois machines virtuelles Debian sur réseau interne |
| **Compétences travaillées** | B3.4 · B3.5A (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Comment ne laisser passer que ce qui est utile, et le prouver ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. Concevoir un plan de zones (utilisateurs, serveurs, DMZ, administration) et la matrice de flux ;
2. Écrire un jeu de règles nftables à politique par défaut restrictive ;
3. Journaliser le trafic refusé ;
4. Vérifier le filtrage depuis une autre machine (nmap, curl) et interpréter les résultats.

## Contenu de la séance

| Document | Rôle |
|---|---|
| [Cours – Filtrage avancé et zones réseau](01-cours.md) | Cours |
| [TP – Un pare-feu à trois zones](02-tp.md) | TP |
| [Aide-mémoire – nftables et matrice de flux](03-aide-memoire.md) | Aide-mémoire |

## Déroulé conseillé (4 h)

| Durée | Activité | Format |
|---|---|---|
| 0 h 00 – 0 h 20 | **Accroche : « le serveur web est piraté : jusqu'où l'attaquant peut-il aller ? »** | Oral |
| 0 h 20 – 1 h 10 | **Cours** | Cours et questions |
| 1 h 10 – 4 h 00 | **TP**, puis bilan | Binôme puis individuel |

## Retour en entreprise

Si ta situation le permet : **observer** comment ton entreprise traite le sujet de la séance, **documenter** en une demi-page l'écart avec le TP, ou **réaliser** une partie après accord de ton tuteur. Voir [Transfert en entreprise](../../ressources/transfert-entreprise.md).


## Évaluation

- Compte rendu avec captures d'écran datées, nommé `RENDU-B3A2-S05-NOM.pdf`.
- Bilan de compétences rempli en fin de séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)) ; le choix des compétences pour cette séance est une proposition à valider.
- Les règles de la séance S01 (politique par défaut `drop`, suivi de connexion, SSH limité à un réseau) ont été vérifiées dans le laboratoire de l'auteur. Reprend S14 de la première année et la partie pare-feu du bloc 2.

</details>
