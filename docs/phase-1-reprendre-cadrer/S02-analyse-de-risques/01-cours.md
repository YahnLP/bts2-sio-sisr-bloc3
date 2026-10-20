# Cours – Analyser les risques

*BTS SIO SISR 2e année – Bloc 3 – S02*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

Tu sais désormais mettre en place des mesures de sécurité. Reste une question : **lesquelles, dans quel ordre, et pourquoi celles-là ?** Une organisation n'a ni le temps ni l'argent de tout protéger. L'**analyse de risques** sert à décider.

> [!NOTE]
> **Une méthode simplifiée.** Cette séance s'inspire de la méthode **EBIOS Risk Manager** publiée par l'ANSSI (démarche en cinq ateliers). Elle en garde l'esprit et allège le formalisme. Les échelles de gravité et de vraisemblance ci-dessous sont celles **de la séance** ; la méthode officielle a les siennes. Le guide de l'ANSSI reste la référence.

---

## 1. Le vocabulaire du risque

| Mot | Définition | Exemple (une menuiserie industrielle) |
|---|---|---|
| **Valeur métier** | Ce qui compte pour l'organisation : un service, une information, un savoir-faire | Fabriquer et livrer à temps ; garder confidentiels les plans des clients |
| **Bien support** | Ce sur quoi repose une valeur métier : serveur, poste, réseau, logiciel, local, personne | Le serveur de fichiers des plans ; la machine à commande numérique et son poste |
| **Événement redouté** | Ce qui arrive à une valeur métier et qu'on ne veut pas | Les plans sont publiés ; la production est à l'arrêt trois jours |
| **Source de risque** | Qui ou quoi peut provoquer l'événement | Un cybercriminel, un concurrent, un salarié mécontent |
| **Objectif visé** | Ce que la source cherche à obtenir | Une rançon, copier un savoir-faire, nuire |
| **Scénario** | L'enchaînement des étapes qui mène de la source à l'événement redouté | Message piégé → poste infecté → serveur de fichiers chiffré |
| **Risque** | Un scénario évalué par sa **gravité** et sa **vraisemblance** | Gravité forte, vraisemblance forte : risque élevé |

On retrouve les critères vus en première année : un événement redouté **atteint** la disponibilité, l'intégrité, la confidentialité ou la preuve d'une valeur métier.

---

## 2. La démarche en cinq étapes

| Étape | On répond à la question | On produit |
|---|---|---|
| **1. Cadrer** | Qu'est-ce qui compte, et qu'est-ce qui est déjà en place ? | Valeurs métier, biens supports, événements redoutés avec leur gravité, mesures existantes |
| **2. Sources de risque** | Qui pourrait nous nuire, et pour obtenir quoi ? | Couples source de risque / objectif visé, retenus selon leur pertinence |
| **3. Scénarios stratégiques** | Par quels chemins globaux (dont les **partenaires et prestataires**) peut-on atteindre nos valeurs ? | Quelques scénarios de haut niveau |
| **4. Scénarios opérationnels** | Comment, techniquement, étape par étape ? | Chaînes d'attaque, avec leur vraisemblance |
| **5. Traiter** | Que fait-on de chaque risque ? | Plan de traitement, risque résiduel |

Dans la séance, les étapes 3 et 4 sont regroupées en un seul tableau de **scénarios**.

> [!WARNING]
> **Un chemin d'attaque passe souvent par un tiers.** Un prestataire de maintenance, un hébergeur, un logiciel en ligne : s'ils sont compromis, ils ouvrent l'accès à l'organisation. Une analyse qui ne regarde que l'intérieur du réseau est incomplète.

---

## 3. Mesurer : gravité, vraisemblance, niveau de risque

**Gravité** de l'événement redouté pour l'organisation (échelle de la séance) :

| Niveau | Nom | Repère |
|---|---|---|
| 1 | Mineure | Gêne, rattrapable sans coût notable |
| 2 | Significative | Perturbation de quelques jours ou perte financière supportable |
| 3 | Grave | Arrêt d'une activité clé, atteinte à l'image, obligation de notification |
| 4 | Critique | Survie de l'organisation menacée |

**Vraisemblance** du scénario (échelle de la séance) :

| Niveau | Nom | Repère |
|---|---|---|
| 1 | Improbable | Demande des moyens très importants ou des conditions rares |
| 2 | Peu probable | Possible, mais demande de la compétence ou une circonstance particulière |
| 3 | Probable | Attaque courante, protections faibles |
| 4 | Très probable | Déjà arrivée, ou à la portée de n'importe qui, aucune protection |

**Niveau de risque = gravité × vraisemblance.**

| Produit | Niveau | Que fait-on ? |
|---|---|---|
| 1 à 3 | **Faible** | On accepte, on surveille |
| 4 à 8 | **Moyen** | On réduit si le coût est raisonnable |
| 9 à 16 | **Élevé** | On traite en priorité |

> [!NOTE]
> Une règle de bon sens complète le tableau : un événement de gravité **4** ne s'accepte pas sans que la direction l'ait décidé par écrit, même si le produit est faible.

---

## 4. Traiter un risque

Quatre décisions possibles :

| Décision | Sens | Exemple |
|---|---|---|
| **Réduire** | Ajouter des mesures qui baissent la gravité ou la vraisemblance | Sauvegarde isolée, cloisonnement du réseau |
| **Éviter** | Supprimer la cause | Ne plus exposer un service sur Internet |
| **Transférer** | Faire porter une partie du risque par un tiers | Assurance cyber, hébergement chez un prestataire (avec contrat) |
| **Accepter** | Décider en connaissance de cause de ne rien faire | Risque faible, coût de la mesure disproportionné |

Une mesure se choisit sur trois critères : **efficacité** (quel risque baisse-t-il, et de combien ?), **coût** (achat, temps, gêne pour les utilisateurs) et **délai**.

Après traitement, il reste un **risque résiduel** : on le réévalue avec les mêmes échelles et c'est la **direction** qui l'accepte, pas le technicien.

---

## 5. Une chaîne d'attaque, pas une liste de failles

Un scénario opérationnel se lit comme une histoire :

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 363.60 533.60" style="max-width:485px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 522.8)">
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M262.5,-512C262.5,-512 79.5,-512 79.5,-512 73.5,-512 67.5,-506 67.5,-500 67.5,-500 67.5,-487 67.5,-487 67.5,-481 73.5,-475 79.5,-475 79.5,-475 262.5,-475 262.5,-475 268.5,-475 274.5,-481 274.5,-487 274.5,-487 274.5,-500 274.5,-500 274.5,-506 268.5,-512 262.5,-512"/>
<text text-anchor="start" x="86.5" y="-490" font-family="Helvetica,sans-Serif" font-size="15.00">Source : cybercriminel</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M306,-417C306,-417 36,-417 36,-417 30,-417 24,-411 24,-405 24,-405 24,-392 24,-392 24,-386 30,-380 36,-380 36,-380 306,-380 306,-380 312,-380 318,-386 318,-392 318,-392 318,-405 318,-405 318,-411 312,-417 306,-417"/>
<text text-anchor="start" x="43" y="-395" font-family="Helvetica,sans-Serif" font-size="15.00">Message piégé reçu par un salarié</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M171,-474.57C171,-460.84 171,-441.7 171,-426.18"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="174.15,-426.06 171,-417.06 167.85,-426.06 174.15,-426.06"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M226.5,-322C226.5,-322 115.5,-322 115.5,-322 109.5,-322 103.5,-316 103.5,-310 103.5,-310 103.5,-297 103.5,-297 103.5,-291 109.5,-285 115.5,-285 115.5,-285 226.5,-285 226.5,-285 232.5,-285 238.5,-291 238.5,-297 238.5,-297 238.5,-310 238.5,-310 238.5,-316 232.5,-322 226.5,-322"/>
<text text-anchor="start" x="122.5" y="-300" font-family="Helvetica,sans-Serif" font-size="15.00">Poste infecté</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M171,-379.57C171,-365.84 171,-346.7 171,-331.18"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="174.15,-331.06 171,-322.06 167.85,-331.06 174.15,-331.06"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M327,-227C327,-227 15,-227 15,-227 9,-227 3,-221 3,-215 3,-215 3,-202 3,-202 3,-196 9,-190 15,-190 15,-190 327,-190 327,-190 333,-190 339,-196 339,-202 339,-202 339,-215 339,-215 339,-221 333,-227 327,-227"/>
<text text-anchor="start" x="22" y="-205" font-family="Helvetica,sans-Serif" font-size="15.00">Déplacement vers le serveur de fichiers</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M171,-284.57C171,-270.84 171,-251.7 171,-236.18"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="174.15,-236.06 171,-227.06 167.85,-236.06 174.15,-236.06"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M245.5,-132C245.5,-132 96.5,-132 96.5,-132 90.5,-132 84.5,-126 84.5,-120 84.5,-120 84.5,-107 84.5,-107 84.5,-101 90.5,-95 96.5,-95 96.5,-95 245.5,-95 245.5,-95 251.5,-95 257.5,-101 257.5,-107 257.5,-107 257.5,-120 257.5,-120 257.5,-126 251.5,-132 245.5,-132"/>
<text text-anchor="start" x="103.5" y="-110" font-family="Helvetica,sans-Serif" font-size="15.00">Données chiffrées</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M171,-189.57C171,-175.84 171,-156.7 171,-141.18"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="174.15,-141.06 171,-132.06 167.85,-141.06 174.15,-141.06"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M330,-37C330,-37 12,-37 12,-37 6,-37 0,-31 0,-25 0,-25 0,-12 0,-12 0,-6 6,0 12,0 12,0 330,0 330,0 336,0 342,-6 342,-12 342,-12 342,-25 342,-25 342,-31 336,-37 330,-37"/>
<text text-anchor="start" x="19" y="-15" font-family="Helvetica,sans-Serif" font-size="15.00">Événement redouté : production arrêtée</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M171,-94.57C171,-80.84 171,-61.7 171,-46.18"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="174.15,-46.06 171,-37.06 167.85,-46.06 174.15,-46.06"/>
</g>
</g>
</svg>
</figure>

Chaque flèche est une **occasion de couper la chaîne** : filtrer le message, limiter les droits du poste, cloisonner le réseau, sauvegarder hors ligne. On choisit les mesures **là où elles coupent plusieurs scénarios à la fois**.

---

## 6. S'appuyer sur une norme ou un guide

Une analyse de risques dit **quoi protéger en priorité**. Pour choisir les **mesures**, on ne part pas d'une page blanche : on puise dans un catalogue reconnu (guide d'hygiène de l'ANSSI, ISO 27002, CIS Controls). Chaque mesure retenue se **justifie** par un risque identifié et se **rattache** à un référentiel : « risque R3 (rançongiciel) → mesure : sauvegarde déconnectée → recommandation du guide d'hygiène ».

La page [Normes et référentiels de sécurité](../../ressources/normes-securite.md) donne le panorama (loi, norme, guide, méthode) et un exercice de classement. L'exercice se fait en 15 minutes en fin de séance si le temps le permet.

---

## 7. Ce que l'épreuve E7 attend

Dans l'étude de cas, on demande rarement « l'analyse EBIOS complète ». On demande de **repérer les risques dans le dossier documentaire**, de les **classer**, de **proposer des mesures** et de les **justifier**. La structure **risque → mesure → justification → limite** de la page [L'épreuve E7](../../ressources/epreuve-e7.md) est exactement le fruit de cette séance.

**Test flash.** Un hébergeur de messagerie est victime d'une attaque et les courriels d'une PME sont consultés. Quelle étape de la démarche aurait dû le faire apparaître ?

<details markdown="1">
<summary>Voir la réponse</summary>

Les **scénarios stratégiques** : ils regardent les **partenaires et prestataires** comme chemins d'attaque. Mesures possibles : exigences de sécurité dans le contrat, chiffrement des données sensibles avant dépôt, authentification multifacteur sur le compte.

</details>
