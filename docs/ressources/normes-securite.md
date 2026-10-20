# Normes et référentiels de sécurité

Une organisation ne définit pas sa sécurité « à l'intuition » : elle s'appuie sur des textes reconnus. Le référentiel du BTS demande de **vérifier la conformité d'une infrastructure à un référentiel, une norme ou un standard de sécurité**. Cette page donne le panorama minimal à connaître.

> [!NOTE]
> **À vérifier avant diffusion.** Les numéros d'édition et les nombres de mesures ci-dessous sont donnés de mémoire de l'auteur et n'ont pas été relus sur les textes. Vérifier sur le site de l'éditeur avant de les imposer en évaluation. Les normes ISO sont payantes : on en étudie la structure, pas le texte intégral.

## 1. Le panorama

| Référentiel | Éditeur | Nature | À quoi ça sert |
|---|---|---|---|
| **ISO/CEI 27001** | ISO / CEI | Norme de **management** (SMSI) certifiable | Organiser la sécurité comme un cycle d'amélioration continue (planifier, déployer, vérifier, corriger) |
| **ISO/CEI 27002** | ISO / CEI | Guide de **mesures** | Catalogue de mesures de sécurité, regroupées en quatre thèmes : organisationnel, humain, physique, technologique (édition 2022) |
| **ISO/CEI 27005** | ISO / CEI | Gestion des risques | Cadre pour l'appréciation et le traitement des risques |
| **EBIOS Risk Manager** | ANSSI | **Méthode** d'analyse de risques | Voir [S02](../phase-1-reprendre-cadrer/S02-analyse-de-risques/01-cours.md) |
| **Guide d'hygiène informatique** | ANSSI | Mesures essentielles | Socle minimal pour toute organisation (une quarantaine de mesures) |
| **Cadre de cybersécurité (CSF)** | NIST (États-Unis) | Cadre de **fonctions** | Identifier, protéger, détecter, répondre, récupérer (version 2.0 : s'ajoute « gouverner ») |
| **CIS Controls** et **CIS Benchmarks** | Center for Internet Security | Mesures priorisées et réglages par système | Durcissement concret (voir S14 de 1re année) |
| **OWASP Top 10** | OWASP | Risques applicatifs | Sécurité des applications Web (voir S08) |
| **RGPD** | Union européenne | **Loi** | Protection des données personnelles (obligatoire, ce n'est pas une norme volontaire) |

Quatre distinctions à savoir faire :

1. **Loi** (obligatoire : RGPD, loi Godfrain) ou **norme** (volontaire, certifiable : ISO 27001) ou **guide** (recommandé : ANSSI, CIS).
2. **Management** (ISO 27001 : *comment piloter*) ou **mesures** (ISO 27002, hygiène ANSSI : *quoi mettre en place*) ou **méthode** (EBIOS : *comment décider*).
3. **Certifier** (un organisme indépendant atteste) ou **être conforme** (on a vérifié soi-même).
4. Un référentiel est un **point de départ** : on adapte au contexte et on documente les écarts assumés.

## 2. Comment on s'en sert en tant que technicien

- **Choisir des mesures** : l'analyse de risques donne les priorités, le catalogue (ISO 27002, hygiène ANSSI) donne les mesures candidates.
- **Justifier** une mesure devant un client : « cette mesure répond à la recommandation X du guide Y ».
- **Auditer** : on compare l'existant au référentiel, mesure par mesure, et on classe chaque écart (voir [S14](../phase-3-detecter-reagir/S14-audit-tests-intrusion/01-cours.md)).
- **Rédiger** un dossier : citer le référentiel utilisé et la version.

## 3. Exercice : classer des mesures

**Partie A.** Pour chaque mesure, indique le thème ISO 27002 (organisationnel, humain, physique ou technologique).

| # | Mesure |
|---|---|
| 1 | Politique de sécurité de l'information approuvée par la direction |
| 2 | Clause de confidentialité dans le contrat des nouveaux arrivants |
| 3 | Badge pour entrer dans le local technique |
| 4 | Chiffrement du disque des ordinateurs portables |
| 5 | Sensibilisation annuelle au hameçonnage |
| 6 | Journalisation centralisée des accès aux serveurs |
| 7 | Plan de continuité d'activité testé chaque année |

**Partie B.** Pour chaque mesure du tableau suivant, indique la fonction du cadre NIST (identifier, protéger, détecter, répondre, récupérer).

| # | Mesure |
|---|---|
| a | Inventaire des équipements et des logiciels |
| b | Sonde de détection d'intrusion sur le réseau |
| c | Restauration d'un serveur depuis la sauvegarde |
| d | Authentification multifacteur |
| e | Isolement d'un poste infecté du réseau |

<details markdown="1">
<summary>Voir les réponses</summary>

**Partie A.** 1 organisationnel ; 2 humain ; 3 physique ; 4 technologique ; 5 humain ; 6 technologique ; 7 organisationnel. Certaines mesures se discutent (la clause de confidentialité est aussi un acte juridique) : l'important est de **justifier** le classement.

**Partie B.** a identifier ; b détecter ; c récupérer ; d protéger ; e répondre.

</details>

## 4. Pour aller plus loin

- Guide d'hygiène informatique et guides de recommandations : site de l'ANSSI.
- EBIOS Risk Manager : site de l'ANSSI.
- CIS Benchmarks : site du Center for Internet Security (inscription demandée pour les versions complètes).
- Les plans cœur et complément : cette page est un **complément** de S02 et S14, pas un prérequis.
