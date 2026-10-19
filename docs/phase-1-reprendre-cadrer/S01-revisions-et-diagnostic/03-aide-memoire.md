# Aide-mémoire – Commandes et notions à connaître

*BTS SIO SISR 2e année – Bloc 3 – S01*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## Les critères de sécurité

| Critère | Question | Exemple d'atteinte |
|---|---|---|
| **Disponibilité** | Le service répond-il quand on en a besoin ? | Rançongiciel, panne, attaque par déni de service |
| **Intégrité** | Les données sont-elles exactes et non modifiées ? | Fichier falsifié, virement détourné |
| **Confidentialité** | Seuls les ayants droit y accèdent-ils ? | Fuite de données, accès non autorisé |
| **Preuve** | Peut-on démontrer qui a fait quoi, et quand ? | Journaux absents ou modifiables |

## Valeurs et règles à connaître

| Notion | À retenir |
|---|---|
| Facteurs d'authentification | Savoir (mot de passe), avoir (téléphone, clé), être (biométrie) |
| Sauvegarde | **3-2-1** : 3 copies, 2 supports différents, 1 hors site |
| RPO / RTO | Perte de données acceptable / durée d'interruption acceptable |
| Notification d'une violation | CNIL sous **72 heures**, sauf risque improbable pour les personnes |
| Pare-feu | Politique par défaut : **refuser**, puis autoriser le nécessaire |
| Réponse à incident | Préparer, détecter, contenir, éradiquer, restaurer, tirer les leçons |

## Droits Linux

| Valeur | Propriétaire | Groupe | Autres |
|---|---|---|---|
| `640` | lecture, écriture | lecture | rien |
| `644` | lecture, écriture | lecture | lecture |
| `750` | tous | lecture, exécution | rien |
| `600` | lecture, écriture | rien | rien |

Lecture = 4, écriture = 2, exécution = 1 ; on additionne par catégorie.

## Commandes de l'inventaire

| Besoin | Commande |
|---|---|
| Configuration SSH réellement appliquée | `sudo sshd -T \| grep -Ei '^(permitrootlogin\|passwordauthentication\|maxauthtries\|port) '` |
| Tester une configuration SSH avant de l'appliquer | `sudo sshd -t` (aucun message = valide) |
| Comptes d'identifiant 0 | `awk -F: '$3==0 {print $1}' /etc/passwd` |
| Services à l'écoute | `sudo ss -tulpn` |
| Droits d'un fichier | `stat -c '%a %U:%G %n' fichier` |
| Fichiers à bit setuid | `find / -xdev -perm -4000 -type f 2>/dev/null` |
| Membres du groupe d'administration | `getent group sudo` |
| Mises à jour en attente | `sudo apt update` puis `apt list --upgradable` |
| Journal du service SSH | `sudo journalctl -u ssh -n 20 --no-pager` |

## Pare-feu nftables

| Besoin | Commande |
|---|---|
| Vérifier la syntaxe d'un fichier sans l'appliquer | `sudo nft -c -f fichier.nft` |
| Appliquer un fichier | `sudo nft -f fichier.nft` |
| Afficher les règles actives | `sudo nft list ruleset` |
| Tout effacer (retour arrière) | `sudo nft flush ruleset` |

> [!WARNING]
> Avant d'appliquer un pare-feu à distance, **garde une deuxième session ouverte** et prévois comment revenir en arrière. Une règle de trop peut t'enfermer dehors.
