# Corrigé – S07 : 802.1X, RADIUS et Wi-Fi d'entreprise

*Réservé à l'enseignant.*

## Vérification

Exécuté dans un laboratoire Ubuntu 24.04 de l'auteur (FreeRADIUS 3.2.5, `radtest`, `eapol_test` du paquet `eapoltest`) :

| Test | Résultat constaté |
|---|---|
| `radtest alice Lab-2026 … Secret-Borne-Lab` | `Access-Accept` avec `Tunnel-Type = VLAN`, `Tunnel-Medium-Type = IEEE-802`, `Tunnel-Private-Group-Id = "20"` |
| `radtest alice mauvais …` | `Access-Reject` |
| `radtest … testing123` (mauvais secret) | **Aucune réponse** (la commande attend jusqu'à abandon) |
| `eapol_test` PEAP, bon mot de passe | `SUCCESS` (plusieurs `Access-Challenge`, puis `Access-Accept`) |
| `eapol_test` PEAP, mauvais mot de passe | `FAILURE` |
| PEAP + `ca_cert` du certificat du serveur | `SUCCESS` |
| PEAP + `ca_cert` d'un autre magasin | `FAILURE` |

**Adaptations de l'environnement de l'auteur** : le laboratoire n'avait pas d'IPv6, ce qui faisait échouer le démarrage de FreeRADIUS (blocs `listen` IPv6 retirés de la configuration du site). **Une machine virtuelle Debian avec IPv6 n'a pas ce problème**, mais si l'erreur « Failed opening auth address :: » apparaît, commenter les blocs `listen` qui contiennent `ipv6addr = ::` dans `/etc/freeradius/3.0/sites-enabled/default`.

**Non vérifié** : le nom du paquet qui fournit `eapol_test` sous la version de Debian de la salle (`eapoltest` sous Ubuntu 24.04) ; une authentification avec une vraie borne Wi-Fi ou un vrai switch ; l'intégration à un annuaire Active Directory ; le comportement de `radtest` avec un mauvais secret sur une autre version (délai avant abandon).

## Partie A

Voir les éléments de réponse du TP.

## Partie B

- B2 : `secret = Secret-Borne-Lab` dans le bloc `client localhost`.
- B3 : les cinq lignes ajoutées à la fin de `users` (l'indentation des lignes d'attributs **par au moins une espace ou une tabulation** est obligatoire).
- B4 : `Ready to process requests`.

## Partie C

| Étape | Attendu |
|---|---|
| C1 | `Access-Accept` avec les trois attributs de VLAN |
| C2 | `Access-Reject` ; dans le journal, une ligne indiquant l'échec d'authentification (`Login incorrect`) |
| C3 | `Access-Accept` **sans** attributs de VLAN : la borne laisse `bob` dans le VLAN par défaut du port ou du réseau |
| C4 | Aucune réponse ; le journal signale le secret erroné ou une requête invalide |

## Partie D

D1 `SUCCESS` ; D2 `FAILURE` ; D3 `SUCCESS` avec le certificat du serveur, **`FAILURE`** avec une autre autorité. L'explication attendue : sans `ca_cert`, le client accepte tout serveur qui lui présente un certificat ; un attaquant qui monte une fausse borne et un faux serveur RADIUS **collecte les identifiants PEAP**. La vérification (autorité **et** nom du serveur) lie la confiance du client à **une** identité.

## Partie E – réponse de référence

| Question | Proposition |
|---|---|
| Réseaux | **Personnel** (802.1X), **atelier** si besoin (802.1X ou prise filaire), **invités** (séparé) |
| Méthode EAP | PEAP si pas de PKI et peu de moyens (avec vérification du serveur imposée) ; EAP-TLS si une autorité de certification interne existe (plus sûr, pas de mot de passe à voler) |
| VLAN et zones | Personnel : VLAN utilisateurs (zone LAN) ; atelier : VLAN machines, zone séparée (S05) ; invités : VLAN invités, Internet seulement |
| Profil des postes | Stratégie de groupe qui pousse le profil avec l'autorité de confiance et le **nom du serveur** |
| Machines à commande numérique | Prise filaire isolée dans un VLAN restreint ; si MAC, protection **faible** : flux limités par le pare-feu, pas d'accès à Internet ni aux zones internes |
| Arrivée et départ | Création et **désactivation immédiate** du compte ; plus de clé partagée à changer |

## Pièges fréquents

- Oublier de **stopper le service** avant `freeradius -X` (port déjà utilisé).
- **Indentation** des attributs dans `users`.
- Croire qu'un **refus** et un **silence** sont la même chose : le silence indique un problème de **secret** ou de joignabilité.
- Valider le certificat du serveur **sans** vérifier son nom.
- Utiliser l'adresse MAC comme protection forte.
