# S06 – Annuaire sécurisé et comptes à privilèges

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 2e année – bloc 3 |
| **Séance** | S06 (séance 6 sur 19) – Phase 2 |
| **Durée** | 4 heures |
| **Prérequis** | S01 ; bloc 2 : Active Directory |
| **Matériel** | VirtualBox : Windows Server (contrôleur de domaine) et un poste Windows |
| **Compétences travaillées** | B3.3 · B3.5A (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Comment empêcher qu'un seul compte compromis donne accès à tout le domaine ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. Expliquer l'authentification Kerberos et ses limites face à NTLM ;
2. Appliquer des stratégies de groupe de sécurité (mots de passe, verrouillage, restrictions) ;
3. Séparer les comptes d'administration des comptes courants (modèle en niveaux) ;
4. Mettre en place un mot de passe local géré (LAPS) ou une alternative documentée ;
5. Situer le rôle d'un bastion d'administration.

## Contenu de la séance

| Document | Rôle |
|---|---|
| [Cours – Annuaire sécurisé et comptes à privilèges](01-cours.md) | Cours |
| [TP – Durcir un domaine de laboratoire](02-tp.md) | TP |
| [Aide-mémoire – Annuaire sécurisé](03-aide-memoire.md) | Aide-mémoire |

## Déroulé conseillé (4 h)

| Durée | Activité | Format |
|---|---|---|
| 0 h 00 – 0 h 20 | **Accroche : « Un compte d'administrateur de domaine est volé : que perd-on ? »** | Oral |
| 0 h 20 – 1 h 10 | **Cours** | Cours et questions |
| 1 h 10 – 4 h 00 | **TP**, puis bilan | Binôme puis individuel |

## Retour en entreprise

Si ta situation le permet : **observer** comment ton entreprise traite le sujet de la séance, **documenter** en une demi-page l'écart avec le TP, ou **réaliser** une partie après accord de ton tuteur. Voir [Transfert en entreprise](../../ressources/transfert-entreprise.md).

## Évaluation

- Compte rendu avec captures d'écran datées, nommé `RENDU-B3A2-S06-NOM.pdf`.
- Bilan de compétences rempli en fin de séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)) ; le choix des compétences pour cette séance est une proposition à valider.
- Prérequis fort sur Active Directory du bloc 2 : vérifier que les machines Windows du laboratoire sont disponibles. Prolonge S04 de la première année (droits et privilèges).
- **Non testé :** le TP suppose un domaine Active Directory sous Windows Server, non disponible dans l'environnement de l'auteur. Les commandes sont à essayer avant la séance. Voir le corrigé.

</details>
