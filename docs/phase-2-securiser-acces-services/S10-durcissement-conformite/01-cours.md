# Cours – Durcissement, conformité et gestion des correctifs

*BTS SIO SISR 2e année – Bloc 3 – S10*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

En première année, tu as **appliqué** des mesures de durcissement à un serveur. Une organisation doit répondre à une autre question : **« cette machine est-elle conforme à ce qu'on a décidé, et comment le prouve-t-on ? »** Cette séance passe de **faire** à **mesurer, documenter et maintenir**.

---

## 1. Durcir : réduire la surface et fixer une référence

**Durcir** un système, c'est **réduire sa surface d'attaque** : supprimer ce qui est inutile, restreindre ce qui reste, et configurer au plus sûr.

| Famille | Exemples |
|---|---|
| **Services et logiciels** | Désinstaller les paquets inutiles ; désactiver les services non nécessaires ; fermer les ports inutiles (séance S01) |
| **Comptes et authentification** | Supprimer les comptes inutiles ; verrouiller les comptes génériques ; politique de mots de passe ; connexion d'administration par clé |
| **Droits et fichiers** | Droits stricts sur les fichiers sensibles ; `umask` restrictif pour les nouveaux fichiers ; sauvegarde des configurations |
| **Réseau** | Pare-feu local ; paramètres du noyau (pas de redirection ni de réponse aux redirections d'itinéraire inutiles) |
| **Journalisation** | Journaux activés, horodatés, envoyés ailleurs (séance S11) |
| **Mises à jour** | Correctifs de sécurité appliqués dans des délais fixés |

Pour ne pas durcir « au feeling », on part d'une **référence** (*baseline*) : une liste de réglages reconnus.

| Source de référence | Idée |
|---|---|
| **Guides de configuration de l'ANSSI** | Recommandations de configuration de systèmes et services |
| **Guides de durcissement du CIS** (par système) | Listes de réglages, avec niveaux d'exigence |
| **Politique interne** (PSSI, séance S03) | Ce que **l'organisation** a décidé de rendre obligatoire |

> [!NOTE]
> Une référence **s'adapte**. Désactiver un service que l'application utilise est une panne, pas du durcissement. Chaque **écart volontaire** est **documenté** avec sa justification et son responsable.

---

## 2. Mesurer la conformité

Comparer à la main des centaines de réglages est impossible : des **outils d'audit** le font.

| Outil | Usage |
|---|---|
| **Lynis** | Audit **local** d'un système Linux : tests, avertissements, suggestions, **indice** de durcissement |
| **OpenSCAP** | Évalue un système par rapport à un **profil de conformité** formalisé |
| **Scanneurs de vulnérabilités** | Cherchent des **failles connues** (séance S13) : autre question |

### Lire un rapport d'audit

| Élément | Sens |
|---|---|
| **Avertissement** (*warning*) | Un problème à traiter en priorité |
| **Suggestion** | Une amélioration possible ; **toutes** ne se valent pas |
| **Indice de durcissement** | Un **score** de synthèse |
| **Identifiant du test** (par exemple `AUTH-9328`) | Permet de retrouver le détail et de suivre le point dans le temps |

> [!WARNING]
> **Un indice n'est pas une certification, et 100 n'est pas l'objectif.** Un score augmente quand on traite beaucoup de petites suggestions, pas nécessairement les plus importantes. On **trie** : gravité (risques de la séance S02), effort, effet de bord, et on **justifie** ce qu'on ne fait pas. Un rapport d'audit non exploité est du bruit.

### La boucle de conformité

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 389.10 438.60" style="max-width:519px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 427.8)">
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M341,-417C341,-417 188,-417 188,-417 182,-417 176,-411 176,-405 176,-405 176,-392 176,-392 176,-386 182,-380 188,-380 188,-380 341,-380 341,-380 347,-380 353,-386 353,-392 353,-392 353,-405 353,-405 353,-411 347,-417 341,-417"/>
<text text-anchor="start" x="195" y="-395" font-family="Helvetica,sans-Serif" font-size="15.00">Référence retenue</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M355.5,-322C355.5,-322 173.5,-322 173.5,-322 167.5,-322 161.5,-316 161.5,-310 161.5,-310 161.5,-297 161.5,-297 161.5,-291 167.5,-285 173.5,-285 173.5,-285 355.5,-285 355.5,-285 361.5,-285 367.5,-291 367.5,-297 367.5,-297 367.5,-310 367.5,-310 367.5,-316 361.5,-322 355.5,-322"/>
<text text-anchor="start" x="180.5" y="-300" font-family="Helvetica,sans-Serif" font-size="15.00">Audit : mesurer l&#39;écart</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M264.5,-379.57C264.5,-365.84 264.5,-346.7 264.5,-331.18"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="267.65,-331.06 264.5,-322.06 261.35,-331.06 267.65,-331.06"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M261,-227C261,-227 128,-227 128,-227 122,-227 116,-221 116,-215 116,-215 116,-202 116,-202 116,-196 122,-190 128,-190 128,-190 261,-190 261,-190 267,-190 273,-196 273,-202 273,-202 273,-215 273,-215 273,-221 267,-227 261,-227"/>
<text text-anchor="start" x="135" y="-205" font-family="Helvetica,sans-Serif" font-size="15.00">Trier et planifier</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M251,-284.57C240.28,-270.33 225.17,-250.24 213.27,-234.43"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="215.65,-232.36 207.72,-227.06 210.61,-236.15 215.65,-232.36"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M299,-132C299,-132 12,-132 12,-132 6,-132 0,-126 0,-120 0,-120 0,-107 0,-107 0,-101 6,-95 12,-95 12,-95 299,-95 299,-95 305,-95 311,-101 311,-107 311,-107 311,-120 311,-120 311,-126 305,-132 299,-132"/>
<text text-anchor="start" x="19" y="-110" font-family="Helvetica,sans-Serif" font-size="15.00">Corriger ou accepter l&#39;écart par écrit</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M186.98,-189.57C181.17,-175.71 173.04,-156.34 166.5,-140.74"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="169.25,-139.14 162.86,-132.06 163.44,-141.58 169.25,-139.14"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M355,-37C355,-37 172,-37 172,-37 166,-37 160,-31 160,-25 160,-25 160,-12 160,-12 160,-6 166,0 172,0 172,0 355,0 355,0 361,0 367,-6 367,-12 367,-12 367,-25 367,-25 367,-31 361,-37 355,-37"/>
<text text-anchor="start" x="179" y="-15" font-family="Helvetica,sans-Serif" font-size="15.00">Nouvel audit : prouver</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M176.07,-94.79C193.03,-80.18 217.26,-59.32 235.91,-43.26"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="238.24,-45.41 243.01,-37.15 234.13,-40.63 238.24,-45.41"/>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M286.6,-37.17C302.58,-50.94 322.52,-71.62 331.5,-95 356.37,-159.77 311.29,-238.16 283.67,-277.46"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="281.1,-275.64 278.4,-284.79 286.21,-279.32 281.1,-275.64"/>
</g>
</g>
</svg>
</figure>

À l'échelle de dizaines de machines, on **n'applique pas à la main** : on décrit la configuration cible dans un outil d'automatisation (par exemple **Ansible**, vu au bloc 2), qui **applique** et **remet en conformité**. Le rapport d'audit devient un **contrôle régulier**.

---

## 3. La gestion des correctifs

Une très grande partie des intrusions exploitent des failles **dont le correctif existe déjà**. Appliquer les correctifs est donc une mesure **de base**… et la plus difficile à tenir dans la durée, parce qu'un correctif peut **casser** quelque chose.

### Un processus, pas un geste

| Étape | Question |
|---|---|
| **1. Inventorier** | Quels systèmes, quels logiciels, quelles versions ? (On ne corrige pas ce qu'on ne connaît pas.) |
| **2. Se tenir informé** | D'où viennent les alertes ? (éditeur, liste de l'ANSSI / CERT-FR, flux de la distribution) |
| **3. Évaluer** | La faille concerne-t-elle **mes** systèmes ? Est-elle **exposée** à Internet ? Est-elle **exploitée** ? (séance S13) |
| **4. Tester** | Sur une machine **pilote** ou un environnement de test |
| **5. Déployer** | Par **vagues**, hors heures sensibles, avec **sauvegarde ou instantané** préalable |
| **6. Vérifier** | Le correctif est-il bien appliqué ? Le service fonctionne-t-il ? |
| **7. Tracer** | Qui a appliqué quoi, quand ; exceptions et échéances |
| **8. Prévoir le retour arrière** | Comment revenir à l'état précédent ? |

### Délais selon la gravité

Les délais d'application se **fixent par politique** (par exemple « sous quelques jours pour une faille critique exposée, sous quelques semaines pour les autres ») : **à décider avec la direction**, pas à emprunter à un chiffre générique. L'important est qu'ils soient **écrits, suivis et tenus**.

### Cas particuliers

| Cas | Traitement |
|---|---|
| **Logiciel en fin de support** | Plus de correctifs : **migrer**, ou **isoler** (réseau séparé, séance S05) en attendant ; c'est le cas des PC sous Windows 7 de l'Atelier Verdier |
| **Système qui ne peut pas être arrêté** | Fenêtre de maintenance planifiée ; redondance (bloc 2) |
| **Mises à jour de sécurité automatiques** | Possibles sur les systèmes simples (outil de mises à jour automatiques de la distribution), avec **surveillance** du résultat ; plus risqué sur un serveur d'application critique |
| **Noyau** | Un redémarrage est souvent nécessaire pour que le correctif soit **réellement actif** |

**Test flash.** Un audit donne un indice de 72 après correction, contre 58 avant. Le responsable dit « objectif atteint ». Que lui réponds-tu ?

<details markdown="1">
<summary>Voir la réponse</summary>

L'indice est un **indicateur**, pas un objectif : il faut regarder **quelles** suggestions ont été traitées (les plus graves d'abord ?), lesquelles restent, et si les **écarts acceptés** sont **justifiés par écrit**. Un score peut monter en traitant beaucoup de détails sans corriger l'exposition principale (par exemple une version non supportée).

</details>
