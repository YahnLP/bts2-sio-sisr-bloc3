# Corrigé – S19 : Épreuve blanche E7

*Réservé à l'enseignant.*

## Vérification

Sujet **documentaire** : aucune machine. Ont été **recalculés par ​programme** : le délai de détection, les jours de la semaine, la disponibilité, les totaux de l'annexe 6 et la somme du barème.

| Élément | Résultat |
|---|---|
| Délai entre l'accès frauduleux (mardi 6 octobre, 02 h 41) et l'appel de la stagiaire (jeudi 8 octobre, 09 h 15) | **54 h 34 min** (2 jours 6 h 34) |
| Jours | 6 octobre 2026 = mardi ; 8 octobre = jeudi ; **11 octobre = ​dimanche** |
| 99,5 % sur un mois de 30 jours | 720 h × 0,5 % = **3,6 h = 3 h 36 min** |
| Les 12 mesures | **23 000 €** et **40 jours** |
| Plan proposé : M1, M2, M3, M4, M5, M7, M8, M9 | **13 300 €** et **25 jours** |
| Reporté : M6, M10, M11, M12 | **9 700 €** et **15 jours** (13 300 + 9 700 = 23 000 ; 25 + 15 = 40) |
| Barème | 20 + 25 + 30 + 25 = **100** |

> [!WARNING]
> **À valider par l'enseignant avant de s'en servir comme évaluation :**
>
> - Le **sujet et le barème** sont une production de l'auteur, **pas un sujet officiel**. La répartition des ​points est une proposition.
> - Les **règles juridiques** (72 heures, un mois, effacement, sous-traitant) sont les règles courantes du RGPD, résumées de mémoire dans l'annexe 7. **Les durées de conservation propres aux financements de formation ne sont pas vérifiées** : le corrigé n'en donne aucune, volontairement.
> - La **qualification** « responsable de traitement » pour l'association est une ​hypothèse du sujet.
> - La durée à demander à l'hébergeur pour l'article 9 est une **proposition de négociation**, pas une règle.

## Remarques sur la construction du sujet

Quatre **pièges** volontaires :

1. Les **deux plafonds** (15 000 € et 25 jours) : le plan retenu atteint **exactement 25 jours**, sans marge.
2. La **liste de mesures est incomplète** : elle ne contient ni **chiffrement des ​disques** ni **segmentation du réseau**, deux faiblesses pourtant relevées dans l'annexe 2. Un bon candidat les cite en 3.5 comme risque restant ou comme mesure à ajouter.
3. **Huit autres connexions réussies** dans la même fenêtre : l'enquête ne se limite pas à un compte.
4. Le champ **handicap** : donnée de santé, qui change le ​niveau de risque.

## Dossier 1 (20 points)

**1.1 [4]** Catégories : identité et coordonnées (stagiaires et personnel), financeur, résultats d'évaluation, données de connexion, **aménagement lié au handicap**. Classement attendu : coordonnées (sensibilité moyenne), résultats et financement (moyenne à élevée), **handicap = donnée de santé, la plus sensible**. *Barème : au moins quatre catégories (1) ; ​classement justifié (2) ; donnée de santé identifiée (1).*

**1.2 [5]** Faits : conservation sans limite « au cas où » (annexe 2). Règle : une donnée ne se conserve que le temps **nécessaire à la finalité** (limitation de la conservation, minimisation). « Au cas où » n'est pas une ​finalité ; de plus, la conservation illimitée **augmente l'exposition** en cas de violation (le dossier 2 le montre). Règle proposée : conservation **active** pendant la formation et le suivi, **archivage à accès restreint** pour les obligations légales et les ​financeurs, puis **purge ou anonymisation** ; le champ handicap n'est conservé que le temps nécessaire. Mise en œuvre : **M8**. *Barème : principe (2) ; règle proposée par étapes (2) ; mise en œuvre (1).* Ne pas accepter de durées chiffrées présentées comme certaines sans source.

**1.3 [5]** Droit d'accès. ​Délai : **un mois** à compter de la réception, soit le **5 novembre** (reçue le 5 octobre), extensible dans certains cas avec information de la personne dans le mois. Points à vérifier : **identité du demandeur** (justificatif proportionné) ; **exhaustivité** (plateforme, messagerie, partages, archives, ​sauvegardes) ; **données de tiers** à ne pas divulguer ; **envoi sécurisé** (canal chiffré, secret transmis séparément). Procédure : **responsable désigné**, **registre des demandes** (date de réception, échéance, réponse), modèle de réponse. *Barème : délai (1) ; identité (1) ; exhaustivité (1) ; ​sécurité et tiers (1) ; procédure (1).*

**1.4 [6]** Faits : formation terminée depuis 4 ans, financement public (annexe 5), aucune durée définie. Règle : l'effacement n'est **pas absolu** ; il ne s'applique pas dans la mesure où la conservation est **nécessaire pour respecter une obligation légale** ou pour constater, exercer ou défendre un droit. Conséquence : ​effacer ce qui **n'est plus nécessaire** (coordonnées, résultats détaillés, éventuel champ handicap), **conserver le strict minimum** pour les justificatifs de financement **pendant la durée applicable (à vérifier)**, en **accès restreint**, puis purger. Répondre dans le **mois**, en ​expliquant **ce qui est conservé, pourquoi et jusqu'à quand**. *Barème : faits (1) ; règle (2) ; conséquence (2) ; réponse pratique (1).* Une réponse « oui, on efface tout » ou « non, on garde tout » est insuffisante.

## Dossier 2 (25 points)

**2.1 [4]** 1 480 échecs, 63 adresses, 410 identifiants différents, au plus 5 essais ​chacun, 9 réussites : ce n'est pas un classique brute force sur un compte, mais un **bourrage d'identifiants** (*credential stuffing*) : des couples identifiant/mot de passe issus de fuites ailleurs. Hypothèse : **mot de passe ​réutilisé** par c.lambert, favorisé par l'absence de blocage et de double authentification. L'hypothèse est **à confirmer** (hameçonnage non exclu). *Barème : description (1) ; type justifié par les chiffres (2) ; hypothèse prudente (1).*

**2.2 [4]** ​Chronologie : mardi 6 octobre 02 h 10 début du bourrage ; 02 h 41 accès frauduleux ; 02 h 44 export de 412 lignes ; 02 h 47 changement d'adresse (**persistance**, et empêche la récupération du compte) ; ​jeudi 8 octobre 09 h 15 **détection par un tiers** ; 09 h 40 confirmation. Délai : **54 h 34 min**. Interprétation : l'association n'a **ni supervision ni alerte** ; c'est une stagiaire victime qui a détecté ; le journal est conservé 30 jours seulement. *Barème : chronologie (1) ; calcul (1,5) ; interprétation (1,5).*

**2.3 [5]** C'est une **violation** (atteinte à la confidentialité : export par un ​tiers non autorisé). Données : nom, adresse électronique, téléphone, formation et financeur de **412 personnes**, plus le **handicap pour 38** (donnée de santé). Risque : **avéré** pour l'ensemble (SMS d'hameçonnage ciblé déjà reçu), **élevé** pour les 38 (atteinte à la vie privée, discrimination). *Barème : qualification (1) ; données (1,5) ; niveau de risque argumenté (2,5).*

**2.4 [5]** Notification à la CNIL **dans les 72 heures après la prise de connaissance** : si la prise de ​connaissance est l'appel de **jeudi 8 octobre à 09 h 15**, l'échéance est le **dimanche 11 octobre à 09 h 15** ; en pratique, **avant le vendredi soir**. Une prise de connaissance fixée à 09 h 40 (confirmation) est acceptée si elle est **justifiée** ; la prudence retient l'appel. Notification possible **en plusieurs ​temps**. Informer **les personnes**, car le risque est élevé (au moins les 38, probablement tous les 412). **Registre** des violations. Informer le **prestataire** (journaux, coopération), la **direction**. *Barème : délai et date (2) ; information des ​personnes (1) ; registre (1) ; autres acteurs (1).*

**2.5 [7]** 24 heures, dans l'ordre : (1) **contenir** : désactiver le compte, réinitialiser le mot de passe, révoquer les sessions, **rétablir l'adresse électronique** ; (2) **préserver les preuves** : demander **tout de suite** au prestataire les journaux (rétention de 30 jours) et en calculer l'empreinte ; (3) **examiner les huit ​autres connexions réussies** de la même fenêtre : origine, actions (exports ?), changements d'adresse ; **réinitialiser** ces comptes par précaution ; (4) **activer en urgence** le blocage et la limitation par adresse (**M2**) ; (5) **informer** la direction et préparer la notification. Semaine suivante : notification et information complétées ; recherche sur tous les comptes ​ciblés ; **double authentification (M1)** ; retour d'expérience. *Barème : actions des 24 h ordonnées et justifiées (4) ; huit autres connexions (1,5) ; semaine suivante (1,5).*

## Dossier 3 (30 points)

**3.1 [5]** Huit faiblesses parmi : réseau interne unique (**B3.5A**) ; deux formateurs administrateurs du domaine (**B3.2**, B3.4) ; session commune de salle avec mot de ​passe affiché (**B3.3**) ; plateforme sans double authentification ni blocage (**B3.2**) ; portables non chiffrés et gérés à la main (**B3.3**) ; NAS dans le domaine, 7 jours, jamais testé (**B3.4**) ; journaux non centralisés, 30 jours (**B3.4**) ; messagerie à mot de ​passe seul (**B3.2**) ; conservation illimitée (**B3.1**) ; absence de plan de reprise (**B3.4**) ; antivirus classique (**B3.3**). *Barème : environ 0,6 point par faiblesse avec risque et compétence.*

**3.2 [5]** ​Cause **immédiate** : compte compromis par réutilisation de mot de passe. Causes **profondes** : absence de double authentification et de blocage ; droits qui permettent à un formateur d'exporter **412 stagiaires** (moindre privilège) ; pas de sensibilisation ; pas de supervision. **Détection plus tôt** : alertes sur échecs massifs (1 480 en 45 minutes), ​connexion depuis l'étranger, export volumineux, changement d'adresse — **M3**. *Barème : cause immédiate (1) ; causes profondes (2,5) ; détection (1,5).*

**3.3 [12]** Plan **proposé** :

| Réf. | Risque réduit | Coût | Temps | Décision |
|---|---|---|---|---|
| M1 | Accès par mot de passe volé | 1 800 € | 2 j | **Faire** |
| M2 | Bourrage d'identifiants | 1 500 € | 1 j | **Faire** |
| M3 | ​Détection tardive | 3 000 € | 8 j | **Faire** |
| M4 | Compromission d'un compte à privilèges | 0 € | 3 j | **Faire** |
| M5 | Rançongiciel, perte de données | 4 200 € | 6 j | **Faire** |
| M6 | Session commune | 0 € | 5 j | **Reporter** |
| M7 | Erreurs humaines | 1 600 € | 0 j | **Faire** |
| M8 | Exposition par conservation excessive | 0 € | 3 j | **Faire** |
| M9 | Dépendance au prestataire | 1 200 € | 2 j | **Faire** |
| M10 | Assurance indépendante | 4 500 € | 2 j | **Reporter** (après les mesures) |
| M11 | Reprise après ​sinistre | 2 500 € | 5 j | **Reporter** |
| M12 | Postes | 2 700 € | 3 j | **Reporter** |
| **Retenu** | | **13 300 €** | **25 j** | |

Reste : 15 000 − 13 300 = **1 700 €** et **0 jour** de marge. Limites à citer : marge nulle de temps, donc risque de dérapage ; M5 sans M11 : sauvegarde sans plan de reprise documenté ; M6 ​reporté : en attendant, **changer et ne plus afficher** le mot de passe de la session commune (gratuit). Autre plan accepté s'il **respecte les deux plafonds**, couvre **accès, détection, sauvegarde, droits, conservation** et se **justifie**. *Barème : sélection cohérente avec les risques (4) ; calculs ​justes et plafonds vérifiés (3) ; justification de ce qui est reporté (3) ; limites (2).* Un plan qui **dépasse un plafond** perd au moins la moitié des points de la sélection.

**3.4 [4]** Exemples : **M1** : une connexion avec le bon mot de passe sans second facteur est refusée ; **M2** : après les échecs prévus, la connexion est bloquée et l'événement ​apparaît au journal ; **M3** : 20 échecs simulés produisent une alerte reçue en moins de N minutes ; **M4** : le compte d'un formateur n'ouvre pas la console d'administration du domaine ; **M5** : restauration chronométrée d'un partage depuis la ​copie hors ligne, et suppression de la copie refusée depuis un compte du domaine. *Barème : 1 par test précis, observable, avec le résultat attendu (trois tests) ; 1 pour la ​trace conservée.*

**3.5 [4]** Risques restants : **disques non chiffrés** (la liste ne propose pas de chiffrement : à signaler, souvent sans coût), **réseau interne non segmenté** (aucune mesure ​candidate), session commune, hameçonnage de la messagerie, pas de plan de reprise, marge nulle. Suivi : registre des risques avec responsable, revue ​trimestrielle, indicateurs (comptes sans second facteur, test de restauration réussi, alertes traitées), audit M10 en phase 2. *Barème : risques résiduels (2) ; suivi (2).*

## Dossier 4 (25 points)

**4.1 [8]**

| Art. | Risque | Modification ​demandée |
|---|---|---|
| 4 | 3 h 36 par mois tolérées, y compris en période critique | Engagement plus élevé ou exigences par période, pénalités |
| 6 | Sauvegarde dans le **même centre de données** : un sinistre ou une compromission détruit service et copie | Copie dans un **site distinct**, test de restauration |
| 8 | Sous-traitants dont un **hors de l'Union**, sans information : perte de maîtrise, transfert | ​Liste, **information préalable**, droit d'opposition, garanties de transfert |
| 9 | **5 jours ouvrés** : trop long face à l'obligation de notifier en 72 heures | Information **dans les meilleurs délais**, par exemple sous 24 à 48 heures *(proposition à négocier)* |
| 11 | **Format propriétaire**, 60 jours, payant : ​dépendance | Format ouvert, délai raisonnable, coût fixé, test de réversibilité |
| 12 | Aucun audit : impossible de vérifier | Droit d'audit ou rapports indépendants |

*Barème : par article, environ 1,3 point (0,7 pour le risque, 0,6 pour la modification), total arrondi à 8.*

**4.2 [6]** 720 h × 0,5 % = **3,6 h, soit 3 h 36 min par mois** (mois de 30 ​jours). Acceptable ou non : cela dépend de la **criticité** ; en période d'inscription, quelques heures d'arrêt peuvent bloquer des inscriptions, mais le contrat ne **distingue** pas les périodes. Objectifs à fixer avec la direction : **DMIA / RTO** (durée maximale de reprise) et **RPO** (perte de données maximale) ; les sauvegardes quotidiennes de l'article 6 donnent un RPO de **24 heures** au mieux. Les ​valeurs sont **décidées avec la direction**, l'élève doit justifier une proposition. *Barème : calcul (2) ; analyse de la période critique (2) ; objectifs et vocabulaire (2).*

**4.3 [3]** Sauvegarde **quotidienne** (RPO de 24 h), **14 jours** (couvre les 54 h de l'incident), mais **même centre de données** et aucun test connu. Proposition : copie dans un **site distinct** (avenant), **export ​périodique** des données vers la sauvegarde hors ligne de l'association (M5) si le format le permet, **test de restauration**. *Barème : analyse (1,5) ; proposition (1,5).*

**4.4 [8]** Note d'une page, sans jargon : **situation** (incident, 412 personnes dont 38 avec donnée de santé, détection tardive) ; **trois décisions** : (1) valider le plan **M1, M2, M3, M4, M5, M7, M8, M9** (13 300 €, 25 jours), (2) **notifier la CNIL avant dimanche 11 octobre 09 h 15** (donc avant le ​vendredi soir) et informer les personnes, (3) engager l'**avenant** avec l'hébergeur (articles 6, 8, 9, 11, 12) ; **coût** ; **non fait** : M6, M10, M11, M12 (9 700 €, 15 jours) ; **risque restant** : disques non chiffrés, réseau non segmenté, hameçonnage. *Barème : situation (1) ; trois décisions (2) ; coût (1) ; non fait (1) ; risque restant (1) ; lisibilité pour une directrice (2).*

## Pièges fréquents

- Un plan qui respecte le **budget** mais pas les **25 jours**.
- Oublier les **huit autres connexions**.
- Ne **pas calculer** la date ​limite, ou la placer un dimanche sans le relever.
- Répondre « on efface tout » à la demande B.
- Ignorer que la **donnée de santé** change le niveau de risque.
- Accepter le contrat tel quel parce que « c'est standard ».
- Une note de direction qui ne contient **aucune décision**.
