# Aide-mémoire – Messagerie et DNS

*BTS SIO SISR 2e année – Bloc 3 – S09*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## Les trois protections

| | Où ? | Vérifie | Casse si… |
|---|---|---|---|
| **SPF** | TXT sur `domaine` | L'**adresse du serveur** émetteur est autorisée | Transfert par un serveur non listé |
| **DKIM** | TXT sur `sélecteur._domainkey.domaine` | La **signature** du message | Le message est modifié |
| **DMARC** | TXT sur `_dmarc.domaine` | Le **From: visible** est **aligné** avec un SPF ou un DKIM valide ; dit quoi faire | Aucun des deux n'est aligné |

## Syntaxe

```text
domaine.  IN TXT "v=spf1 ip4:192.0.2.25 include:spf.prestataire.example -all"
sel1._domainkey.domaine.  IN TXT "v=DKIM1; k=rsa; p=CLE_PUBLIQUE"
_dmarc.domaine.  IN TXT "v=DMARC1; p=quarantine; rua=mailto:dmarc@domaine"
```

| SPF | Sens |
|---|---|
| `-all` | Échec pour tout le reste |
| `~all` | Échec « souple » |
| `include:` | Autorise les serveurs d'un autre domaine |

| DMARC | Sens |
|---|---|
| `p=none` | Observer |
| `p=quarantine` | Spam |
| `p=reject` | Refuser |
| `rua=` | Rapports agrégés |

**Mise en place :** `none` → corriger → `quarantine` → `reject`.

## Lire un message

| En-tête | Question |
|---|---|
| `From:` | Domaine **exact** (lettres proches ?) |
| `Return-Path:` | Différent du `From:` ? |
| `Reply-To:` | Réponse vers ailleurs ? |
| `Received:` | Lire de **bas en haut** |
| `Authentication-Results:` | SPF, DKIM, DMARC : **aligné** sur le `From:` ? |

Un message qui **passe tout** peut venir d'un **domaine proche** ou d'un **compte compromis**.

## Commandes DNS

| Besoin | Commande |
|---|---|
| Interroger un type | `dig @serveur nom TYPE +short` (`MX`, `TXT`, `A`, `NS`) |
| Transfert de zone | `dig @serveur domaine AXFR` |
| Version annoncée | `dig @serveur version.bind CH TXT +short` |
| Vérifier une zone | `named-checkzone domaine fichier` |
| Vérifier la configuration | `named-checkconf` |
| Recharger | `rndc reload` |
| Voir les signatures | `dig @serveur nom A +dnssec` |
| Valider | `delv @serveur -a ancre.conf +root=domaine nom A` |

## Durcir le serveur DNS

| Mesure | Directive BIND |
|---|---|
| Interdire les transferts de zone | `allow-transfer { none; };` (dans la zone) |
| Masquer la version | `version "texte";` (dans `options`) |
| Limiter la récursivité à son réseau | `allow-recursion { réseau; };` |

## DNSSEC

| Terme | Sens |
|---|---|
| **RRSIG** | Signature d'un ensemble d'enregistrements |
| **DNSKEY** | Clés publiques (KSK signe les clés, ZSK signe la zone) |
| **DS** | Empreinte de la KSK, publiée dans la zone **parente** |
| Garantit | **Intégrité et origine** des réponses |
| Ne garantit pas | Confidentialité ; protection du compte chez le bureau d'enregistrement |
| Exploitation | Signatures qui **expirent** ; erreur = domaine injoignable pour les résolveurs qui valident |

Chaîne : racine → domaine de premier niveau → domaine (le DS lie chaque niveau au suivant).
