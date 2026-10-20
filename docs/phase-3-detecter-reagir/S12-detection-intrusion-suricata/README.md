# S12 – Détection d'intrusion : règles, réglage et faux positifs

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 2e année – bloc 3 |
| **Séance** | S12 (séance 12 sur 19) – Phase 3 |
| **Durée** | 4 heures |
| **Parcours** | **Cœur** – Détection d'intrusion : seule séance sur la détection réseau et le réglage des règles. Voir le [parcours cœur et complément](../../ressources/parcours-coeur-complement.md). |
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

## Contenu de la séance

| Document | Rôle |
|---|---|
| [Cours – Détection d'intrusion : règles, réglage et faux positifs](01-cours.md) | Cours |
| [TP – Une sonde Suricata : écrire, tester, régler](02-tp.md) | TP |
| [Aide-mémoire – Détection d'intrusion avec Suricata](03-aide-memoire.md) | Aide-mémoire |

## Déroulé conseillé (4 h)

| Durée | Activité | Format |
|---|---|---|
| 0 h 00 – 0 h 20 | **Accroche : « La sonde a émis 400 alertes cette nuit : qu'en fait-on ? »** | Oral |
| 0 h 20 – 1 h 10 | **Cours** | Cours et questions |
| 1 h 10 – 4 h 00 | **TP**, puis bilan | Binôme puis individuel |

## Retour en entreprise

Si ta situation le permet : **observer** comment ton entreprise traite le sujet de la séance, **documenter** en une demi-page l'écart avec le TP, ou **réaliser** une partie après accord de ton tuteur. Voir [Transfert en entreprise](../../ressources/transfert-entreprise.md).

## Évaluation

- Compte rendu avec captures d'écran datées, nommé `RENDU-B3A2-S12-NOM.pdf`.
- Bilan de compétences rempli en fin de séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)) ; le choix des compétences pour cette séance est une proposition à valider.
- Attaque uniquement dans le laboratoire isolé. Recouvre en partie S15 de la première année (IDS) : l'accent est mis sur le réglage et la corrélation.
- Labo testé avec Suricata 7.0.3 (Debian 12 fournit la série 6.0 : syntaxe des tampons à vérifier). Attaques uniquement dans le laboratoire isolé. Voir le corrigé.

</details>
