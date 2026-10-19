# Cours – Gestion des vulnérabilités : de la découverte à la correction

*BTS SIO SISR 2e année – Bloc 3 – S13*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

Un scanneur de vulnérabilités sait produire un rapport de **quatre cents lignes** en une nuit. Le métier, c'est **ce qu'on en fait** : décider laquelle corriger en premier, avec quels moyens, et **prouver** que c'est fait. Cette séance prolonge l'audit de conformité de la séance S10 (« est-ce conforme à ce qu'on a décidé ? ») par une autre question : « **qu'est-ce qui est faible, et qui peut s'en servir ?** »

---

## 1. Les mots à ne pas confondre

| Terme | Sens | Exemple |
|---|---|---|
| **Vulnérabilité** | Faiblesse dans un logiciel, un matériel ou une configuration | Une version d'un logiciel qui accepte une requête mal formée |
| **Correctif** | Mise à jour ou réglage qui supprime la faiblesse | Version corrigée ; désactivation d'une option |
| **Exposition** | Qui peut **atteindre** la faiblesse | Machine joignable depuis Internet, ou seulement depuis un réseau interne |
| **Exploit** | Code ou méthode qui **tire parti** de la faiblesse | Un programme publié qui réussit l'attaque |
| **Exploitation** | L'exploit est **utilisé**, en vrai, par des attaquants | Alerte d'une autorité : « activement exploitée » |

Une vulnérabilité **non exposée** et **sans exploit connu** n'a pas le même niveau d'urgence qu'une vulnérabilité **exposée** et **exploitée**, même si leur note est identique : c'est tout l'enjeu de la priorisation.

Deux origines différentes :

| | Faille de **logiciel** | Faille de **configuration** |
|---|---|---|
| Cause | Erreur de conception ou de programmation | Réglage laissé par défaut ou mal choisi |
| Remède | Correctif de l'éditeur | **Réglage** (souvent gratuit et immédiat) |
| Exemples | Exécution de code à distance | Identifiants par défaut ; liste de fichiers ouverte ; sauvegarde laissée en accès public |

---

## 2. Identifier et noter : CVE et CVSS

| Sigle | Rôle |
|---|---|
| **CVE** | **Identifiant** public et unique d'une vulnérabilité (forme `CVE-année-numéro`) |
| **CWE** | **Famille** de faiblesse (par exemple l'injection) |
| **CVSS** | **Note de gravité** de 0 à 10, calculée à partir de critères |
| **NVD** | Base publique qui rassemble les fiches CVE et leurs notes |

### Lire un vecteur CVSS (version 3.1)

`AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H`

| Critère | Valeurs | Question |
|---|---|---|
| **AV** (vecteur d'attaque) | N réseau, A réseau voisin, L local, P physique | **D'où** peut-on attaquer ? |
| **AC** (complexité) | L faible, H élevée | L'attaque réussit-elle **à coup sûr** ? |
| **PR** (privilèges requis) | N aucun, L faibles, H élevés | Faut-il **déjà** un compte ? |
| **UI** (interaction) | N aucune, R requise | Faut-il qu'un utilisateur **clique** ? |
| **S** (portée) | U inchangée, C changée | L'attaque **déborde**-t-elle sur d'autres composants ? |
| **C / I / A** | N aucun, L faible, H élevé | Effet sur la **confidentialité**, l'**intégrité**, la **disponibilité** |

Les notes se classent ainsi : **0** aucune ; **0,1 à 3,9** faible ; **4,0 à 6,9** moyenne ; **7,0 à 8,9** élevée ; **9,0 à 10** critique.

> [!NOTE]
> Une version **4.0** du CVSS existe aussi et se rencontre de plus en plus ; ce cours utilise la **3.1**, encore très présente dans les rapports. Le calcul diffère : vérifie la version affichée dans un rapport avant de comparer deux notes.

### Ce que la note ne dit pas

| Limite | Conséquence |
|---|---|
| La note de base mesure la **gravité technique**, **pas le risque pour toi** | Une faille critique sur un logiciel que tu n'utilises pas ne te concerne pas |
| Elle ignore l'**exposition** de ta machine | La même faille est urgente sur un serveur public, moins sur un poste isolé |
| Elle ignore l'**exploitation réelle** | Une faille moyenne **activement exploitée** passe avant une faille critique sans exploit connu |
| Elle ignore la **valeur de l'actif** (séance S02) | Une faille « moyenne » sur la sauvegarde peut être plus grave qu'une faille « élevée » sur un poste de test |
| Beaucoup de rapports comptent **les failles de configuration** comme des CVE | Mais leur note est **estimée**, pas officielle |

Des sources aident à savoir **ce qui est exploité** : le **catalogue des vulnérabilités connues comme exploitées** (KEV) de l'agence américaine CISA, les **alertes du CERT-FR**, et des **scores de probabilité d'exploitation** comme l'EPSS. À consulter au moment de prioriser ; leurs données **changent** et ne s'apprennent pas par cœur.

---

## 3. Le cycle de gestion des vulnérabilités

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 342.60 533.60" style="max-width:457px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 522.8)">
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M304.5,-512C304.5,-512 188.5,-512 188.5,-512 182.5,-512 176.5,-506 176.5,-500 176.5,-500 176.5,-487 176.5,-487 176.5,-481 182.5,-475 188.5,-475 188.5,-475 304.5,-475 304.5,-475 310.5,-475 316.5,-481 316.5,-487 316.5,-487 316.5,-500 316.5,-500 316.5,-506 310.5,-512 304.5,-512"/>
<text text-anchor="start" x="195.5" y="-490" font-family="Helvetica,sans-Serif" font-size="15.00">1. Inventorier</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M305.5,-417C305.5,-417 187.5,-417 187.5,-417 181.5,-417 175.5,-411 175.5,-405 175.5,-405 175.5,-392 175.5,-392 175.5,-386 181.5,-380 187.5,-380 187.5,-380 305.5,-380 305.5,-380 311.5,-380 317.5,-386 317.5,-392 317.5,-392 317.5,-405 317.5,-405 317.5,-411 311.5,-417 305.5,-417"/>
<text text-anchor="start" x="194.5" y="-395" font-family="Helvetica,sans-Serif" font-size="15.00">2. Rechercher</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M246.5,-474.57C246.5,-460.84 246.5,-441.7 246.5,-426.18"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="249.65,-426.06 246.5,-417.06 243.35,-426.06 249.65,-426.06"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M234,-322C234,-322 139,-322 139,-322 133,-322 127,-316 127,-310 127,-310 127,-297 127,-297 127,-291 133,-285 139,-285 139,-285 234,-285 234,-285 240,-285 246,-291 246,-297 246,-297 246,-310 246,-310 246,-316 240,-322 234,-322"/>
<text text-anchor="start" x="146" y="-300" font-family="Helvetica,sans-Serif" font-size="15.00">3. Prioriser</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M234.93,-379.57C225.83,-365.46 213.02,-345.61 202.87,-329.87"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="205.36,-327.92 197.83,-322.06 200.06,-331.33 205.36,-327.92"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M250.5,-227C250.5,-227 46.5,-227 46.5,-227 40.5,-227 34.5,-221 34.5,-215 34.5,-215 34.5,-202 34.5,-202 34.5,-196 40.5,-190 46.5,-190 46.5,-190 250.5,-190 250.5,-190 256.5,-190 262.5,-196 262.5,-202 262.5,-202 262.5,-215 262.5,-215 262.5,-221 256.5,-227 250.5,-227"/>
<text text-anchor="start" x="53.5" y="-205" font-family="Helvetica,sans-Serif" font-size="15.00">4. Corriger ou compenser</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M179.17,-284.57C173.51,-270.71 165.59,-251.34 159.22,-235.74"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="162,-234.2 155.68,-227.06 156.16,-236.58 162,-234.2"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M261,-132C261,-132 12,-132 12,-132 6,-132 0,-126 0,-120 0,-120 0,-107 0,-107 0,-101 6,-95 12,-95 12,-95 261,-95 261,-95 267,-95 273,-101 273,-107 273,-107 273,-120 273,-120 273,-126 267,-132 261,-132"/>
<text text-anchor="start" x="19" y="-110" font-family="Helvetica,sans-Serif" font-size="15.00">5. Vérifier par un nouveau scan</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M146.19,-189.57C144.42,-175.84 141.94,-156.7 139.94,-141.18"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="143.04,-140.58 138.77,-132.06 136.79,-141.39 143.04,-140.58"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M309,-37C309,-37 162,-37 162,-37 156,-37 150,-31 150,-25 150,-25 150,-12 150,-12 150,-6 156,0 162,0 162,0 309,0 309,0 315,0 321,-6 321,-12 321,-12 321,-25 321,-25 321,-31 315,-37 309,-37"/>
<text text-anchor="start" x="169" y="-15" font-family="Helvetica,sans-Serif" font-size="15.00">6. Rendre compte</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M155.59,-94.57C171.03,-80.07 192.91,-59.51 209.87,-43.58"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="212.4,-45.52 216.81,-37.06 208.09,-40.93 212.4,-45.52"/>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M254.09,-37.04C267.65,-51.2 284.93,-72.42 292.5,-95 325.53,-193.56 281.19,-318.19 258.46,-371.45"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="255.46,-370.45 254.75,-379.95 261.23,-372.96 255.46,-370.45"/>
</g>
</g>
</svg>
</figure>

| Étape | Points clés |
|---|---|
| **Inventorier** | On ne scanne que ce qu'on connaît : sans inventaire (séance S10), des machines échappent au cycle |
| **Rechercher** | Scanner **régulièrement**, pas une fois l'an ; surveiller les **alertes** (éditeurs, CERT-FR) entre deux scans |
| **Prioriser** | Note **+** exposition **+** exploitation **+** valeur de l'actif **+** disponibilité d'un correctif |
| **Corriger ou compenser** | Correctif ; sinon **mesure compensatoire** (isoler, filtrer, désactiver le service) |
| **Vérifier** | Un **nouveau scan** prouve que la faille a disparu : « corrigé » sans preuve n'est qu'une déclaration |
| **Rendre compte** | Indicateurs lisibles par la direction : nombre de failles ouvertes par priorité, **délai moyen de correction**, exceptions en cours |

### Que faire quand il n'y a pas de correctif ?

| Situation | Réponse |
|---|---|
| Logiciel en **fin de support** (les PC de l'Atelier Verdier sous Windows 7) | **Migrer** ; en attendant **isoler** dans une zone dédiée aux flux minimaux (séance S05) |
| Correctif pas encore publié | **Contourner** : désactiver le composant, filtrer l'accès, surveiller (séance S12) |
| Correctif qui **casse** l'application | Tester, négocier une fenêtre ; **accepter le risque par écrit** avec date de revue (séance S10) |

---

## 4. Les outils : ce qu'ils font et ne font pas

| Outil | Fait | Ne fait pas |
|---|---|---|
| **Nmap** | Découvre les machines et services ouverts, **identifie les versions** | Ne note pas la gravité à lui seul |
| **Scripts de Nmap** (`--script`) | Vérifie des faiblesses précises (listes de fichiers, algorithmes faibles…) | Couverture limitée aux scripts disponibles |
| **Nikto** | Cherche des faiblesses **web** courantes (fichiers oubliés, en-têtes absents) | Ne comprend pas votre application |
| **Scanneurs complets** (par exemple OpenVAS / Greenbone, Nessus) | Comparent versions et configurations à une **base de failles** mise à jour | Demandent une **installation lourde** et des mises à jour de base |
| **Scan authentifié** (avec un compte sur la machine) | Voit les **paquets installés** et les configurations : bien plus complet | Demande un compte : à encadrer |

> [!WARNING]
> **Un scan peut perturber un service** (requêtes inhabituelles, saturation d'un équipement fragile) et **ressemble à une attaque**. On ne scanne **que** avec une **autorisation écrite** qui précise le **périmètre** (machines, adresses), les **dates et heures**, les **outils**, et un **contact** en cas d'incident (séances S04 et S14). Un scan sans autorisation d'une machine qui n'est pas la tienne est une infraction, même « pour voir ».

Les résultats d'un scanneur contiennent des **faux positifs** (faille signalée qui n'existe pas : version détectée à tort) et des **faux négatifs** (faille présente mais non vue). On **vérifie à la main** les points qui comptent avant de réveiller quelqu'un.

**Test flash.** Un rapport affiche 240 failles « critiques ou élevées ». Le responsable demande de tout corriger avant la fin du mois. Que réponds-tu ?

<details markdown="1">
<summary>Voir la réponse</summary>

On **priorise** : exposition, exploitation connue, valeur de l'actif, disponibilité d'un correctif. Les premières corrections vont à ce qui est **exposé et exploité** ou qui touche un actif **critique** (par exemple la sauvegarde), puis aux corrections **rapides et gratuites** (réglages). Le reste est planifié avec des **délais** selon la priorité, et les failles qu'on ne peut pas corriger reçoivent une **mesure compensatoire** ou une **acceptation de risque** écrite. « Tout corriger » sans méthode épuise l'équipe et ne réduit pas le risque plus vite.

</details>
