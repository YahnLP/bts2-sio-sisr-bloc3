# Parcours « cœur » et « complément »

Les 19 séances de 4 h représentent **76 h** par an. Le volume prévu pour ce bloc en deuxième année dans la grille sous statut scolaire est de **96 h** (annexe III.A du référentiel) : le parcours en apprentissage en offre environ quatre cinquièmes. Quand le temps manque, ce parcours indique **quelles séances garder en priorité**.

> [!NOTE]
> Ce classement est une **proposition de l'auteur, à valider** par l'équipe pédagogique. Il ne retire rien du site : chaque séance reste disponible, et son statut est rappelé dans sa fiche.

## Pourquoi seulement deux compléments

Les séances s'enchaînent : S05 (filtrage) alimente S07 à S11, S10 alimente S11 et S13, S11 alimente S12 et S15, S15 alimente S16, et S17 rassemble les mesures de tout le bloc. Chaque séance de la progression est soit un prérequis, soit la seule à porter un savoir de l'épreuve E7. Seules **S07** et **S08** sont des approfondissements thématiques dont les compétences restent portées ailleurs.

## Principe

Une séance est **cœur** si l'une au moins de ces conditions est vraie :

1. elle est la **seule** à porter une compétence ou un savoir du bloc ;
2. elle est un **prérequis** d'une autre séance cœur (le site l'indique dans chaque fiche) ;
3. elle prépare directement **l'épreuve E7** (S18 et S19).

Sinon elle est **complément**.

## Résultat

- **17 séances cœur** (68 h) ;
- **2 séances complément** (8 h) : S07 et S08.

| Séance | Thème | Parcours | Pourquoi |
|---|---|---|---|
| S01 | Reprendre la main : révisions rapides et auto-diagnostic | **Cœur** | Remise à niveau et diagnostic ; prérequis de S02, S04, S05 et S06. |
| S02 | Analyse de risques : une méthode simplifiée inspirée d'EBIOS RM | **Cœur** | Analyse de risques : prérequis de S03, S16 et S17 ; méthode réutilisée dans S10, S13 et S14. |
| S03 | Référentiels, normes et politique de sécurité | **Cœur** | Référentiels et politique de sécurité : prérequis de S10 et S17. |
| S04 | Cadre juridique et responsabilités en entreprise | **Cœur** | Cadre juridique : prérequis de S14 et S15 ; avec S09, seule séance sur l'identité numérique et le droit (B3.1, B3.2). |
| S05 | Filtrage avancé et zones réseau | **Cœur** | Filtrage et zones : prérequis de S07 à S11. |
| S06 | Annuaire sécurisé et comptes à privilèges | **Cœur** | Annuaire et comptes à privilèges : seule séance sur ce point ; repris en S16 (administration séparée) et S17 (revue des comptes). |
| S07 | Authentification des équipements : 802.1X, RADIUS et Wi-Fi d'entreprise | **Complément** | 802.1X, RADIUS et Wi-Fi : approfondissement thématique ; les compétences B3.3 et B3.5A restent portées par d'autres séances, et S17 ne le cite qu'en exemple. |
| S08 | Sécuriser les services web : reverse proxy, en-têtes et OWASP | **Complément** | Reverse proxy, TLS et OWASP : approfondissement thématique ; les compétences B3.4 et B3.5A restent portées par d'autres séances, et S11 et S12 ne le citent qu'en exemple. |
| S09 | Messagerie et DNS : usurpation et protection | **Cœur** | Messagerie et DNS (usurpation) : avec S04, seule séance sur l'identité numérique de l'organisation (B3.2). |
| S10 | Durcissement, conformité et gestion des correctifs | **Cœur** | Durcissement et conformité : prérequis de S11 et S13. |
| S11 | Journaux centralisés et supervision de sécurité | **Cœur** | Journaux centralisés : prérequis de S12 et S15. |
| S12 | Détection d'intrusion : règles, réglage et faux positifs | **Cœur** | Détection d'intrusion : seule séance sur la détection réseau et le réglage des règles. |
| S13 | Gestion des vulnérabilités : de la découverte à la correction | **Cœur** | Gestion des vulnérabilités : prérequis de S14. |
| S14 | Audit et tests d'intrusion en laboratoire | **Cœur** | Audit et tests d'intrusion : seule séance sur l'audit en laboratoire. |
| S15 | Réponse à incident et investigation | **Cœur** | Réponse à incident : prérequis de S16. |
| S16 | Continuité d'activité face à une cyberattaque | **Cœur** | Continuité face à une cyberattaque : seule séance sur ce point. |
| S17 | La sécurité dans un projet d'infrastructure | **Cœur** | Sécurité dans un projet d'infrastructure : seule séance sur ce point (B3.5A) ; prépare l'étude de cas. |
| S18 | Méthode de l'étude de cas pour l'épreuve E7 | **Cœur** | Méthode de l'étude de cas E7 : prépare directement l'épreuve. |
| S19 | Épreuve blanche E7 | **Cœur** | Épreuve blanche E7. |

## Les compétences restent couvertes

Compétences travaillées par les séances cœur (S01, séance de révision, S18 et S19, qui entraînent à toutes, ne sont pas comptées) :

| Compétence | Séances cœur | Nombre |
|---|---|---|
| B3.1 | S04, S15 | 2 |
| B3.2 | S04, S09 | 2 |
| B3.3 | S03, S06, S10 | 3 |
| B3.4 | S02, S03, S05, S09, S10, S11, S12, S13, S14, S15, S16, S17 | 12 |
| B3.5A | S02, S05, S06, S10, S11, S12, S13, S14, S15, S16, S17 | 11 |

## Si l'on saute un complément

- **S07 – 802.1X, RADIUS et Wi-Fi.** S17 ne cite l'authentification des équipements que comme exemple de mesure. Donner à lire le cours et l'aide-mémoire (environ 1 h) pour garder les trois rôles de 802.1X et le principe d'un Wi-Fi d'entreprise.
- **S08 – Reverse proxy, TLS et OWASP.** S11 et S12 prennent les journaux du reverse proxy comme exemple, et S17 vérifie la version de TLS. Donner à lire le cours (environ 1 h) : le reverse proxy, le réglage de TLS et les failles d'applications.

## Pour aller plus loin si le temps manque encore

Deux compléments ne libèrent que 8 h. Au-delà, il faut alléger **à l'intérieur** des séances cœur (par exemple ne faire que certaines parties d'un TP) ou regrouper des séances. S06 (annuaire) est repris par S16 et S17 : il est le plus délicat à retirer ensuite.

## Utilisation

- Si **toutes** les séances sont faites, rien ne change.
- Si le temps manque, retirer d'abord S07 et S08 en appliquant la consigne ci-dessus.
- Les prérequis écrits dans chaque fiche ont été relus pour que ce classement ne casse aucune dépendance entre séances cœur.
