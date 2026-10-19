# S05 – Filtrage avancé et zones réseau

> [!WARNING]
> **Séance à rédiger.** Cette page donne le cadre prévu (objectifs, compétences, contenu). Le cours, le TP et l'aide-mémoire arrivent avec la phase 1.

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 2e année – bloc 3 |
| **Séance** | S05 (séance 5 sur 19) – Phase 1 |
| **Durée** | 4 heures |
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

## Contenu prévu

- Cours : filtrage sans état et avec suivi de connexion, zones, DMZ, bonnes pratiques de règles
- TP : trois machines (client, pare-feu, serveur) ; règles nftables, journalisation, tests
- Aide-mémoire : syntaxe nftables, matrice de flux

## Évaluation

- Compte rendu avec captures d'écran datées, nommé `RENDU-B3A2-S05-NOM.pdf`.
- Bilan de compétences rempli en fin de séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)) ; le choix des compétences pour cette séance est une proposition à valider.
- **Programme :** cette séance fait partie d'un programme proposé, à valider avant rédaction.
- Les règles de la séance S01 (politique par défaut `drop`, suivi de connexion, SSH limité à un réseau) ont été vérifiées dans le laboratoire de l'auteur. Reprend S14 de la première année et la partie pare-feu du bloc 2.

</details>
