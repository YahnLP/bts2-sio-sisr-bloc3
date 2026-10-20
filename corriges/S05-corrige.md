# Corrigé – S05 : Filtrage avancé et zones

*Réservé à l'enseignant.*

## Partie A – Matrice de référence

| Source ↓ / Destination → | LAN | DMZ | ​Internet |
|---|---|---|---|
| **LAN** | — | TCP 80 et 443 ; TCP 22 **depuis `192.168.10.50` seulement** | TCP 80 et 443 ; UDP 53 |
| **DMZ** | **rien** | — | TCP 443 ; UDP 53 |
| **Internet** | **rien** | TCP 443 | — |

Réponse à A1 « flux le plus dangereux » : **DMZ vers LAN** (un serveur compromis atteint le réseau interne). Cases vides : **trois** (DMZ → LAN, Internet → LAN, et les flux non listés), écrites comme **refus par la politique par défaut**.

## Partie C – Chaîne `transit` complète

```text
  chain transit {
    type filter hook forward priority 0; policy drop;
    ct state established,related accept
    ct state invalid drop
    iifname "fwlan" oifname "fwdmz" ip saddr $LAN tcp dport { 80, 443 } accept
    iifname "fwlan" oifname "fwdmz" ip saddr $ADMIN tcp dport 22 accept
    iifname "fwlan" oifname "fwext" tcp dport { 80, 443 } accept
    iifname "fwlan" oifname "fwext" udp dport 53 accept
    iifname "fwext" oifname "fwdmz" tcp dport 443 accept
    iifname "fwdmz" oifname "fwext" tcp dport 443 accept
    iifname "fwdmz" oifname "fwext" udp dport 53 accept
    counter limit rate 5/minute log prefix "REFUS-TRANSIT "
  }
```

Variantes acceptées : une seule règle `tcp dport { 80, 443 }` regroupant plusieurs ​sources ; des `set` pour les ports ; `reject` à la place du `drop` côté LAN. **Refusé** : une règle `accept` sans `iifname`/`oifname` ni adresses (trop large), un `accept` de tout le LAN vers la DMZ sur tous les ports.

## Partie D – Résultats attendus

| N° | Résultat | Explication |
|---|---|---|
| 1 | **Passe** (200) | LAN → DMZ 80 |
| 2 | **Passe** | LAN → DMZ 443 |
| 3 | **Passe** | Internet → DMZ 443 |
| 4 | **Bloqué** (000) | Internet → DMZ 80 : seul HTTPS est publié |
| 5 | **Passe** | SSH depuis `.50` |
| 6 | **Bloqué** | SSH depuis `.10` : la règle est limitée à `$ADMIN` |
| 7 | **Bloqué** | SSH depuis ​Internet |
| 8 | **Bloqué** | DMZ → LAN |
| 9 | **Bloqué** | Internet → LAN |
| 10 | **Passe** | LAN → Internet 443 |
| 11 | **Passe** | DMZ → Internet 443 |
| 12 | **Passe** | La chaîne `entrant` accepte l'écho ICMP venu du LAN |
| 13 | **Bloqué** | Aucune règle n'autorise l'ICMP du LAN vers la DMZ |

**Réponse « test 5 réussit, 6 échoue »** : la règle SSH est conditionnée par l'adresse **source** `192.168.10.50`, et non par la zone entière ; les deux ​machines sont dans la même zone mais n'ont pas le même **droit**.

**D2** : chaque test refusé ajoute environ **2 paquets** (SYN renvoyé une fois pendant les 2 s de `curl -m 2`). **D3** : avec `iifname "fwext" accept` placé avant les règles précises, les tests 4, 7 et 9 **passent** : la règle large masque tout le reste.

## Partie E – Matrice prouvée

| Flux | Autorisé ? | Test |
|---|---|---|
| Utilisateurs → DMZ web | Oui | 1, 2 |
| Admin → DMZ SSH | Oui | 5 |
| Poste ordinaire → DMZ SSH | Non | 6 |
| ​Internet → DMZ HTTPS | Oui | 3 |
| Internet → DMZ HTTP | Non | 4 |
| DMZ → utilisateurs | Non | 8 |
| Internet → utilisateurs | Non | 9 |

**E2 – attaques non bloquées** (deux au choix) : message piégé sur un flux 80/443 autorisé (le filtrage ne voit pas le contenu) ; attaque applicative contre le site web (HTTPS ​autorisé) ; compromission du poste d'administration (qui a le droit d'ouvrir SSH) ; fuite par un flux autorisé (exfiltration en HTTPS vers Internet) ; vol de mot de passe SSH.

## Pannes fréquentes

- **`nft -c` signale une erreur** : accolades du `{ 80, 443 }` oubliées, variable `$LAN` non définie, point-virgule manquant après `policy drop`.
- **Test 1 qui échoue** : les écouteurs n'ont pas fini de ​démarrer (relancer), ou une règle comporte `fwdmz` et `fwlan` inversés.
- **`ip netns` : « Operation not permitted »** : commande lancée sans `sudo`.
- **Services déjà en écoute après un `down` raté** : relancer `sudo ./lab-zones.sh down`, puis `up`.

## Vérification

Le script du laboratoire et le fichier de règles complet ont été exécutés dans un laboratoire Debian/Ubuntu de l'auteur (espaces de noms réseau), avec du trafic réel : **les 13 ​tests ont donné les résultats ci-dessus**, ainsi que D2 (compteur à +2 par test) et D3 (règle large). **Non vérifiés** : la lecture des messages `log` avec `dmesg` (nécessite `nf_log_all_netns` et un journal du noyau accessible), la version de Debian de la salle (`netcat-openbsd` fournit `nc -z -w -s`), le comportement dans VirtualBox (le laboratoire n'en dépend pas, mais il faut une machine avec le noyau Linux standard).
