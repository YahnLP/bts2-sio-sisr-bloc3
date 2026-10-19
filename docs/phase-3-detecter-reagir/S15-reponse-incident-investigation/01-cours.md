# Cours – Réponse à incident et investigation

*BTS SIO SISR 2e année – Bloc 3 – S15*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

Lundi, 7 h 45 : un salarié ne peut plus ouvrir ses plans, un message réclame une rançon. Les **premières heures** décident de la suite : ce qu'on **perd**, ce qu'on **prouve**, ce qu'on **doit déclarer**. Cette séance apprend à réagir **dans l'ordre**, à **conserver les preuves** et à **reconstituer** ce qui s'est passé à partir de journaux.

---

## 1. Les phases de la réponse à incident

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 325.60 533.60" style="max-width:435px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 522.8)">
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M234.5,-512C234.5,-512 137.5,-512 137.5,-512 131.5,-512 125.5,-506 125.5,-500 125.5,-500 125.5,-487 125.5,-487 125.5,-481 131.5,-475 137.5,-475 137.5,-475 234.5,-475 234.5,-475 240.5,-475 246.5,-481 246.5,-487 246.5,-487 246.5,-500 246.5,-500 246.5,-506 240.5,-512 234.5,-512"/>
<text text-anchor="start" x="144.5" y="-490" font-family="Helvetica,sans-Serif" font-size="15.00">1. Préparer</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M196,-417C196,-417 12,-417 12,-417 6,-417 0,-411 0,-405 0,-405 0,-392 0,-392 0,-386 6,-380 12,-380 12,-380 196,-380 196,-380 202,-380 208,-386 208,-392 208,-392 208,-405 208,-405 208,-411 202,-417 196,-417"/>
<text text-anchor="start" x="19" y="-395" font-family="Helvetica,sans-Serif" font-size="15.00">2. Détecter et qualifier</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M170.19,-474.57C157.52,-460.2 139.6,-439.88 125.61,-424"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="127.8,-421.73 119.48,-417.06 123.07,-425.89 127.8,-421.73"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M162,-322C162,-322 64,-322 64,-322 58,-322 52,-316 52,-310 52,-310 52,-297 52,-297 52,-291 58,-285 64,-285 64,-285 162,-285 162,-285 168,-285 174,-291 174,-297 174,-297 174,-310 174,-310 174,-316 168,-322 162,-322"/>
<text text-anchor="start" x="71" y="-300" font-family="Helvetica,sans-Serif" font-size="15.00">3. Contenir</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M105.74,-379.57C107.06,-365.84 108.92,-346.7 110.42,-331.18"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="113.57,-331.32 111.3,-322.06 107.3,-330.72 113.57,-331.32"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M184.5,-227C184.5,-227 77.5,-227 77.5,-227 71.5,-227 65.5,-221 65.5,-215 65.5,-215 65.5,-202 65.5,-202 65.5,-196 71.5,-190 77.5,-190 77.5,-190 184.5,-190 184.5,-190 190.5,-190 196.5,-196 196.5,-202 196.5,-202 196.5,-215 196.5,-215 196.5,-221 190.5,-227 184.5,-227"/>
<text text-anchor="start" x="84.5" y="-205" font-family="Helvetica,sans-Serif" font-size="15.00">4. Éradiquer</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M116.47,-284.57C119.13,-270.84 122.83,-251.7 125.84,-236.18"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="128.98,-236.5 127.6,-227.06 122.8,-235.3 128.98,-236.5"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M191.5,-132C191.5,-132 80.5,-132 80.5,-132 74.5,-132 68.5,-126 68.5,-120 68.5,-120 68.5,-107 68.5,-107 68.5,-101 74.5,-95 80.5,-95 80.5,-95 191.5,-95 191.5,-95 197.5,-95 203.5,-101 203.5,-107 203.5,-107 203.5,-120 203.5,-120 203.5,-126 197.5,-132 191.5,-132"/>
<text text-anchor="start" x="87.5" y="-110" font-family="Helvetica,sans-Serif" font-size="15.00">5. Reprendre</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M131.96,-189.57C132.7,-175.84 133.73,-156.7 134.57,-141.18"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="137.72,-141.22 135.06,-132.06 131.43,-140.88 137.72,-141.22"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M292,-37C292,-37 108,-37 108,-37 102,-37 96,-31 96,-25 96,-25 96,-12 96,-12 96,-6 102,0 108,0 108,0 292,0 292,0 298,0 304,-6 304,-12 304,-12 304,-25 304,-25 304,-31 298,-37 292,-37"/>
<text text-anchor="start" x="115" y="-15" font-family="Helvetica,sans-Serif" font-size="15.00">6. Retour d&#39;expérience</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M148.34,-94.57C158.05,-80.46 171.71,-60.61 182.54,-44.87"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="185.41,-46.26 187.92,-37.06 180.22,-42.69 185.41,-46.26"/>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M211.24,-37.12C230.79,-69.5 269,-141.27 269,-207.5 269,-304.5 269,-304.5 269,-304.5 269,-367.52 229.48,-433.08 204.98,-467.67"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="202.42,-465.83 199.71,-474.97 207.53,-469.52 202.42,-465.83"/>
</g>
</g>
</svg>
</figure>

| Phase | Question | Exemples |
|---|---|---|
| **Préparer** | Sait-on **qui fait quoi** avant l'incident ? | Liste de contacts, procédures, sauvegardes **testées**, journaux centralisés (S11) |
| **Détecter et qualifier** | Est-ce un incident ? De quelle gravité ? | Alerte (S12), signalement d'un salarié ; **incident** ou **simple événement** ? |
| **Contenir** | Comment **arrêter l'extension** ? | Isoler la machine du réseau, couper un compte, bloquer une adresse |
| **Éradiquer** | Comment **supprimer** la cause ? | Retirer le compte créé par l'attaquant, fermer l'accès d'entrée, reconstruire les machines |
| **Reprendre** | Comment **revenir** à un fonctionnement sûr ? | Restaurer depuis une sauvegarde **saine**, surveillance renforcée |
| **Retour d'expérience** | Qu'**apprend-on** ? | Chronologie, causes, plan d'amélioration |

> [!NOTE]
> **Contenir avant d'éradiquer.** Réinstaller une machine tout de suite efface les preuves et ne règle rien si l'attaquant a encore un accès ailleurs. On **isole**, on **comprend le périmètre**, puis on **nettoie**.

### Le premier quart d'heure

| Geste | Pourquoi |
|---|---|
| **Noter l'heure** et ce qui est observé (photographier l'écran) | La première trace est souvent la plus précieuse |
| **Isoler du réseau** la machine touchée (câble ou Wi-Fi coupé) | Empêche l'extension |
| **Ne pas effacer, ne pas « nettoyer »** | Les traces disparaîtraient |
| **Alerter** la chaîne définie (responsable, direction, prestataire) | Évite de décider seul |
| **Ne pas utiliser** la machine ni les comptes touchés | Évite d'altérer les preuves |
| **Préserver** les journaux et les sauvegardes encore saines | Condition de la reprise |
| **Changer** les mots de passe des comptes concernés, **depuis une machine saine** | L'attaquant a peut-être déjà ces mots de passe |

**Éteindre ou laisser allumé ?** Un arrêt brutal fait **perdre la mémoire** (des traces utiles, parfois la clé de chiffrement) ; laisser allumé **peut laisser le chiffrement continuer**. Le choix dépend de la situation et se fait **avec** la personne compétente, de préférence selon la procédure préparée. Le guide de l'ANSSI sur les rançongiciels est la référence à consulter (à vérifier dans sa version à jour).

---

## 2. Les preuves

### L'ordre de volatilité

On collecte d'abord ce qui **disparaît le plus vite** (principe décrit par la note **RFC 3227**) :

| Ordre | Élément | Durée de vie |
|---|---|---|
| 1 | Mémoire, processus en cours, connexions réseau | Jusqu'à l'arrêt |
| 2 | Fichiers temporaires | Court |
| 3 | Disque | Persistant, mais **modifiable** |
| 4 | **Journaux distants** (collecteur, pare-feu, NAS) | Selon la conservation (S11) |
| 5 | Sauvegardes, archives | Long |

### La chaîne de preuve

Une preuve n'a de valeur que si l'on peut **démontrer qu'elle n'a pas été modifiée** :

| Règle | Mise en œuvre |
|---|---|
| **Travailler sur des copies** | L'original reste intact, rangé |
| **Empreinte** | Calculer une **empreinte** (hachage, par exemple SHA-256) de l'original **avant** et la **conserver séparément** : si le fichier change d'un octet, l'empreinte change |
| **Traçabilité** | Qui a pris la preuve, quand, où elle est rangée, qui y a accédé |
| **Horodatage fiable** | Heure de la machine et **décalage** noté (S11) |
| **Minimisation** | Ne copier que ce qui est nécessaire (données personnelles, RGPD, S04) |

> [!WARNING]
> Les **journaux d'une machine compromise** peuvent avoir été **modifiés** par l'attaquant. D'où l'intérêt des copies **distantes** (S11) et du **recoupement** de plusieurs sources : une trace absente d'un journal peut apparaître dans un autre.

---

## 3. Reconstituer la chronologie

Une chronologie est un tableau **daté** qui rassemble les événements de **toutes** les sources (S11) et distingue ce qui est **prouvé** de ce qui est **supposé**.

| Heure | Source | Événement | Interprétation | Niveau de certitude |
|---|---|---|---|---|

On cherche ensuite :

| Question | Réponse attendue |
|---|---|
| **Entrée** | Par où l'attaquant est-il entré ? (accès distant, message piégé, faille) |
| **Progression** | Quels comptes, quelles machines ? |
| **Actions** | Création de comptes, arrêt de protections, suppression de sauvegardes |
| **Données** | Y a-t-il eu **vol** (flux sortants inhabituels) avant le chiffrement ? |
| **Périmètre** | Qu'est-ce qui est **touché**, **menacé**, **sain** ? |
| **Fin** | L'attaquant est-il encore présent ? |

Dans les attaques par rançongiciel, un **vol de données avant le chiffrement** est courant (« double extorsion », S01) : retrouver les fichiers chiffrés **ne suffit pas** à clore l'incident.

---

## 4. Les obligations et la communication

| Sujet | À savoir (renvoie à la séance S04) |
|---|---|
| **Violation de données personnelles** | Notification à la **CNIL** dans les **72 heures** après en avoir pris connaissance, **si** elle présente un risque pour les personnes ; information des personnes concernées si le risque est **élevé** |
| **Plainte** | Dépôt auprès des autorités ; les preuves conservées servent |
| **Assurance** | Contrat cyber éventuel : délai de déclaration à respecter |
| **Assistance** | Dispositif national d'assistance aux victimes (cybermalveillance.gouv.fr) ; ANSSI selon les cas |
| **Clients, partenaires** | Information **maîtrisée** si leurs données ou leurs travaux sont touchés |
| **Rançon** | Les autorités recommandent de **ne pas payer** : payer ne garantit ni la restitution ni l'absence de publication, et finance les attaquants |

### Communiquer en crise

| Public | Message |
|---|---|
| **Direction** | **Faits** connus, **hypothèses**, décisions à prendre, **prochain point** à heure fixe |
| **Salariés** | Quoi faire et **ne pas faire** (ne pas éteindre, ne pas brancher de clé, ne pas répondre aux demandes de l'attaquant) |
| **Clients, autorités** | Communication **validée** par la direction, sans spéculation |

On ne communique **jamais** de supposition comme un fait.

**Test flash.** Le prestataire propose : « on réinstalle tout ce soir, ce sera réglé demain ». Que réponds-tu ?

<details markdown="1">
<summary>Voir la réponse</summary>

**Pas avant d'avoir contenu et conservé.** Réinstaller efface les **preuves** (entrée, périmètre, vol éventuel) et **ne garantit pas** que l'attaquant n'a plus d'accès ailleurs ni que la sauvegarde de reprise est saine. On isole, on **copie** ce qui doit l'être (avec empreintes), on **comprend** le périmètre, puis on reconstruit. Les délais de **notification** continuent de courir pendant ce temps.

</details>
