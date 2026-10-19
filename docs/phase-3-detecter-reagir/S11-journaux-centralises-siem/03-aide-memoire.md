# Aide-mémoire – Journaux centralisés

*BTS SIO SISR 2e année – Bloc 3 – S11*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## Où sont les journaux (Debian)

| Fichier | Contenu |
|---|---|
| `/var/log/auth.log` | Authentification, `sudo`, SSH (si `rsyslog` est installé) |
| `/var/log/syslog` | Journal général |
| `/var/log/kern.log` | Noyau |
| `journalctl -u ssh` | Journal du service SSH (via `systemd`) |

## Tester sans attendre

```bash
logger -t sshd -p authpriv.warning "message de test"
```

## Lire et filtrer

| Besoin | Commande |
|---|---|
| Dernières lignes | `tail -n 20 fichier` |
| Suivre en direct | `tail -f fichier` |
| Chercher | `grep "Failed password" fichier` |
| Compter par adresse | `grep "Failed password" f \| grep -o 'from [0-9.]*' \| sort \| uniq -c \| sort -rn` |
| Vérifier la syntaxe de rsyslog | `sudo rsyslogd -N1` |
| Relancer | `sudo systemctl restart rsyslog` |
| Voir les ports en écoute | `ss -ltn` |

## Les deux fichiers de configuration du TP

| Machine | Fichier | Idée |
|---|---|---|
| Collecteur | `/etc/rsyslog.d/10-collecteur.conf` | `imtcp` sur le port 514, un dossier par machine |
| Source | `/etc/rsyslog.d/90-envoi.conf` | `omfwd` en TCP vers le collecteur, file d'attente |

Le dossier de stockage appartient à **`syslog:adm`**, sinon : `Permission denied`.

## Protocoles d'envoi

| | UDP | TCP |
|---|---|---|
| Perte silencieuse | Possible | Reprise après coupure |
| Chiffrement | Non | Possible avec TLS |
| Choix pour la sécurité | À éviter | **Recommandé** |

## Règles de corrélation

| Type | Exemple |
|---|---|
| Seuil | 5 échecs depuis la même adresse |
| Multi-machines | Même adresse sur plusieurs serveurs |
| Séquence | Échecs, puis succès, puis création de compte |
| Absence | Plus de journal d'une machine |
| Horaire | Administration à 3 h du matin |

**Régler** : trop bas = fausses alertes, trop haut = attaque manquée.

## Conserver

| Repère | Valeur |
|---|---|
| Recommandation CNIL (délibération 2021-122) | Journalisation courante : **6 mois à 1 an** |
| Au-delà | Besoin à **démontrer et documenter** |
| Mise en œuvre | `logrotate`, droits restreints, suppression à l'échéance |

## Temps

`date -u` · `timedatectl` · service de synchronisation (par exemple `chrony`) sur **toutes** les machines.
