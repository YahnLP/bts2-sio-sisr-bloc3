# Aide-mémoire – 802.1X et RADIUS

*BTS SIO SISR 2e année – Bloc 3 – S07*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## Les trois rôles

| Rôle | Qui | Fait quoi |
|---|---|---|
| Demandeur | Appareil ou utilisateur | Présente identité et preuve |
| Authentificateur | Switch ou borne | Garde la porte, relaie |
| Serveur d'authentification | RADIUS | Accepte ou refuse |

## RADIUS

| Élément | Valeur |
|---|---|
| Authentification | UDP **1812** |
| Comptabilité | UDP **1813** |
| Protection des échanges | **Secret partagé** par authentificateur |
| Réponses | `Access-Accept` · `Access-Reject` · `Access-Challenge` |
| VLAN dynamique | `Tunnel-Type = VLAN` · `Tunnel-Medium-Type = IEEE-802` · `Tunnel-Private-Group-Id = <n°>` |

## Méthodes EAP

| Méthode | Preuve | À retenir |
|---|---|---|
| EAP-TLS | Certificats (client et serveur) | La plus sûre ; demande une PKI |
| PEAP (MSCHAPv2) | Mot de passe dans un tunnel TLS | Le client **doit** vérifier le certificat du serveur |
| EAP-TTLS | Mot de passe dans un tunnel TLS | Idem |

> [!WARNING]
> Sans vérification du certificat du serveur, une **fausse borne** récupère les identifiants.

## FreeRADIUS sous Debian

| Besoin | Commande ou fichier |
|---|---|
| Installer | `sudo apt install freeradius freeradius-utils` |
| Authentificateurs et secrets | `/etc/freeradius/3.0/clients.conf` |
| Utilisateurs (laboratoire) | `/etc/freeradius/3.0/users` |
| Lancer en mode debug | `sudo systemctl stop freeradius` puis `sudo freeradius -X` |
| Tester un mot de passe | `radtest utilisateur mot_de_passe serveur 0 secret` |
| Tester PEAP | `eapol_test -c profil.conf -a 127.0.0.1 -p 1812 -s secret` |
| Résultat de `eapol_test` | `SUCCESS` ou `FAILURE` à la dernière ligne |

## Lecture d'un résultat

| Constat | Cause probable |
|---|---|
| `Access-Reject` | Mauvais mot de passe ou utilisateur inconnu |
| Aucune réponse, `radtest` attend | **Secret** différent, ou serveur injoignable |
| `FAILURE` avec `ca_cert` | Le certificat du serveur **n'est pas** signé par l'autorité indiquée |
| Erreur au démarrage | Syntaxe d'un fichier, écoute IPv6 impossible, port déjà pris |

## Wi-Fi : bonnes pratiques

- **802.1X** pour le personnel (clé partagée à éviter) ; départ d'un salarié = **désactiver le compte**.
- **Invités** dans un VLAN et une zone **séparés**, Internet seulement.
- Profil des postes **imposé** (autorité de confiance, nom du serveur).
- **MAC** : protection faible, réserver aux équipements isolés.
