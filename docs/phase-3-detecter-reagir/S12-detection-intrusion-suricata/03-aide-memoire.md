# Aide-mémoire – Détection d'intrusion avec Suricata

*BTS SIO SISR 2e année – Bloc 3 – S12*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## IDS ou IPS

| | IDS | IPS |
|---|---|---|
| Position | Copie du trafic | En coupure |
| Action | Alerte | Alerte et bloque |
| On commence par | **Oui** | Quand les règles sont mûres |

## Structure d'une règle

```text
action protocole source port -> destination port (options)
alert http any any -> $HOME_NET any (msg:"..."; http.uri; content:"..."; nocase; sid:1000001; rev:1;)
```

| Option | Rôle |
|---|---|
| `msg` | Texte de l'alerte |
| `http.uri` | Adresse demandée, **normalisée** |
| `http.uri.raw` | Adresse **brute** (pour `../` et autres astuces) |
| `http.user_agent` | En-tête `User-Agent` |
| `content:"x"` | Chercher `x` ; `nocase` ignore la casse |
| `distance:0` | Après le contenu précédent |
| `flags:S` | Paquets de demande de connexion |
| `threshold:type both, track by_src, count N, seconds T` | N événements en T secondes, une alerte |
| `classtype` | Catégorie (donne la priorité) |
| `sid`, `rev` | Identifiant (**≥ 1 000 000** pour les règles locales) et révision |

## Commandes

| Besoin | Commande |
|---|---|
| Tester la configuration | `sudo suricata -T -c /etc/suricata/suricata.yaml -S règles` |
| Lancer sur une interface | `sudo suricata -c /etc/suricata/suricata.yaml -S règles --af-packet=IFACE -l dossier` |
| Définir son réseau | `--set vars.address-groups.HOME_NET="[10.40.0.0/24]"` |
| Voir les alertes | `cat dossier/fast.log` |
| Détail des alertes | `jq 'select(.event_type=="alert")' dossier/eve.json` |
| Voir ce que la sonde voit | `jq 'select(.event_type=="http")' dossier/eve.json` |
| Mettre à jour des règles publiées | `suricata-update` (non testé dans ce laboratoire) |

`-S` charge **uniquement** ton fichier : plus rapide pour apprendre, mais **sans** les règles publiées.

## Régler

| Problème | Levier |
|---|---|
| Faux positif | **Préciser** la règle ; sinon **suppression** pour une source connue |
| Attaque manquée | **Élargir** ou ajouter une règle ; vérifier le **bon tampon** |
| Source légitime bruyante | `suppress gen_id 1, sig_id N, track by_src, ip A.B.C.D` dans `threshold.config` |
| Règle inutile | La **désactiver** (commentaire) et le noter |

Toute **exception** est documentée : règle, source, raison, responsable, date de revue.

## Ce qu'une sonde ne voit pas

- Le contenu des échanges **chiffrés** ;
- Le trafic qui ne passe pas devant elle ;
- Ce qui n'a pas de motif réseau reconnaissable.

## Vérifier qu'une règle fonctionne

1. Écrire la règle ; 2. `-T` ; 3. lancer la sonde ; 4. rejouer **l'attaque** de laboratoire ; 5. rejouer une action **légitime** ; 6. lire `fast.log` **et** `eve.json` (la sonde a-t-elle vu la requête ?).
