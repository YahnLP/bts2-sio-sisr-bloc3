# Cours – Annuaire sécurisé et comptes à privilèges

*BTS SIO SISR 2e année – Bloc 3 – S06*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

L'annuaire (Active Directory) sait **qui est qui** et **qui peut quoi** dans toute l'organisation. C'est donc la cible préférée des attaquants : celui qui contrôle l'annuaire contrôle **tout le domaine**. Cette séance traite de ce qu'il faut protéger en priorité : l'**authentification** et les **comptes à privilèges**.

---

## 1. Comment un utilisateur s'authentifie dans un domaine

### Kerberos (le protocole par défaut)

Un utilisateur prouve son identité **une fois** ; ensuite, des **tickets** l'authentifient auprès des services, sans renvoyer son mot de passe.

<figure class="graphe diagramme"><svg viewBox="0 0 1393 406" style="max-width:1393px" role="img" aria-label="Diagramme de séquence" xmlns="http://www.w3.org/2000/svg">
<defs><marker id="s62e2e5" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="8" markerHeight="8" orient="auto"><path d="M0,0 L10,5 L0,10 z" class="seq-head"/></marker></defs>
<line class="seq-life" x1="232" y1="62" x2="232" y2="400"/>
<rect class="seq-box" x="117" y="12" width="230" height="40" rx="8"/><text x="232" y="37" text-anchor="middle" class="seq-title">Utilisateur (poste)</text>
<line class="seq-life" x1="697" y1="62" x2="697" y2="400"/>
<rect class="seq-box" x="582" y="12" width="230" height="40" rx="8"/><text x="697" y="37" text-anchor="middle" class="seq-title">Contrôleur de domaine (KDC)</text>
<line class="seq-life" x1="1161" y1="62" x2="1161" y2="400"/>
<rect class="seq-box" x="1046" y="12" width="230" height="40" rx="8"/><text x="1161" y="37" text-anchor="middle" class="seq-title">Serveur de fichiers</text>
<line class="seq-msg" x1="232" y1="96" x2="693" y2="96" marker-end="url(#s62e2e5)"/><text x="464" y="88" text-anchor="middle">1. Je suis alice (preuve dérivée du mot de passe)</text>
<line class="seq-msg dash" x1="697" y1="146" x2="236" y2="146" marker-end="url(#s62e2e5)"/><text x="464" y="138" text-anchor="middle">2. Ticket d'authentification (TGT)</text>
<line class="seq-msg" x1="232" y1="196" x2="693" y2="196" marker-end="url(#s62e2e5)"/><text x="464" y="188" text-anchor="middle">3. Je veux accéder au serveur de fichiers (avec mon TGT)</text>
<line class="seq-msg dash" x1="697" y1="246" x2="236" y2="246" marker-end="url(#s62e2e5)"/><text x="464" y="238" text-anchor="middle">4. Ticket de service</text>
<line class="seq-msg" x1="232" y1="296" x2="1157" y2="296" marker-end="url(#s62e2e5)"/><text x="697" y="288" text-anchor="middle">5. Voici mon ticket de service</text>
<line class="seq-msg dash" x1="1161" y1="346" x2="236" y2="346" marker-end="url(#s62e2e5)"/><text x="697" y="338" text-anchor="middle">6. Accès accordé</text>
</svg></figure>

Points à retenir :

- Les tickets ont une **durée limitée** et sont horodatés : une **horloge décalée** de plus de quelques minutes (la tolérance par défaut est de cinq minutes) fait **échouer** l'authentification. Un bon **service de temps** est donc une mesure de sécurité.
- Le contrôleur de domaine détient le **secret de chaque compte** : le compromettre revient à tout compromettre.
- On désigne les services par leur **nom** : une connexion par **adresse IP** retombe souvent sur NTLM.

### NTLM (l'ancien protocole, encore présent)

Mécanisme de **défi-réponse** : le serveur envoie un défi, le client répond avec un calcul fondé sur le **hachage** du mot de passe. Faiblesses :

| Attaque | Principe |
|---|---|
| **Passer le hachage** (*pass-the-hash*) | Le hachage volé suffit pour s'authentifier : pas besoin du mot de passe |
| **Relais** (*relay*) | L'attaquant fait suivre la réponse d'un client vers un autre serveur |
| **Force brute hors ligne** | Un hachage capturé se teste à très grande vitesse |

Mesure : imposer des **versions récentes** (NTLMv2), puis **réduire** et si possible **désactiver** NTLM, en commençant par **observer** qui l'emploie. Les anciennes variantes (LM, NTLMv1) doivent être **refusées**.

---

## 2. Les comptes à privilèges : la cible

| Groupe ou rôle | Pourquoi c'est critique |
|---|---|
| **Administrateurs du domaine** | Contrôle total du domaine |
| **Administrateurs de l'entreprise, du schéma** | Contrôle de toute la forêt, modification de la structure de l'annuaire |
| **Opérateurs de compte, de sauvegarde, de serveur…** | Peuvent souvent **s'élever** jusqu'à l'administration du domaine |
| **Comptes de service** | Souvent trop puissants, mot de passe ancien et jamais changé |
| **Administrateur local** des postes | Identique sur tous les postes : une compromission **se propage** |

> [!NOTE]
> **Les noms de groupes changent selon la langue** du système (« Domain Admins », « Admins du domaine »…). Pour les retrouver sans erreur, on emploie leur **identifiant de sécurité** : le groupe d'identifiant relatif **512** est celui des administrateurs du domaine, **518** celui du schéma et **519** celui de l'entreprise.

### Les bonnes pratiques

1. **Peu de comptes privilégiés**, **nominatifs** (pas de compte « admin » partagé), revus régulièrement.
2. **Séparer** le compte de tous les jours du compte d'administration : un **administrateur a deux comptes**. On ne lit pas ses courriels, on ne navigue pas avec le compte d'administration.
3. **Moindre privilège dans le temps** : un droit élevé accordé **pour la tâche**, retiré ensuite.
4. **Groupe « Utilisateurs protégés »** pour les comptes d'administration : durcit l'authentification (pas de NTLM, pas de mise en cache des identifiants, tickets à durée courte).
5. **Authentification multifacteur** pour les accès d'administration.
6. **Journaliser** chaque action privilégiée, vers un serveur que l'administrateur ne contrôle pas (voir S11).

---

## 3. Le modèle en niveaux (*tier model*)

L'idée : **un identifiant d'un niveau ne se connecte jamais sur un niveau moins sûr.** Un attaquant qui vole des identifiants sur un poste ne doit pas y trouver ceux d'un administrateur du domaine.

| Niveau | Contenu | Qui s'y connecte |
|---|---|---|
| **0** | Contrôleurs de domaine, comptes qui les administrent | Administrateurs du domaine, uniquement ici |
| **1** | Serveurs d'applications et de fichiers | Administrateurs de serveurs |
| **2** | Postes des utilisateurs | Support, utilisateurs |

Mise en œuvre : des **comptes distincts** par niveau, et des règles qui **interdisent** l'ouverture de session d'un compte de niveau supérieur sur un niveau inférieur (droits « interdire l'ouverture de session » appliqués par stratégie de groupe).

> [!WARNING]
> **Un administrateur du domaine qui ouvre une session sur un poste d'utilisateur y laisse des identifiants exploitables.** C'est l'erreur la plus fréquente dans les incidents où l'attaquant « monte » du poste au domaine.

---

## 4. Les stratégies de groupe de sécurité

Une **stratégie de groupe (GPO)** applique des paramètres à des ordinateurs ou des utilisateurs, selon l'**unité d'organisation (OU)** où elle est liée. Exemples de paramètres de sécurité :

| Domaine | Exemple |
|---|---|
| **Mots de passe** | Longueur minimale, historique ; **verrouillage** après quelques échecs |
| **Authentification** | Niveau d'authentification réseau : refuser LM et NTLMv1 |
| **Droits** | Interdire l'ouverture de session locale ou par bureau à distance aux comptes de niveau supérieur |
| **Pare-feu et services** | Activer le pare-feu local, désactiver les services inutiles |
| **Journalisation** | Activer l'audit des ouvertures de session et des changements de privilèges |

Bon réflexe : **ne pas modifier la stratégie par défaut du domaine** au-delà de la politique de mots de passe ; créer des GPO **nommées par leur objet** (« Durcissement-Postes »), liées à la **bonne OU**, et **tester sur une OU pilote**.

**Longueur plutôt que complexité.** Les recommandations actuelles (CNIL, ANSSI) privilégient des mots de passe **longs** (des phrases) plutôt que des règles de composition lourdes, avec un blocage des essais répétés et, si possible, un second facteur. **À relire dans la recommandation à jour** avant de fixer une valeur.

---

## 5. Le mot de passe de l'administrateur local

Si tous les postes partagent le même mot de passe d'administrateur local, **un seul poste volé = tous les postes ouverts**. La solution : un mot de passe **unique et aléatoire par poste**, **renouvelé** automatiquement et **stocké dans l'annuaire**, que seuls les rôles habilités peuvent lire. Microsoft propose pour cela la solution **LAPS** (version historique et version intégrée aux versions récentes de Windows : **à vérifier** selon les systèmes de la salle).

---

## 6. Le bastion d'administration

Un **bastion** (ou serveur de rebond) est la **porte unique** d'administration : on se connecte **au bastion** (avec un second facteur), et **depuis lui** aux serveurs. Il permet de **limiter** les accès, d'**enregistrer** les sessions et de **couper** un accès en un seul endroit.

**Test flash.** Un administrateur a un seul compte « admin » qu'il utilise aussi pour lire ses courriels. Quel scénario de la séance S02 cela rend-il plus vraisemblable, et quelle mesure ?

<details markdown="1">
<summary>Voir la réponse</summary>

Le scénario du **message piégé** (S1) : si un administrateur clique, l'attaquant obtient un compte à tous les droits. Mesure : **séparer** les comptes (un compte courant sans privilège, un compte d'administration réservé aux tâches d'administration, sur des machines dédiées).

</details>
