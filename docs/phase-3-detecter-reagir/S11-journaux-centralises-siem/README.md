# S11 – Journaux centralisés et supervision de sécurité

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 2e année – bloc 3 |
| **Séance** | S11 (séance 11 sur 19) – Phase 3 |
| **Durée** | 4 heures |
| **Prérequis** | S05 · S10 |
| **Matériel** | VirtualBox : un collecteur (par exemple Wazuh ou rsyslog) et deux machines |
| **Compétences travaillées** | B3.4 · B3.5A (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Comment voir une attaque quand elle a lieu sur plusieurs machines à la fois ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. Envoyer les journaux de plusieurs machines vers un serveur central ;
2. Normaliser et horodater les événements (synchronisation du temps) ;
3. Écrire des règles de corrélation simples et lire des alertes ;
4. Décider d'une durée de conservation en lien avec le cadre juridique.

## Contenu de la séance

| Document | Rôle |
|---|---|
| [Cours – Journaux centralisés et supervision de sécurité](01-cours.md) | Cours |
| [TP – Un collecteur de journaux et une alerte multi-machines](02-tp.md) | TP |
| [Aide-mémoire – Journaux centralisés](03-aide-memoire.md) | Aide-mémoire |

## Déroulé conseillé (4 h)

| Durée | Activité | Format |
|---|---|---|
| 0 h 00 – 0 h 20 | **Accroche : « Une attaque touche trois serveurs à la fois : comment la voit-on ? »** | Oral |
| 0 h 20 – 1 h 10 | **Cours** | Cours et questions |
| 1 h 10 – 4 h 00 | **TP**, puis bilan | Binôme puis individuel |

## Retour en entreprise

Si ta situation le permet : **observer** comment ton entreprise traite le sujet de la séance, **documenter** en une demi-page l'écart avec le TP, ou **réaliser** une partie après accord de ton tuteur. Voir [Transfert en entreprise](../../ressources/transfert-entreprise.md).

## Évaluation

- Compte rendu avec captures d'écran datées, nommé `RENDU-B3A2-S11-NOM.pdf`.
- Bilan de compétences rempli en fin de séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)) ; le choix des compétences pour cette séance est une proposition à valider.
- L'outil central (Wazuh, ou rsyslog avec un tableau de bord léger) est à choisir selon les machines de la salle. Prolonge S15 de la première année. Étapes basées sur journald non testées dans le laboratoire de l'auteur : à tester avant la séance.
- Labo testé sous Ubuntu 24.04 avec `logger` pour simuler les événements ; les vraies connexions SSH échouées, Debian 12 et Wazuh ne sont **pas** testés. Voir le corrigé.

</details>
