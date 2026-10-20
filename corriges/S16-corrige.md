# Corrigé – S16 : Continuité d'activité face à une cyberattaque

*Réservé à l'enseignant.*

## Vérification

Exécuté dans un laboratoire Ubuntu 24.04 de l'auteur (**restic 0.16.4**, deux comptes locaux `prod` et `sauve`) :

| Test | Résultat constaté |
|---|---|
| ​Dépôt isolé : `init`, `backup`, deuxième `backup`, `snapshots` | Deux instantanés ; le deuxième est beaucoup plus petit |
| `restic check` | `no errors were found` |
| `forget --keep-last 1 --dry-run` | Annonce qu'une version serait supprimée, sans rien supprimer |
| Compte `prod` « compromis » : `find … mv {} {}.verrou` | Fichiers de données renommés |
| `prod` supprime le dépôt **qu'il peut écrire** (`rm -rf /srv/depot-mal/*`) | **Dépôt vidé** (le message `Permission denied` visible porte sur le dossier ​parent `/srv`, appartenant à `root`, pas sur le contenu) |
| `prod` essaie de lire ou supprimer le dépôt isolé | `Permission denied` |
| `restic restore latest` puis vérification par manifeste | Fichiers restaurés conformes (0 non ​conforme) quand le manifeste est pris **après** la dernière sauvegarde |
| `chattr +i` sur une archive : suppression par son propriétaire | `Operation not permitted` |

**Mesures de temps** (20 fichiers de 300 ko et 10 petits fichiers, environ 6 Mo, ou 60 fichiers pour 19 Mo lors d'un essai antérieur) : restauration en **moins d'une seconde**. Ces durées sont **sans valeur** pour une extrapolation (mémoire cache, petit volume, machine ​locale) : c'est le sujet de la partie F, et il faut le **faire constater** aux élèves.

**Essai négatif à connaître** : un `chattr -R +a` sur **tout** le dépôt `restic` **bloque** l'outil (`rename … operation not permitted` sur les verrous, puis sur les fichiers de données) ; limité à `data`, `index` et `snapshots`, il ​bloque encore les écritures (`rename` des fichiers temporaires). Cette approche est **écartée** du TP et signalée par un avertissement.

**Non vérifié** : le TP sur **Debian 12**, dont le paquet `restic` est plus ancien (autour de la 0.14) ; le comportement de `forget --prune` réel ; une **vraie machine de sauvegarde séparée** (SSH, administration hors annuaire) ; le serveur de dépôt « ajout seulement » et le stockage à verrouillage d'objet, **décrits** mais non ​testés ; les durées sur des volumes réalistes. Le paragraphe « 3-2-1 renforcé » reprend une pratique courante et non une norme précise : à citer comme **recommandation usuelle**.

## Partie A

Perte maximale avec la sauvegarde actuelle : **une journée de travail** (copie de nuit), un mardi à 10 h : tout ce qui a été fait depuis la nuit ​précédente, soit plusieurs heures. L'atelier peut s'arrêter si les programmes de découpe sont sur le serveur ou les PC de commande (S02).

Tableau (exemples, **à argumenter**, pas de valeur unique) :

| Activité | DMIA | PDMA | RTO | RPO |
|---|---|---|---|---|
| Bureau d'études | 2 à 3 jours | 1 journée | 1 jour | 24 h |
| Comptabilité et paie | 1 semaine (hors échéances) | 1 journée | 2 jours | 24 h |
| Atelier (programmes) | **Quelques ​heures** (production à l'arrêt) | 1 journée | 4 h | 24 h ou moins |
| Messagerie | 1 jour | Négligeable (hébergée) | 1 jour | Sans objet |

Ce qui compte : une **justification par l'impact** (S02), des valeurs **cohérentes** (RTO ≤ DMIA, RPO ≤ PDMA), et l'idée que la **direction décide**. Un RPO d'une heure coûte plus cher parce qu'il faut sauvegarder **plus souvent** (ou répliquer en continu), avec **plus de stockage, de bande passante et d'exploitation**.

## Partie B

Droits `750` : propriétaire `prod` (lecture, écriture, accès), groupe `sauve` (lecture, accès), **autres rien** : `sauve` **lit** les données ; `700` sur `/srv/sauvegarde` : **seul `sauve`** y accède : `prod` ne **lit** donc **rien** et **ne peut rien ​supprimer** de la sauvegarde.

## Partie C

- Deux instantanés ; la deuxième sauvegarde est **plus petite** (restic ne stocke que les **différences**).
- **Plusieurs versions** permettent de remonter **avant** la compromission (ou avant le chiffrement d'un fichier : une sauvegarde nocturne **écrasée** par une version chiffrée n'est plus saine). La **rétention** (nombre de versions, durée) détermine jusqu'où on remonte : elle doit dépasser le **temps de présence** de l'attaquant (S15 : ​environ 52 heures).

## Partie D

| Sauvegarde | Détruite ? | Message | Pourquoi |
|---|---|---|---|
| `/srv/depot-mal` | **Oui** (dépôt vidé) | Aucun (la suppression réussit) | Le compte `prod` **a les droits d'écriture** : l'attaquant **hérite** des droits du compte ​compromis |
| `/srv/sauvegarde/depot` | **Non** | `Permission denied` | Propriété d'un **autre compte**, mode `700` : le compte compromis n'a **aucun droit** dessus |

Faiblesses du NAS de l'Atelier Verdier : **accessible depuis la production** (monté ou joignable avec des droits suffisants), **identifiants d'administration par défaut** (S13, S15), **non isolé**, **jamais testé**.

## Partie E

Restauration conforme : **0** fichier non conforme. Un fichier non conforme apparaît **uniquement** si le manifeste a été pris **avant** une modification suivie d'une nouvelle ​sauvegarde (piège rencontré lors de la mise au point) : il faut le prendre **après la dernière sauvegarde**.

Fiabilité de l'empreinte : elle détecte **tout** écart, même d'un octet ; ouvrir quelques fichiers ne prouve rien sur les autres. **Avant la remise en service** : éradiquer la cause, changer les ​secrets, vérifier un réseau isolé (S15 et cours, partie 3).

## Partie F

L'extrapolation est **optimiste** : petit volume, **cache**, absence de réseau, de disques lents, de gros fichiers nombreux ; on peut la comparer à un essai d'un volume plus grand pour le montrer. Attendre une **estimation prudente** (par ​exemple le calcul brut multiplié par un facteur et complété d'une demi-journée à plusieurs jours de reconstruction et de vérification) **argumentée**, jamais une valeur unique.

Compatibilité avec la DMIA : si l'estimation dépasse la DMIA, solutions : **copie locale supplémentaire** (restauration rapide), **restauration par priorité** (programmes de découpe d'abord), **PCA** (machines de secours, travail dégradé).

**Ordre de reprise ​attendu** (argumenté ; un autre ordre justifié est accepté) : 1. accès distant **fermé** et réseau **sûr** (sinon on restaure dans une maison ouverte) ; 2. serveur de fichiers (plans et programmes) ; 3. PC des machines à commande numérique (production, **isolés** : S13) ; 4. poste de la comptable (reconstruit, **pas** réutilisé) ; 5. messagerie (hébergée, peu de restauration) ; 6. NAS (reconstruit avec une conception corrigée **avant** la ​prochaine sauvegarde).

## Partie G

1. **Oui** : `root` peut faire `chattr -i` : l'attribut protège d'un compte ordinaire, **pas** d'un attaquant administrateur ; la dernière commande le montre.
2. Une **machine séparée** (administration indépendante), une copie **hors ligne** (physiquement déconnectée) ou un **stockage verrouillé** (même un administrateur ne peut pas supprimer avant l'échéance) ​retirent à l'attaquant **la possibilité d'atteindre** la copie avec les droits qu'il a obtenus.
3. Recommandation (à argumenter) : au moins une copie **hors ligne** (disque rotatif ou support déconnecté) **plus** une copie **hors site** ; **test de restauration** complet au moins annuel, **vérification** automatique à chaque sauvegarde ; coût d'un disque externe ou d'un ​service de sauvegarde en ligne **sans prix précis** (à demander en devis).

## Pièges fréquents

- Croire qu'**une sauvegarde sur un partage** protège d'un rançongiciel.
- **Ne jamais tester** la restauration.
- Rétention **trop courte** par rapport au délai de détection.
- Restaurer **avant d'éradiquer**.
- Extrapoler un **débit mesuré sur un ​petit volume**.
- **Perdre le mot de passe** du dépôt.
- Confondre **DMIA** (limite métier) et **RTO** (objectif technique).
