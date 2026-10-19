# S07 – Authentification des équipements : 802.1X, RADIUS et Wi-Fi d'entreprise

> [!WARNING]
> **Séance à rédiger.** Cette page donne le cadre prévu (objectifs, compétences, contenu). Le cours, le TP et l'aide-mémoire arrivent avec la phase 2.

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 2e année – bloc 3 |
| **Séance** | S07 (séance 7 sur 19) – Phase 2 |
| **Durée** | 4 heures |
| **Prérequis** | S05 |
| **Matériel** | VirtualBox : un serveur RADIUS, un client, éventuellement un point d'accès ou un simulateur |
| **Compétences travaillées** | B3.3 · B3.5A (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Comment ne laisser entrer sur le réseau que des équipements et des personnes identifiés ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. Expliquer le rôle du demandeur, de l'authentificateur et du serveur d'authentification ;
2. Configurer un serveur RADIUS de laboratoire et un client ;
3. Distinguer WPA2/WPA3 personnel et entreprise ;
4. Tester une authentification réussie et refusée, lire les journaux.

## Contenu prévu

- Cours : 802.1X, EAP, RADIUS, WPA-Entreprise, certificats côté serveur
- TP : serveur FreeRADIUS de laboratoire et client de test
- Aide-mémoire : flux d'authentification, codes de réponse

## Évaluation

- Compte rendu avec captures d'écran datées, nommé `RENDU-B3A2-S07-NOM.pdf`.
- Bilan de compétences rempli en fin de séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)) ; le choix des compétences pour cette séance est une proposition à valider.
- **Programme :** cette séance fait partie d'un programme proposé, à valider avant rédaction.
- Prévoir la solution de repli si aucun point d'accès n'est disponible : test avec un client RADIUS en ligne de commande. À tester avant la séance.

</details>
