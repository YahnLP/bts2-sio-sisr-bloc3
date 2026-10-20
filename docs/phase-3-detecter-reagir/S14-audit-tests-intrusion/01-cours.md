# Cours – Audit de sécurité : cadre, démarche et rapport

*BTS SIO SISR 2e année – Bloc 3 – S14*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

Un audit de sécurité n'est pas « chercher des failles pour voir » : c'est une **mission encadrée**, qui répond à une question posée par l'organisation, et dont le **livrable** est un rapport qu'un dirigeant peut utiliser. Cette séance traite le **cadre**, la **démarche** et le **rapport**. Elle s'appuie sur ce que tu sais déjà faire (analyse de risques S02, scan S13) et ne demande **aucune attaque**.

---

## 1. Les types d'audit

| Type | Question posée | Méthode |
|---|---|---|
| **Organisationnel** | Les règles, rôles et procédures existent-ils et sont-ils appliqués ? | Documents, entretiens |
| **De configuration** | Les systèmes sont-ils réglés selon la référence ? (S10) | Revue de configuration, outils d'audit |
| **D'architecture** | Le découpage réseau, les flux, les accès sont-ils cohérents ? (S05) | Schémas, règles de filtrage |
| **De vulnérabilités** | Quelles failles connues sont présentes ? (S13) | Scans |
| **Test d'intrusion** | Un attaquant réaliste peut-il atteindre un objectif précis ? | Tentatives **encadrées** d'exploitation |
| **D'ingénierie sociale** | Le personnel résiste-t-il à la manipulation ? | Campagnes de sensibilisation encadrées |

Un **test d'intrusion** est l'audit le plus intrusif : il se déroule sous un cadre contractuel très précis, par des professionnels, et **jamais** « pour s'entraîner » sur un système qui n'est pas dédié à cet usage. En France, l'ANSSI qualifie des prestataires d'audit (les **PASSI**) : leur existence rappelle que le métier est encadré. Les détails (périmètre, exigences, liste à jour) sont à vérifier auprès de l'ANSSI.

---

## 2. Le cadre : avant la première commande

### L'autorisation écrite

Sans autorisation, un accès ou une tentative d'accès à un système est **pénalement répréhensible**, même sans intention de nuire (séance S04, atteintes aux systèmes de traitement automatisé de données). L'autorisation doit venir d'une personne **qui a le pouvoir** de la donner.

| Élément | Pourquoi |
|---|---|
| **Qui signe** | Le dirigeant ou son délégué **habilité** ; pas la première personne rencontrée |
| **Périmètre** | Liste **précise** : adresses, applications, locaux, comptes. Ce qui n'est pas écrit est **hors périmètre** |
| **Les tiers** | Un système **hébergé chez un prestataire** (ERP en ligne, messagerie) appartient au prestataire : **son** accord est nécessaire |
| **Dates et horaires** | Évite les confusions avec une vraie attaque et protège la production |
| **Ce qui est interdit** | Saturer un service, détruire ou copier des données, tromper des tiers… |
| **Contact d'urgence** | Pour **arrêter** immédiatement si un incident survient |
| **Confidentialité** | Les résultats et les données vues restent confidentiels ; sort des preuves à la fin |
| **Responsabilités** | Que se passe-t-il si un service tombe ? Qui est assuré ? |

### Les règles d'engagement pendant la mission

- On reste **dans le périmètre**, même si un système voisin est visiblement accessible.
- On **s'arrête et on prévient** dès qu'on trouve un **danger immédiat** (donnée sensible exposée sur Internet, intrusion déjà en cours par un tiers) : cela se signale **tout de suite**, pas dans le rapport final.
- On **minimise** les données personnelles vues : on prouve l'accès par une **capture limitée**, pas par une copie du contenu (RGPD, S04).
- On **trace** ses propres actions (qui, quoi, quand) : elles se distinguent ainsi d'une vraie attaque.

---

## 3. La démarche

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 240.60 628.60" style="max-width:321px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 617.8)">
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M151.5,-607C151.5,-607 67.5,-607 67.5,-607 61.5,-607 55.5,-601 55.5,-595 55.5,-595 55.5,-582 55.5,-582 55.5,-576 61.5,-570 67.5,-570 67.5,-570 151.5,-570 151.5,-570 157.5,-570 163.5,-576 163.5,-582 163.5,-582 163.5,-595 163.5,-595 163.5,-601 157.5,-607 151.5,-607"/>
<text text-anchor="start" x="74.5" y="-585" font-family="Helvetica,sans-Serif" font-size="15.00">1. Cadrer</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M159.5,-512C159.5,-512 59.5,-512 59.5,-512 53.5,-512 47.5,-506 47.5,-500 47.5,-500 47.5,-487 47.5,-487 47.5,-481 53.5,-475 59.5,-475 59.5,-475 159.5,-475 159.5,-475 165.5,-475 171.5,-481 171.5,-487 171.5,-487 171.5,-500 171.5,-500 171.5,-506 165.5,-512 159.5,-512"/>
<text text-anchor="start" x="66.5" y="-490" font-family="Helvetica,sans-Serif" font-size="15.00">2. Collecter</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M109.5,-569.57C109.5,-555.84 109.5,-536.7 109.5,-521.18"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="112.65,-521.06 109.5,-512.06 106.35,-521.06 112.65,-521.06"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M159,-417C159,-417 60,-417 60,-417 54,-417 48,-411 48,-405 48,-405 48,-392 48,-392 48,-386 54,-380 60,-380 60,-380 159,-380 159,-380 165,-380 171,-386 171,-392 171,-392 171,-405 171,-405 171,-411 165,-417 159,-417"/>
<text text-anchor="start" x="67" y="-395" font-family="Helvetica,sans-Serif" font-size="15.00">3. Analyser</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M109.5,-474.57C109.5,-460.84 109.5,-441.7 109.5,-426.18"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="112.65,-426.06 109.5,-417.06 106.35,-426.06 112.65,-426.06"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M205,-322C205,-322 14,-322 14,-322 8,-322 2,-316 2,-310 2,-310 2,-297 2,-297 2,-291 8,-285 14,-285 14,-285 205,-285 205,-285 211,-285 217,-291 217,-297 217,-297 217,-310 217,-310 217,-316 211,-322 205,-322"/>
<text text-anchor="start" x="21" y="-300" font-family="Helvetica,sans-Serif" font-size="15.00">4. Qualifier les constats</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M109.5,-379.57C109.5,-365.84 109.5,-346.7 109.5,-331.18"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="112.65,-331.06 109.5,-322.06 106.35,-331.06 112.65,-331.06"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M155,-227C155,-227 64,-227 64,-227 58,-227 52,-221 52,-215 52,-215 52,-202 52,-202 52,-196 58,-190 64,-190 64,-190 155,-190 155,-190 161,-190 167,-196 167,-202 167,-202 167,-215 167,-215 167,-221 161,-227 155,-227"/>
<text text-anchor="start" x="71" y="-205" font-family="Helvetica,sans-Serif" font-size="15.00">5. Rédiger</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M109.5,-284.57C109.5,-270.84 109.5,-251.7 109.5,-236.18"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="112.65,-236.06 109.5,-227.06 106.35,-236.06 112.65,-236.06"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M160,-132C160,-132 59,-132 59,-132 53,-132 47,-126 47,-120 47,-120 47,-107 47,-107 47,-101 53,-95 59,-95 59,-95 160,-95 160,-95 166,-95 172,-101 172,-107 172,-107 172,-120 172,-120 172,-126 166,-132 160,-132"/>
<text text-anchor="start" x="66" y="-110" font-family="Helvetica,sans-Serif" font-size="15.00">6. Restituer</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M109.5,-189.57C109.5,-175.84 109.5,-156.7 109.5,-141.18"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="112.65,-141.06 109.5,-132.06 106.35,-141.06 112.65,-141.06"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M207,-37C207,-37 12,-37 12,-37 6,-37 0,-31 0,-25 0,-25 0,-12 0,-12 0,-6 6,0 12,0 12,0 207,0 207,0 213,0 219,-6 219,-12 219,-12 219,-25 219,-25 219,-31 213,-37 207,-37"/>
<text text-anchor="start" x="19" y="-15" font-family="Helvetica,sans-Serif" font-size="15.00">7. Suivre les corrections</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M109.5,-94.57C109.5,-80.84 109.5,-61.7 109.5,-46.18"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="112.65,-46.06 109.5,-37.06 106.35,-46.06 112.65,-46.06"/>
</g>
</g>
</svg>
</figure>

| Étape | Contenu |
|---|---|
| **Cadrer** | Objectif, périmètre, méthode, calendrier, autorisation signée |
| **Collecter** | Documents, entretiens, configurations, résultats d'outils |
| **Analyser** | Comparer **ce qui est** à **ce qui devrait être** (référence : politique de sécurité, guides) |
| **Qualifier** | Pour chaque constat : **preuve**, **gravité**, **facilité**, **priorité** |
| **Rédiger** | Un rapport **pour deux lecteurs** : la direction et les techniciens |
| **Restituer** | Une présentation orale, un échange, des décisions |
| **Suivre** | Un nouveau contrôle prouve que les corrections ont eu lieu (S13) |

### La qualité d'un constat

Un bon constat est : **factuel** (ce qui est observé, pas ce qui est supposé), **prouvé** (extrait, capture, mesure), **daté**, **reproductible**, **mesuré** (gravité, effet pour l'organisation), **relié** à une exigence (référentiel, politique).

| Niveau de preuve | Exemple |
|---|---|
| **Solide** | Capture de la configuration qui montre le port exposé |
| **Partielle** | Le responsable dit que « les sauvegardes fonctionnent » : à vérifier |
| **Insuffisante** | « Il paraît qu'il n'y a pas de journaux » : **ne se met pas dans un rapport** tant que c'est non vérifié |

> [!WARNING]
> Un constat **sans preuve** discrédite tout le rapport. Mieux vaut un constat **à confirmer** (indiqué comme tel) qu'une affirmation fausse.

---

## 4. Le rapport

| Partie | Lecteur | Contenu |
|---|---|---|
| **Résumé managérial** | Direction | Une page : le **bilan**, les **trois risques majeurs**, les **actions prioritaires**, sans jargon |
| **Contexte et méthode** | Tous | Mission, périmètre, dates, limites (ce qui n'a pas été regardé) |
| **Constats** | Techniciens | Une **fiche par constat** |
| **Plan d'action** | Direction et techniciens | Actions classées par **priorité**, responsable proposé, délai |
| **Annexes** | Techniciens | Preuves détaillées, sorties d'outils |

### Une fiche de constat

| Champ | Contenu |
|---|---|
| Identifiant et titre | `C03 – Sauvegarde jamais testée` |
| Description | Ce qui a été observé |
| Preuve | Référence à l'annexe |
| Risque | Ce que cela permet, pour **quelle valeur métier** (S02) |
| Gravité et facilité | Échelles de 1 à 4 |
| Recommandation | Action **précise** et **réaliste** |
| Priorité | Selon une règle écrite (S13) |

Une recommandation utile est **précise** (« désactiver la redirection du port 3389 sur la box, ouvrir un accès par VPN ») et non générique (« améliorer la sécurité »).

### La restitution orale

Cinq minutes pour un dirigeant : **ce qui va bien** (commencer par là, c'est vrai et cela se reçoit mieux), **les trois risques**, **les décisions à prendre aujourd'hui**, **ce que cela coûte** (temps, argent), **quand on revérifie**.

---

### Auditer par rapport à un référentiel

Un audit de conformité compare l'existant à un référentiel (guide d'hygiène de l'ANSSI, CIS Benchmark, politique de sécurité interne). Pour chaque mesure du référentiel, on relève une **preuve** (capture, extrait de configuration, entretien) et on classe :

| Verdict | Sens |
|---|---|
| **Conforme** | La mesure est en place, la preuve existe |
| **Partiellement conforme** | Elle est en place sur une partie du périmètre |
| **Non conforme** | Elle est absente ou inefficace |
| **Non applicable** | Elle ne concerne pas le périmètre (à justifier) |

Un **écart assumé** est un écart non corrigé par choix, avec une justification et un responsable. Un verdict sans preuve n'est pas un résultat d'audit. Panorama des référentiels : [Normes et référentiels de sécurité](../../ressources/normes-securite.md).

**Test flash.** Le référentiel demande une authentification multifacteur sur tous les accès d'administration. Tu constates qu'elle est active sur le VPN mais pas sur l'interface du pare-feu. Quel verdict ? Que notes-tu comme preuve ?

<details markdown="1">
<summary>Voir la réponse</summary>

**Partiellement conforme** : la mesure existe sur une partie du périmètre. Preuves : la capture du réglage MFA du VPN et la capture de la page de connexion du pare-feu sans second facteur. Le constat précise le périmètre non couvert.

</details>

## 5. Ce qu'on fait des découvertes imprévues

| Situation | Réflexe |
|---|---|
| **Danger immédiat** (accès ouvert, intrusion en cours) | **Prévenir tout de suite** le contact d'urgence, par un canal sûr |
| **Données personnelles** sensibles découvertes | **Ne pas les copier**, minimiser, signaler dans le rapport sans les reproduire |
| **Activité manifestement illicite** (hors sujet de la mission) | S'arrêter, prévenir le donneur d'ordre, se faire conseiller juridiquement |
| **Système hors périmètre** accessible | **Ne pas y toucher** ; le signaler |

**Test flash.** On te demande « un test d'intrusion de l'entreprise » par courriel, sans plus de précisions. Que fais-tu ?

<details markdown="1">
<summary>Voir la réponse</summary>

**Rien de technique.** Tu demandes un cadrage écrit : objectif, périmètre précis, tiers concernés (leur accord), dates, interdits, contact d'urgence, signataire habilité. Sans cela, ni test ni scan : la demande, aussi bienveillante soit-elle, ne vaut pas autorisation.

</details>
