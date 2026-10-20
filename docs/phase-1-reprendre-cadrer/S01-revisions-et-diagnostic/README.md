# S01 – Reprendre la main : révisions rapides et auto-diagnostic

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 2e année – bloc 3 |
| **Séance** | S01 (séance 1 sur 19) – Phase 1 |
| **Durée** | 4 heures |
| **Prérequis** | Séances du bloc 3 de la première année |
| **Matériel** | VirtualBox, une machine virtuelle Debian (celle de l'an dernier ou une nouvelle) |
| **Compétences travaillées** | B3.1 · B3.2 · B3.3 · B3.4 (révision) (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Ce que tu as appris en cybersécurité l'an dernier tient-il encore ? Où faut-il revenir avant d'aller plus loin ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. **Rappeler** les notions clés de la première année (menaces, postes, authentification, droits, sauvegarde, RGPD, chiffrement, architecture, journaux, incident) ;
2. **Mesurer** ses acquis avec un auto-diagnostic de 24 questions réparties en 8 thèmes ;
3. **Faire l'inventaire** de sécurité d'un serveur Debian en lecture seule, puis **appliquer** un durcissement guidé et le **vérifier** ;
4. **Construire** son plan de révision personnel ;
5. **Situer** l'épreuve E7 et le plan de la deuxième année.

## Contenu de la séance

| Document | Rôle |
|---|---|
| [Cours – Fiche de révision de la première année](01-cours.md) | Cours |
| [TP – Auto-diagnostic, inventaire et durcissement d'un serveur](02-tp.md) | TP |
| [Aide-mémoire – Commandes et notions à connaître](03-aide-memoire.md) | Aide-mémoire |

## Déroulé conseillé (4 h)

| Durée | Activité | Format |
|---|---|---|
| 0 h 00 – 0 h 20 | **Accroche** : « un client reprend le serveur que tu as sécurisé l'an dernier ; que sais-tu encore en expliquer ? » ; présentation de l'année et de l'épreuve E7 | Oral |
| 0 h 20 – 1 h 20 | **Cours** : fiche de révision en 8 thèmes, avec un test flash par thème | Cours et questions |
| 1 h 20 – 2 h 00 | **TP, partie A** : auto-diagnostic de 24 questions | Individuel |
| 2 h 00 – 3 h 30 | **TP, parties B et C** : inventaire puis durcissement du serveur | Binôme |
| 3 h 30 – 4 h 00 | **Plan de révision et bilan de compétences** | Individuel |

## Retour en entreprise

Si ta situation le permet : **observer** comment ton entreprise traite le sujet de la séance, **documenter** en une demi-page l'écart avec le TP, ou **réaliser** une partie après accord de ton tuteur. Voir [Transfert en entreprise](../../ressources/transfert-entreprise.md).

## Évaluation

- Compte rendu avec captures d'écran datées, nommé `RENDU-B3A2-S01-NOM.pdf`.
- Plan de révision personnel et bilan de compétences remplis en fin de séance (individuels).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)) ; le choix des compétences pour cette séance est une proposition à valider.
- L'auto-diagnostic n'est pas noté : il sert à orienter le plan de révision de chacun.
- Les commandes des parties B et C ont été vérifiées dans un laboratoire Debian/Ubuntu de l'auteur, sauf celles qui lisent le journal du système (`journalctl`), non testées : voir le corrigé.
- Le TP modifie la configuration SSH et le pare-feu d'une machine virtuelle de laboratoire : prévoir un instantané (snapshot) VirtualBox avant la partie C.

</details>
