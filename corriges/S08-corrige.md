# Corrigé – S08 : Reverse proxy, en-têtes et OWASP

*Réservé à l'enseignant.*

## Vérification

Exécuté dans un laboratoire Ubuntu 24.04 de l'auteur (nginx 1.24, `curl` 8.5), la configuration du TP **telle quelle** :

| Test | Résultat constaté |
|---|---|
| `curl -sI http://127.0.0.1:8000/` | `Server: SimpleHTTP/0.6 Python/…` (l'application annonce sa version) |
| HTTPS sur le proxy | `200` |
| HTTP sur le port 80 | `301` avec `Location: https://proxy.lab.local/` **et `Server: nginx/1.24.0 (Ubuntu)`** : fuite de version (partie C) |
| Après `server_tokens off;` au niveau général | `Server: nginx` |
| En-têtes HTTPS | HSTS, `nosniff`, `X-Frame-Options`, `Referrer-Policy`, `Content-Security-Policy` ; `Server: nginx` sans version ; l'en-tête de l'application est masqué |
| `curl --tls-max 1.1` | **échec** (code de retour 35) ; la connexion normale négocie **TLS 1.3** |
| `PUT` et `TRACE` | `405` |
| 30 requêtes à la suite | environ 10 `200` puis des `503` avec quelques `200` isolés |
| Injection SQL, script injecté | `200` (le proxy relaie) ; `POST` : `501` (l'application de test ne gère pas cette méthode) |
| Remontée de dossiers avec `--path-as-is` | `400` (normalisation de nginx) |

**Adaptation de l'environnement de l'auteur** : le laboratoire envoyait le trafic par un mandataire (variable d'environnement), d'où l'option `--noproxy '*'` pour ses essais ; **elle n'est pas nécessaire dans la machine virtuelle de la salle**.

**Non vérifié** : le comportement sous Debian (versions de nginx et d'OpenSSL de la salle) ; `systemctl reload nginx` (l'auteur a utilisé `nginx -s reload` hors systemd) .

## Partie A–B

- A2 : `Server: SimpleHTTP/0.6 Python/<version>` ; pas d'en-tête de sécurité ; HTTP clair.
- B2 : `limit_req_zone` définit la zone de limitation ; le serveur du port 80 redirige ; le serveur du 443 termine TLS, ajoute les en-têtes, refuse les méthodes et relaie ; `proxy_pass` envoie vers l'application.
- B3 : `200`. B4 : `301`, `Location: https://proxy.lab.local/`, `Server: nginx/<version>` (**fuite**).

## Partie C

C1 : fuite sur le port 80 (voir éléments de réponse du TP). C2 : `Server: nginx` sans version après correction.

## Partie D

| Étape | Attendu |
|---|---|
| D1 | Les cinq en-têtes présents ; `Server: nginx` sans version |
| D2 | TLS 1.1 **refusé** ; TLS 1.3 négocié |
| D3 | `PUT` et `TRACE` : 405 ; `POST` : relayé (la réponse de l'application de test est une erreur `501` du serveur Python, ce qui est **normal** : ce serveur n'accepte que `GET` et `HEAD`) |
| D4 | Rafale d'environ 10 `200`, puis `503` |

> [!NOTE]
> `POST` est relayé jusqu'à l'application : le serveur de test (Python) ne gère que `GET` et `HEAD` et répond **501**, ce qui est **normal** (vérifié). Le proxy, lui, n'a pas bloqué la méthode.

Journal : les refus de débit apparaissent dans `access.log` avec le code 503 et dans `error.log` avec des lignes « limiting requests, excess: … by zone "parip" » (vérifié).

## Partie E

E1 : 1 et 2 passent (200), 3 est refusée (400) sans règle de sécurité. E2 : le journal permet de voir les tentatives (paramètres suspects, chemins, agents) même non bloquées : à lire régulièrement, ou mieux, à centraliser et alerter (S11).

| Cas | Famille | Qui corrige ? |
|---|---|---|
| `?facture=1042` → `1043` | Contrôle d'accès défaillant | Code de l'application |
| Essais de connexion illimités | Authentification défaillante / conception non sécurisée | Application (verrouillage, second facteur) ; proxy en **complément** (limitation de débit) |
| Bibliothèque vulnérable | Composants vulnérables | **Mise à jour** |
| Page d'erreur bavarde | Mauvaise configuration | Configuration de l'application et du serveur |

## Pièges fréquents

- Croire que `server_tokens off` dans **un** bloc masque la version **partout**.
- Penser que le proxy **bloque** les injections parce qu'il a « durci » le site.
- Oublier `always` sur `add_header` (l'en-tête disparaît des réponses d'erreur).
- Recharger sans `nginx -t`.
- Utiliser `-k` ailleurs qu'en laboratoire.
