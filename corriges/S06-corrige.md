# Corrigé – S06 : Annuaire sécurisé

*Réservé à l'enseignant.*

> [!WARNING]
> **Séance non testée par l'auteur.** Les commandes sont des cmdlets d'administration Active Directory et de stratégie de groupe courantes, mais **aucune n'a été exécutée** (le laboratoire de l'auteur ne comprend pas de Windows Server). À essayer sur le laboratoire de la salle avant la séance, en particulier : la combinaison de paramètres de `Set-ADDefaultDomainPasswordPolicy`, la recherche du groupe « Utilisateurs protégés », les chemins de menus de la GPO (selon la version de Windows Server) et le champ « Package d'authentification » de l'événement 4624.

## Partie A

| Étape | Attendu |
|---|---|
| A1 | Dans le domaine préparé : quelques comptes dans le groupe 512, dont des comptes qui ne devraient pas y être (compte de service, ancien administrateur). L'étudiant justifie chaque compte ou propose son retrait. **Une PME n'a normalement que quelques administrateurs du domaine** (à discuter ; le chiffre exact dépend de l'organisation). |
| A2 | Comptes à mot de passe permanent, comptes inactifs : relever, proposer désactivation après vérification (on ne supprime pas tout de suite). |
| A3 | Valeurs par défaut du domaine **préparé** (à consigner par l'enseignant). Réponse à « 6 caractères, aucun verrouillage » : essais répétés illimités depuis n'importe quel poste du réseau (devinette de mots de passe), qui aboutit vite sur des mots de passe faibles. |

## Partie B

Après la modification : `Get-ADDefaultDomainPasswordPolicy` affiche les nouvelles valeurs. Test des cinq essais faux : le compte se **verrouille** ; le bon mot de passe échoue ensuite pendant la durée de verrouillage ; `Unlock-ADAccount` le rend utilisable. **Compromis** attendu : le verrouillage ralentit la devinette mais permet le **déni de service** (verrouiller un compte volontairement) ; les valeurs retenues sont justifiées.

## Partie C

- **C1** : OU `Administration`, compte `adm-technicien` (pas de messagerie, pas d'usage courant).
- **C2** : le groupe « Utilisateurs protégés » durcit l'authentification des membres : **pas de NTLM** (Kerberos seulement), **pas de mise en cache** des identifiants de connexion, **tickets à durée courte**, pas de délégation. Les valeurs exactes sont à relire dans la documentation Microsoft du système de la salle.
- **C3** : règle exemple : « un droit d'administration du domaine est accordé par écrit, pour une tâche et une durée, et retiré à la fin ; chaque octroi est consigné ».

## Partie D

- D1 : GPO créée et liée à l'OU `Postes`.
- D2 : le **niveau d'authentification LAN Manager** en « réponses NTLMv2 uniquement, refuser LM et NTLM » ; le refus de l'ouverture de session des administrateurs du domaine sur les postes coupe le scénario « un administrateur ouvre une session sur un poste infecté, l'attaquant récupère ses identifiants ».
- D3 : `gpresult` liste `Durcissement-Postes` ; l'ouverture de session d'un administrateur du domaine sur PC1 est **refusée** (message « la méthode de connexion que vous essayez d'utiliser n'est pas autorisée »).

**Pannes fréquentes.** GPO liée à la mauvaise OU (ou à l'OU des utilisateurs au lieu de celle des ordinateurs) ; poste dans le conteneur `Computers` plutôt que dans l'OU `Postes` (la GPO ne s'applique pas) ; `gpupdate` sans redémarrage pour les paramètres de sécurité qui l'exigent ; horloge décalée entre PC1 et DC1 (échec Kerberos).

## Partie E

- E1 : le premier ticket est le **TGT** (service `krbtgt/LAB.LOCAL`) ; l'accès à `\\DC1\NETLOGON` fait apparaître un **ticket de service** (par exemple `cifs/DC1.lab.local`).
- E2 : avec le **nom** : package **Kerberos** ; avec l'**adresse IP** : **NTLM** (cas courant). Conclusion : désigner les services par leur nom, et auditer l'usage de NTLM avant de le restreindre.

## Partie F

- F1 : tous les postes s'ouvrent avec le même mot de passe : un portable volé donne accès à tous. LAPS : mot de passe **unique, aléatoire et renouvelé** par poste, stocké dans l'annuaire, lisible par des rôles désignés.
- F2 : le bastion se place dans la zone d'administration (S05), joignable **seulement** depuis le poste d'administration, avec **second facteur** et **journalisation vers un serveur tiers**.

## Pièges fréquents

- Chercher le groupe « Domain Admins » par son nom sur un système en français.
- Appliquer une GPO à la **mauvaise OU**.
- Confondre **droit d'administration** et **appartenance à un groupe privilégié permanente**.
- Penser que le verrouillage de compte est **gratuit** : il offre une cible de déni de service.
- Oublier que l'**horloge** est une dépendance de Kerberos.
