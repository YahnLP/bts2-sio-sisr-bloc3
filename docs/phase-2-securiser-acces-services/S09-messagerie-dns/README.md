# S09 – Messagerie et DNS : usurpation et protection

> [!WARNING]
> **Séance à rédiger.** Cette page donne le cadre prévu (objectifs, compétences, contenu). Le cours, le TP et l'aide-mémoire arrivent avec la phase 2.

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 2e année – bloc 3 |
| **Séance** | S09 (séance 9 sur 19) – Phase 2 |
| **Durée** | 4 heures |
| **Prérequis** | S05 |
| **Matériel** | VirtualBox : un serveur DNS de laboratoire, un poste |
| **Compétences travaillées** | B3.2 · B3.4 (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Comment empêcher qu'on envoie un message en se faisant passer pour ton organisation ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. Expliquer SPF, DKIM et DMARC et ce que chacun protège ;
2. Lire l'en-tête d'un message et repérer une usurpation ;
3. Situer les risques liés au DNS (détournement, empoisonnement) et la protection par signature (DNSSEC) ;
4. Rédiger les enregistrements SPF et DMARC d'un domaine de laboratoire.

## Contenu prévu

- Cours : chemin d'un message, authentification de l'expéditeur, DNS et sécurité
- TP : lecture d'en-têtes, écriture des enregistrements, test sur un domaine de laboratoire
- Aide-mémoire : syntaxe SPF et DMARC

## Évaluation

- Compte rendu avec captures d'écran datées, nommé `RENDU-B3A2-S09-NOM.pdf`.
- Bilan de compétences rempli en fin de séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)) ; le choix des compétences pour cette séance est une proposition à valider.
- **Programme :** cette séance fait partie d'un programme proposé, à valider avant rédaction.
- Le TP se fait sur un domaine de laboratoire interne, jamais sur un domaine réel de l'établissement. Lien avec B3.2 (identité numérique de l'organisation).

</details>
