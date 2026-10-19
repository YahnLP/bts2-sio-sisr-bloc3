# Corrigé – S01 : Reprendre la main (révisions et auto-diagnostic)

*Réservé à l'enseignant. Les éléments de réponse de l'auto-diagnostic sont dans le TP (blocs « Éléments de réponse ») ; ce document ajoute les attendus et les pièges.*

## Partie A – Auto-diagnostic

Barème : 1 point par bonne réponse, 3 par thème, **sans note** ; l'objectif est le plan de révision.

| Question | Piège fréquent |
|---|---|
| 2 | Confondre menace et risque : le risque combine une menace, une vulnérabilité **et** une gravité. |
| 4 | Dire que le ver « est plus dangereux » : la différence est le **mode de propagation**. |
| 8 | Répondre que le sel « rend le mot de passe plus long » : il rend le hachage **propre à chaque compte** et empêche les tables précalculées. |
| 9 | Oublier l'**heure** : le secret seul ne suffit pas à produire un code qui change. |
| 11 | Lire `640` comme « 6 pour tous, 4 pour le reste » : trois chiffres = propriétaire, groupe, autres. |
| 14 | Inverser RPO (données) et RTO (temps). |
| 15 | Dire qu'un RAID « copie les données » : il copie aussi les **erreurs**. |
| 16 | Penser que l'adresse IP n'est pas une donnée personnelle. |
| 17 | Oublier la condition : pas de notification si **aucun risque** pour les personnes (la violation reste à consigner en interne). |
| 21 | Confondre intégrité et authenticité : une empreinte publiée au même endroit que le fichier ne prouve pas l'origine. |
| 23 | Citer « autoriser par défaut » parce que « c'est plus simple » : un oubli est alors un accès ouvert. |

## Partie B – Attendus de l'inventaire

| Étape | Résultat attendu sur une Debian par défaut |
|---|---|
| B1 | `port 22`, `passwordauthentication yes`, `maxauthtries 6`, `permitrootlogin prohibit-password` (ou `without-password` selon la version) |
| B2 | Un seul compte d'identifiant 0 : `root`. Groupe `sudo` : le compte créé à l'installation |
| B3 | Au moins SSH (22). Selon la machine : serveur web (80), client DHCP (68/udp), résolveur local. Rappeler la différence entre `127.0.0.1` et `*` |
| B4 | `640 root:shadow` pour `/etc/shadow` ; `644 root:root` pour `/etc/passwd` |
| B5 | Quelques dizaines de programmes au plus (`passwd`, `sudo`, `su`, `mount`, `umount`, `chsh`, `chfn`, `gpasswd`, `newgrp`…) ; tout programme hors des chemins système est suspect |
| B6 | Dépend de la date de l'image : une image ancienne a de nombreux paquets en attente, ce qui illustre le risque de correctifs manquants |
| B7 | Connexions réussies du binôme ; sur une machine exposée, des échecs répétés |

**Exemple d'écarts pour B8** (au moins quatre) : mot de passe autorisé en SSH (risque d'essais répétés, confidentialité) ; six essais autorisés ; services inutiles à l'écoute (surface d'attaque, disponibilité) ; pare-feu absent (tous les ports atteignables) ; paquets non à jour (vulnérabilités connues) ; droits trop larges sur des données.

## Partie C – Attendus du durcissement

| Étape | Résultat attendu |
|---|---|
| C1 | `sshd -t` : aucun message d'erreur (« configuration valide ») ; `sshd -T` : `maxauthtries 3` et `permitrootlogin no` |
| C2 | `nft -c` : aucune erreur ; ping, SSH (depuis `192.168.50.0/24`) et web fonctionnent ; le test du port 3306 expire sans réponse |
| C3 | Avant : `666 root:root` ; après : `640 root:compta` |

**Pannes fréquentes.**

- **Se couper l'accès SSH** : fichier invalide rechargé, ou règle `ip saddr` qui ne correspond pas au réseau réel du binôme. Remède : console VirtualBox, `sudo nft flush ruleset`, correction du fichier. Vérifier le réseau avec `ip -br a`.
- **Fichier de réglages SSH sans effet** : une valeur identique lue **avant** dans un autre fichier de `sshd_config.d/` l'emporte ; la configuration appliquée se lit avec `sshd -T`.
- **`nft -f` ne remplace pas tout** : le fichier commence par `flush ruleset`, qui efface aussi des règles existantes (par exemple celles d'un autre outil) ; le signaler.

## Vérification

Les commandes suivantes ont été exécutées dans un laboratoire Debian/Ubuntu de l'auteur : `sshd -T` (avec le réglage de `sshd_config.d`), `sshd -t`, `nft -c -f` sur le fichier de règles, `awk` sur `/etc/passwd`, `ss`, `stat`, `find -perm -4000`, `getent group sudo`, les commandes de la partie C3. **Non vérifiées** : `journalctl -u ssh` (le laboratoire de l'auteur n'avait pas de journal systemd), l'application réelle des règles `nft -f` sur un réseau interne VirtualBox, `nc -zv -w 3`, l'appartenance du compte créé à l'installation au groupe `sudo`, et le contenu de B6. À tester sur la machine virtuelle de la salle avant la séance.
