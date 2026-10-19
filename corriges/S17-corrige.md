# Corrigé – S17 : La sécurité dans un projet d'infrastructure

*Réservé à l'enseignant.*

## Vérification

Séance **sans manipulation technique** : tout se fait sur un dossier **fictif**. Les **prix** de l'annexe 3 sont **inventés** ; les calculs ci-dessous ont été refaits. Les repères juridiques (contrat de sous-traitant, notification, analyse d'impact) renvoient à la séance S04 et sont **à faire valider par un juriste**. **Non vérifié** : le caractère obligatoire d'une analyse d'impact pour ce projet (dépend de critères précis de la CNIL à consulter ; une boutique de vente en ligne classique n'en relève pas forcément) ; les valeurs de disponibilité du tableau de l'aide-mémoire sont un **calcul** à partir de 8 760 heures.

## Partie A

Défauts de l'article 4 : **vague** (aucun chiffre), **non vérifiable**, **sans lien avec un risque**, **responsabilité renvoyée** à l'hébergeur sans mesure, pas de **test**.

| Phrase | Exigence (exemple) | Risque | Séance |
|---|---|---|---|
| Site sécurisé, résiste aux attaques | « La boutique n'accepte que TLS 1.2 ou 1.3 ; en-têtes de sécurité activés ; interface d'administration inaccessible depuis Internet ; audit avant mise en ligne sans non-conformité critique » | Compromission du site, vol de comptes | S08, S14 |
| Mots de passe robustes | « 12 caractères minimum, verrouillage après 5 échecs, double authentification pour l'administration » | Prise de contrôle de comptes | S06 |
| Données clients protégées | « Collecte limitée à ce qui est nécessaire ; durée de conservation fixée ; accès restreint ; chiffrement des sauvegardes ; contrat de sous-traitance avec l'hébergeur » | Fuite de données (RGPD) | S04 |
| Accès distant sécurisé | « Accès uniquement par VPN avec double authentification ; comptes nominatifs ; journalisation des connexions » | Intrusion par accès distant (cf. S15) | S06, S07 |
| Sauvegarde régulière | « Sauvegarde quotidienne de la base clients ; une copie hors ligne et hors site ; restauration testée chaque année ; RPO 24 h, RTO fixé avec la direction » | Perte ou chiffrement des données | S16 |
| L'hébergeur garantira | « Contrat avec niveau de service mesurable, notification d'incident, droit d'audit, réversibilité » | Dépendance au prestataire | S17, S04 |

Quatre exigences supplémentaires attendues (exemples) : **journalisation centralisée** des authentifications et de l'administration (S11) ; **tablettes** sur un réseau Wi-Fi **dédié** avec authentification des équipements (S05, S07) ; **correctifs** critiques du site et du serveur appliqués sous un délai fixé (S10, S13) ; **sécurisation du serveur de fichiers et de la messagerie** existants (droits, mises à jour, S06, S10).

Exigence **vérifiable** : on peut écrire un test ; sans : « mot de passe robuste » ; avec : « 12 caractères minimum, verrouillage après 5 échecs ».

## Partie B

Coûts de la **première année** (investissement + fonctionnement) :

| Réf. | Risque principal | Coût (€) | Temps (jours) |
|---|---|---|---|
| M1 | Intrusion, flux non maîtrisés | 2 760 | 3 |
| M2 | Prise de contrôle de comptes | 72 | 1 |
| M3 | Attaques web | 480 | 1 |
| M4 | Perte, chiffrement des données | 1 200 | 2 (+1 par test) |
| M5 | Failles de la boutique avant exposition | 3 200 | 2 |
| M6 | Intrusion non détectée | 0 | 4 |
| M7 | Compromission via Wi-Fi des tablettes | 1 200 | 3 |
| M8 | Intrusion non détectée | 3 900 | 5 (+1 par mois) |
| M9 | Hameçonnage, erreurs | 1 500 | — |
| M10 | Vulnérabilités du serveur et de la messagerie existants | 0 | 5 |

**Total : 14 312 €** (investissement : 12 700 €), contre **8 500 €** : **il faut arbitrer**. Temps interne : environ **26 jours** (plus les tests et le suivi mensuel), pour une personne, en quatre mois : **tenable mais serré**, sans compter l'exploitation courante.

Proposition de solution (**autres choix argumentés acceptés**) :

| Décision | Mesures | Coût |
|---|---|---|
| **Maintenant** | M1, M2, M3, M4, M5, M6, M10 | 7 712 € (reste **788 €** dans l'enveloppe) |
| **Phase 2** | M7 (Wi-Fi tablettes), M9 (formation : une session courte en interne en attendant), M8 (sonde, une fois la journalisation en place) | 1 200 € + 1 500 € + 3 900 € |
| **Pas faire (pour l'instant)** | Rien n'est abandonné ; M8 est la plus discutable | |

Justifications attendues : **M2, M10, M6** coûtent presque rien en euros et réduisent beaucoup le risque (souvent oubliés car **invisibles** et demandent du **temps**) ; **M5** protège la mise en ligne de la **seule** application exposée ; **M4** conditionne la **reprise** (S16) ; **M7** est reporté (réseau de production non exposé à Internet) **mais** un risque sur la traçabilité sanitaire subsiste, à **accepter explicitement** ou à compenser (tablettes sur un réseau séparé avec un mot de passe fort, en attendant). **M8** n'a de valeur que si quelqu'un **lit** les alertes (S12) : à retarder tant que la **journalisation** n'est pas maîtrisée. Le **risque résiduel** est validé par le **dirigeant**.

## Partie C

Exemples de tests attendus :

| Exigence | Test | Attendu |
|---|---|---|
| Administration non exposée | Depuis Internet, ouvrir l'adresse d'administration | Pas de réponse |
| TLS | Tester les protocoles (S08) | Seulement TLS 1.2 et 1.3 |
| Double authentification | Se connecter à l'administration avec le seul mot de passe | Refus |
| Verrouillage | 6 mauvais mots de passe de suite | Compte verrouillé après le cinquième |
| Journalisation | Provoquer des échecs, chercher sur le collecteur (S11) | Événements présents et horodatés |
| Sauvegarde | Restauration chronométrée de la base clients (S16) | Restauration conforme dans le RTO |
| VPN | Accès distant sans VPN | Impossible |
| Wi-Fi des tablettes (si M7) | Tablette non enrôlée tente de se connecter | Refusée |

Test **non conforme** : on **corrige** puis on **rejoue** le test. Livraison avec **réserve** : seulement si la non-conformité n'est **pas critique**, avec une **date de levée** et l'accord du dirigeant.

## Partie D

| Article | Verdict | Problème | Clause demandée |
|---|---|---|---|
| 3 | À négocier | 99 % est modeste ; **mesuré par l'hébergeur lui-même** | Niveau de service précis (par exemple 99,9 %), mesure **contrôlable**, pénalités |
| 7 | Acceptable | Bon principe, à compléter | Étendre à la **confidentialité** et à l'**usage** des données (aucune réutilisation) |
| 9 | **Inacceptable** | L'hébergeur se décharge des **pertes de données** | **Sauvegardes** à sa charge, périodicité et durée fixées, responsabilité pour faute |
| 11 | **Inacceptable** | Suppression **sans restitution** : perte des données et du service | **Réversibilité** : restitution des données dans un format exploitable, **avant** suppression |
| 12 | **Inacceptable** | Sous-traitants au choix, sans information | **Liste** des sous-traitants, **accord préalable**, mêmes obligations |

**Document nécessaire** (S04) : un **contrat de sous-traitance** (ou clauses équivalentes) entre la fromagerie (responsable de traitement) et l'hébergeur (sous-traitant), précisant instructions, sécurité, sous-traitants ultérieurs, notification des violations, restitution ou suppression.

Disponibilité 99 % : `8 760 × 0,01 ≈ 87,6 heures` d'arrêt par an, soit plus de trois jours et demi : **peu compatible** avec une boutique en ligne qui vend en continu ; on peut accepter un niveau plus faible **si** la boutique n'est pas vitale (à justifier) mais pas **sans mesure ni pénalité**.

## Partie E

1. Éléments à documenter : **finalité** (vendre et livrer), **base juridique** (exécution du contrat), **données** collectées, **durée de conservation**, **destinataires** (hébergeur, prestataire de paiement, transporteur), **droits** des personnes, **mesures de sécurité**, inscription au **registre des traitements**.
2. Protection dès la conception : minimum de données (pas de champs inutiles), **conservation limitée** des comptes inactifs, **chiffrement** (TLS, sauvegardes), **mots de passe hachés**, **réglages protecteurs** par défaut, **pas de données de carte** (déléguées).
3. À consulter : le **DPO** s'il existe ou un référent, la **direction**, éventuellement un **juriste** ; la CNIL **n'est consultée en amont** que dans les cas prévus (à vérifier).

## Partie F

Critères : chaque proposition suit **risque, mesure, justification, limite** ; chiffres **issus du dossier** (14 312 € si tout, 7 712 € retenus) ; **phasage** ; **exploitation** (qui maintient, avec quel temps : environ 26 jours internes la première année) ; **risque résiduel** nommé et validé ; pas de jargon.

## Pièges fréquents

- Recopier des **exigences génériques**.
- Choisir des mesures **sans lien** avec les risques.
- Oublier le **temps interne** et la **maintenance**.
- Dépasser le budget **sans le dire**.
- Ne pas **justifier** ce qu'on écarte.
- **Accepter** un contrat sans réversibilité ni sauvegarde.
- Confondre **recette** (preuve) et **intention**.
