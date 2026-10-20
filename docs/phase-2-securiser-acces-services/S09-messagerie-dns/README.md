# S09 – Messagerie et DNS : usurpation et protection

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 2e année – bloc 3 |
| **Séance** | S09 (séance 9 sur 19) – Phase 2 |
| **Durée** | 4 heures |
| **Prérequis** | S05 |
| **Matériel** | VirtualBox : un serveur DNS de laboratoire, un poste |
| **Compétences travaillées** | B3.2 · B3.4 (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Comment empêcher qu'on envoie un message en se faisant passer pour ton organisation ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. Expliquer SPF, DKIM et DMARC et ce que chacun protège ;
2. Lire l'en-tête d'un message et repérer une usurpation ;
3. Situer les risques liés au DNS (détournement, empoisonnement) et la protection par signature (DNSSEC) ;
4. Rédiger les enregistrements SPF et DMARC d'un domaine de laboratoire.

## Contenu de la séance

| Document | Rôle |
|---|---|
| [Cours – Messagerie et DNS : usurpation et protection](01-cours.md) | Cours |
| [TP – Usurpation de messages et protection du DNS](02-tp.md) | TP |
| [Aide-mémoire – Messagerie et DNS](03-aide-memoire.md) | Aide-mémoire |

## Déroulé conseillé (4 h)

| Durée | Activité | Format |
|---|---|---|
| 0 h 00 – 0 h 20 | **Accroche : « Un faux message de la direction demande un virement : qu'est-ce qui aurait dû l'arrêter ? »** | Oral |
| 0 h 20 – 1 h 10 | **Cours** | Cours et questions |
| 1 h 10 – 4 h 00 | **TP**, puis bilan | Binôme puis individuel |

## Retour en entreprise

Si ta situation le permet : **observer** comment ton entreprise traite le sujet de la séance, **documenter** en une demi-page l'écart avec le TP, ou **réaliser** une partie après accord de ton tuteur. Voir [Transfert en entreprise](../../ressources/transfert-entreprise.md).

## Évaluation

- Compte rendu avec captures d'écran datées, nommé `RENDU-B3A2-S09-NOM.pdf`.
- Bilan de compétences rempli en fin de séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)) ; le choix des compétences pour cette séance est une proposition à valider.
- Le TP se fait sur un domaine de laboratoire interne, jamais sur un domaine réel de l'établissement. Lien avec B3.2 (identité numérique de l'organisation).
- Le TP se fait sur un domaine de laboratoire interne (`lab.local`), jamais sur un domaine réel de l'établissement. Lien avec B3.2 (identité numérique de l'organisation). Voir le corrigé pour ce qui a été vérifié.

</details>
