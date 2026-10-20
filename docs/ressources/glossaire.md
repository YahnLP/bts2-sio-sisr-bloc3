# Glossaire

Tous les mots techniques du bloc 3 (repris de la première année, complétés au fil de la deuxième), expliqués simplement. Dans les pages du site, **passe la souris sur un sigle** (RGPD, MFA, PKI…) : sa définition s'affiche.

> [!NOTE]
> Les termes de la deuxième année s'ajoutent au fil des phases.

La colonne « Vu en » indique la séance où le mot apparaît pour la première fois dans le cours : **A1** pour la première année, **A2** pour la deuxième.

| Terme | Sigle | Anglais | Définition | Vu en |
|---|---|---|---|---|
| **Actif** |  | *asset* | Ce qu'il faut protéger : donnée, serveur, application, service. | A1 · S01 |
| **Active Directory** | AD |  | Annuaire de Microsoft qui gère comptes, groupes, machines et stratégies d'un domaine Windows. | A2 · S06 |
| **Advanced Encryption Standard** | AES | *advanced encryption standard* | Chiffrement symétrique par blocs de 128 bits, avec des clés de 128, 192 ou 256 bits. | A1 · S10 |
| **Agence nationale de la sécurité des systèmes d'information** | ANSSI |  | Autorité française de cybersécurité, qui publie guides, recommandations et alertes. | A1 · S01 |
| **Analyse d'impact relative à la protection des données** | AIPD | *data protection impact assessment (DPIA)* | Analyse des risques exigée avant un traitement susceptible d'engendrer un risque élevé. | A1 · S09 |
| **Annuaire** |  | *directory* | Base centrale des comptes, groupes et machines d'une organisation (par exemple Active Directory). | A2 · S06 |
| **Anonymisation** |  | *anonymisation* | Rendre la ré-identification impossible : la donnée n'est plus personnelle. | A1 · S08 |
| **Audit de sécurité** |  | *security audit* | Mission encadrée qui évalue la sécurité d'un système par rapport à une référence. | A2 · S14 |
| **Audit de vulnérabilités** |  | *vulnerability assessment* | Recherche des failles d'un système, dans un cadre autorisé. | A1 · S16 |
| **Authentificateur** |  | *authenticator* | Commutateur ou borne Wi-Fi qui relaie la demande vers le serveur RADIUS. | A2 · S07 |
| **Authentification** |  | *authentication* | Prouver que l'on est bien la personne que l'on prétend être. | A1 · S03 |
| **Authentification multifacteur** | MFA | *multi-factor authentication* | Authentification qui exige au moins deux facteurs de types différents. | A1 · S03 |
| **Authentification résistante à l'hameçonnage** | FIDO2 |  | Norme de clés de sécurité et de passkeys qui ne répondent qu'au site réel. | A1 · S03 |
| **Autorisation** |  | *authorization* | Décider de ce qu'une personne authentifiée a le droit de faire. | A1 · S03 |
| **Autorité de certification** | AC | *certificate authority (CA)* | Organisme qui émet et signe des certificats. | A1 · S11 |
| **Autorité nationale de la sécurité des systèmes d'information** | ANSSI |  | Agence française chargée de la cybersécurité de l'État et des opérateurs. | A1 · S09 |
| **Base légale** |  | *lawful basis* | Fondement juridique d'un traitement : consentement, contrat, obligation légale, intérêts vitaux, mission d'intérêt public, intérêt légitime. | A1 · S07 |
| **Bastion d'administration** |  | *jump host* | Machine unique et surveillée par laquelle passent les connexions d'administration. | A2 · S06 |
| **Bien support** |  | *supporting asset* | Ce sur quoi repose une valeur métier : serveur, poste, réseau, logiciel, local, personne. | A2 · S02 |
| **Bilan d'impact sur l'activité** | BIA | *business impact analysis* | Étude des conséquences de l'arrêt de chaque activité dans le temps, point de départ des objectifs de reprise. | A2 · S16 |
| **Bit setgid** |  | *setgid* | Sur un dossier Linux, fait hériter les nouveaux fichiers du groupe du dossier. | A1 · S04 |
| **Bit setuid** |  | *setuid bit* | Droit spécial : le programme s'exécute avec les droits de son propriétaire (souvent root) et non de celui qui le lance. | A2 · S01 |
| **Bourrage d'identifiants** |  | *credential stuffing* | Réessayer sur un service des identifiants volés sur un autre. | A1 · S03 |
| **Cahier des charges** |  | *requirements specification* | Document qui décrit les besoins d'un projet, y compris les exigences de sécurité, et sert de base au choix et à la recette. | A2 · S17 |
| **Centre gouvernemental de veille, d'alerte et de réponse aux attaques** | CERT-FR | *computer emergency response team* | Équipe de l'ANSSI qui publie avis et alertes de sécurité. | A1 · S01 |
| **Certificat auto-signé** |  | *self-signed certificate* | Certificat signé par sa propre clé : non reconnu par défaut. | A1 · S12 |
| **Certificat X.509** |  | *X.509 certificate* | Document qui lie une identité à une clé publique, signé par une autorité de certification. | A1 · S11 |
| **Chaîne de confiance** |  | *chain of trust* | Suite de certificats qui remonte du serveur à une racine connue du système. | A1 · S11 |
| **Chaîne de possession** |  | *chain of custody* | Suivi de qui détient et manipule une preuve. | A1 · S17 |
| **Chaîne de preuve** |  | *chain of custody* | Traçabilité qui démontre qu'une preuve n'a pas été modifiée depuis sa collecte. | A2 · S15 |
| **Charte informatique** |  | *acceptable use policy* | Document signé par les utilisateurs qui fixe les règles d'usage du système d'information. | A1 · S01 |
| **Cheval de Troie** |  | *trojan* | Logiciel qui se présente comme utile pour se faire installer par l'utilisateur. | A1 · S02 |
| **Chiffrement asymétrique** |  | *asymmetric encryption* | Chiffrement à paire de clés : une publique, une privée. | A1 · S11 |
| **Chiffrement de disque de Windows** | BitLocker |  | Fonction de Windows qui chiffre un disque entier. | A1 · S02 |
| **Chiffrement de volume de Linux** | LUKS | *linux unified key setup* | Standard de chiffrement de disques et de volumes sous Linux. | A1 · S05 |
| **Chiffrement hybride** |  | *hybrid encryption* | On chiffre le message en symétrique et la clé de session en asymétrique. | A1 · S11 |
| **Chiffrement symétrique** |  | *symmetric encryption* | Chiffrement qui utilise la même clé pour chiffrer et déchiffrer. | A1 · S10 |
| **Clauses contractuelles types** |  | *standard contractual clauses* | Clauses modèles qui encadrent un transfert de données personnelles hors de l'Union européenne. | A2 · S04 |
| **Clé privée** |  | *private key* | Clé secrète de son propriétaire : sert à déchiffrer et à signer. | A1 · S11 |
| **Clé publique** |  | *public key* | Clé que l'on peut diffuser : sert à chiffrer pour son propriétaire ou à vérifier sa signature. | A1 · S11 |
| **Code d'authentification de message à clé** | HMAC | *hash-based message authentication code* | Empreinte calculée avec une clé secrète : garantit intégrité et authenticité. | A1 · S10 |
| **Collecteur de journaux** |  | *log collector* | Serveur central qui reçoit et range les journaux de plusieurs machines. | A2 · S11 |
| **Commission nationale de l'informatique et des libertés** | CNIL |  | Autorité française de protection des données personnelles. | A1 · S03 |
| **Commission nationale de l'informatique et des libertés** | CNIL |  | Autorité française de protection des données personnelles. | A1 · S06 |
| **Common Vulnerabilities and Exposures** | CVE | *CVE* | Identifiant unique d'une vulnérabilité connue (CVE-année-numéro). | A1 · S16 |
| **Common Vulnerability Scoring System** | CVSS | *CVSS* | Score de gravité technique d'une vulnérabilité, de 0 à 10. | A1 · S16 |
| **Confidentialité** |  | *confidentiality* | Seules les personnes autorisées peuvent lire l'information. | A1 · S01 |
| **Confidentialité persistante** |  | *forward secrecy* | Propriété qui protège les sessions passées même si une clé privée est volée plus tard. | A1 · S11 |
| **Consentement** |  | *consent* | Accord libre, spécifique, éclairé et univoque de la personne. | A1 · S07 |
| **Contrôle d'accès au port** | 802.1X | *port-based access control* | Norme où un équipement doit prouver son identité avant d'obtenir l'accès au réseau. | A2 · S07 |
| **Contrôle d'accès discrétionnaire** | DAC | *discretionary access control* | Le propriétaire d'une ressource décide qui y accède. | A1 · S04 |
| **Contrôle d'accès obligatoire** | MAC | *mandatory access control* | Une politique centrale fixe les accès, que l'utilisateur ne peut pas modifier. | A1 · S04 |
| **Contrôle d'accès par rôles** | RBAC | *role-based access control* | Les droits sont donnés à des rôles, auxquels on affecte des utilisateurs. | A1 · S04 |
| **Cookie** |  | *cookie* | Petit fichier déposé par un site dans le navigateur. | A1 · S07 |
| **Correctif** |  | *patch* | Mise à jour qui corrige une faille ou un défaut. | A1 · S02 |
| **Corrélation** |  | *correlation* | Mise en relation d'événements de sources différentes pour détecter une attaque que chacun pris seul ne révèle pas. | A2 · S11 |
| **Cryptographie** |  | *cryptography* | Science des secrets et de la preuve : chiffrement, hachage, signature. | A1 · S10 |
| **Cybersécurité** |  | *cybersecurity* | Ensemble des moyens qui protègent un système d'information et ses données. | A1 · S01 |
| **Déduplication** |  | *deduplication* | Technique qui ne stocke qu'une fois chaque morceau de données identique. | A1 · S05 |
| **Défense en profondeur** |  | *defense in depth* | Empilement de protections : si l'une est contournée, les autres restent. | A1 · S02 |
| **Défense en profondeur** |  | *defense in depth* | Plusieurs couches de protection superposées. | A1 · S14 |
| **Délégué à la protection des données** | DPO | *data protection officer* | Personne chargée de conseiller et de contrôler la conformité au RGPD. | A1 · S06 |
| **Demande de signature de certificat** | CSR | *certificate signing request* | Demande envoyée à l'AC : contient le nom et la clé publique du demandeur. | A1 · S12 |
| **Demandeur** |  | *supplicant* | Équipement ou logiciel qui demande l'accès dans 802.1X. | A2 · S07 |
| **Démarrage sécurisé** |  | *secure boot* | Chaque élément du démarrage vérifie la signature du suivant avant de lui donner la main. | A1 · S02 |
| **Détection et réponse sur les terminaux** | EDR | *endpoint detection and response* | Outil qui surveille le comportement des postes et permet de réagir à distance. | A1 · S02 |
| **Disponibilité** |  | *availability* | Le service et les données sont accessibles quand on en a besoin. | A1 · S01 |
| **Domain-based Message Authentication, Reporting and Conformance** | DMARC | *dmarc* | Politique qui dit quoi faire des messages qui échouent à SPF ou DKIM. | A1 · S09 |
| **DomainKeys Identified Mail** | DKIM | *domainkeys identified mail* | Signature cryptographique des courriels sortants d'un domaine. | A1 · S09 |
| **Donnée à caractère personnel** |  | *personal data* | Information qui permet d'identifier une personne, directement ou indirectement. | A1 · S06 |
| **Donnée sensible** |  | *special category data* | Santé, origine, opinions, religion, syndicat, génétique, biométrie, vie sexuelle : traitement interdit sauf exception. | A1 · S06 |
| **Dossier documentaire** |  | *documentary file* | Ensemble des documents qui présentent le contexte de l'étude de cas. | A1 · S18 |
| **Double extorsion** |  | *double extortion* | Les données sont volées avant d'être chiffrées, et l'attaquant menace de les publier. | A1 · S01 |
| **Droit à l'effacement** |  | *right to erasure* | Droit de faire supprimer ses données, sauf obligation légale de les conserver. | A1 · S07 |
| **Droit d'accès** |  | *right of access* | Droit d'obtenir une copie des données détenues sur soi. | A1 · S07 |
| **Durcissement** |  | *hardening* | Réduction de la surface d'attaque d'un système par sa configuration. | A1 · S14 |
| **Durée de conservation** |  | *retention period* | Durée pendant laquelle des données sont gardées, fixée selon la finalité. | A1 · S08 |
| **Durée maximale d'interruption admissible** | DMIA | *maximum tolerable downtime* | Durée d'arrêt d'une activité que l'organisation peut tolérer ; limite métier dont découle le RTO. | A2 · S16 |
| **Écart accepté** |  | *accepted deviation* | Différence avec la référence, décidée et justifiée par écrit, avec un responsable et une date de revue. | A2 · S10 |
| **Échange de clés de Diffie-Hellman** | DH | *Diffie-Hellman key exchange* | Permet à deux interlocuteurs de fabriquer un secret commun sur un canal observable. | A1 · S11 |
| **Empreinte** |  | *hash* | Résultat d'un calcul à sens unique sur un contenu : même contenu, même empreinte ; un octet change, tout change. | A1 · S02 |
| **Empreinte** |  | *hash, digest* | Résultat d'une fonction de hachage ; change entièrement si les données changent. | A1 · S10 |
| **Enregistreur de frappe** |  | *keylogger* | Logiciel espion qui enregistre ce que l'on tape au clavier. | A1 · S02 |
| **Entropie** |  | *entropy* | Mesure en bits de la difficulté de deviner un secret : chaque bit double le nombre d'essais. | A1 · S03 |
| **Environnement automatique de gestion de certificats** | ACME | *automatic certificate management environment* | Protocole d'obtention et de renouvellement automatiques de certificats (Let's Encrypt). | A1 · S12 |
| **Espace de noms réseau** |  | *network namespace* | Fonction de Linux qui isole des interfaces, adresses et règles : une machine réseau simulée dans une autre. | A2 · S05 |
| **Étude de cas** |  | *case study* | Épreuve écrite fondée sur un dossier documentaire. | A1 · S18 |
| **Événement redouté** |  | *feared event* | Ce qui peut arriver à une valeur métier et qu'on veut éviter. | A2 · S02 |
| **Exploit** |  | *exploit* | Méthode ou programme qui tire parti d'une vulnérabilité. | A2 · S13 |
| **Extensions de sécurité du DNS** | DNSSEC | *DNS security extensions* | Signature des réponses DNS qui garantit leur origine et leur intégrité, sans les chiffrer. | A2 · S09 |
| **Faux négatif** |  | *false negative* | Attaque réelle qui n'est pas signalée. | A2 · S12 |
| **Faux positif** |  | *false positive* | Alerte déclenchée par un comportement légitime. | A1 · S15 |
| **Fin de support** | EOL | *end of life* | Date à partir de laquelle l'éditeur ne publie plus de correctifs. | A1 · S02 |
| **Finalité** |  | *purpose* | Objectif précis et légitime pour lequel des données sont collectées. | A1 · S06 |
| **Fonction de dérivation de clé** | PBKDF2 | *password-based key derivation function 2* | Calcule une clé de chiffrement à partir d'un mot de passe, de façon lente et salée. | A1 · S10 |
| **Fonction de hachage** |  | *hash function* | Fonction à sens unique qui transforme des données en empreinte de longueur fixe. | A1 · S10 |
| **Force brute** |  | *brute force* | Essayer toutes les combinaisons possibles. | A1 · S03 |
| **Force brute** |  | *brute force* | Attaque qui essaie de nombreux mots de passe ou identifiants. | A1 · S15 |
| **Fraude au président** |  | *CEO fraud* | Faux ordre de virement attribué à un dirigeant, urgent et confidentiel. | A1 · S01 |
| **Gestion des événements et des informations de sécurité** | SIEM | *security information and event management* | Outil qui centralise les journaux, les corrèle et déclenche des alertes. | A2 · S11 |
| **Gestion des informations et des événements de sécurité** | SIEM | *security information and event management* | Plateforme qui centralise et corrèle les journaux et déclenche des alertes. | A1 · S15 |
| **Gestionnaire de mots de passe** |  | *password manager* | Application qui génère, stocke et remplit des mots de passe dans une base chiffrée. | A1 · S03 |
| **Grappe de disques** | RAID | *redundant array of independent disks* | Plusieurs disques utilisés ensemble pour résister à la panne d'un disque. Ce n'est pas une sauvegarde. | A1 · S05 |
| **Guide de mesures de sécurité** | ISO 27002 | *ISO/IEC 27002* | Catalogue de bonnes pratiques de sécurité ; non certifiable. | A2 · S03 |
| **Hameçonnage** |  | *phishing* | Message frauduleux qui se fait passer pour un tiers de confiance pour obtenir une information ou une action. | A1 · S01 |
| **Hameçonnage ciblé de domaine** |  | *typosquatting* | Enregistrement d'un nom de domaine très proche d'un nom connu pour tromper les visiteurs. | A1 · S09 |
| **Harponnage** |  | *spear phishing* | Hameçonnage personnalisé pour une cible précise. | A1 · S01 |
| **HTTP Strict Transport Security** | HSTS | *HTTP strict transport security* | En-tête qui impose à un navigateur de n'utiliser que HTTPS pour un site. | A1 · S12 |
| **Hygiène numérique** |  | *cyber hygiene* | Gestes simples et réguliers qui préviennent la plupart des incidents. | A1 · S01 |
| **Identifiant de vulnérabilité** | CVE | *common vulnerabilities and exposures* | Identifiant unique d'une vulnérabilité publique, par exemple CVE-2017-0144. | A1 · S02 |
| **Identifiant de vulnérabilité commune** | CVE | *common vulnerabilities and exposures* | Identifiant public et unique d'une vulnérabilité (forme CVE-année-numéro). | A2 · S13 |
| **Identité numérique** |  | *digital identity* | Ensemble de ce qui représente une personne ou une organisation en ligne. | A1 · S09 |
| **Incident de sécurité** |  | *security incident* | Événement qui compromet ou menace la sécurité d'un système ou de données. | A1 · S17 |
| **Infrastructure à clés publiques** | PKI | *public key infrastructure* | Ensemble des acteurs et règles qui émettent, distribuent et révoquent les certificats. | A1 · S11 |
| **Ingénierie sociale** |  | *social engineering* | Techniques qui manipulent la confiance, la peur ou l'urgence d'une personne. | A1 · S01 |
| **Injection** |  | *injection* | Faille où des données saisies sont interprétées comme des commandes (SQL, système). | A2 · S08 |
| **Instantané** |  | *snapshot* | État d'un stockage à un instant donné, conservé sur le même stockage : ce n'est pas une sauvegarde. | A1 · S05 |
| **Instantané de machine virtuelle** |  | *VM snapshot* | Photographie de l'état d'une machine virtuelle, à laquelle on peut revenir en cas d'erreur. | A2 · S01 |
| **Intégrité** |  | *integrity* | Les données sont exactes et n'ont pas été modifiées à l'insu de leur propriétaire. | A1 · S01 |
| **Internet Protocol Security** | IPsec | *IPsec* | Suite de protocoles de sécurisation du protocole IP, très utilisée pour les VPN site à site. | A1 · S13 |
| **Journal d'événements** |  | *log* | Enregistrement horodaté d'événements d'un système. | A1 · S15 |
| **Journalisation** |  | *logging* | Enregistrement horodaté des événements d'un système, pour contrôler, enquêter et prouver. | A2 · S11 |
| **Kerberos** |  |  | Protocole d'authentification par tickets délivrés par un centre de confiance, sans envoyer le mot de passe. | A2 · S06 |
| **Limitation de débit** |  | *rate limiting* | Plafond du nombre de requêtes acceptées par client et par durée. | A2 · S08 |
| **Liste de contrôle d'accès** | ACL | *access control list* | Liste des utilisateurs et groupes autorisés (ou refusés) sur une ressource, avec leurs droits. | A1 · S04 |
| **Liste de révocation de certificats** | CRL | *certificate revocation list* | Liste signée des certificats révoqués, publiée par l'AC. | A1 · S12 |
| **Logiciel espion** |  | *spyware* | Logiciel qui collecte discrètement des informations sur l'utilisateur. | A1 · S02 |
| **Logiciel malveillant** |  | *malware* | Logiciel conçu pour nuire : voler, détruire, espionner, extorquer. | A1 · S02 |
| **Loi Godfrain** |  | *computer fraud law (France)* | Loi de 1988 sur les atteintes aux systèmes de traitement automatisé de données, reprise dans le Code pénal (articles 323-1 et suivants). | A2 · S04 |
| **Lynis** |  |  | Outil d'audit local de systèmes Linux qui produit avertissements, suggestions et un indice de durcissement. | A2 · S10 |
| **Main courante** |  | *incident log* | Journal horodaté de ce qui est constaté et décidé pendant une crise. | A1 · S17 |
| **Mandataire inverse** |  | *reverse proxy* | Serveur placé devant une application, qui reçoit les requêtes à sa place, les filtre et les transmet. | A2 · S08 |
| **Matrice de droits** |  | *access matrix* | Tableau croisant groupes et ressources avec le niveau d'accès de chacun. | A1 · S04 |
| **Matrice de flux** |  | *flow matrix* | Tableau des flux autorisés entre zones, avec les ports ; tout le reste est refusé. | A1 · S14 |
| **Menace** |  | *threat* | Ce qui peut causer un dommage : attaquant, logiciel malveillant, erreur, sinistre. | A1 · S01 |
| **Mesure compensatoire** |  | *compensating control* | Mesure qui réduit un risque quand la cause ne peut pas être corrigée. | A2 · S13 |
| **Méthode d'analyse de risques de l'ANSSI** | EBIOS RM | *EBIOS risk manager* | Méthode française d'analyse de risques en cinq ateliers. | A2 · S02 |
| **Micrologiciel de démarrage moderne** | UEFI | *unified extensible firmware interface* | Remplaçant moderne du BIOS ; permet le démarrage sécurisé. | A1 · S02 |
| **Minimisation** |  | *data minimisation* | Ne collecter que les données nécessaires à la finalité. | A1 · S06 |
| **Mode opératoire** |  | *mode of operation* | Manière d'enchaîner les blocs d'un chiffrement par blocs (ECB, CBC, CTR, GCM). | A1 · S10 |
| **Modèle en niveaux** |  | *tier model* | Séparation des comptes d'administration selon ce qu'ils administrent, pour qu'un vol à un niveau n'ouvre pas les autres. | A2 · S06 |
| **Module de plateforme sécurisée** | TPM | *trusted platform module* | Puce qui stocke des clés et mesure l'état du démarrage. | A1 · S02 |
| **Moindre privilège** |  | *least privilege* | Ne donner que les droits strictement nécessaires, pour la durée nécessaire. | A1 · S04 |
| **Mot de passe à usage unique basé sur l'heure** | TOTP | *time-based one-time password* | Code à 6 chiffres calculé à partir d'un secret partagé et de l'heure, renouvelé toutes les 30 secondes. | A1 · S03 |
| **Noms alternatifs du sujet** | SAN | *subject alternative name* | Champ du certificat qui liste les noms de domaine valables. | A1 · S11 |
| **Non-répudiation** |  | *non-repudiation* | L'auteur d'un acte ne peut pas nier en être l'auteur. | A1 · S11 |
| **Norme de management de la sécurité** | ISO 27001 | *ISO/IEC 27001* | Norme d'exigences d'un SMSI ; seule norme de cette famille sur laquelle on peut se faire certifier. | A2 · S03 |
| **Notification à la CNIL** |  | *breach notification* | Déclaration d'une violation à la CNIL, sous 72 heures en cas de risque. | A1 · S08 |
| **NTLM** |  |  | Ancien protocole d'authentification Windows par défi-réponse, plus fragile que Kerberos. | A2 · S06 |
| **Objectif de point de reprise** | RPO | *recovery point objective* | Durée maximale de données que l'on accepte de perdre. | A1 · S05 |
| **Objectif de temps de reprise** | RTO | *recovery time objective* | Durée maximale d'interruption que l'on accepte. | A1 · S05 |
| **Open Web Application Security Project** | OWASP |  | Communauté qui publie des listes et guides sur la sécurité des applications web. | A2 · S08 |
| **Ordre de volatilité** |  | *order of volatility* | Ordre de collecte des preuves, du plus éphémère au plus durable. | A1 · S17 |
| **Pare-feu** |  | *firewall* | Dispositif qui filtre les flux selon des règles. | A1 · S14 |
| **Pare-feu du noyau Linux** | nftables | *nftables* | Outil de filtrage des paquets intégré à Linux, qui remplace iptables. | A2 · S01 |
| **PEAP** |  | *protected EAP* | Méthode EAP où un mot de passe est transporté dans un tunnel TLS ouvert grâce au certificat du serveur. | A2 · S07 |
| **Perte de données maximale admissible** | PDMA | *maximum tolerable data loss* | Quantité de données, exprimée en durée, que l'organisation accepte de perdre ; limite métier dont découle le RPO. | A2 · S16 |
| **Plan de continuité d'activité** | PCA | *business continuity plan* | Comment continuer à travailler pendant un incident. | A1 · S05 |
| **Plan de reprise d'activité** | PRA | *disaster recovery plan* | Comment redémarrer et restaurer après un incident. | A1 · S05 |
| **Politique de sécurité du système d'information** | PSSI | *information security policy* | Document signé par la direction : ce qu'on protège, selon quels principes, qui en répond. | A2 · S03 |
| **Politique par défaut** |  | *default policy* | Décision appliquée à tout paquet qui ne correspond à aucune règle du pare-feu ; elle doit être restrictive. | A2 · S01 |
| **Portabilité** |  | *data portability* | Droit de récupérer ses données dans un format structuré et lisible par une machine. | A1 · S07 |
| **Porte dérobée** |  | *backdoor* | Accès caché laissé par un attaquant pour revenir sur la machine. | A1 · S02 |
| **Prestataire d'audit de la sécurité des systèmes d'information** | PASSI |  | Prestataire d'audit qualifié par l'ANSSI. | A2 · S14 |
| **Preuve** |  | *non-repudiation* | Capacité de démontrer qui a fait quoi, et quand. | A1 · S01 |
| **Protocole d'authentification extensible** | EAP | *extensible authentication protocol* | Cadre qui transporte différentes méthodes de preuve d'identité (mot de passe, certificat). | A2 · S07 |
| **Protocole d'état des certificats en ligne** | OCSP | *online certificate status protocol* | Interrogation en ligne de l'état de révocation d'un certificat. | A1 · S12 |
| **Protocole de synchronisation du temps** | NTP | *network time protocol* | Protocole qui met les horloges des machines à la même heure. | A2 · S11 |
| **Pseudonymisation** |  | *pseudonymisation* | Remplacement de l'identité par un code : la donnée reste personnelle. | A1 · S08 |
| **Rançongiciel** |  | *ransomware* | Logiciel malveillant qui chiffre les fichiers et réclame une rançon. | A1 · S01 |
| **Rançongiciel** |  | *ransomware* | Logiciel malveillant qui chiffre les données et exige une rançon. | A1 · S17 |
| **Recette** |  | *acceptance testing* | Vérification, avec des tests définis à l'avance, que la solution livrée respecte les exigences du cahier des charges. | A2 · S17 |
| **Référence de configuration** |  | *baseline* | Liste de réglages reconnus servant de point de comparaison pour mesurer la conformité. | A2 · S10 |
| **Registre des traitements** |  | *record of processing activities* | Document qui recense les traitements de données personnelles (article 30). | A1 · S06 |
| **Règle 3-2-1** |  | *3-2-1 backup rule* | Trois copies des données, sur deux supports différents, dont une hors site ; renforcée en ajoutant une copie hors ligne ou non modifiable. | A2 · S16 |
| **Règlement général sur la protection des données** | RGPD | *general data protection regulation (GDPR)* | Règlement européen qui encadre le traitement des données personnelles. | A1 · S06 |
| **Règles d'engagement** |  | *rules of engagement* | Limites écrites d'une mission d'audit : périmètre, interdits, horaires, contact d'urgence. | A2 · S14 |
| **Réponse à incident** |  | *incident response* | Démarche pour détecter, contenir, éradiquer, reprendre et tirer les leçons d'un incident. | A2 · S15 |
| **Réseau de machines zombies** |  | *botnet* | Ensemble de machines compromises pilotées à distance par un attaquant. | A1 · S02 |
| **Réseau local virtuel** | VLAN | *virtual LAN* | Découpage logique d'un réseau en segments isolés. | A1 · S14 |
| **Réseau privé virtuel** | VPN | *virtual private network* | Tunnel chiffré et authentifié à travers un réseau non sûr. | A1 · S13 |
| **Responsable de traitement** |  | *data controller* | Organisme qui décide des finalités et des moyens d'un traitement. | A1 · S06 |
| **Retour d'expérience** | REX | *lessons learned* | Analyse d'un incident pour en tirer des actions d'amélioration. | A1 · S17 |
| **Réversibilité** |  | *reversibility* | Possibilité de récupérer ses données dans un format exploitable et de changer de prestataire à la fin d'un contrat. | A2 · S17 |
| **Risque** |  | *risk* | Possibilité qu'une menace exploite une vulnérabilité, mesurée par sa gravité et sa vraisemblance. | A1 · S01 |
| **Risque résiduel** |  | *residual risk* | Risque qui reste après application des mesures ; la direction l'accepte. | A2 · S02 |
| **Rivest-Shamir-Adleman** | RSA | *RSA* | Algorithme asymétrique de chiffrement et de signature. | A1 · S11 |
| **Rootkit** |  | *rootkit* | Logiciel qui masque sa présence et celle d'autres codes malveillants au système. | A1 · S02 |
| **Rotation des journaux** |  | *log rotation* | Archivage et suppression périodiques des fichiers de journaux. | A1 · S08 |
| **Sauvegarde complète** |  | *full backup* | Copie de toutes les données. | A1 · S05 |
| **Sauvegarde différentielle** |  | *differential backup* | Copie de ce qui a changé depuis la dernière sauvegarde complète. | A1 · S05 |
| **Sauvegarde incrémentielle** |  | *incremental backup* | Copie de ce qui a changé depuis la dernière sauvegarde, quelle qu'elle soit. | A1 · S05 |
| **Scan de ports** |  | *port scan* | Test des ports ouverts d'une machine. | A1 · S16 |
| **Scénario de risque** |  | *risk scenario* | Enchaînement d'étapes qui mène d'une source de risque à un événement redouté. | A2 · S02 |
| **Script intersite** | XSS | *cross-site scripting* | Faille où un script injecté dans une page s'exécute dans le navigateur d'un autre utilisateur. | A2 · S08 |
| **Secure Shell** | SSH | *secure shell* | Protocole d'administration à distance chiffré. | A1 · S14 |
| **Sel** |  | *salt* | Valeur aléatoire ajoutée à un mot de passe avant hachage, propre à chaque utilisateur. | A1 · S03 |
| **Sender Policy Framework** | SPF | *sender policy framework* | Enregistrement DNS qui déclare les serveurs autorisés à envoyer du courrier pour un domaine. | A1 · S09 |
| **Séparation des tâches** |  | *separation of duties* | Une action sensible exige l'intervention de deux personnes. | A1 · S04 |
| **Serveur d'authentification RADIUS** | RADIUS | *remote authentication dial-in user service* | Protocole et serveur qui décident de l'accès au réseau et peuvent renvoyer des attributs, comme le VLAN. | A2 · S07 |
| **Serveur de mises à jour de Windows** | WSUS | *windows server update services* | Service qui distribue et contrôle les mises à jour dans un domaine. | A1 · S02 |
| **Signature** |  | *signature* | Motif connu d'attaque, recherché dans le trafic ou les journaux. | A2 · S12 |
| **Signature électronique** |  | *electronic signature* | Procédé qui identifie un signataire et manifeste son consentement. | A1 · S09 |
| **Signature numérique** |  | *digital signature* | Empreinte signée avec la clé privée : garantit intégrité, authenticité et non-répudiation. | A1 · S11 |
| **Solution de mot de passe administrateur local** | LAPS | *local administrator password solution* | Outil qui donne à chaque machine un mot de passe administrateur local unique et renouvelé. | A2 · S06 |
| **Source de risque** |  | *risk source* | Personne ou entité qui peut provoquer un événement redouté. | A2 · S02 |
| **Sous-traitant** |  | *data processor* | Organisme qui traite des données pour le compte du responsable, sous contrat. | A1 · S06 |
| **Stratégie de groupe** | GPO | *group policy object* | Ensemble de réglages appliqués automatiquement aux comptes et machines d'un domaine. | A2 · S06 |
| **Suivi de connexion** |  | *connection tracking* | Fonction du pare-feu qui retient les connexions en cours pour laisser passer leurs réponses. | A2 · S05 |
| **Sûreté** |  | *safety* | Protection contre les événements non intentionnels (panne, incendie, eau, coupure électrique), par opposition à la sécurité, qui vise les actes malveillants. | A2 · S03 |
| **Surface d'attaque** |  | *attack surface* | Ensemble des points par lesquels un attaquant peut tenter d'entrer. | A1 · S14 |
| **Système de détection d'intrusion** | IDS | *intrusion detection system* | Observe le trafic ou une machine et émet des alertes. | A1 · S15 |
| **Système de management de la sécurité de l'information** | SMSI | *ISMS* | Organisation qui gère la sécurité de façon continue : planifier, réaliser, vérifier, agir. | A2 · S03 |
| **Système de notation des vulnérabilités** | CVSS | *common vulnerability scoring system* | Note de gravité d'une vulnérabilité de 0 à 10. | A1 · S02 |
| **Système de prévention d'intrusion** | IPS | *intrusion prevention system* | Comme un IDS, mais bloque le trafic suspect. | A1 · S15 |
| **Tâche planifiée** | cron | *scheduled job* | Mécanisme Unix qui exécute une commande à heure fixe. | A1 · S08 |
| **Test d'intrusion** |  | *penetration test* | Exploitation contrôlée des failles pour mesurer l'impact réel. | A1 · S16 |
| **Traceur** |  | *tracker* | Dispositif qui permet de suivre un utilisateur (cookie, pixel, identifiant d'appareil). | A1 · S07 |
| **Transfert de zone** | AXFR | *zone transfer* | Copie complète d'une zone DNS vers un autre serveur ; à restreindre aux serveurs autorisés. | A2 · S09 |
| **Transport Layer Security** | TLS | *transport layer security* | Protocole de sécurisation des échanges, utilisé par HTTPS. | A1 · S11 |
| **Tunnel complet** |  | *full tunnel* | Tout le trafic du client passe par le VPN. | A1 · S13 |
| **Tunnel partiel** |  | *split tunnel* | Seul le trafic vers le réseau d'entreprise passe par le VPN. | A1 · S13 |
| **Tunnelisation** |  | *tunneling* | Encapsulation de paquets dans d'autres paquets, après chiffrement. | A1 · S13 |
| **Usurpation d'expéditeur** |  | *email spoofing* | Envoi d'un message avec une fausse adresse d'expéditeur. | A2 · S09 |
| **Valeur métier** |  | *business value* | Ce qui compte pour l'organisation : un service, une information, un savoir-faire. | A2 · S02 |
| **Vecteur d'initialisation** | IV | *initialization vector* | Valeur non secrète, imprévisible ou unique, qui démarre un chiffrement. | A1 · S10 |
| **Ver** |  | *worm* | Logiciel malveillant autonome qui se propage de machine en machine par le réseau. | A1 · S02 |
| **Virus** |  | *virus* | Code qui s'attache à un fichier hôte et se propage quand on ouvre ce fichier. | A1 · S02 |
| **VPN nomade** |  | *remote access VPN* | Un utilisateur se connecte au réseau de l'entreprise depuis l'extérieur. | A1 · S13 |
| **VPN site à site** |  | *site-to-site VPN* | Deux réseaux sont reliés en permanence par un tunnel. | A1 · S13 |
| **Vulnérabilité** |  | *vulnerability* | Faiblesse qu'une menace peut exploiter. | A1 · S01 |
| **Vulnérabilité** |  | *vulnerability* | Faiblesse d'un système qui peut être exploitée. | A1 · S16 |
| **Vulnérabilité exposée** |  | *exposed vulnerability* | Faille qui peut être atteinte par un attaquant (par exemple depuis Internet). | A2 · S13 |
| **WireGuard** |  | *WireGuard* | Protocole de VPN moderne, simple, fondé sur une paire de clés par machine. | A1 · S13 |
| **Zone de confiance** |  | *security zone* | Partie du réseau regroupant des machines de même niveau de confiance. | A2 · S05 |
| **Zone démilitarisée** | DMZ | *demilitarized zone* | Zone réseau qui héberge les services exposés à Internet, isolée du réseau interne. | A1 · S14 |
