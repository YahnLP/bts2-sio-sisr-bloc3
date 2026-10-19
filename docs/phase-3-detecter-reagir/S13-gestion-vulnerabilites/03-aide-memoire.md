# Aide-mémoire – Lire un rapport de vulnérabilités

*BTS SIO SISR 2e année – Bloc 3 – S13*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## Vocabulaire

| Terme | Sens |
|---|---|
| **Vulnérabilité** | Faiblesse (logiciel ou configuration) |
| **Correctif** | Ce qui la supprime |
| **Exposition** | Qui peut l'atteindre |
| **Exploit** | Méthode pour en tirer parti |
| **Exploitation** | Utilisée **en vrai** par des attaquants |
| **CVE** | Identifiant public (`CVE-année-numéro`) |
| **CVSS** | Note de gravité 0–10 |

## Lire un vecteur CVSS 3.1

`AV:N / AC:L / PR:N / UI:N / S:U / C:H / I:H / A:H`

| Lettre | Question | Pire valeur |
|---|---|---|
| AV | D'où l'attaque ? | N (réseau) |
| AC | Réussite certaine ? | L (facile) |
| PR | Compte nécessaire ? | N (aucun) |
| UI | Clic nécessaire ? | N (aucun) |
| S | Déborde-t-elle ? | C (oui) |
| C, I, A | Effet sur confidentialité, intégrité, disponibilité | H (élevé) |

| Note | Qualification |
|---|---|
| 0 | Aucune |
| 0,1 – 3,9 | Faible |
| 4,0 – 6,9 | Moyenne |
| 7,0 – 8,9 | Élevée |
| 9,0 – 10 | Critique |

## Prioriser : la note ne suffit pas

| Critère | Question |
|---|---|
| Gravité | Note CVSS |
| **Exposition** | Internet, interne, isolée ? |
| **Exploitation** | Un exploit existe-t-il ? Est-elle exploitée ? |
| **Valeur de l'actif** | Sauvegarde ? Serveur de fichiers ? Poste de test ? |
| **Remède** | Correctif, réglage, rien (fin de support) ? |

Sans correctif : **migrer**, **isoler**, **compenser**, ou **accepter par écrit** (avec date de revue).

## Commandes de scan

| Besoin | Commande |
|---|---|
| Ports et versions | `nmap -sV -p 1-1000 CIBLE` |
| Fichiers web courants | `nmap -p 80 --script http-enum CIBLE` |
| Algorithmes SSH | `nmap -p 22 --script ssh2-enum-algos CIBLE` |
| Faiblesses web | `nikto -h http://CIBLE` |
| Score CVSS | `python3 cvss.py "AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H"` |

**Toujours** : autorisation écrite, périmètre, horaires, contact.

## Le cycle

Inventorier → rechercher → **prioriser** → corriger ou compenser → **vérifier par un nouveau scan** → rendre compte.

## Faux positifs et faux négatifs

| | Sens | Réflexe |
|---|---|---|
| Faux positif | Faille signalée qui n'existe pas | Vérifier à la main avant de déranger |
| Faux négatif | Faille présente mais non vue | Scan **authentifié**, plusieurs outils |
