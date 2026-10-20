# S13 – Gestion des vulnérabilités : de la découverte à la correction

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 2e année – bloc 3 |
| **Séance** | S13 (séance 13 sur 19) – Phase 3 |
| **Durée** | 4 heures |
| **Parcours** | **Cœur** – Gestion des vulnérabilités : prérequis de S14. Voir le [parcours cœur et complément](../../ressources/parcours-coeur-complement.md). |
| **Prérequis** | S10 |
| **Matériel** | VirtualBox : un scanneur de vulnérabilités et deux cibles de laboratoire |
| **Compétences travaillées** | B3.4 · B3.5A (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Sur cent failles détectées, laquelle corrige-t-on en premier, et pourquoi ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. Distinguer vulnérabilité, correctif, exposition et exploitation ;
2. Lire un score de gravité (CVSS) et ses limites ;
3. Réaliser un scan de vulnérabilités sur le laboratoire et trier les résultats ;
4. Prioriser et planifier les corrections, suivre leur application.

## Contenu de la séance

| Document | Rôle |
|---|---|
| [Cours – Gestion des vulnérabilités : de la découverte à la correction](01-cours.md) | Cours |
| [TP – Scanner, noter, prioriser, corriger, prouver](02-tp.md) | TP |
| [Aide-mémoire – Lire un rapport de vulnérabilités](03-aide-memoire.md) | Aide-mémoire |

## Déroulé conseillé (4 h)

| Durée | Activité | Format |
|---|---|---|
| 0 h 00 – 0 h 20 | **Accroche : « Le scanneur a trouvé 240 failles : par laquelle commence-t-on ? »** | Oral |
| 0 h 20 – 1 h 10 | **Cours** | Cours et questions |
| 1 h 10 – 4 h 00 | **TP**, puis bilan | Binôme puis individuel |

## Retour en entreprise

Si ta situation le permet : **observer** comment ton entreprise traite le sujet de la séance, **documenter** en une demi-page l'écart avec le TP, ou **réaliser** une partie après accord de ton tuteur. Voir [Transfert en entreprise](../../ressources/transfert-entreprise.md).

## Évaluation

- Compte rendu avec captures d'écran datées, nommé `RENDU-B3A2-S13-NOM.pdf`.
- Bilan de compétences rempli en fin de séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)) ; le choix des compétences pour cette séance est une proposition à valider.
- Scan autorisé uniquement sur le laboratoire. Prolonge S16 de la première année (audit de vulnérabilités). Version et licence de l'outil de scan à vérifier.
- Labo testé avec nmap et Nikto 2.1.5 (la sortie de Nikto change selon la version). Aucun scanneur complet (OpenVAS, Nessus) n'a été testé. Scan autorisé uniquement sur le laboratoire. Voir le corrigé.

</details>
