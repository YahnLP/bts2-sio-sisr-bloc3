# Cours – Cadre juridique et responsabilités en entreprise

*BTS SIO SISR 2e année – Bloc 3 – S04*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

> [!WARNING]
> **Ce cours n'est pas un conseil juridique.** Il donne les repères que l'étude de cas de l'épreuve E7 demande. Les articles, les montants et les délais sont à **relire sur Légifrance et sur le site de la CNIL** avant d'être cités dans un document noté. Si un point est à vérifier, c'est écrit.

Tu connais les bases du RGPD (première année). Cette séance l'applique à la vie d'une entreprise : **qui est responsable de quoi, quand une obligation naît, et ce que risque l'administrateur lui-même.**

---

## 1. Qualifier : qui fait quoi dans un traitement ?

Avant toute décision, on **qualifie** la situation :

| Question | Pourquoi elle compte |
|---|---|
| Quelles **données** ? Sont-elles **personnelles** ? **Sensibles** (santé, opinions, biométrie…) ? | Le régime et la gravité changent |
| Quelle **finalité** ? | Toute donnée a un but précis, écrit |
| Quelle **base légale** ? | Contrat, obligation légale, consentement, intérêt légitime… |
| Qui est **responsable de traitement** ? | Il décide des finalités et des moyens, et **répond** devant la loi |
| Qui est **sous-traitant** ? | Il traite pour le compte du responsable, sur instruction |
| Quelle **durée de conservation** ? | Pas de conservation sans limite |

Un même prestataire peut être **sous-traitant** pour un traitement (il héberge) et **responsable** pour un autre (ses propres clients). C'est la **réalité des décisions** qui qualifie, pas l'étiquette du contrat.

---

## 2. Les sous-traitants

Quand une organisation confie des données personnelles à un prestataire (hébergeur, éditeur en ligne, société de paie, maintenance), le RGPD (**art. 28**) exige un **contrat écrit** qui prévoit notamment :

- l'objet, la durée, la nature du traitement et les catégories de données ;
- le traitement **uniquement sur instruction** du responsable ;
- la **confidentialité** des personnes habilitées ;
- les **mesures de sécurité** ;
- le recours à un **autre sous-traitant** seulement avec accord ;
- l'**aide** au responsable (droits des personnes, violations) ;
- la **suppression ou restitution** des données en fin de contrat ;
- le droit de **contrôle et d'audit**.

Le responsable doit choisir un prestataire qui présente des **garanties suffisantes**. Si le prestataire est compromis, **le responsable reste concerné** : « c'est le prestataire » ne l'exonère pas.

> [!NOTE]
> **Données de santé.** En France, l'hébergement de données de santé à caractère personnel recueillies à l'occasion de soins relève d'un **régime particulier** : l'hébergeur doit être **certifié** pour cette activité. À vérifier sur le site de l'agence du numérique en santé avant de conclure.

---

## 3. Les transferts hors de l'Union européenne

Envoyer des données personnelles **hors de l'Union européenne** (par exemple vers un service en ligne dont les serveurs ou l'assistance sont dans un pays tiers) n'est permis que si un **cadre de protection** existe (RGPD, chapitre V) :

| Mécanisme | Idée |
|---|---|
| **Décision d'adéquation** | La Commission européenne reconnaît que le pays assure un niveau de protection équivalent |
| **Garanties appropriées** | Notamment des **clauses contractuelles types** signées avec l'importateur, parfois avec des mesures complémentaires |
| **Règles d'entreprise contraignantes** | Pour les groupes multinationaux |

Question à se poser dans un dossier : **où sont les serveurs, et qui peut y accéder (y compris l'assistance) ?** Une adresse de société en Europe n'implique pas que les données y restent. Les décisions d'adéquation et les accords évoluent : **à vérifier à la date du sujet**.

---

## 4. Le délégué à la protection des données et la CNIL

- Le **délégué à la protection des données (DPO)** conseille et contrôle ; il est **obligatoire** dans certains cas (autorités publiques, suivi à grande échelle, données sensibles à grande échelle) et **désignable** dans les autres. Il ne reçoit **pas d'instruction** sur sa mission et n'est pas responsable à la place de l'organisation.
- La **CNIL** informe, contrôle, **instruit les plaintes**, peut **mettre en demeure** et **sanctionner**.
- Les **sanctions** pécuniaires du RGPD peuvent aller, selon la gravité des manquements, jusqu'à **10 millions d'euros ou 2 %** du chiffre d'affaires mondial, ou **20 millions d'euros ou 4 %** (art. 83) : à vérifier sur le texte.

---

## 5. La violation de données

Une **violation de données** est une atteinte à la **sécurité** qui entraîne, de manière accidentelle ou illicite, la **destruction**, la **perte**, l'**altération**, la **divulgation** ou l'**accès** non autorisé à des données personnelles. Elle recouvre la confidentialité, l'intégrité **et la disponibilité**.

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 1111.10 638.60" style="max-width:1481px;min-width:900px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 627.8)">
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M552.5,-617C552.5,-617 261.5,-617 261.5,-617 255.5,-617 249.5,-611 249.5,-605 249.5,-605 249.5,-592 249.5,-592 249.5,-586 255.5,-580 261.5,-580 261.5,-580 552.5,-580 552.5,-580 558.5,-580 564.5,-586 564.5,-592 564.5,-592 564.5,-605 564.5,-605 564.5,-611 558.5,-617 552.5,-617"/>
<text text-anchor="start" x="268.5" y="-595" font-family="Helvetica,sans-Serif" font-size="15.00">Prise de connaissance de la violation</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M566.5,-521C566.5,-521 247.5,-521 247.5,-521 241.5,-521 235.5,-515 235.5,-509 235.5,-509 235.5,-496 235.5,-496 235.5,-490 241.5,-484 247.5,-484 247.5,-484 566.5,-484 566.5,-484 572.5,-484 578.5,-490 578.5,-496 578.5,-496 578.5,-509 578.5,-509 578.5,-515 572.5,-521 566.5,-521"/>
<text text-anchor="start" x="254.5" y="-499" font-family="Helvetica,sans-Serif" font-size="15.00">Consigner dans le registre des violations</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M407,-579.82C407,-565.9 407,-546.27 407,-530.41"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="410.15,-530.1 407,-521.1 403.85,-530.1 410.15,-530.1"/>
</g>
<g class="node n&#45;diamond">
<polygon fill="none" stroke="black" stroke-width="1.8" points="407,-425 0,-388 407,-351 814,-388 407,-425"/>
<text text-anchor="start" x="222.5" y="-384.5" font-family="Helvetica,sans-Serif" font-size="15.00">Risque pour les droits et libertés des personnes ?</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M407,-483.92C407,-470.68 407,-451.89 407,-434.52"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="410.15,-434.06 407,-425.06 403.85,-434.06 410.15,-434.06"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M458.5,-279C458.5,-279 235.5,-279 235.5,-279 229.5,-279 223.5,-273 223.5,-267 223.5,-267 223.5,-254 223.5,-254 223.5,-248 229.5,-242 235.5,-242 235.5,-242 458.5,-242 458.5,-242 464.5,-242 470.5,-248 470.5,-254 470.5,-254 470.5,-267 470.5,-267 470.5,-273 464.5,-279 458.5,-279"/>
<text text-anchor="start" x="242.5" y="-257" font-family="Helvetica,sans-Serif" font-size="15.00">Pas de notification à la CNIL</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M390.45,-352.37C380.62,-331.83 368.38,-306.22 359.39,-287.42"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="362.12,-285.81 355.39,-279.05 356.43,-288.53 362.12,-285.81"/>
<text text-anchor="start" x="376" y="-311.6" font-family="Helvetica,sans-Serif" font-size="13.00">Improbable</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M1021,-279C1021,-279 523,-279 523,-279 517,-279 511,-273 511,-267 511,-267 511,-254 511,-254 511,-248 517,-242 523,-242 523,-242 1021,-242 1021,-242 1027,-242 1033,-248 1033,-254 1033,-254 1033,-267 1033,-267 1033,-273 1027,-279 1021,-279"/>
<text text-anchor="start" x="530" y="-257" font-family="Helvetica,sans-Serif" font-size="15.00">Notifier la CNIL, au plus tard 72 h après la prise de connaissance</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M489.82,-358.52C557.58,-335.22 651.79,-302.83 712.33,-282.02"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="713.53,-284.94 721.01,-279.03 711.48,-278.98 713.53,-284.94"/>
<text text-anchor="start" x="633" y="-311.6" font-family="Helvetica,sans-Serif" font-size="13.00">Oui</text>
</g>
<g class="node n&#45;diamond">
<polygon fill="none" stroke="black" stroke-width="1.8" points="772,-183 625,-146 772,-109 919,-146 772,-183"/>
<text text-anchor="start" x="717.5" y="-142.5" font-family="Helvetica,sans-Serif" font-size="15.00">Risque élevé ?</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M772,-241.92C772,-228.68 772,-209.89 772,-192.52"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="775.15,-192.06 772,-183.06 768.85,-192.06 775.15,-192.06"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M812.5,-37C812.5,-37 323.5,-37 323.5,-37 317.5,-37 311.5,-31 311.5,-25 311.5,-25 311.5,-12 311.5,-12 311.5,-6 317.5,0 323.5,0 323.5,0 812.5,0 812.5,0 818.5,0 824.5,-6 824.5,-12 824.5,-12 824.5,-25 824.5,-25 824.5,-31 818.5,-37 812.5,-37"/>
<text text-anchor="start" x="330.5" y="-15" font-family="Helvetica,sans-Serif" font-size="15.00">Informer aussi les personnes concernées, dans un langage clair</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M730.23,-119.3C693.16,-96.5 639.57,-63.53 604.27,-41.81"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="605.91,-39.12 596.59,-37.09 602.61,-44.49 605.91,-39.12"/>
<text text-anchor="start" x="664" y="-69.6" font-family="Helvetica,sans-Serif" font-size="13.00">Oui</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M1077.5,-37C1077.5,-37 876.5,-37 876.5,-37 870.5,-37 864.5,-31 864.5,-25 864.5,-25 864.5,-12 864.5,-12 864.5,-6 870.5,0 876.5,0 876.5,0 1077.5,0 1077.5,0 1083.5,0 1089.5,-6 1089.5,-12 1089.5,-12 1089.5,-25 1089.5,-25 1089.5,-31 1083.5,-37 1077.5,-37"/>
<text text-anchor="start" x="883.5" y="-15" font-family="Helvetica,sans-Serif" font-size="15.00">Conserver la justification</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M813.98,-119.3C851.22,-96.5 905.08,-63.53 940.55,-41.81"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="942.24,-44.48 948.27,-37.09 938.95,-39.1 942.24,-44.48"/>
<text text-anchor="start" x="899" y="-69.6" font-family="Helvetica,sans-Serif" font-size="13.00">Non</text>
</g>
</g>
</svg>
</figure>

Points à retenir :

- Le délai de **72 heures** court à partir du moment où l'on **en a eu connaissance** ; au-delà, la notification est faite avec les **motifs du retard**.
- Le **sous-traitant** informe le responsable **dans les meilleurs délais** (art. 33) : le contrat doit prévoir comment.
- **Toute** violation est consignée dans un **registre**, même non notifiée.
- Un **chiffrement** bien fait peut rendre les données inintelligibles et **réduire le risque** (disque d'un portable perdu).
- La notification contient : la nature de la violation, les catégories et le nombre approximatif de personnes et d'enregistrements, les **conséquences probables**, les **mesures** prises ou proposées, et un contact.

> [!NOTE]
> **Au-delà du RGPD.** Selon le secteur (opérateurs de services essentiels, entités importantes ou essentielles), d'**autres obligations de sécurité et de notification d'incident** s'ajoutent, issues du cadre européen « NIS 2 ». Sa transposition en droit français **évolue** : vérifier son état à la date du sujet avant d'en parler. Si le dossier la cite, on la **cite**, sans en inventer le détail.

---

## 6. L'administrateur face à la loi

L'administrateur système et réseau dispose de droits techniques étendus : la loi le sait, et lui demande **plus**, pas moins.

### Les atteintes aux systèmes (loi dite « Godfrain »)

Le **Code pénal** (art. **323-1 et suivants**) punit notamment :

| Fait | Article |
|---|---|
| **Accéder** ou **se maintenir** frauduleusement dans un système | 323-1 |
| **Entraver** ou **fausser** le fonctionnement d'un système | 323-2 |
| **Introduire, extraire, modifier ou supprimer** frauduleusement des données | 323-3 |
| Détenir ou diffuser un **outil conçu pour commettre** ces infractions, sans motif légitime | 323-3-1 |

Les peines (emprisonnement et amende, aggravées si le système contient des données personnelles ou relève de l'État) sont à **relire sur Légifrance**. L'élément qui compte pour toi : l'accès est **frauduleux** s'il se fait **sans autorisation**. **Avoir un mot de passe d'administrateur n'est pas une autorisation d'aller partout.** D'où la règle de la formation : on ne teste **jamais** sans **autorisation écrite** et **périmètre défini**.

### Le secret des correspondances et la vie privée

- Le **secret des correspondances** est protégé (Code pénal, art. **226-15** : ouverture ou interception frauduleuse).
- Un salarié conserve un droit au respect de sa **vie privée** sur son lieu de travail. Les fichiers et messages **clairement identifiés comme personnels** sont, en principe, protégés ; l'employeur n'y accède que dans des **cas encadrés** (point à vérifier avec un juriste).
- L'administrateur est tenu à la **confidentialité** de ce qu'il voit en exerçant sa mission ; elle se prévoit dans la **charte** et le **contrat**.
- La **surveillance** des salariés (journaux, filtrage) doit être **proportionnée**, **annoncée** (charte, information des représentants du personnel selon le cas) et **justifiée**.

### Responsabilité civile et pénale

| Responsabilité | Qui ? | Idée |
|---|---|---|
| **Pénale** | La **personne** qui commet l'infraction, dont l'administrateur à titre personnel | Il ne peut pas se retrancher derrière un ordre illégal |
| **Civile** | L'**employeur** répond de ses salariés dans leurs fonctions ; le **prestataire** répond selon son contrat | Réparation du dommage |
| **Contractuelle** | Le prestataire envers son client | Selon les clauses (obligation de moyens ou de résultat, plafonds) |

**Test flash.** Un administrateur voit passer un dossier « Perso » du directeur sur le serveur. A-t-il le droit de l'ouvrir « pour vérifier qu'il n'y a pas de virus » ?

<details markdown="1">
<summary>Voir la réponse</summary>

**Non, en principe.** Un dossier clairement identifié comme personnel est protégé ; l'ouvrir sans cadre légal ni procédure peut constituer une atteinte à la vie privée ou au secret des correspondances. La bonne pratique : s'en tenir à des **mesures techniques** (analyse antivirus automatique), ne **pas lire le contenu**, et référer à la direction ou à un juriste si une ouverture paraît nécessaire.

</details>
