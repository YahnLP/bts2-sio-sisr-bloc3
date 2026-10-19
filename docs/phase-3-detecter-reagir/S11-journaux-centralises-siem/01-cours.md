# Cours – Journaux centralisés et supervision de sécurité

*BTS SIO SISR 2e année – Bloc 3 – S11*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

Une attaque laisse des **traces**, mais réparties : un échec de connexion sur le serveur de fichiers, un autre sur le serveur web, un compte créé sur l'annuaire. Lues machine par machine, ces traces passent inaperçues. Lues **ensemble**, elles racontent une histoire. Cette séance apprend à **rassembler**, **dater**, **croiser** et **conserver** les journaux.

---

## 1. Pourquoi centraliser

| Problème avec des journaux locaux | Ce que la centralisation apporte |
|---|---|
| Il faut se connecter à **chaque** machine | Un **seul** endroit de recherche |
| L'attaquant qui prend la main peut **effacer** les journaux de la machine | Une **copie** déjà partie ailleurs (preuve, séance S15) |
| Les journaux **tournent** et disparaissent vite | **Conservation** décidée et maîtrisée |
| Impossible de **croiser** deux machines | **Corrélation** entre sources |
| Machine **éteinte ou chiffrée** : journaux inaccessibles | Les événements d'**avant** l'incident sont à l'abri |

> [!NOTE]
> La centralisation ne protège que ce qui est **envoyé**. Un attaquant qui **coupe l'envoi** avant d'agir garde ses traces locales hors de portée : surveiller **l'absence** de journaux d'une machine fait partie de la supervision.

---

## 2. Que journaliser

| Source | Événements utiles |
|---|---|
| **Authentification** | Succès et échecs de connexion, changements de mot de passe, élévation de privilèges (`sudo`) |
| **Annuaire** | Création de comptes, ajouts aux groupes sensibles (séance S06) |
| **Pare-feu et sondes** | Flux refusés (séance S05), alertes (séance S12) |
| **Services exposés** | Journaux d'accès et d'erreurs du serveur web et du reverse proxy (séance S08) |
| **Systèmes** | Démarrages, arrêts, installations, arrêt du service de journalisation |

Pour chaque événement, on veut répondre à **qui, quoi, quand, d'où** (et le résultat). Un journal qui n'indique pas **l'heure fiable** ou **l'origine** vaut peu.

> [!WARNING]
> Les journaux contiennent des **données personnelles** (identifiants, adresses IP, parfois des actions d'utilisateurs). Ils relèvent du RGPD (séance S04) : **finalité**, **accès restreint**, **durée limitée**, information des personnes. Ne **jamais** y écrire de mots de passe.

---

## 3. Le trajet d'un événement

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 529.10 551.60" style="max-width:705px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 540.8)">
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M238,-530C238,-530 14,-530 14,-530 8,-530 2,-524 2,-518 2,-518 2,-505 2,-505 2,-499 8,-493 14,-493 14,-493 238,-493 238,-493 244,-493 250,-499 250,-505 250,-505 250,-518 250,-518 250,-524 244,-530 238,-530"/>
<text text-anchor="start" x="21" y="-508" font-family="Helvetica,sans-Serif" font-size="15.00">Source : service ou système</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M179.5,-434C179.5,-434 72.5,-434 72.5,-434 66.5,-434 60.5,-428 60.5,-422 60.5,-422 60.5,-409 60.5,-409 60.5,-403 66.5,-397 72.5,-397 72.5,-397 179.5,-397 179.5,-397 185.5,-397 191.5,-403 191.5,-409 191.5,-409 191.5,-422 191.5,-422 191.5,-428 185.5,-434 179.5,-434"/>
<text text-anchor="start" x="79.5" y="-412" font-family="Helvetica,sans-Serif" font-size="15.00">Journal local</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M126,-492.82C126,-478.9 126,-459.27 126,-443.41"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="129.15,-443.1 126,-434.1 122.85,-443.1 129.15,-443.1"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M185.5,-338C185.5,-338 66.5,-338 66.5,-338 60.5,-338 54.5,-332 54.5,-326 54.5,-326 54.5,-313 54.5,-313 54.5,-307 60.5,-301 66.5,-301 66.5,-301 185.5,-301 185.5,-301 191.5,-301 197.5,-307 197.5,-313 197.5,-313 197.5,-326 197.5,-326 197.5,-332 191.5,-338 185.5,-338"/>
<text text-anchor="start" x="73.5" y="-316" font-family="Helvetica,sans-Serif" font-size="15.00">Agent d&#39;envoi</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M126,-396.82C126,-382.9 126,-363.27 126,-347.41"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="129.15,-347.1 126,-338.1 122.85,-347.1 129.15,-347.1"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M200,-229C200,-229 52,-229 52,-229 46,-229 40,-223 40,-217 40,-217 40,-204 40,-204 40,-198 46,-192 52,-192 52,-192 200,-192 200,-192 206,-192 212,-198 212,-204 212,-204 212,-217 212,-217 212,-223 206,-229 200,-229"/>
<text text-anchor="start" x="59" y="-207" font-family="Helvetica,sans-Serif" font-size="15.00">Collecteur central</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M126,-300.83C126,-283.79 126,-257.78 126,-238.22"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="129.15,-238.2 126,-229.2 122.85,-238.2 129.15,-238.2"/>
<text text-anchor="start" x="126" y="-261.6" font-family="Helvetica,sans-Serif" font-size="13.00">réseau, si possible chiffré</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M194,-133C194,-133 12,-133 12,-133 6,-133 0,-127 0,-121 0,-121 0,-108 0,-108 0,-102 6,-96 12,-96 12,-96 194,-96 194,-96 200,-96 206,-102 206,-108 206,-108 206,-121 206,-121 206,-127 200,-133 194,-133"/>
<text text-anchor="start" x="19" y="-111" font-family="Helvetica,sans-Serif" font-size="15.00">Stockage par machine</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M121.67,-191.82C118.24,-177.77 113.38,-157.9 109.47,-141.96"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="112.51,-141.09 107.31,-133.1 106.39,-142.59 112.51,-141.09"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M495.5,-133C495.5,-133 258.5,-133 258.5,-133 252.5,-133 246.5,-127 246.5,-121 246.5,-121 246.5,-108 246.5,-108 246.5,-102 252.5,-96 258.5,-96 258.5,-96 495.5,-96 495.5,-96 501.5,-96 507.5,-102 507.5,-108 507.5,-108 507.5,-121 507.5,-121 507.5,-127 501.5,-133 495.5,-133"/>
<text text-anchor="start" x="265.5" y="-111" font-family="Helvetica,sans-Serif" font-size="15.00">Règles : filtrage et corrélation</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M172.92,-191.93C214.95,-176.19 276.67,-153.07 321.22,-136.39"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="322.56,-139.25 329.89,-133.14 320.35,-133.35 322.56,-139.25"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M467.5,-37C467.5,-37 286.5,-37 286.5,-37 280.5,-37 274.5,-31 274.5,-25 274.5,-25 274.5,-12 274.5,-12 274.5,-6 280.5,0 286.5,0 286.5,0 467.5,0 467.5,0 473.5,0 479.5,-6 479.5,-12 479.5,-12 479.5,-25 479.5,-25 479.5,-31 473.5,-37 467.5,-37"/>
<text text-anchor="start" x="293.5" y="-15" font-family="Helvetica,sans-Serif" font-size="15.00">Alerte vers un humain</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M377,-95.82C377,-81.9 377,-62.27 377,-46.41"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="380.15,-46.1 377,-37.1 373.85,-46.1 380.15,-46.1"/>
</g>
</g>
</svg>
</figure>

| Choix | À savoir |
|---|---|
| **Protocole d'envoi** | **UDP** : simple mais des messages peuvent se perdre sans que personne le sache. **TCP** : accusé de réception de transport, reprise après coupure. Pour un événement de sécurité, on choisit **TCP** |
| **Chiffrement** | Les journaux circulent en clair par défaut : sur un réseau non maîtrisé, on ajoute **TLS** (séance S08 pour le principe) |
| **File d'attente** | Si le collecteur est injoignable, l'agent **garde** les messages et les renvoie. Une file **en mémoire** est perdue si l'agent redémarre : une file **sur disque** est plus sûre |
| **Format** | Le **syslog** est le format classique (priorité, date, machine, programme, message). Les journaux structurés (JSON) se filtrent plus facilement |

---

## 4. Dater : la synchronisation du temps

Pour **reconstituer** une chronologie (séance S15), toutes les machines doivent avoir **la même heure**.

| Règle | Pourquoi |
|---|---|
| Un service de **synchronisation** (NTP, par exemple `chrony`) sur **toutes** les machines, avec une source commune | Écart de quelques secondes = événements dans le mauvais ordre |
| Horodatage avec **fuseau** (UTC de préférence sur les serveurs) | Évite les confusions d'heure d'été |
| **Surveiller** la dérive | Une machine qui dérive est une source de preuves douteuses |

---

## 5. Corréler : transformer des lignes en alertes

Un événement isolé n'a souvent aucune signification. La **corrélation** relie des événements :

| Règle | Exemple | Ce qu'elle détecte |
|---|---|---|
| **Seuil** | 5 échecs de connexion depuis la même adresse | Essai de mots de passe |
| **Multi-machines** | La même adresse échoue sur **plusieurs** serveurs | Balayage d'une plage de machines |
| **Séquence** | Plusieurs échecs, **puis** un succès, **puis** création d'un compte | Intrusion réussie |
| **Absence** | Plus aucun journal de la machine X depuis 10 minutes | Panne, ou coupure volontaire |
| **Horaire** | Connexion d'administration à 3 h du matin | Usage inhabituel |

Les outils complets de supervision de sécurité (SIEM, par exemple **Wazuh**) font cela à grande échelle, avec tableaux de bord, règles prêtes à l'emploi et recherche. Le **principe** reste celui du TP : collecter, normaliser, comparer à des règles, alerter.

> [!WARNING]
> **Une alerte n'a de valeur que si quelqu'un la traite.** Trop d'alertes sans importance et l'équipe n'en lit plus aucune (séance S12). Chaque règle a un **seuil** réglé, un **responsable** et une **procédure** de réaction.

---

## 6. Conserver : combien de temps ?

La durée **n'est pas libre** : elle se justifie par la **finalité** et le cadre juridique.

| Repère | Contenu |
|---|---|
| **Recommandation de la CNIL sur la journalisation** (délibération n° 2021-122 du 14 octobre 2021) | Pour la journalisation courante : conservation **entre six mois et un an**. Au-delà, jusqu'à trois ans dans les cas les plus courants, si le besoin est **démontré et documenté** |
| **Obligations légales particulières** | Certains acteurs (par exemple les hébergeurs et fournisseurs d'accès) ont des durées imposées : à vérifier avec un juriste pour chaque organisation |
| **Besoin de sécurité** | Une intrusion est souvent découverte **des mois** après : une durée trop courte rend l'enquête impossible |

On conserve **assez** pour enquêter, **pas plus** que justifié, et on **supprime** à l'échéance.

| Outil | Rôle |
|---|---|
| **Rotation** (`logrotate`) | Découpe les fichiers, compresse, supprime après N cycles |
| **Droits** | Lecture limitée aux personnes habilitées ; écriture réservée au service |
| **Intégrité** | Copie vers un support en **écriture unique**, ou signature (pour la valeur de preuve) |

**Test flash.** Un administrateur dit : « on garde tout cinq ans, au cas où ». Que lui réponds-tu ?

<details markdown="1">
<summary>Voir la réponse</summary>

La durée doit se **justifier** par une finalité (RGPD, séance S04). Au-delà de ce que la recommandation de la CNIL admet pour la journalisation courante, il faut **documenter le besoin** ; « au cas où » n'est pas une justification. À l'inverse, deux semaines serait trop court pour enquêter sur une intrusion découverte tardivement.

</details>
