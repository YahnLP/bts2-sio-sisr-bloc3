# Cours – La méthode de l'étude de cas pour l'épreuve E7

*BTS SIO SISR 2e année – Bloc 3 – S18*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

Tu connais désormais les notions : risques, droit, filtrage, annuaire, services, journaux, vulnérabilités, incident, reprise, projet. L'épreuve **E7** ne demande pas de les réciter : elle demande de les **appliquer à une organisation que tu ne connais pas**, en **quatre heures**, **par écrit**. Cette séance apprend la **méthode**. Le format officiel est décrit dans la page [L'épreuve E7](../../ressources/epreuve-e7.md), à relire sur les textes officiels.

---

## 1. Ce que le correcteur cherche

Les critères d'évaluation sont les **critères de performance** des compétences du bloc (page [Référentiel](../../ressources/referentiel.md)). Concrètement, une bonne copie :

| Qualité | Signe |
|---|---|
| **Elle s'appuie sur le dossier** | Elle cite les faits : « d'après l'annexe 2, le serveur de fichiers… » |
| **Elle identifie le bon problème** | Elle répond à la question posée, pas à une question voisine |
| **Elle propose des mesures adaptées** | Au **budget**, à la **taille**, aux **compétences** de l'organisation |
| **Elle argumente** | Risque, mesure, justification, **limite** |
| **Elle applique le droit** | Elle qualifie, cite la règle, en déduit une obligation (sans inventer d'article) |
| **Elle communique** | Phrases courtes, tableaux utiles, sans jargon inutile |

> [!WARNING]
> **Une réponse de cours est une réponse faible.** « Il faut un pare-feu » est vrai partout ; « le réseau de l'atelier est plat (annexe 2) : la machine de commande sous Windows 7 peut joindre le serveur de fichiers ; on la place dans une zone dédiée avec un seul flux autorisé vers le serveur de programmes » **prouve** que tu as lu le dossier.

---

## 2. Gérer les quatre heures

| Temps | Activité | Détail |
|---|---|---|
| **0 h 00 – 0 h 20** | **Lire tout le sujet** | Dossiers de questions d'abord, puis dossier documentaire, en surlignant |
| **0 h 20 – 0 h 35** | **Fiche des faits** | Une page : organisation, chiffres, budget, outils, incidents, obligations |
| **0 h 35 – 3 h 20** | **Répondre**, dossier par dossier | Temps réparti **proportionnellement aux points** |
| **3 h 20 – 3 h 50** | **Compléter** | Questions sautées, justifications |
| **3 h 50 – 4 h 00** | **Relire** | Une réponse par question ; sources citées |

Si le barème est donné, **répartis le temps selon les points** : une question à 2 points ne mérite pas 20 minutes. Une question **bloquée** se laisse **cinq minutes** : on passe, on revient.

### Lire le dossier : la fiche des faits

| Rubrique | À relever |
|---|---|
| **Organisation** | Activité, taille, sites, métiers, **valeurs métier** |
| **Système d'information** | Réseau, serveurs, postes, services, hébergement externalisé |
| **Données** | Quelles données, **qui** les traite, **où** |
| **Moyens** | Budget, personnel, compétences, délais |
| **Événements** | Incidents, alertes, demandes de clients |
| **Obligations** | Contrats, réglementation, secteurs |
| **Incohérences ou pièges** | Un chiffre qui contredit un autre, un point volontairement flou |

Un dossier contient souvent des **faits sans rapport** avec les questions (distracteurs) et des **faits cachés** dans une annexe qu'on n'aurait pas pensé à lire.

---

## 3. Répondre : le schéma en quatre temps

Pour chaque proposition :

| Temps | Question | Exemple |
|---|---|---|
| **Risque** | Qu'est-ce qui peut mal tourner, pour quelle valeur ? | « Un attaquant peut ouvrir une session sur le poste de la comptable depuis Internet » |
| **Mesure** | Que fait-on, **précisément** ? | « Fermer la redirection du port 3389 ; accès par VPN avec double authentification » |
| **Justification** | Pourquoi **celle-là**, dans **ce** contexte ? | « Les deux commerciaux travaillent à distance (annexe 2) ; coût faible ; réponse au vecteur d'entrée » |
| **Limite** | Qu'est-ce qui **reste** ? | « Ne protège pas d'un poste personnel infecté ; prévoir aussi la sensibilisation » |

Ce schéma remplace les listes : **trois propositions complètes** valent mieux que **dix** réduites à un mot.

### Types de questions et réponses attendues

| La question dit… | Tu fais… |
|---|---|
| **Identifier** | Relever dans le dossier, **citer** |
| **Analyser** | Relier faits et risques, hiérarchiser |
| **Proposer** | Mesure **précise**, adaptée au contexte |
| **Justifier** | Argument **lié au dossier** (coût, taille, risque) |
| **Comparer** | Un **tableau** : critères, avantages, limites, choix argumenté |
| **Qualifier juridiquement** | Les **faits**, la **règle**, la **conséquence** |
| **Rédiger une note** | Destinataire, objet, faits, décisions, ton adapté |
| **Chiffrer** | Calcul **visible**, unités, hypothèses |

### Le cadre juridique en réponse

Trois temps : **les faits** (« des données de salariés, dossier RH, ont été exposées »), **la règle** (« violation de données à caractère personnel : notification à la CNIL sous 72 heures si risque, séance S04 »), **la conséquence** (« le dirigeant doit notifier ; documenter ; informer les personnes si le risque est élevé »). Ne cite **jamais** un numéro d'article dont tu n'es pas sûr : une règle **bien expliquée** vaut plus qu'un numéro faux.

---

## 4. Les erreurs fréquentes

| Erreur | Remède |
|---|---|
| **Répondre hors dossier** | Une citation du dossier par réponse |
| **Lister sans argumenter** | Risque, mesure, justification, limite |
| **Mesure impossible** (budget, temps) | Relire les moyens ; proposer par **phases** |
| **Oublier la question** | Souligner le **verbe** de la question |
| **Sigles non expliqués** | Les développer à la première occurrence |
| **Copie illisible** | Titres, numéros de questions, tableaux |
| **Négliger l'humain** | Formation, procédures, gouvernance : pas que la technique |
| **Inventer des chiffres** | Utiliser ceux du dossier ; signaler une **hypothèse** |
| **Ne pas finir** | Gérer le temps ; mieux vaut un plan court de chaque question |

---

## 5. Vérifier sa copie en dix minutes

- [ ] Chaque question a une **réponse** ?
- [ ] Chaque réponse **cite le dossier** ?
- [ ] Les mesures sont **précises** et **adaptées au budget** ?
- [ ] Les propositions importantes ont une **limite** ?
- [ ] Les **obligations juridiques** sont reliées aux faits ?
- [ ] Les **calculs** sont refaits ?
- [ ] La note finale est lisible par un **non-informaticien** ?

**Test flash.** Question : « Proposez des mesures pour réduire le risque de rançongiciel. » Réponse d'un élève : « Mettre un antivirus, un pare-feu et sauvegarder. » Que lui manque-t-il ?

<details markdown="1">
<summary>Voir la réponse</summary>

Tout ce qui fait la **note** : aucune **citation du dossier**, aucune mesure **précise** (quel type de sauvegarde, où, testée comment ?), aucune **justification** liée au contexte (budget, taille, ce qui a déjà été vu dans l'annexe), aucune **limite**. Une bonne réponse prend **trois** mesures, chacune en **quatre temps**, et les **priorise**.

</details>
