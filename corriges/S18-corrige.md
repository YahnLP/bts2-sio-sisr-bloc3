# Corrigé – S18 : Méthode de l'étude de cas E7

*Réservé à l'enseignant.*

## Vérification

TP **documentaire** : aucune machine. Les calculs de l'annexe 5 ont été **recalculés par programme** :

| Ensemble | Coût ​première année | Temps technicien |
|---|---|---|
| Les dix mesures T1 à T10 | **4 654 €** | **14 jours** |
| Plan proposé : T1, T2, T3, T4, T5, T7, T8 | **1 650 €** | **10 jours** |
| Reste (phase 2) : T6, T9, T10 | **3 004 €** | **4 jours** |

**Le piège du sujet** : le **budget** (6 000 €) n'est **pas** le facteur limitant (tout coûte 4 654 €) ; c'est le **temps** (14 jours demandés pour 10 disponibles). Un élève qui ne compare qu'au budget conclut « tout est ​possible » : c'est la faute à relever.

> [!WARNING]
> Les prix et les durées sont **fictifs**. Les **points juridiques** (délais, qualification responsable de traitement ou sous-traitant) reflètent les règles courantes du RGPD (articles 33 et 34) ; ils sont **à valider** par l'enseignant avant utilisation en évaluation, et la qualification exacte d'un cabinet comptable dépend des prestations (non vérifiée ici).

## Fiche des faits (modèle)

| ​Rubrique | Faits |
|---|---|
| Organisation | Cabinet comptable de 14 personnes, 220 clients, **paie**, secret professionnel, pic d'activité avril-juin (A1) |
| SI | Serveur Linux dans un placard, dossier `Clients` ouvert à tous, comptes génériques `stagiaire1/2` ; 12 portables non chiffrés, mises à jour à la main ; réseau et Wi-Fi uniques, mot de passe ​partagé avec les visiteurs ; VPN à compte unique inchangé depuis 4 ans ; messagerie sans double authentification ; sauvegarde sur disque branché en permanence ; aucune supervision (A2) |
| Données | Dossiers clients, **fiches de paie**, coordonnées bancaires : ​sensibilité **élevée** (A1, A3) |
| Moyens | 6 000 € ; 10 jours de technicien avant avril ; associés motivés (A4) |
| Événements | 14 mars : portable perdu, 40 clients, disque non chiffré ; 2 avril : demande écrite de garanties ; hameçonnage cliqué, **non signalé** (A3) |
| Obligations | RGPD (violation, délais), secret professionnel, ​relation client (sous-traitance) |
| Pièges | « Il y a un mot de passe » ; le **temps**, pas le budget, est le plafond ; la violation date du 14 mars (délais probablement dépassés au 2 avril) ; l'hameçonnage non signalé peut avoir compromis un compte de messagerie |

## Partie A2 – Répartition

Pour 20/25/30/25 points sur 200 minutes, avec 2 minutes par point : **40, 50, 60 et 50 minutes**. ​Accepter toute répartition **proportionnelle** et justifiée.

## Dossier 1

**1.1** Données : dossiers de **40 clients**, dont **fiches de paie** (salaires, identité, numéro de sécurité sociale si présent : à confirmer) et **coordonnées bancaires** (A3). Sensibilité élevée : elles permettent l'usurpation et la fraude ; ce ne sont pas des « données sensibles » au sens strict de l'article 9 sauf mention ​particulière, mais leur compromission est **grave**.

**1.2** Trois temps :

1. **Faits** : portable perdu, disque **non chiffré** (A2), seule la session est protégée par mot de passe.
2. **Règle** : une violation est une atteinte à la **confidentialité, l'intégrité ou la disponibilité** de données personnelles (RGPD, article 4). Le mot de passe de session **ne protège pas un disque non ​chiffré** : on lit le disque en le retirant ou en démarrant un autre système.
3. **Conséquence** : c'est une **violation** (perte de confidentialité probable). À documenter dans le **registre des violations** ; **notification** à la CNIL **dans les 72 heures** après en avoir pris connaissance, sauf risque improbable pour les personnes (article 33) ; **information des personnes** si le risque est ​élevé (article 34). Ici, aucun signalement n'a été fait : le délai est probablement **dépassé** au 2 avril. Il faut le dire, notifier **sans attendre** en expliquant le retard.

**1.3** Distinguer :

| Données | Rôle du cabinet | Obligation |
|---|---|---|
| Celles du **cabinet** (salariés, associés) | Responsable de traitement | Notifier la CNIL, informer les ​personnes si risque élevé |
| Celles des **clients** (paie de leurs salariés) | Souvent **sous-traitant** (agit sur instruction) : à valider | Informer **chaque client sans délai injustifié** pour qu'il décide de notifier ; aider le client (article 28 et 33.2) |

Rappeler aussi le **secret professionnel** et le contrat de sous-traitance.

**1.4** Trois mesures ​acceptables, avec le schéma en quatre temps :

| Mesure | Risque | Justification | Limite |
|---|---|---|---|
| **T1** chiffrer les 12 portables | Lecture des données en cas de perte (A3) | Coût nul, 2 jours | Perte de la clé de récupération : la conserver à part |
| **Limiter les copies locales** de dossiers sur les portables | ​Données qui voyagent | Le serveur reste la source | Gêne en déplacement : prévoir le VPN |
| **T2** VPN nominatif avec double authentification | Accès à distance volé | Comptes nominatifs, traçabilité | Coût de 240 €, formation |
| **T7** sensibilisation | Erreurs humaines (hameçonnage) | 900 €, sans ​temps technicien | Effet qui s'érode : à refaire |

**1.5** Le message : sobre, factuel, **sans minimiser ni promettre l'impossible**. À attendre : reconnaître l'incident (portable perdu, 40 dossiers), dire ce qui a été **établi** et ce qui reste à établir, annoncer les **mesures engagées avec un calendrier** (chiffrement, comptes nominatifs, double ​authentification, droits), indiquer l'interlocuteur. **Refuser** une phrase comme « vos données sont totalement sécurisées ».

## Dossier 2

**2.1** Classement possible :

| Rang | Faiblesse (annexe) | Risque | Valeur métier |
|---|---|---|---|
| 1 | `Clients` ouvert à tous, comptes génériques (A2) | Accès excessif, aucune traçabilité | Secret ​professionnel |
| 2 | VPN à compte unique, mot de passe de 4 ans (A2) | Intrusion à distance, comme à l'Atelier Verdier | Confidentialité, continuité |
| 3 | Sauvegarde branchée en permanence (A2) | Chiffrée avec le reste par un rançongiciel | Continuité |
| 4 | Portables non ​chiffrés, mises à jour à la main (A2, A3) | Perte, faille non corrigée | Confidentialité |
| 5 | Wi-Fi unique partagé avec les visiteurs, réseau plat (A2) | Un visiteur atteint le serveur | Confidentialité |

Accepter aussi la messagerie sans double authentification et l'absence de supervision, si le **classement est ​argumenté**.

**2.2** Risque : n'importe quel salarié (ou ancien salarié) connaît le mot de passe ; on ne sait **pas qui** s'est connecté (séance S11) ; quatre ans sans changement ; pas de second facteur. Parallèle avec l'Atelier Verdier : **un accès distant mal protégé est une porte d'entrée**. Mesure : **T2** (comptes nominatifs, double authentification), ​journalisation des connexions, désactivation du compte unique après bascule. Limite : un second facteur ne protège pas d'un poste infecté.

**2.3** Constat : ​disque **branché en permanence** → un rançongiciel le chiffre avec le reste, du lundi au vendredi ; copie **hebdomadaire** → jusqu'à 7 jours de perte pendant le pic (RPO élevé) ; disque **non chiffré** et transporté → perte ou vol ; aucun **test de restauration** mentionné. Point **positif** : l'emport hors du cabinet ​protège d'un incendie ou d'un vol sur place, mais seulement une partie de la semaine. Stratégie : **T3** (deux disques en rotation, hors ligne, plus une copie en ligne chiffrée), fréquence ​quotidienne pour la copie en ligne, **test de restauration** trimestriel, chiffrement des disques, rétention supérieure au temps de présence possible d'un attaquant (S15).

**2.4** Plan chiffré : **T1, T2, T3, T4, T5, T7, T8 = 1 650 € et 10 jours**.

| Réf. | Coût | Temps | Décision |
|---|---|---|---|
| T1 | 0 € | 2 j | **Faire** (cause de l'incident) |
| T2 | 240 € | 1 j | **Faire** |
| T3 | 510 € | 2 j | **Faire** |
| T4 | 0 € | 3 j | **Faire** (secret professionnel) |
| T5 | 0 € | 1 j | **Faire** |
| T6 | 504 € | 1 j | **Phase 2** (plafond de temps) |
| T7 | 900 € | 0 j | **Faire** (n'utilise pas le ​temps du technicien) |
| T8 | 0 € | 1 j | **Faire** |
| T9 | 2 500 € | 1 j | **Phase 2**, après le pic, une fois les mesures en place |
| T10 | 0 € | 2 j | **Phase 2** : en attendant, mises à jour manuelles contrôlées |
| **Retenu** | **1 650 €** | **10 j** | |

Budget restant : 6 000 − 1 650 = **4 350 €** ; la phase 2 (T6, T9, T10) coûte 3 004 € et 4 jours. Une autre répartition est acceptée si le plafond de **10 jours** est respecté et justifié. Pièges : dépasser les 10 jours ; ne raisonner qu'avec le ​budget ; ne pas dire ce qu'on écarte.

**Limites à citer** : l'audit (T9) donnerait une assurance indépendante mais coûte le plus cher ; sans T10, un portable peut rester non corrigé ; le risque d'hameçonnage ne disparaît pas (sensibilisation + double authentification le réduisent).

**2.5** Exemples de recettes : **T1** : le disque d'un portable monté sur une autre machine est **illisible** ; **T2** : l'ancien compte est refusé, un compte ​nominatif avec second facteur réussit, le journal affiche le **nom** ; **T3** : restauration d'un fichier depuis chaque copie, **chronométrée**, et tentative de suppression de la copie depuis le serveur : refusée ; **T4** : un compte d'un autre groupe ne peut pas ouvrir un dossier client.

## Partie D – Note aux associés (modèle)

**Trois risques** : accès de tout le personnel aux ​dossiers clients, accès à distance par un compte partagé, sauvegarde atteignable par un rançongiciel. **Décisions cette semaine** : valider le plan (1 650 €, 10 jours), désigner un ​responsable, **déclarer l'incident du 14 mars** et prévenir les clients concernés. **Ce qu'on ne fait pas maintenant** : audit externe, gestionnaire de mots de passe, mises à jour centralisées (3 004 € et 4 jours, après le pic). **Risque restant** : ​hameçonnage et mises à jour manuelles tant que la phase 2 n'est pas faite.

## Pièges fréquents

- Comparer seulement au **budget** et oublier le **temps**.
- « Il y a un mot de passe » accepté comme protection.
- Ne pas voir que les **délais de ​notification** sont déjà dépassés.
- Qualifier le cabinet de responsable de traitement **partout** sans nuance.
- Une note aux associés pleine de **jargon**.
- Un total faux (**vérifier : 1 650 €, 10 jours**).
