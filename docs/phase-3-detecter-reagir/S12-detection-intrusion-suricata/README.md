# S12 – Détection d'intrusion : règles, réglage et faux positifs

> [!WARNING]
> **Séance à rédiger.** Cette page donne le cadre prévu (objectifs, compétences, contenu). Le cours, le TP et l'aide-mémoire arrivent avec la phase 3.

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 2e année – bloc 3 |
| **Séance** | S12 (séance 12 sur 19) – Phase 3 |
| **Durée** | 4 heures |
| **Prérequis** | S11 |
| **Matériel** | VirtualBox : une sonde Suricata, une machine d'attaque de laboratoire, une cible |
| **Compétences travaillées** | B3.4 · B3.5A (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Comment passer d'une sonde qui alerte sur tout à une sonde utile ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. Installer une sonde réseau et lire ses alertes ;
2. Écrire et tester une règle de détection simple ;
3. Distinguer vrai positif, faux positif et attaque manquée, et ajuster ;
4. Relier les alertes de la sonde aux journaux de la séance précédente.

## Contenu prévu

- Cours : détection par signature et par comportement, emplacement des sondes, réglage
- TP : scénario d'attaque de laboratoire, règles, réduction des faux positifs
- Aide-mémoire : syntaxe d'une règle, fichiers de configuration

## Évaluation

- Compte rendu avec captures d'écran datées, nommé `RENDU-B3A2-S12-NOM.pdf`.
- Bilan de compétences rempli en fin de séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)) ; le choix des compétences pour cette séance est une proposition à valider.
- **Programme :** cette séance fait partie d'un programme proposé, à valider avant rédaction.
- Attaque uniquement dans le laboratoire isolé. Recouvre en partie S15 de la première année (IDS) : l'accent est mis sur le réglage et la corrélation.

</details>
