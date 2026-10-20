# S07 – Authentification des équipements : 802.1X, RADIUS et Wi-Fi d'entreprise

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 2e année – bloc 3 |
| **Séance** | S07 (séance 7 sur 19) – Phase 2 |
| **Durée** | 4 heures |
| **Prérequis** | S05 |
| **Matériel** | VirtualBox : un serveur RADIUS, un client, éventuellement un point d'accès ou un simulateur |
| **Compétences travaillées** | B3.3 · B3.5A (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Comment ne laisser entrer sur le réseau que des équipements et des personnes identifiés ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. Expliquer le rôle du demandeur, de l'authentificateur et du serveur d'authentification ;
2. Configurer un serveur RADIUS de laboratoire et un client ;
3. Distinguer WPA2/WPA3 personnel et entreprise ;
4. Tester une authentification réussie et refusée, lire les journaux.

## Contenu de la séance

| Document | Rôle |
|---|---|
| [Cours – 802.1X, RADIUS et Wi-Fi d'entreprise](01-cours.md) | Cours |
| [TP – Un serveur RADIUS de laboratoire](02-tp.md) | TP |
| [Aide-mémoire – 802.1X et RADIUS](03-aide-memoire.md) | Aide-mémoire |

## Déroulé conseillé (4 h)

| Durée | Activité | Format |
|---|---|---|
| 0 h 00 – 0 h 20 | **Accroche : « Quelqu'un branche un portable inconnu sur une prise murale : que se passe-t-il ? »** | Oral |
| 0 h 20 – 1 h 10 | **Cours** | Cours et questions |
| 1 h 10 – 4 h 00 | **TP**, puis bilan | Binôme puis individuel |

## Retour en entreprise

Si ta situation le permet : **observer** comment ton entreprise traite le sujet de la séance, **documenter** en une demi-page l'écart avec le TP, ou **réaliser** une partie après accord de ton tuteur. Voir [Transfert en entreprise](../../ressources/transfert-entreprise.md).

## Évaluation

- Compte rendu avec captures d'écran datées, nommé `RENDU-B3A2-S07-NOM.pdf`.
- Bilan de compétences rempli en fin de séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)) ; le choix des compétences pour cette séance est une proposition à valider.
- Prévoir la solution de repli si aucun point d'accès n'est disponible : test avec un client RADIUS en ligne de commande. À tester avant la séance.
- Le TP tient sur **une seule** machine Debian (serveur RADIUS et client de test). Le paquet fournissant `eapol_test` sous Debian est à vérifier avant la séance. Voir le corrigé.

</details>
