# Corrigé – S10 : Durcissement, conformité et correctifs

*Réservé à l'enseignant.*

## Vérification

Exécuté dans un laboratoire Ubuntu 24.04 de l'auteur (Lynis 3.0.9) :

| Test | Résultat constaté |
|---|---|
| `lynis audit system --quick --no-colors` | Environ une minute ; rapport dans `/var/log/lynis-report.dat` |
| Mesure de départ | Indice **60**, 48 suggestions |
| Après `UMASK 027`, `PASS_MAX_DAYS 90`, `PASS_MIN_DAYS 1`, installation de `debsums` et `apt-show-versions` | Indice **63**, 43 suggestions ; les suggestions `AUTH-9328`, `AUTH-9286`, `PKGS-7370`, `PKGS-7394` ont disparu |
| `lynis show details IDENTIFIANT` | Fonctionne, à condition que l'audit n'ait pas été lancé avec `--no-log` |
| `apt-get -s upgrade` | Simule sans rien installer |

> [!WARNING]
> **Les chiffres (60, 63, 48, 43) sont propres à la machine de l'auteur** et ne seront pas ceux des élèves. Seules la **tendance** (l'indice augmente, les suggestions traitées disparaissent) et les identifiants de test cités sont à attendre. Les identifiants et la liste des suggestions dépendent de la version de Lynis et de la distribution.

**Non vérifié** : le comportement exact sur une **Debian** de la salle (le test a été fait sous Ubuntu) ; la version de Lynis proposée par le dépôt Debian de la salle (plus ancienne, ses tests peuvent différer) ; l'effet de `chage` sur un compte existant (commande standard, non rejouée).

## Partie A

Réponses attendues, à titre d'exemples : politique de mots de passe, droits par défaut, absence d'outils de vérification d'intégrité, pare-feu non actif ou non configuré, services inutiles, journalisation non centralisée, mises à jour en attente.

**Un score qui monte** n'implique pas que la sécurité s'améliore : il mesure la **proportion de tests réussis**, pas leur gravité (voir le test flash du cours).

## Partie B

Valeurs propres à chaque machine. Vérifier que l'élève :

- relève bien trois valeurs distinctes (indice, avertissements, suggestions) ;
- ne confond pas **avertissement** (à traiter en priorité) et **suggestion**.

## Partie C

Attendu : au moins six lignes avec **gravité** (échelle 1–4 de la séance S02), **effort** et **effet de bord** réellement renseignés, et une **décision** parmi corriger, planifier, accepter.

Exemples d'**effets de bord** à faire trouver :

| Suggestion | Effet de bord possible |
|---|---|
| Âge maximal des mots de passe | Mots de passe affaiblis par des changements « mécaniques » (`Motdepasse1`, `Motdepasse2`) ; comptes de service qui expirent |
| `UMASK 027` | Un service qui crée des fichiers lus par un autre compte ne les lira plus |
| Désactiver un service | Application qui en dépend |
| Règles de pare-feu | Coupure d'un accès d'administration |

**Exemple de suggestion inutile ou dangereuse** : une suggestion qui concerne un composant **absent ou non utilisé** sur la machine, ou qui casserait l'application. Toute réponse **argumentée** est acceptée.

## Partie D

- D1 : `grep UMASK` affiche `027` après correction ; effet sur les **nouvelles** sessions.
- D2 : valeurs de laboratoire. **Point à faire remarquer** : se référer à la politique de mots de passe de la séance S06, qui peut ne **pas** imposer de changement périodique. La suggestion de l'outil n'est pas une obligation.
- D3 : `debsums -s` sans affichage = aucun fichier de paquet modifié. Si une ligne apparaît, l'élève doit **expliquer** si la modification est légitime (configuration modifiée volontairement) ou à investiguer.
- D4 : attendre **commande, fichier, test et retour arrière**. Sans retour arrière documenté, la correction est incomplète.

## Partie E

Attendu : l'indice **augmente** (même légèrement) et les suggestions traitées **disparaissent**. Si l'indice n'a pas bougé, chercher : audit relancé dans la même session sans effet (`umask`), mauvais fichier modifié, test non concerné.

La réponse à la dernière question doit faire apparaître que **trois petites corrections** font moins progresser la sécurité réelle qu'une seule correction grave : ce n'est pas l'indice qui mesure la gravité.

## Partie F

**F1** : le registre doit comporter, pour chaque ligne, une **mesure compensatoire** et une **date de revue**. Un écart sans date de revue n'est pas « géré », il est oublié.

**F2** : dépend de la machine. Vérifier que l'élève distingue **simuler** (`-s`) et **appliquer**, et qu'il repère l'origine des paquets (dépôt de sécurité ou non).

**F3 : éléments d'un bon processus pour l'Atelier Verdier** :

| Étape | Proposition |
|---|---|
| Inventaire | Liste des postes et serveurs avec système et version |
| Alertes | Éditeurs, CERT-FR, distribution |
| Évaluation | Concerné ? exposé ? exploité ? |
| Test | Un poste pilote avant la vague générale |
| Déploiement | Hors heures de production, par vagues |
| Vérification | Contrôle que le correctif est actif et que les logiciels métier fonctionnent |
| Trace | Registre des correctifs et des exceptions |
| Retour arrière | Instantané ou sauvegarde avant application |

**Windows 7** : plus de correctifs de sécurité. Trois réponses acceptables, de la meilleure à la moins bonne : **migrer** ; à défaut, **isoler** dans une zone dédiée avec flux minimaux (séance S05), sans accès à Internet ni messagerie ; en dernier recours, **accepter le risque par écrit**, avec responsable et date de revue. Dans tous les cas, le sujet est **présenté à la direction**.

## Pièges fréquents

- Rechercher le **score maximal** au lieu de trier.
- Appliquer une suggestion **sans la comprendre** (`show details`).
- Modifier `login.defs` et croire que **les comptes existants** sont concernés.
- Appliquer une mise à jour **sans instantané** ni retour arrière.
- Oublier le **redémarrage** après une mise à jour du noyau.
- Laisser un écart accepté **sans date de revue**.
- Confondre audit de **conformité** (Lynis) et recherche de **vulnérabilités** (séance S13).
