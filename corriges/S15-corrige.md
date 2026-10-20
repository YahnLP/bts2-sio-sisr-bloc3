# Corrigé – S15 : Réponse à incident et investigation

*Réservé à l'enseignant.*

## Vérification

Les trois journaux sont **fictifs**, **générés** par un script de l'auteur : 205 ​lignes d'authentification (dont **173 échecs RDP** depuis `203.0.113.77`, un seul succès), 10 lignes de pare-feu, 422 lignes de fichiers (**420 renommages**). Commandes **exécutées** et vérifiées : `grep | sort | uniq -c`, fusion par `sort`, `sha256sum` puis `sha256sum -c` (détection d'une altération : `FAILED`). **Non vérifié** : le TP sur une **Debian** de la salle (les commandes sont celles de GNU/coreutils) ; la conformité au ​guide de l'ANSSI sur les rançongiciels (consulter la **version à jour**) ; les montants et délais juridiques (notification **sous 72 h**, rappel de la séance S04, à faire valider par un juriste). Aucune donnée réelle : adresses de documentation (`203.0.113.x`, `198.51.100.x`).

## Partie A

Cinq gestes attendus, dans l'ordre : noter l'heure et photographier ; **isoler du réseau** ; ne rien effacer ; **alerter** la direction et le ​prestataire ; **préserver** journaux et sauvegardes ; (changer les mots de passe depuis une machine saine).

**Éteindre le serveur** : avantages : le chiffrement en cours s'arrête ; inconvénients : **perte de la mémoire** (traces, clé éventuelle), possibles dégâts de l'arrêt brutal. Mais ici les journaux montrent que le chiffrement s'est **terminé dimanche ​matin** : l'urgence n'est pas l'arrêt, c'est l'**isolement** et la **préservation**. Décision : **la direction, avec** l'avis du prestataire compétent, pas le seul responsable administratif.

## Partie B

- B1 : `sha256sum -c` lit les **chemins** écrits dans `empreintes.sha256` (`originaux/...`) : lancé depuis `copies/`, il ne trouve pas les fichiers. Pour vérifier les copies : `sha256sum copies/*.log | sed 's#copies/#originaux/#' | diff - empreintes.sha256` (aucune sortie = ​conforme).
- B2 : la commande signale **`pare-feu.log`** ; un seul octet modifié change **totalement** l'empreinte.
- B3 : l'empreinte doit être rangée **à part** : dans le même dossier modifiable, un attaquant (ou une erreur) pourrait **modifier le fichier et recalculer l'empreinte** : elle ne prouverait plus rien.

## Partie C

C1 : adresse dominante : **`203.0.113.77`** (173 échecs, du samedi 3 h 12 à 3 h 41). Les deux échecs isolés (`192.168.1.22` et `192.168.1.21`, suivis d'un succès ​quelques secondes après) sont des **fautes de frappe** légitimes : vrai négatif.

Chronologie attendue :

| Heure | Source | Événement | Interprétation | Certitude |
|---|---|---|---|---|
| Sam. 03:12:03 | pare-feu | Premier flux `203.0.113.77` → `192.168.1.20:3389` | Début de l'attaque | Établi |
| 03:12 → 03:41 | authentification | 173 ​échecs RDP depuis cette adresse | Force brute (essais de comptes) | Établi |
| 03:41:22 | authentification | Succès `comptable` depuis `203.0.113.77` | **Entrée** : mot de passe du compte `comptable` trouvé | Établi (l'hypothèse « trouvé par force ​brute » est vraisemblable) |
| 03:55:10 | authentification | Création de `svc-maint` (groupe Administrateurs) par `comptable` | **Persistance** | Établi |
| 03:58:31 | authentification | Arrêt de l'antivirus par `svc-maint` | Neutralisation d'une protection | Établi |
| 04:10:02 | authentification | `svc-maint` se connecte au serveur de fichiers depuis `192.168.1.20` | **Rebond** interne | Établi |
| 04:12:47 | authentification | Arrêt de la copie instantanée | **Empêche la reprise** | Établi |
| 04:30:15 / 04:33:50 | authentification | Connexion `admin` au NAS ; ​suppression de **14 sauvegardes** | **Empêche la reprise** ; compte par défaut | Établi |
| 04:45:12-13 | pare-feu | Flux sortant `192.168.1.20` → `198.51.100.200` : **2,1 Go** | **Vol de données probable** | **Supposé** (le contenu n'est pas visible) |
| Sam. 23:30 | fichiers | Sauvegarde nocturne **en échec** (cible injoignable) | Conséquence de la suppression | Établi |
| Dim. 02:00:03 | authentification | `svc-maint` se ​reconnecte au serveur de fichiers | Début du chiffrement | Établi |
| Dim. 02:04 → 06:08 | fichiers | **420 renommages** `.verrou` | **Chiffrement** | Établi |
| Dim. 06:08 | fichiers | Création de `LISEZ-MOI.txt` | Demande de rançon | Établi |
| Lun. 07:42 | (appel) | Découverte par le bureau d'études | Détection ​tardive : **environ 52 heures** après l'entrée | Établi |

C4 : 420 renommages ; premier à 02:04:33, dernier à 06:08:45 (**environ quatre heures**). Répartition : `Plans/Mairie-Dinan` 98, `Plans/Gabarits` 82, `Plans/Ecole-Rennes` 66, `Compta/2025` 53, `RH/Dossiers` 47, `Compta/2026` 41, `RH/Paies` 33.

Réponses :

1. **Entrée** : accès distant (RDP, port 3389) **redirigé sur la box**, protégé par un **mot de ​passe seul** : c'est la faiblesse de l'annexe 2 de S02 (télétravail).
2. **Environ 22 heures** entre l'entrée (sam. 03:41) et le début du chiffrement (dim. 02:04) ; l'attaquant a **préparé** (compte caché, antivirus arrêté, sauvegardes effacées, données copiées) et **choisi** une nuit de week-end pour retarder la détection. Hypothèse : à marquer comme telle.
3. **Arrêt de l'antivirus, arrêt de la copie instantanée, suppression de 14 sauvegardes du NAS.**
4. Un **flux sortant de 2,1 Go** ​avant le chiffrement suggère un **vol de données** : l'incident est donc aussi une **violation de confidentialité** ; il y aura **notification** et peut-être information des personnes, et la **restauration** ne suffit pas.
5. **Le journal du PC de la comptable** (événements locaux de la machine d'entrée, par exemple les connexions interactives, les programmes lancés) **manque** : il n'est pas dans les ​fichiers fournis, et il est **sur la machine compromise** (modifiable par l'attaquant). On le préserve **par copie**, et surtout on **centralise** les journaux (S11) pour l'avenir. Il manque aussi le **journal du NAS**, sur la machine elle-même.

## Partie D

| Question | Réponse |
|---|---|
| Touchées | PC de la comptable (entrée, compte créé, ​antivirus arrêté) ; serveur de fichiers (chiffré) ; NAS (sauvegardes supprimées) |
| Menacées | Toute machine accessible avec les comptes `comptable` et `svc-maint` ; les identifiants **ont pu être volés** |
| Chiffrées | `Plans/*`, `Compta/*`, `RH/*` (les sept ​dossiers du tableau de C4) |
| Personnelles | `RH/Paies`, `RH/Dossiers` (salariés) ; coordonnées de clients et prospects si présentes dans `Compta` ou l'ERP (à vérifier) |
| Probablement volées | Données copiées vers `198.51.100.200` : **contenu ​inconnu**, à **supposer** étendu (au moins ce que le compte `svc-maint` pouvait lire) |
| Attaquant présent ? | **Peut-être** : vérifier comptes créés, connexions récentes depuis l'extérieur, tâches planifiées, règles de la box ; **ne pas** le supposer ​parti |

**Notification** : les dossiers RH relèvent des **données personnelles** : **violation** probable ; le délai de **72 heures** court à partir de la **prise de connaissance**, c'est-à-dire **ce lundi matin**, avec **dossier à compléter** ensuite si les faits ne sont pas encore tous connus ; **information des personnes** à étudier si le risque est ​élevé (fiches de paie : probable). À valider avec le DPO ou un juriste.

## Partie E

Plan attendu (exemples) :

| Phase | Action | Responsable | Quand |
|---|---|---|---|
| Contenir | Isoler le serveur, le PC de la comptable et le NAS ; **fermer la redirection 3389** sur la box | Prestataire / responsable administratif | Immédiat |
| Contenir | **Désactiver** `svc-maint` et les comptes concernés ; changer les mots de passe depuis une machine saine | ​Prestataire | Immédiat |
| Préserver | **Copie et empreintes** des journaux ; copie du disque du PC de la comptable (si compétences) ; **ne rien réinstaller** | Prestataire | Avant tout nettoyage |
| Éradiquer | Reconstruire le PC de la comptable et le serveur **depuis des sources saines** | Prestataire | Après la préservation |
| Éradiquer | Chercher d'autres persistances (comptes, ​tâches, règles de la box) | Prestataire | Avec la préservation |
| Reprendre | Restaurer ce qui peut l'être depuis une sauvegarde **saine** (voir ci-dessous) ; **surveillance renforcée** | Prestataire / direction | Après éradication |
| Notifier | **CNIL** (violation), plainte, assureur, **information** des clients concernés (architecte, mairies) | ​Dirigeant (avec DPO / juriste) | Dans les 72 h |

1. **Reprise** : les sauvegardes du NAS sont **supprimées** : options : **copies hors ligne** (si elles existent : le dossier S02 n'en prévoit pas), **copies chez les clients** pour les plans, **ERP hébergé** pour la ​gestion commerciale, **récupération partielle** (outils de restauration éventuels : **aucune garantie**), ressaisie. Cela montre l'absence de **sauvegarde déconnectée et testée** (S02, S10) et d'**authentification forte** sur l'accès distant.
2. **Payer ?** Trois points : **aucune garantie** de ​restitution ni de non-publication des données ; cela **finance** les attaquants et rend probable une **nouvelle** attaque ; **les autorités le déconseillent** ; la décision éventuelle est celle de la **direction**, avec avis juridique et assureur, **jamais** celle d'un technicien seul. Elle **ne dispense pas** de la notification.
3. **Avant de rebrancher** : ​cause **fermée** (accès 3389), comptes de l'attaquant supprimés, **tous** les mots de passe changés, machines **reconstruites** ou **vérifiées**, sauvegarde de reprise **saine**, **surveillance** active.

## Partie F

- Message à la direction : faits **établis** (entrée par le port 3389, comptes créés, sauvegardes supprimées, serveur chiffré) ; **hypothèses** (vol de données de volume 2,1 Go, attaquant encore ​présent) ; **décisions** (isolement, notification CNIL, plainte, assureur, pas de paiement sans conseil) ; **prochain point** à heure fixe (par exemple 11 h).
- Consigne aux salariés : ne pas éteindre ni ​brancher quoi que ce soit, ne pas ouvrir de fichiers `.verrou`, ne pas répondre à la demande de rançon, signaler tout élément inhabituel, attendre les consignes.
- Compte rendu : **une page** avec chronologie résumée, causes (accès distant faible, administration par défaut du NAS, sauvegarde non déconnectée, droits trop larges, absence de ​supervision), périmètre, mesures, obligations, **trois actions** (accès distant par VPN avec double authentification ; sauvegarde **hors ligne et testée** ; **journaux centralisés** avec alertes).

## Pièges fréquents

- **Réinstaller d'abord** et perdre les preuves.
- Travailler sur les **originaux** ; empreinte **rangée avec** les ​fichiers.
- Présenter une **hypothèse** (vol de données, attaquant encore présent) comme un **fait**.
- Oublier que le **vol** précède souvent le chiffrement : restaurer ne **clôt pas** l'incident.
- Ne pas **dater** le point de départ des **72 heures**.
- **Payer** sans avis juridique ni assureur.
