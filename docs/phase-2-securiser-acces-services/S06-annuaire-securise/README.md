# S06 – Annuaire sécurisé et comptes à privilèges

> [!WARNING]
> **Séance à rédiger.** Cette page donne le cadre prévu (objectifs, compétences, contenu). Le cours, le TP et l'aide-mémoire arrivent avec la phase 2.

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 2e année – bloc 3 |
| **Séance** | S06 (séance 6 sur 19) – Phase 2 |
| **Durée** | 4 heures |
| **Prérequis** | S01 ; bloc 2 : Active Directory |
| **Matériel** | VirtualBox : Windows Server (contrôleur de domaine) et un poste Windows |
| **Compétences travaillées** | B3.3 · B3.5A (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Comment empêcher qu'un seul compte compromis donne accès à tout le domaine ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. Expliquer l'authentification Kerberos et ses limites face à NTLM ;
2. Appliquer des stratégies de groupe de sécurité (mots de passe, verrouillage, restrictions) ;
3. Séparer les comptes d'administration des comptes courants (modèle en niveaux) ;
4. Mettre en place un mot de passe local géré (LAPS) ou une alternative documentée ;
5. Situer le rôle d'un bastion d'administration.

## Contenu prévu

- Cours : Kerberos, NTLM, comptes à privilèges, modèle en niveaux, bastion
- TP : durcir un domaine de laboratoire (stratégies de sécurité, comptes d'administration distincts, mot de passe local géré)
- Aide-mémoire : stratégies et commandes utiles

## Évaluation

- Compte rendu avec captures d'écran datées, nommé `RENDU-B3A2-S06-NOM.pdf`.
- Bilan de compétences rempli en fin de séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)) ; le choix des compétences pour cette séance est une proposition à valider.
- **Programme :** cette séance fait partie d'un programme proposé, à valider avant rédaction.
- Prérequis fort sur Active Directory du bloc 2 : vérifier que les machines Windows du laboratoire sont disponibles. Prolonge S04 de la première année (droits et privilèges).

</details>
