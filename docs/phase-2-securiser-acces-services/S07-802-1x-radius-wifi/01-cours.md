# Cours – 802.1X, RADIUS et Wi-Fi d'entreprise

*BTS SIO SISR 2e année – Bloc 3 – S07*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

Jusqu'ici on a protégé les **services** et les **comptes**. Reste la **porte du réseau** : qui a le droit de **brancher** un câble ou de **se connecter** au Wi-Fi ? Un réseau où **n'importe qui** peut brancher un appareil est un réseau où le pare-feu de la séance S05 est contourné de l'intérieur.

---

## 1. Les trois rôles de 802.1X

La norme **802.1X** contrôle l'accès **par port** ou **par association Wi-Fi** : tant que l'appareil ne s'est pas authentifié, **seul** le trafic d'authentification passe.

| Rôle | Qui | Fait quoi |
|---|---|---|
| **Demandeur** (*supplicant*) | L'appareil ou l'utilisateur qui veut entrer | Présente une identité et une preuve |
| **Authentificateur** | Le **switch** ou la **borne Wi-Fi** | Garde la porte fermée ; relaie la demande |
| **Serveur d'authentification** | Un serveur **RADIUS** | Décide : accepter ou refuser |

<figure class="graphe diagramme"><svg viewBox="0 0 1193 606" style="max-width:1193px" role="img" aria-label="Diagramme de séquence" xmlns="http://www.w3.org/2000/svg">
<defs><marker id="s599575" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="8" markerHeight="8" orient="auto"><path d="M0,0 L10,5 L0,10 z" class="seq-head"/></marker></defs>
<line class="seq-life" x1="199" y1="62" x2="199" y2="600"/>
<rect class="seq-box" x="66" y="12" width="267" height="40" rx="8"/><text x="199" y="37" text-anchor="middle" class="seq-title">Demandeur (poste, téléphone)</text>
<line class="seq-life" x1="597" y1="62" x2="597" y2="600"/>
<rect class="seq-box" x="463" y="12" width="267" height="40" rx="8"/><text x="597" y="37" text-anchor="middle" class="seq-title">Authentificateur (borne, switch)</text>
<line class="seq-life" x1="994" y1="62" x2="994" y2="600"/>
<rect class="seq-box" x="861" y="12" width="267" height="40" rx="8"/><text x="994" y="37" text-anchor="middle" class="seq-title">Serveur RADIUS</text>
<line class="seq-msg" x1="199" y1="96" x2="593" y2="96" marker-end="url(#s599575)"/><text x="398" y="88" text-anchor="middle">Je veux accéder au réseau</text>
<line class="seq-msg" x1="597" y1="146" x2="203" y2="146" marker-end="url(#s599575)"/><text x="398" y="138" text-anchor="middle">Qui êtes-vous ? (demande d'identité)</text>
<line class="seq-msg" x1="199" y1="196" x2="593" y2="196" marker-end="url(#s599575)"/><text x="398" y="188" text-anchor="middle">Mon identité</text>
<line class="seq-msg" x1="597" y1="246" x2="990" y2="246" marker-end="url(#s599575)"/><text x="796" y="238" text-anchor="middle">Access-Request (identité)</text>
<line class="seq-msg dash" x1="994" y1="296" x2="601" y2="296" marker-end="url(#s599575)"/><text x="796" y="288" text-anchor="middle">Access-Challenge (échanges EAP, tunnel chiffré)</text>
<line class="seq-msg dash" x1="597" y1="346" x2="203" y2="346" marker-end="url(#s599575)"/><text x="398" y="338" text-anchor="middle">relaie</text>
<line class="seq-msg" x1="199" y1="396" x2="593" y2="396" marker-end="url(#s599575)"/><text x="398" y="388" text-anchor="middle">preuve (mot de passe ou certificat)</text>
<line class="seq-msg" x1="597" y1="446" x2="990" y2="446" marker-end="url(#s599575)"/><text x="796" y="438" text-anchor="middle">Access-Request (preuve)</text>
<line class="seq-msg dash" x1="994" y1="496" x2="601" y2="496" marker-end="url(#s599575)"/><text x="796" y="488" text-anchor="middle">Access-Accept (+ VLAN) ou Access-Reject</text>
<line class="seq-msg dash" x1="597" y1="546" x2="203" y2="546" marker-end="url(#s599575)"/><text x="398" y="538" text-anchor="middle">porte ouverte (dans le bon VLAN) ou fermée</text>
</svg></figure>

L'authentificateur **ne connaît pas** les mots de passe : il **fait confiance** au serveur RADIUS. C'est ce qui permet de **centraliser** : une seule base (souvent l'annuaire) pour tous les switchs et toutes les bornes.

---

## 2. RADIUS

**RADIUS** est le protocole entre l'authentificateur et le serveur.

| Élément | À retenir |
|---|---|
| Transport | **UDP**, ports **1812** (authentification) et **1813** (comptabilité) |
| **Secret partagé** | Entre **chaque authentificateur** et le serveur ; il protège les échanges RADIUS. Un secret faible ou identique partout est une faiblesse |
| Réponses | **Access-Accept**, **Access-Reject**, **Access-Challenge** (le serveur demande une étape de plus) |
| **Attributs** | Informations jointes à la réponse : par exemple le **VLAN** à attribuer, la durée de session |

### Le VLAN dynamique

Le serveur peut répondre « accepté, **et placez cet utilisateur dans le VLAN 20** » grâce à trois attributs (`Tunnel-Type = VLAN`, `Tunnel-Medium-Type = IEEE-802`, `Tunnel-Private-Group-Id = 20`). Un salarié, un invité et un équipement peuvent ainsi arriver sur la **même prise** ou la **même borne** et se retrouver dans des **zones différentes** (S05).

---

## 3. EAP : les méthodes de preuve

**EAP** est le cadre dans lequel l'appareil prouve son identité. Plusieurs **méthodes** :

| Méthode | Preuve | Forces | Faiblesses |
|---|---|---|---|
| **EAP-TLS** | **Certificat** du client **et** du serveur | La plus sûre : pas de mot de passe à voler | Demande une **infrastructure de certificats** (PKI) pour tous les appareils |
| **PEAP (MSCHAPv2)** | Mot de passe, dans un **tunnel TLS** ouvert avec le certificat du serveur | Simple, s'appuie sur l'annuaire | Si le client **ne vérifie pas** le certificat du serveur, on peut le piéger |
| **EAP-TTLS** | Mot de passe dans un tunnel TLS | Souple | Même condition sur le certificat du serveur |

> [!WARNING]
> **Le certificat du serveur doit être vérifié par le client.** Sinon, une **fausse borne** (« jumeau maléfique », *evil twin*) portant le même nom de réseau peut recevoir les identifiants des utilisateurs. La vérification se règle **dans le profil du client** : autorité de certification de confiance et **nom du serveur** attendu.

---

## 4. Le Wi-Fi d'entreprise

| | Personnel (clé partagée) | Entreprise (802.1X) |
|---|---|---|
| Principe | **Un seul** mot de passe pour tous | Chaque utilisateur ou appareil a **sa propre** preuve |
| Départ d'un salarié | Il **connaît encore** la clé : il faut la changer pour tous | On **désactive son compte** |
| Traçabilité | Aucune (tous pareils) | **Qui** s'est connecté, quand |
| Affectation à un VLAN | Non (un réseau pour tous) | **Oui**, selon l'identité |

Dans le dossier de l'Atelier Verdier (S02), un **Wi-Fi unique** partagé depuis trois ans est exactement le cas à éviter : tout ancien salarié a encore la clé.

**Évolution des protocoles.** Le **WPA3** améliore le WPA2 (en mode personnel comme en mode entreprise). Les détails (modes, versions, obligations selon les appareils) sont à **relire dans la documentation à jour** avant de les citer.

### L'invité

Un réseau **invité** est **séparé** : un VLAN et une zone dédiés, accès à Internet seulement, **aucun accès au réseau interne** (matrice de flux, S05), éventuellement authentifié par un portail et **limité dans le temps**.

### Appareils personnels et terminaux mobiles (BYOD)

Un salarié veut connecter son téléphone personnel. Trois réponses possibles :

| Option | Accès | Contrôle |
|---|---|---|
| **Invité** | Internet seulement (VLAN invités) | Aucun sur l'appareil |
| **BYOD encadré** | Services ciblés, via un **certificat propre à l'appareil** (EAP-TLS) ou un compte personnel | **Profil professionnel** géré à distance |
| **Terminal fourni** | Réseau du personnel (802.1X) | Gestion complète par l'entreprise |

Un outil de **gestion de terminaux mobiles** (MDM) applique au profil professionnel : **chiffrement**, code de verrouillage, mises à jour, liste d'applications autorisées, **effacement sélectif** de la partie professionnelle (perte, départ). Il fournit aussi l'état de **conformité** : un appareil non conforme est placé en quarantaine (VLAN restreint) ou refusé.

> [!NOTE]
> Sur un appareil personnel, l'entreprise ne contrôle et n'efface **que la partie professionnelle**. Les règles sont écrites dans la charte d'usage (S03) et acceptées par l'agent. Choix de l'outil et conditions juridiques précises : **à valider** avec l'enseignant.

---

## 5. Au-delà du Wi-Fi : la prise réseau

La même mécanique protège les **prises** : un switch **802.1X** n'ouvre le port qu'après authentification. Pour les équipements qui ne savent pas le faire (imprimante, caméra), on utilise parfois l'**authentification par adresse MAC** (MAB). **Attention** : une adresse MAC **se copie** facilement : c'est une protection **faible**, à réserver à des équipements isolés dans un VLAN restreint.

**Test flash.** Un attaquant installe une borne Wi-Fi portant le même nom que celle de l'entreprise. Des salariés se connectent avec PEAP. Dans quel cas leurs mots de passe sont-ils compromis ?

<details markdown="1">
<summary>Voir la réponse</summary>

Quand le **profil du client ne vérifie pas le certificat du serveur** (ou accepte n'importe quel certificat). Mesures : profil imposé par stratégie de groupe avec l'autorité de certification de confiance et le **nom du serveur RADIUS** ; ou **EAP-TLS** (certificats mutuels).

</details>
