# Aide-mémoire – Reverse proxy, en-têtes et OWASP

*BTS SIO SISR 2e année – Bloc 3 – S08*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## En-têtes de sécurité

| En-tête | Effet |
|---|---|
| `Strict-Transport-Security` | Navigateur : HTTPS uniquement |
| `X-Content-Type-Options: nosniff` | Pas de devinette du type de fichier |
| `X-Frame-Options: DENY` | Pas d'affichage dans un cadre d'un autre site |
| `Content-Security-Policy` | D'où la page peut charger scripts et images |
| `Referrer-Policy` | Origine transmise lors d'un clic |

## Directives nginx utiles

| Besoin | Directive |
|---|---|
| Masquer la version (**partout**) | `server_tokens off;` au niveau général |
| TLS récent uniquement | `ssl_protocols TLSv1.2 TLSv1.3;` |
| Rediriger HTTP vers HTTPS | `return 301 https://$host$request_uri;` |
| Ajouter un en-tête | `add_header NOM "valeur" always;` |
| Limiter les méthodes | `if ($request_method !~ ^(GET\|HEAD\|POST)$) { return 405; }` |
| Limiter le débit | `limit_req_zone …` puis `limit_req zone=… burst=… nodelay;` |
| Relayer vers l'application | `proxy_pass http://127.0.0.1:8000;` |
| Masquer l'en-tête de l'application | `proxy_hide_header Server;` |

## Commandes

| Besoin | Commande |
|---|---|
| Tester la configuration | `sudo nginx -t` |
| Appliquer | `sudo systemctl reload nginx` |
| En-têtes d'une réponse | `curl -I URL` |
| Détail TLS | `curl -v URL` |
| Joindre un nom sans DNS | `curl --resolve nom:443:127.0.0.1 https://nom/` |
| Une méthode précise | `curl -X PUT URL` |
| Limiter la version TLS | `curl --tls-max 1.1 URL` |
| Code de réponse seul | `curl -s -o /dev/null -w "%{http_code}\n" URL` |
| Journaux | `/var/log/nginx/access.log` · `/var/log/nginx/error.log` |

## Familles OWASP à reconnaître

Contrôle d'accès défaillant · Défaut de chiffrement · Injection (SQL, script) · Conception non sécurisée · Mauvaise configuration · Composants vulnérables · Authentification défaillante · Défaut d'intégrité · Journalisation insuffisante · Falsification de requête côté serveur.

(Intitulés et ordre **à vérifier** sur la liste à jour.)

## Qui corrige quoi ?

| Problème | Qui corrige |
|---|---|
| TLS, en-têtes, méthodes, débit, version annoncée | **Proxy** |
| Motifs d'attaque connus | **WAF** (aide, ne remplace pas) |
| Injection, contrôle d'accès, authentification | **Code de l'application** |
| Composant vulnérable | **Mise à jour** |
