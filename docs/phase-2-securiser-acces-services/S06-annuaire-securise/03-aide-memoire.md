# Aide-mémoire – Annuaire sécurisé

*BTS SIO SISR 2e année – Bloc 3 – S06*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

> [!WARNING]
> Commandes **non testées par l'auteur** (pas de Windows Server dans son laboratoire) : à essayer avant usage. Les noms de groupes et de menus changent selon la langue.

## Kerberos et NTLM

| | Kerberos | NTLM |
|---|---|---|
| Principe | **Tickets** délivrés par le contrôleur de domaine | **Défi-réponse** fondé sur le hachage |
| Faiblesses | Horloge décalée, compromission du contrôleur | Passer le hachage, relais, force brute |
| Se déclenche si… | On désigne le service par son **nom** | On le désigne par son **adresse IP**, ou service ancien |
| Mesure | Temps synchronisé | Imposer NTLMv2, observer, réduire, désactiver |

## Groupes critiques (identifiant relatif)

| Groupe | Identifiant relatif |
|---|---|
| Administrateurs du domaine | **512** |
| Administrateurs du schéma | **518** |
| Administrateurs de l'entreprise | **519** |

## Commandes PowerShell

| Besoin | Commande |
|---|---|
| Identifiant du domaine | `(Get-ADDomain).DomainSID.Value` |
| Membres d'un groupe par identifiant | `Get-ADGroupMember -Identity "$sid-512"` |
| Mots de passe qui n'expirent pas | `Search-ADAccount -PasswordNeverExpires -UsersOnly` |
| Comptes inactifs depuis 90 jours | `Search-ADAccount -AccountInactive -TimeSpan 90.00:00:00 -UsersOnly` |
| Politique de mots de passe | `Get-ADDefaultDomainPasswordPolicy` |
| Modifier cette politique | `Set-ADDefaultDomainPasswordPolicy -Identity domaine -MinPasswordLength 12 …` |
| Créer un compte | `New-ADUser …` |
| Ajouter / retirer d'un groupe | `Add-ADGroupMember` · `Remove-ADGroupMember` |
| Déverrouiller | `Unlock-ADAccount -Identity compte` |
| Créer et lier une GPO | `New-GPO -Name …` · `New-GPLink -Name … -Target "OU=…"` |
| Forcer et vérifier l'application | `gpupdate /force` · `gpresult /r` · `gpresult /h rapport.html` |
| Tickets Kerberos du poste | `klist` · `klist purge` |

## Les bonnes pratiques en une phrase chacune

- **Peu** de comptes privilégiés, **nominatifs**, revus.
- **Deux comptes** par administrateur : courant et d'administration.
- **Utilisateurs protégés** + second facteur pour l'administration.
- **Niveaux** : un identifiant d'un niveau ne s'ouvre pas sur un niveau inférieur.
- Mot de passe local **unique** par poste (LAPS).
- **Bastion** pour les accès d'administration ; actions **journalisées** ailleurs.
