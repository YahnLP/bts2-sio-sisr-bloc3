# Aide-mémoire – Exigences, arbitrage et recette

*BTS SIO SISR 2e année – Bloc 3 – S17*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## Du risque à la preuve

**Risque** → **objectif** → **exigence vérifiable** → **mesure** → **test de recette** → **preuve**.

## Une bonne exigence

| Critère | Test |
|---|---|
| **Précise** | Un chiffre, une version, un nom |
| **Vérifiable** | On peut écrire un test |
| **Justifiée** | Renvoie à un risque ou une obligation |
| **Réaliste** | Compatible avec budget, délai, compétences |

| Mauvaise | Bonne |
|---|---|
| « Mots de passe robustes » | « 12 caractères minimum ; verrouillage après 5 échecs » |
| « Accès distant sécurisé » | « Accès uniquement par VPN avec authentification à deux facteurs » |
| « Sauvegarde régulière » | « Sauvegarde quotidienne, une copie hors ligne, restauration testée chaque année, RTO de X heures » |

## Exemples d'exigences types

| Domaine | Exigence |
|---|---|
| Accès | Double authentification pour l'administration et l'accès distant |
| Réseau | Zones séparées ; flux autorisés listés ; administration depuis un réseau dédié |
| Web | TLS 1.2 ou 1.3 seulement ; en-têtes de sécurité ; administration non exposée |
| Données | Minimum collecté ; durée de conservation fixée ; chiffrement des sauvegardes |
| Journaux | Authentifications et administration journalisées, centralisées, conservées X mois |
| Mises à jour | Correctifs critiques appliqués sous N jours |
| Continuité | RPO et RTO écrits, restauration testée |

## Arbitrer

1. Mesure rattachée à un **risque** ;
2. **Coût** (investissement, fonctionnement, **temps interne**) ;
3. **Réduction de risque** ;
4. D'abord : **forte réduction, faible coût** (souvent des réglages) ;
5. **Justifier** ce qu'on ne fait pas ; **risque résiduel** accepté et validé ;
6. **Phaser**.

Un prix sans devis est une **hypothèse**.

## Recette

| Colonne | Contenu |
|---|---|
| Exigence | Référence |
| Test | Action précise |
| Attendu | Ce qui prouve |
| Obtenu / Verdict | Conforme, non conforme, réserve |
| Preuve | Capture, extrait |

**Réserve** = non-conformité acceptée **provisoirement**, avec **date de levée**. Pas de livraison avec une non-conformité **critique**.

## Prestataires : clauses à demander

- Niveau de service **mesurable** (et mesuré par qui ?)
- Mesures de **sécurité** minimales, correctifs
- **Contrat de sous-traitance RGPD** (S04)
- **Notification d'incident** dans un délai court
- **Droit d'audit**
- **Sauvegarde** et **réversibilité** (restitution des données)
- **Sous-traitants** : liste et accord préalable
- **Localisation** des données

## Disponibilité en heures d'arrêt par an

`heures par an ≈ 8 760 × (1 − disponibilité)`

| Disponibilité | Arrêt annuel approximatif |
|---|---|
| 99 % | 87,6 h (plus de 3 jours et demi) |
| 99,9 % | 8,76 h |
| 99,99 % | 52,6 min |

## Après la livraison

Correctifs · supervision · revue des droits · tests de restauration · nouvelle analyse de risques à chaque changement notable.
