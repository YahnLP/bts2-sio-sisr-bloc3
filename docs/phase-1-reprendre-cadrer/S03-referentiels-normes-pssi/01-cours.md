# Cours – Référentiels, normes et politique de sécurité

*BTS SIO SISR 2e année – Bloc 3 – S03*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

L'analyse de risques (S02) dit **quoi** protéger en priorité. Cette séance répond à : **avec quelles bonnes pratiques reconnues, et comment l'organisation écrit-elle ses règles ?** On n'invente pas ses mesures : on s'appuie sur des **référentiels**, et on décide par écrit dans une **politique de sécurité**.

> [!WARNING]
> **Les intitulés, les versions et les numéros de mesures changent.** Cette page donne l'esprit et l'usage de chaque référentiel. Avant de citer une mesure précise dans un document, **relis le texte à jour** à la source.

---

## 1. Pourquoi des référentiels ?

- Ne pas partir d'une page blanche : des mesures éprouvées existent.
- **Parler le même langage** avec un client, un auditeur, un assureur.
- **Justifier** une mesure : « le guide d'hygiène de l'ANSSI la recommande » pèse plus que « je pense que ».
- **Mesurer** : on peut comparer son état à une liste.

Un référentiel n'est **pas** une analyse de risques : il dit ce qui se fait en général, pas ce qui compte **chez toi**. On utilise les deux ensemble : le risque choisit, le référentiel fournit les mesures.

---

## 2. Les grandes familles

| Référentiel | Nature | À quoi il sert |
|---|---|---|
| **ISO/IEC 27001** | Norme d'**exigences** d'un **système de management de la sécurité de l'information (SMSI)** | On peut être **certifié** : un organisme indépendant vérifie que l'organisation gère la sécurité de façon organisée et continue |
| **ISO/IEC 27002** | Guide de **bonnes pratiques** : catalogue de mesures | On y choisit des mesures ; on ne se fait **pas** certifier sur ce guide seul |
| **Guide d'hygiène informatique de l'ANSSI** | Recommandations **françaises**, accessibles, pour toute organisation | Un socle de base, très utilisé en France |
| **CIS Controls** (et guides de configuration CIS) | Mesures **priorisées** et guides de durcissement par système | Savoir par quoi commencer ; configurer un système précisément |
| **RGPD** | **Loi** européenne | Obligation de sécuriser les données personnelles (voir S04) |

> [!NOTE]
> **Norme, guide, loi : trois forces différentes.** Une loi s'**impose** ; une norme se **choisit** (et se certifie, s'il y a intérêt) ; un guide se **suit** ou non. Dans une étude de cas, repère laquelle de ces trois forces s'applique à l'organisation.

### Le SMSI et la roue d'amélioration continue

ISO/IEC 27001 demande de faire **vivre** la sécurité, pas de la poser une fois :

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 442.60 343.60" style="max-width:591px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 332.8)">
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M409,-322C409,-322 116,-322 116,-322 110,-322 104,-316 104,-310 104,-310 104,-297 104,-297 104,-291 110,-285 116,-285 116,-285 409,-285 409,-285 415,-285 421,-291 421,-297 421,-297 421,-310 421,-310 421,-316 415,-322 409,-322"/>
<text text-anchor="start" x="123" y="-300" font-family="Helvetica,sans-Serif" font-size="15.00">Planifier : risques, objectifs, politique</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M289,-227C289,-227 36,-227 36,-227 30,-227 24,-221 24,-215 24,-215 24,-202 24,-202 24,-196 30,-190 36,-190 36,-190 289,-190 289,-190 295,-190 301,-196 301,-202 301,-202 301,-215 301,-215 301,-221 295,-227 289,-227"/>
<text text-anchor="start" x="43" y="-205" font-family="Helvetica,sans-Serif" font-size="15.00">Réaliser : appliquer les mesures</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M243.22,-284.57C227.63,-270.07 205.52,-249.51 188.39,-233.58"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="190.12,-230.88 181.38,-227.06 185.83,-235.5 190.12,-230.88"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M297,-132C297,-132 12,-132 12,-132 6,-132 0,-126 0,-120 0,-120 0,-107 0,-107 0,-101 6,-95 12,-95 12,-95 297,-95 297,-95 303,-95 309,-101 309,-107 309,-107 309,-120 309,-120 309,-126 303,-132 297,-132"/>
<text text-anchor="start" x="19" y="-110" font-family="Helvetica,sans-Serif" font-size="15.00">Vérifier : contrôles, audits, incidents</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M160.96,-189.57C159.78,-175.84 158.13,-156.7 156.79,-141.18"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="159.92,-140.76 156.01,-132.06 153.64,-141.3 159.92,-140.76"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M360.5,-37C360.5,-37 162.5,-37 162.5,-37 156.5,-37 150.5,-31 150.5,-25 150.5,-25 150.5,-12 150.5,-12 150.5,-6 156.5,0 162.5,0 162.5,0 360.5,0 360.5,0 366.5,0 372.5,-6 372.5,-12 372.5,-12 372.5,-25 372.5,-25 372.5,-31 366.5,-37 360.5,-37"/>
<text text-anchor="start" x="169.5" y="-15" font-family="Helvetica,sans-Serif" font-size="15.00">Agir : corriger, améliorer</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M174.88,-94.79C191.69,-80.18 215.69,-59.32 234.16,-43.26"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="236.47,-45.43 241.2,-37.15 232.34,-40.67 236.47,-45.43"/>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M284.27,-37.24C300.02,-51.05 319.67,-71.74 328.5,-95 349.36,-149.92 342.66,-172.19 321.5,-227 314.1,-246.16 300.11,-264.4 287.62,-278.16"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="285.13,-276.2 281.26,-284.92 289.72,-280.52 285.13,-276.2"/>
</g>
</g>
</svg>
</figure>

---

## 3. Les familles de mesures d'hygiène

Les guides se ressemblent. Les mesures se rangent en grandes familles, à connaître comme **plan de lecture** d'un dossier :

| Famille | Exemples de mesures |
|---|---|
| **Sensibiliser et former** | Charte, formation, exercices d'hameçonnage |
| **Connaître son système** | Inventaire des équipements, des logiciels, des comptes |
| **Authentifier et contrôler les accès** | Mots de passe robustes, multifacteur, moindre privilège, revue des droits |
| **Sécuriser les postes** | Mises à jour, chiffrement du disque, antivirus ou EDR, pas de droits d'administrateur |
| **Sécuriser le réseau** | Segmentation, filtrage, Wi-Fi sécurisé, accès distant protégé |
| **Sécuriser l'administration** | Comptes d'administration distincts, accès d'administration limités |
| **Assurer la sûreté** | Onduleur et parafoudre, détection et extinction d'incendie, protection contre l'eau, climat du local, accès physique contrôlé, redondance des alimentations et des disques |
| **Gérer le nomadisme** | Postes portables chiffrés, connexion distante par VPN |
| **Maintenir à jour** | Correctifs, matériel et logiciels encore supportés |
| **Superviser, auditer, réagir** | Journaux, alertes, audit, plan de réponse à incident |
| **Sauvegarder et reprendre** | Sauvegarde isolée testée, plan de reprise |

> [!NOTE]
> **Sûreté et sécurité.** La sûreté protège des événements **non intentionnels** (panne, incendie, eau, coupure électrique), la sécurité des actes **malveillants**. Une analyse de risques (S02) qui ne contient que des scénarios d'attaque oublie la moitié des sinistres réels ; la politique doit nommer les deux.

---

## 4. La politique de sécurité (PSSI)

La **politique de sécurité du système d'information (PSSI)** est le document par lequel la **direction** dit : voici ce que nous protégeons, selon quels principes, et qui est responsable de quoi. Elle est **signée par la direction** : sans elle, la sécurité reste l'affaire d'un technicien seul.

Contenu type :

| Rubrique | Contenu |
|---|---|
| **Périmètre et enjeux** | Ce que couvre la politique ; les valeurs métier à protéger |
| **Principes** | Moindre privilège, défense en profondeur, sauvegardes, journalisation… |
| **Organisation** | Qui décide, qui administre, qui contrôle ; qui prévenir en cas d'incident |
| **Règles** | Mots de passe, postes, accès distant, supports amovibles, données personnelles… |
| **Contrôle et révision** | Audits, indicateurs, date de révision, sanctions |

### Politique, procédure, mode opératoire

| Niveau | Question | Exemple |
|---|---|---|
| **Politique** | Que veut-on, pourquoi ? | « Les données sont sauvegardées et la restauration est testée. » |
| **Procédure** | Qui fait quoi, quand ? | « Chaque mois, l'administrateur teste une restauration et en rend compte à la direction. » |
| **Mode opératoire** | Comment, geste par geste ? | « Étapes pour restaurer un dossier depuis le NAS. » |

### La charte d'usage

La **charte informatique** est le versant **utilisateur** : ce qu'on a le droit et l'interdiction de faire avec les moyens de l'entreprise, ce que l'entreprise surveille et pourquoi. Elle gagne à être courte, claire et **annexée au règlement intérieur** pour être opposable (point à vérifier avec le service juridique ; voir S04).

---

## 5. Relier risque, référentiel et politique

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 439.60 438.60" style="max-width:587px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 427.8)">
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M403.5,-417C403.5,-417 204.5,-417 204.5,-417 198.5,-417 192.5,-411 192.5,-405 192.5,-405 192.5,-392 192.5,-392 192.5,-386 198.5,-380 204.5,-380 204.5,-380 403.5,-380 403.5,-380 409.5,-380 415.5,-386 415.5,-392 415.5,-392 415.5,-405 415.5,-405 415.5,-411 409.5,-417 403.5,-417"/>
<text text-anchor="start" x="211.5" y="-395" font-family="Helvetica,sans-Serif" font-size="15.00">Analyse de risques : S02</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M341.5,-322C341.5,-322 44.5,-322 44.5,-322 38.5,-322 32.5,-316 32.5,-310 32.5,-310 32.5,-297 32.5,-297 32.5,-291 38.5,-285 44.5,-285 44.5,-285 341.5,-285 341.5,-285 347.5,-285 353.5,-291 353.5,-297 353.5,-297 353.5,-310 353.5,-310 353.5,-316 347.5,-322 341.5,-322"/>
<text text-anchor="start" x="51.5" y="-300" font-family="Helvetica,sans-Serif" font-size="15.00">Mesures choisies dans les référentiels</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M282.86,-379.79C265.35,-365.11 240.31,-344.14 221.11,-328.05"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="222.98,-325.51 214.06,-322.15 218.94,-330.34 222.98,-325.51"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M352,-227C352,-227 12,-227 12,-227 6,-227 0,-221 0,-215 0,-215 0,-202 0,-202 0,-196 6,-190 12,-190 12,-190 352,-190 352,-190 358,-190 364,-196 364,-202 364,-202 364,-215 364,-215 364,-221 358,-227 352,-227"/>
<text text-anchor="start" x="19" y="-205" font-family="Helvetica,sans-Serif" font-size="15.00">Politique de sécurité signée par la direction</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M190.88,-284.57C189.26,-270.84 186.99,-251.7 185.16,-236.18"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="188.26,-235.63 184.08,-227.06 182.01,-236.37 188.26,-235.63"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M332.5,-132C332.5,-132 71.5,-132 71.5,-132 65.5,-132 59.5,-126 59.5,-120 59.5,-120 59.5,-107 59.5,-107 59.5,-101 65.5,-95 71.5,-95 71.5,-95 332.5,-95 332.5,-95 338.5,-95 344.5,-101 344.5,-107 344.5,-107 344.5,-120 344.5,-120 344.5,-126 338.5,-132 332.5,-132"/>
<text text-anchor="start" x="78.5" y="-110" font-family="Helvetica,sans-Serif" font-size="15.00">Procédures et modes opératoires</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M185.86,-189.57C188.81,-175.84 192.93,-156.7 196.26,-141.18"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="199.41,-141.52 198.22,-132.06 193.25,-140.2 199.41,-141.52"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M406,-37C406,-37 202,-37 202,-37 196,-37 190,-31 190,-25 190,-25 190,-12 190,-12 190,-6 196,0 202,0 202,0 406,0 406,0 412,0 418,-6 418,-12 418,-12 418,-25 418,-25 418,-31 412,-37 406,-37"/>
<text text-anchor="start" x="209" y="-15" font-family="Helvetica,sans-Serif" font-size="15.00">Contrôle, audit, incidents</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M221.67,-94.57C237.71,-79.94 260.52,-59.14 278.06,-43.15"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="280.21,-45.45 284.74,-37.06 275.97,-40.8 280.21,-45.45"/>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M321.95,-37.09C335.55,-51.43 353.6,-72.88 364,-95 382.36,-134.05 379.53,-147.08 384,-190 390.1,-248.55 397.43,-268.44 373,-322 363.95,-341.85 347.68,-360.05 333.22,-373.59"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="330.86,-371.48 326.3,-379.86 335.09,-376.15 330.86,-371.48"/>
</g>
</g>
</svg>
</figure>

**Test flash.** Une PME dit : « nous sommes conformes à ISO/IEC 27002 ». Pourquoi cette phrase ne prouve-t-elle rien à un client ?

<details markdown="1">
<summary>Voir la réponse</summary>

ISO/IEC 27002 est un **guide de mesures**, pas une norme de certification : on ne peut pas s'y faire certifier. La preuve attendue serait une certification **ISO/IEC 27001** (un SMSI audité), ou à défaut un **audit** ou une **liste de mesures appliquées** vérifiable.

</details>
