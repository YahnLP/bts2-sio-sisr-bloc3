# Cours – Fiche de révision de la première année

*BTS SIO SISR 2e année – Bloc 3 – S01*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

Cette fiche rappelle **l'essentiel** de la cybersécurité de la première année en huit thèmes. Elle ne remplace pas les cours de l'an dernier : elle t'aide à savoir **ce que tu dois encore pouvoir faire sans aide**. Après chaque thème, un **test flash** : réponds de tête, puis ouvre la réponse.

---

## 1. Menaces et hygiène numérique

| À retenir | Détail |
|---|---|
| Critères de sécurité | **Disponibilité**, **intégrité**, **confidentialité**, auxquels on ajoute la **preuve** |
| Vocabulaire | **Actif** (ce qu'on protège), **menace** (ce qui peut nuire), **vulnérabilité** (la faiblesse exploitée), **risque** (probabilité × gravité) |
| Attaques courantes | Hameçonnage, harponnage, fraude au président, rançongiciel, **double extorsion** (vol puis chiffrement) |
| Hygiène | Mises à jour, authentification forte, sauvegardes testées, moindre privilège, sensibilisation |

**Test flash.** Un comptable reçoit un message « urgent et confidentiel » du dirigeant lui demandant un virement. De quelle attaque s'agit-il, et quelle parade organisationnelle ?

<details markdown="1">
<summary>Voir la réponse</summary>

**Fraude au président**, une forme d'**ingénierie sociale**. Parade : une **procédure de vérification par un second canal** (rappeler le dirigeant à un numéro connu) et une double validation pour les virements inhabituels.

</details>

---

## 2. Malwares et protection du poste

- **Virus** : s'attache à un fichier et agit quand on l'exécute. **Ver** : se propage **seul** par le réseau. **Cheval de Troie** : se présente comme un programme utile. **Rançongiciel** : chiffre les données et réclame une rançon. **Logiciel espion** : collecte des informations.
- Protection du poste : antivirus ou **EDR**, mises à jour du système et des applications, **chiffrement du disque**, verrouillage de session, pas de droits d'administrateur pour l'usage courant, pare-feu local.
- Le facteur humain reste la première porte d'entrée : pièce jointe, lien, clé USB trouvée.

**Test flash.** Qu'est-ce qui distingue un ver d'un virus ?

<details markdown="1">
<summary>Voir la réponse</summary>

Le **ver** se propage **de lui-même** à travers le réseau, sans action de l'utilisateur. Le **virus** a besoin qu'un fichier hôte soit exécuté.

</details>

---

## 3. Authentification et mots de passe

| À retenir | Détail |
|---|---|
| Trois familles de facteurs | **Savoir** (mot de passe), **avoir** (téléphone, clé de sécurité), **être** (empreinte) |
| Authentification multifacteur | Au moins **deux familles différentes** : un mot de passe et un code ne valent pas un seul mot de passe long |
| Stockage | On stocke un **hachage salé** du mot de passe, jamais le mot de passe |
| Code à usage unique | TOTP : le serveur et le téléphone partagent un **secret** et utilisent l'**heure** pour calculer le même code |
| Pratique | Phrase de passe longue, gestionnaire de mots de passe, un mot de passe par service |

**Test flash.** Pourquoi stocker un hachage salé plutôt que le mot de passe chiffré ?

<details markdown="1">
<summary>Voir la réponse</summary>

Un **hachage** ne se « déchiffre » pas : si la base fuit, l'attaquant doit tester des mots de passe un par un. Le **sel**, propre à chaque compte, empêche de réutiliser des tables précalculées et fait que deux mots de passe identiques n'ont pas le même hachage. Un mot de passe chiffré, lui, peut être déchiffré avec la clé.

</details>

---

## 4. Droits et privilèges

- **Moindre privilège** : chacun n'a que les droits nécessaires à sa mission, pour la durée nécessaire.
- **Séparation des tâches** : une même personne ne cumule pas les rôles qui permettraient une fraude.
- Droits Linux : `r` = 4, `w` = 2, `x` = 1, pour le **propriétaire**, le **groupe**, les **autres**. `640` = propriétaire en lecture et écriture, groupe en lecture, autres rien.
- Élévation : `sudo` pour une commande précise, plutôt qu'une session ouverte en `root`.
- **Revue des droits** : à chaque arrivée, changement de poste ou départ, et régulièrement.

**Test flash.** Que signifie `-rw-r----- 1 root compta clients.csv` ?

<details markdown="1">
<summary>Voir la réponse</summary>

Fichier appartenant à `root` et au groupe `compta` ; `root` peut lire et écrire, les membres de `compta` peuvent **lire**, **les autres n'ont aucun accès**. C'est le droit `640`.

</details>

---

## 5. Sauvegarde et restauration

| À retenir | Détail |
|---|---|
| Règle **3-2-1** | 3 copies, sur 2 types de supports, dont 1 hors site |
| Types | **Complète**, **différentielle** (depuis la dernière complète), **incrémentale** (depuis la dernière sauvegarde) |
| **RPO** | Perte de données maximale acceptée (« jusqu'à quand revient-on en arrière ? ») |
| **RTO** | Durée maximale d'interruption acceptée (« en combien de temps redémarre-t-on ? ») |
| Test | Une sauvegarde qui n'a jamais été **restaurée** n'est qu'une hypothèse |
| Piège | Un **RAID n'est pas une sauvegarde** : il protège d'une panne de disque, pas d'une suppression ni d'un rançongiciel |

**Test flash.** On sauvegarde chaque nuit à 2 h. Un serveur tombe à 17 h. Quelle perte de données subit-on ce jour-là, quelle est la perte au pire, et quel RPO cela suppose-t-il ?

<details markdown="1">
<summary>Voir la réponse</summary>

Une panne à 17 h fait perdre les **15 h** écoulées depuis la sauvegarde de 2 h. Au pire (panne juste avant la sauvegarde suivante), on perd **près de 24 h** de données : l'organisation accepte donc, de fait, un **RPO d'environ 24 heures**. Si c'est trop, il faut sauvegarder plus souvent.

</details>

---

## 6. Données personnelles et RGPD

- **Donnée à caractère personnel** : toute information qui permet d'identifier une personne physique, directement ou non (nom, courriel nominatif, adresse IP, identifiant).
- **Responsable de traitement** : décide des finalités et des moyens. **Sous-traitant** : traite pour son compte, sur instruction.
- Principes : **finalité**, **minimisation**, **exactitude**, **limitation de la conservation**, **intégrité et confidentialité**.
- **Bases légales** : consentement, contrat, obligation légale, intérêts vitaux, mission d'intérêt public, intérêt légitime.
- **Droits** des personnes : accès, rectification, effacement, limitation, portabilité, opposition.
- Outils : **registre des traitements**, **analyse d'impact (AIPD)** quand le risque est élevé, **délégué à la protection des données** dans certains cas.
- **Violation de données** : notification à la **CNIL dans les 72 heures** après en avoir pris connaissance, sauf si elle n'est pas susceptible d'engendrer un risque pour les personnes ; information des personnes si le risque est élevé.

**Test flash.** Une adresse IP est-elle une donnée à caractère personnel ?

<details markdown="1">
<summary>Voir la réponse</summary>

**Oui, en principe** : elle peut permettre d'identifier une personne, directement ou en la rapprochant d'autres informations (par exemple celles d'un fournisseur d'accès). C'est la position retenue par la CNIL. Ce n'est pas le cas d'une raison sociale (personne morale).

</details>

---

## 7. Chiffrement, PKI, HTTPS et VPN

| Notion | À retenir |
|---|---|
| **Chiffrement symétrique** | Une même clé chiffre et déchiffre ; **rapide** ; problème : partager la clé (exemple : AES) |
| **Chiffrement asymétrique** | Clé publique et clé privée ; **plus lent** ; règle le partage des clés (exemples : RSA, courbes elliptiques) |
| **Hachage** | Empreinte de longueur fixe, non réversible ; garantit l'**intégrité** (exemple : SHA-256) |
| **Signature** | Empreinte chiffrée avec la clé **privée** de l'auteur ; vérifiée avec sa clé **publique** : intégrité et origine |
| **Certificat** | Lie une identité à une clé publique, signé par une **autorité de certification** |
| **HTTPS** | HTTP dans un tunnel TLS : le navigateur vérifie le certificat, puis les deux côtés conviennent d'une clé de session **symétrique** |
| **VPN** | Tunnel chiffré entre deux sites ou entre un poste et un réseau (WireGuard, IPsec) |

**Test flash.** Pourquoi HTTPS n'utilise-t-il pas du chiffrement asymétrique pour tout le trafic ?

<details markdown="1">
<summary>Voir la réponse</summary>

Le chiffrement asymétrique est **beaucoup plus lent**. On l'emploie au début pour **authentifier** le serveur et **convenir d'une clé de session**, puis tout le trafic est chiffré en **symétrique**.

</details>

---

## 8. Architecture, durcissement, journaux, audit et incident

- **Segmentation** : séparer utilisateurs, serveurs, administration ; une **zone démilitarisée (DMZ)** accueille les services exposés à Internet.
- **Pare-feu** : politique par défaut **restrictive** (on refuse tout, on autorise le nécessaire), suivi des connexions établies, journalisation des refus.
- **Durcissement** : supprimer ce qui est inutile (services, comptes, paquets), restreindre l'accès d'administration (SSH par clé, pas de connexion directe de `root`), corriger les droits, tenir à jour.
- **Journaux** : centraliser, horodater (temps synchronisé), conserver, protéger contre la modification ; un **IDS** détecte, un **IPS** bloque.
- **Audit et vulnérabilités** : inventaire, scan, tri par gravité et exposition, correction, nouveau scan ; **uniquement avec autorisation**.
- **Réponse à incident** : préparer, détecter, **contenir**, éradiquer, restaurer, **tirer les leçons**.

**Test flash.** Un pare-feu « tout autorisé sauf quelques interdits » ou « tout interdit sauf quelques autorisations » : lequel choisir, et pourquoi ?

<details markdown="1">
<summary>Voir la réponse</summary>

**Tout interdit sauf le nécessaire.** Avec une liste d'interdits, tout ce qu'on a oublié reste ouvert ; avec une liste d'autorisations, un oubli bloque un service, ce qui se voit et se corrige.

</details>

---

## Et cette année ?

La deuxième année **n'ajoute pas un nouveau sujet** : elle fait passer de l'application des mesures à leur **justification** (analyse de risques, référentiels, cadre juridique), à leur **mise en œuvre à l'échelle d'une organisation** (annuaire, accès, services, supervision) et à leur **défense à l'écrit**, dans l'étude de cas de l'épreuve **E7** (4 heures). Voir la page [L'épreuve E7](../../ressources/epreuve-e7.md).
