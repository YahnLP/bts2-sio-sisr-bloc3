# Aide-mémoire – nftables et matrice de flux

*BTS SIO SISR 2e année – Bloc 3 – S05*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## Zones

| Zone | Confiance | Règle |
|---|---|---|
| Utilisateurs | Moyenne | Peu de flux entrants |
| DMZ | Faible | Seuls les flux **écrits** vers l'extérieur ; **rien** vers l'interne |
| Serveurs internes | Haute | Accessibles depuis les zones qui en ont besoin, sur des ports précis |
| Administration | Haute | Source unique des flux d'administration |
| Internet | Nulle | Seulement ce qui est publié |

**Un flux n'existe que s'il est écrit. Une case vide de la matrice devient un refus.**

## Structure nftables

```text
table inet NOM
  chain NOM
    type filter hook input|forward|output priority 0; policy drop;
    règle
```

| Hook | Paquets |
|---|---|
| `input` | Vers le pare-feu lui-même |
| `forward` | Qui le traversent (d'une zone à l'autre) |
| `output` | Émis par le pare-feu |

## Écriture des règles

| Besoin | Écriture |
|---|---|
| Interfaces | `iifname "x" oifname "y"` |
| Adresses | `ip saddr 192.168.10.0/24` · `ip daddr 192.168.20.10` |
| TCP, UDP | `tcp dport 22` · `tcp dport { 80, 443 }` · `udp dport 53` |
| Réponses aux connexions autorisées | `ct state established,related accept` |
| Paquets incohérents | `ct state invalid drop` |
| Compter et journaliser | `counter limit rate 5/minute log prefix "TEXTE "` |
| Définir une variable | `define LAN = 192.168.10.0/24` puis `$LAN` |

**Ordre :** la **première** règle qui correspond à un verdict s'applique : précis avant général.

## Commandes

| Besoin | Commande |
|---|---|
| Vérifier sans appliquer | `sudo nft -c -f fichier.nft` |
| Appliquer | `sudo nft -f fichier.nft` |
| Voir les règles | `sudo nft list ruleset` |
| Voir une chaîne | `sudo nft list chain inet NOM CHAINE` |
| Tout effacer | `sudo nft flush ruleset` |
| Agir dans une zone du laboratoire | `sudo ip netns exec ZONE commande` |

## Tests

| Test | Commande |
|---|---|
| Un web répond | `curl -s -m 2 -o /dev/null -w "%{http_code}\n" http://IP:PORT` |
| Un port TCP est ouvert | `nc -z -w 2 IP PORT` |
| Un port avec une adresse source précise | `nc -z -w 2 -s IP_SOURCE IP PORT` |
| Un ping | `ping -c 1 -W 1 IP` |

## `drop` ou `reject`

| `drop` | `reject` |
|---|---|
| Silence, l'émetteur attend | Refus immédiat |
| Vers Internet | À l'intérieur, pour diagnostiquer |

> [!NOTE]
> Un filtrage par adresses et ports ne voit pas le **contenu** : il cloisonne, il ne remplace pas le reste.
