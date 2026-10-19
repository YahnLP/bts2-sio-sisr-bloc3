# Corrigé – S04 : Cadre juridique et responsabilités

*Réservé à l'enseignant. Les références sont **à relire sur Légifrance et sur le site de la CNIL** avant de noter : ce corrigé est rédigé de mémoire de cours, sans accès aux textes à jour dans le laboratoire de l'auteur. L'étudiant est évalué sur le **raisonnement** (faits → règle → conséquence → action) et sur la **citation relue**.*

## Partie A – PayVéga

| Question | Attendu |
|---|---|
| Responsable de traitement | **Les clients du cabinet** pour leurs propres salariés ; le **cabinet** est lui-même **sous-traitant** de ses clients pour la paie. |
| Rôle de PayVéga | **Sous-traitant du cabinet** (ou sous-traitant ultérieur vis-à-vis des clients du cabinet). Argument : il traite pour le compte du cabinet, sur instruction. |
| Sensibilité | Le **numéro de sécurité sociale** n'est pas une donnée « sensible » au sens de l'art. 9 mais fait l'objet de **règles strictes** et d'un risque élevé (fraude, usurpation) ; coordonnées bancaires et salaires : **risque élevé** en cas de fuite. À défendre. |

**Un point de subtilité : le cabinet est à la fois sous-traitant (envers ses clients) et donneur d'ordre (envers PayVéga).** Ses clients doivent donner leur **accord** pour le recours à un sous-traitant ultérieur. Valoriser les étudiants qui le voient.

| Clause | Problème et demande |
|---|---|
| 4 conservation | Deux ans après la fermeture, sans fondement : exiger **suppression ou restitution** à la fin du contrat (art. 28) et une **durée justifiée** |
| 6 hors UE | Transfert sans cadre : exiger la **liste des sous-traitants et des pays**, l'**accord préalable**, un mécanisme de transfert (adéquation, clauses types) |
| 9 incident | « Délai raisonnable » : exiger un délai **chiffré** et court, compatible avec les **72 h** de notification du cabinet (par exemple, information « sans délai » et sous 24 h : à négocier) |
| 11 responsabilité | Plafond de trois mois de redevances sans rapport avec le risque ; **négocier** un plafond plus élevé et une assurance ; savoir que le plafond **ne dispense pas** le cabinet de sa responsabilité envers ses clients |
| Absentes | Au choix : objet et durée précis, instructions documentées, confidentialité du personnel, mesures de sécurité, audit, aide aux droits des personnes, restitution des données, localisation, certification |

**A3** : recommandation acceptable = ne pas signer en l'état ; conditions : contrat de sous-traitance conforme à l'art. 28, localisation des données et garanties de transfert, délai de notification d'incident chiffré, réversibilité ; alternative : un autre éditeur proposant ces garanties.

## Partie B – Le portable volé

| Question | Attendu |
|---|---|
| Violation ? | **Oui** : perte de **confidentialité** (accès possible par un tiers) et de **disponibilité** (pas de sauvegarde récente). |
| Prise de connaissance | Lundi à **8 h 30** (signalement) ; le délai de 72 h court jusqu'au **jeudi à 8 h 30**. (Discussion acceptée : le vol date de vendredi soir, mais c'est la **connaissance** qui déclenche le délai.) |
| Risque | **Élevé** : disque non chiffré, 1 200 personnes, 150 numéros de sécurité sociale (risque d'usurpation d'identité). |

| Obligation | Réponse |
|---|---|
| Registre des violations | **Oui**, toujours (même sans notification) |
| Notifier la CNIL | **Oui**, risque non improbable, **72 h** |
| Informer les personnes | **Oui**, risque **élevé** (au moins les 150 personnes dont le numéro est exposé ; par prudence, les 1 200) |
| Plainte | Conseillée (vol) ; **pas** une obligation du RGPD |

Notification : nature = vol d'un portable non chiffré ; catégories et nombre = clients (1 200) et numéros de sécurité sociale (150) ; conséquences = usurpation d'identité, hameçonnage ciblé ; mesures = plainte, changement des accès enregistrés sur le portable, information des personnes, chiffrement des disques ; contact = personne désignée (DPO ou associé gérant).

**B4 – mesures** : chiffrement du disque (C), sauvegarde (D), minimisation (ne pas stocker 150 numéros de sécurité sociale dans un tableur), procédure de signalement immédiat, interdiction de laisser un portable dans un véhicule.

## Partie C – Karim

| Fait | Qualification (à vérifier sur Légifrance) |
|---|---|
| 1 Ouvrir le dossier RH | **Accès ou maintien frauduleux** (art. 323-1) : accès **sans autorisation** même avec les droits techniques ; manquement à la confidentialité |
| 2 Lire la messagerie | **Atteinte au secret des correspondances** (art. 226-15) ; accès frauduleux (323-1) |
| 3 Copier la liste | **Extraction frauduleuse de données** (art. 323-3) ; **violation de données** au sens du RGPD (sortie vers un support personnel) |
| 4 Effacer les journaux | **Suppression frauduleuse de données** (art. 323-3) ; circonstance qui montre l'intention |

**C2** : non, l'excuse des « droits administrateur » est écartée : le droit technique n'est pas une autorisation ; l'employeur peut être civilement responsable des actes de son salarié **dans ses fonctions** et peut avoir manqué à son obligation de sécurité (art. 32) ; sanctions possibles : **disciplinaires** (jusqu'au licenciement), **civiles** (dommages-intérêts), **pénales** (à ne pas chiffrer de mémoire).

**C3** : séparation des comptes (compte d'administration distinct, usage limité), **journaux inaltérables** copiés vers un serveur tiers (Karim ne peut pas les effacer), revue des accès, charte et clause de confidentialité signée, accès à la messagerie d'autrui soumis à procédure.

## Pièges fréquents

- Dire que « le prestataire est responsable » et en rester là.
- Compter les 72 h **depuis le vol** et non depuis la **prise de connaissance**.
- Oublier le **registre** quand on ne notifie pas.
- Confondre **notification à la CNIL** et **information des personnes**.
- Penser qu'un administrateur « couvert par son poste » ne peut pas être poursuivi.
- Citer un article **de mémoire** sans le relire.

## À vérifier avant la séance

Numéros d'articles et formulations du RGPD (art. 4, 5, 6, 9, 28, 30, 32, 33, 34, 35, 37, 44 et suivants, 83) et du Code pénal (226-15, 323-1 à 323-3-1), montants des sanctions, état de la transposition de NIS 2 en France, régime de l'hébergement des données de santé.
