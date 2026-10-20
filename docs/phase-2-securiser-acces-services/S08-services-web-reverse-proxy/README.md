# S08 – Sécuriser les services web : reverse proxy, en-têtes et OWASP

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 2e année – bloc 3 |
| **Séance** | S08 (séance 8 sur 19) – Phase 2 |
| **Durée** | 4 heures |
| **Prérequis** | S05 |
| **Matériel** | VirtualBox : un reverse proxy et une application web de laboratoire |
| **Compétences travaillées** | B3.4 · B3.5A (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Comment exposer une application sans exposer ses faiblesses ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. Placer un reverse proxy avec TLS devant une application ;
2. Appliquer des en-têtes de sécurité et limiter les méthodes et les débits ;
3. Situer les familles de failles web les plus fréquentes (liste de l'OWASP) ;
4. Vérifier la configuration et lire les journaux d'accès.

## Contenu de la séance

| Document | Rôle |
|---|---|
| [Cours – Sécuriser les services web : reverse proxy, en-têtes et OWASP](01-cours.md) | Cours |
| [TP – Un reverse proxy durci devant une application](02-tp.md) | TP |
| [Aide-mémoire – Reverse proxy, en-têtes et OWASP](03-aide-memoire.md) | Aide-mémoire |

## Déroulé conseillé (4 h)

| Durée | Activité | Format |
|---|---|---|
| 0 h 00 – 0 h 20 | **Accroche : « Le site est en ligne : qu'est-ce qu'un visiteur malveillant voit dès la première requête ? »** | Oral |
| 0 h 20 – 1 h 10 | **Cours** | Cours et questions |
| 1 h 10 – 4 h 00 | **TP**, puis bilan | Binôme puis individuel |

## Retour en entreprise

Si ta situation le permet : **observer** comment ton entreprise traite le sujet de la séance, **documenter** en une demi-page l'écart avec le TP, ou **réaliser** une partie après accord de ton tuteur. Voir [Transfert en entreprise](../../ressources/transfert-entreprise.md).

## Évaluation

- Compte rendu avec captures d'écran datées, nommé `RENDU-B3A2-S08-NOM.pdf`.
- Bilan de compétences rempli en fin de séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)) ; le choix des compétences pour cette séance est une proposition à valider.
- Liste OWASP et versions des en-têtes à relire à la source. Prolonge S12 de la première année (mini-PKI et HTTPS).
- Le TP tient sur **une seule** machine (nginx en reverse proxy devant une petite application de test). Voir le corrigé pour ce qui a été vérifié.

</details>
