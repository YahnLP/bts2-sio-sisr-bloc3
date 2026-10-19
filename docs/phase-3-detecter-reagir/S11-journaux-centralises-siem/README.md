# S11 – Journaux centralisés et supervision de sécurité

> [!WARNING]
> **Séance à rédiger.** Cette page donne le cadre prévu (objectifs, compétences, contenu). Le cours, le TP et l'aide-mémoire arrivent avec la phase 3.

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 2e année – bloc 3 |
| **Séance** | S11 (séance 11 sur 19) – Phase 3 |
| **Durée** | 4 heures |
| **Prérequis** | S05 · S10 |
| **Matériel** | VirtualBox : un collecteur (par exemple Wazuh ou rsyslog) et deux machines |
| **Compétences travaillées** | B3.4 · B3.5A (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Comment voir une attaque quand elle a lieu sur plusieurs machines à la fois ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. Envoyer les journaux de plusieurs machines vers un serveur central ;
2. Normaliser et horodater les événements (synchronisation du temps) ;
3. Écrire des règles de corrélation simples et lire des alertes ;
4. Décider d'une durée de conservation en lien avec le cadre juridique.

## Contenu prévu

- Cours : journalisation, centralisation, corrélation, conservation
- TP : collecteur central, deux sources, alertes sur des tentatives de connexion échouées
- Aide-mémoire : fichiers de journaux, filtres

## Évaluation

- Compte rendu avec captures d'écran datées, nommé `RENDU-B3A2-S11-NOM.pdf`.
- Bilan de compétences rempli en fin de séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)) ; le choix des compétences pour cette séance est une proposition à valider.
- **Programme :** cette séance fait partie d'un programme proposé, à valider avant rédaction.
- L'outil central (Wazuh, ou rsyslog avec un tableau de bord léger) est à choisir selon les machines de la salle. Prolonge S15 de la première année. Étapes basées sur journald non testées dans le laboratoire de l'auteur : à tester avant la séance.

</details>
