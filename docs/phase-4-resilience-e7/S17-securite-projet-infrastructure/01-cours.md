# Cours – La sécurité dans un projet d'infrastructure

*BTS SIO SISR 2e année – Bloc 3 – S17*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

Tout ce que tu as vu depuis S01 se corrige **après coup** : durcir, filtrer, journaliser, sauvegarder. Cette séance renverse l'ordre : **intégrer la sécurité au projet dès le cahier des charges**, la chiffrer, la faire **tester à la livraison** et la **maintenir** ensuite. C'est aussi ce qu'on attend dans l'épreuve E7 (proposer, justifier, chiffrer). Le cahier des charges lui-même est vu au bloc 2 : ici on n'en refait pas le cours, on y **ajoute la sécurité**.

---

## 1. Pourquoi dès la conception

| Intégrer la sécurité… | Conséquence |
|---|---|
| **Au départ** | Une exigence coûte peu : elle s'ajoute au plan |
| **À la livraison** | Il faut **refaire** : coût élevé, délai, parfois impossible (architecture figée) |
| **Après un incident** | On paie l'incident **et** la correction |

Deux principes, issus du RGPD (séance S04) et de la pratique :

| Principe | Sens |
|---|---|
| **Protection des données dès la conception et par défaut** | Le système collecte **le minimum**, avec les réglages les **plus protecteurs** par défaut |
| **Défense en profondeur** | Plusieurs barrières successives ; la chute d'une ne suffit pas (S02, S05) |

---

## 2. De l'analyse de risques aux exigences

Le chemin :

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 219.60 438.60" style="max-width:293px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 427.8)">
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M157.5,-417C157.5,-417 40.5,-417 40.5,-417 34.5,-417 28.5,-411 28.5,-405 28.5,-405 28.5,-392 28.5,-392 28.5,-386 34.5,-380 40.5,-380 40.5,-380 157.5,-380 157.5,-380 163.5,-380 169.5,-386 169.5,-392 169.5,-392 169.5,-405 169.5,-405 169.5,-411 163.5,-417 157.5,-417"/>
<text text-anchor="start" x="47.5" y="-395" font-family="Helvetica,sans-Serif" font-size="15.00">Risques &#45; S02</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M183.5,-322C183.5,-322 14.5,-322 14.5,-322 8.5,-322 2.5,-316 2.5,-310 2.5,-310 2.5,-297 2.5,-297 2.5,-291 8.5,-285 14.5,-285 14.5,-285 183.5,-285 183.5,-285 189.5,-285 195.5,-291 195.5,-297 195.5,-297 195.5,-310 195.5,-310 195.5,-316 189.5,-322 183.5,-322"/>
<text text-anchor="start" x="21.5" y="-300" font-family="Helvetica,sans-Serif" font-size="15.00">Objectifs de sécurité</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M99,-379.57C99,-365.84 99,-346.7 99,-331.18"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="102.15,-331.06 99,-322.06 95.85,-331.06 102.15,-331.06"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M186,-227C186,-227 12,-227 12,-227 6,-227 0,-221 0,-215 0,-215 0,-202 0,-202 0,-196 6,-190 12,-190 12,-190 186,-190 186,-190 192,-190 198,-196 198,-202 198,-202 198,-215 198,-215 198,-221 192,-227 186,-227"/>
<text text-anchor="start" x="19" y="-205" font-family="Helvetica,sans-Serif" font-size="15.00">Exigences vérifiables</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M99,-284.57C99,-270.84 99,-251.7 99,-236.18"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="102.15,-236.06 99,-227.06 95.85,-236.06 102.15,-236.06"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M137,-132C137,-132 61,-132 61,-132 55,-132 49,-126 49,-120 49,-120 49,-107 49,-107 49,-101 55,-95 61,-95 61,-95 137,-95 137,-95 143,-95 149,-101 149,-107 149,-107 149,-120 149,-120 149,-126 143,-132 137,-132"/>
<text text-anchor="start" x="68" y="-110" font-family="Helvetica,sans-Serif" font-size="15.00">Mesures</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M99,-189.57C99,-175.84 99,-156.7 99,-141.18"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="102.15,-141.06 99,-132.06 95.85,-141.06 102.15,-141.06"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M165,-37C165,-37 33,-37 33,-37 27,-37 21,-31 21,-25 21,-25 21,-12 21,-12 21,-6 27,0 33,0 33,0 165,0 165,0 171,0 177,-6 177,-12 177,-12 177,-25 177,-25 177,-31 171,-37 165,-37"/>
<text text-anchor="start" x="40" y="-15" font-family="Helvetica,sans-Serif" font-size="15.00">Tests de recette</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M99,-94.57C99,-80.84 99,-61.7 99,-46.18"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="102.15,-46.06 99,-37.06 95.85,-46.06 102.15,-46.06"/>
</g>
</g>
</svg>
</figure>

| Étape | Exemple |
|---|---|
| **Risque** | Un attaquant accède au site d'administration depuis Internet |
| **Objectif** | Seules les personnes habilitées administrent le site |
| **Exigence vérifiable** | « L'interface d'administration n'est accessible que depuis le réseau d'administration ou par VPN, avec authentification à deux facteurs. » |
| **Mesure** | Filtrage (S05) + VPN + double authentification (S06, S07) |
| **Test de recette** | Depuis Internet, l'adresse d'administration **ne répond pas** ; depuis le VPN, la connexion **exige** le second facteur |

### Une bonne exigence est…

| Critère | Mauvaise | Bonne |
|---|---|---|
| **Précise** | « Le site doit être sécurisé » | « Le site n'accepte que TLS 1.2 ou 1.3 » |
| **Vérifiable** | « Les mots de passe doivent être robustes » | « Longueur minimale de 12 caractères, comptes verrouillés après 5 échecs » |
| **Justifiée** | Liste sans lien avec un risque | Chaque exigence renvoie à un **risque** ou à une **obligation** |
| **Réaliste** | Exigence impossible avec le budget | Priorisée selon le risque et le coût |

### Où mettre la sécurité dans le cahier des charges

| Rubrique | Contenu sécurité |
|---|---|
| **Contexte, besoins** | Données traitées, sensibilité, obligations (RGPD, contrats clients) |
| **Exigences fonctionnelles** | Authentification, droits, traçabilité |
| **Exigences non fonctionnelles** | Disponibilité (RPO, RTO, S16), performance sous filtrage, journalisation (S11) |
| **Architecture** | Zones, flux autorisés, administration séparée (S05) |
| **Exploitation** | Mises à jour, supervision, sauvegarde, gestion des accès |
| **Contraintes** | Budget, délais, compétences |
| **Recette** | Tests de sécurité avec critères |
| **Contrat** | Clauses sécurité pour les prestataires |

---

## 3. Chiffrer et arbitrer

On ne peut pas tout faire. L'arbitrage compare **le risque réduit** et **le coût** (S02).

| Type de coût | Exemples |
|---|---|
| **Investissement** | Matériel (pare-feu, sonde), licences, prestation d'installation |
| **Fonctionnement** | Abonnements, support, **temps de l'équipe** (le plus oublié) |
| **Formation** | Administrateurs, utilisateurs |
| **Coût du risque** | Ce que coûterait l'incident évité |

On raisonne en **coût total** sur plusieurs années, pas en prix d'achat.

### La méthode d'arbitrage

1. Lister les mesures candidates, rattachées à un **risque** ;
2. Estimer **le coût** (investissement + fonctionnement) ;
3. Estimer **la réduction de risque** (échelles de S02) ;
4. Classer : d'abord ce qui réduit **beaucoup** le risque pour **peu** de coût (souvent des **réglages**) ;
5. **Justifier** ce qu'on **ne fait pas** et le risque résiduel **accepté** (S10) ;
6. **Planifier** par phases.

> [!WARNING]
> **Ne jamais présenter un chiffre inventé comme un fait.** Dans un sujet, on te donne les prix ; dans la vraie vie, on demande des **devis**. Un prix cité sans source est une hypothèse, à signaler comme telle.

---

## 4. Les tests de recette de sécurité

La **recette** est l'étape où le client **vérifie** que le système livré respecte le cahier des charges. Pour la sécurité, on écrit **à l'avance** :

| Colonne | Contenu |
|---|---|
| **Exigence** | Référence à l'exigence testée |
| **Test** | Action précise |
| **Résultat attendu** | Ce qui prouve que l'exigence est remplie |
| **Résultat obtenu** | Rempli lors de la recette |
| **Verdict** | Conforme, non conforme, à réserve |
| **Preuve** | Capture, extrait |

Exemples :

| Exigence | Test | Résultat attendu |
|---|---|---|
| Administration non exposée | Depuis Internet, tenter d'ouvrir l'adresse d'administration | Pas de réponse |
| TLS à jour | Examiner les protocoles acceptés (S08) | Seulement TLS 1.2 et 1.3 |
| Journalisation | Provoquer des échecs de connexion, chercher sur le collecteur (S11) | Événements présents et horodatés |
| Sauvegarde | Restauration chronométrée (S16) | Restauration conforme, dans le RTO |
| Droits | Compte « standard » tente d'accéder à un dossier interdit | Refus |

Une **réserve** est une non-conformité acceptée **provisoirement**, avec une **date de levée**. Un projet n'est pas « recetté » si des non-conformités **critiques** restent.

---

## 5. Les prestataires et tiers

Une grande partie des projets est **externalisée** (hébergement, intégration, maintenance). Le risque ne disparaît pas : il **change de main**, et la responsabilité du **responsable de traitement** reste (S04).

| Clause utile | Pourquoi |
|---|---|
| **Niveau de service** (disponibilité, délai de rétablissement) | Rendre l'engagement mesurable |
| **Sécurité** (mesures minimales, tests, correctifs) | Éviter le « on ne savait pas » |
| **Sous-traitance RGPD** (contrat de sous-traitant, S04) | Obligation légale quand des données personnelles sont traitées |
| **Notification des incidents** | Délai d'information (la tienne est de 72 heures vers la CNIL) |
| **Droit d'audit** | Pouvoir vérifier |
| **Sauvegarde et réversibilité** | Récupérer les données et le service à la fin du contrat |
| **Localisation** des données | Transferts hors Union européenne (S04) |

---

## 6. Après la livraison : maintenir en condition de sécurité

| Activité | Séance |
|---|---|
| Correctifs réguliers | S10, S13 |
| Supervision et journaux | S11, S12 |
| Revue des droits et des comptes | S06 |
| Tests de restauration | S16 |
| Nouvelle analyse de risques à chaque changement notable | S02 |

Un projet sans **budget de maintenance** est un projet qui se dégrade : la sécurité est un **processus**, pas un état livré.

**Test flash.** Le prestataire annonce « le site sera sécurisé » dans le contrat, sans plus. Que demandes-tu ?

<details markdown="1">
<summary>Voir la réponse</summary>

Des **exigences précises et vérifiables** (versions de protocoles, authentification, journalisation, sauvegarde, délai de correction), un **test de recette** pour chacune, un **contrat de sous-traitance** si des données personnelles sont concernées, une **notification d'incident**, un **droit d'audit** et la **réversibilité**. « Sécurisé » n'est ni mesurable ni opposable.

</details>
