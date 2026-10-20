# Corrigé – S14 : Audit et rapport

*Réservé à l'enseignant.*

## Vérification

Séance **sans manipulation technique** : tout se fait sur un dossier fictif ; il n'y a rien à tester en ​machine. Les éléments juridiques (autorisation, périmètre, accord des tiers, atteintes aux systèmes) sont des **rappels de la séance S04**, à faire valider par un juriste avant diffusion. **Non vérifié** : le détail actuel de la qualification **PASSI** de l'ANSSI (cité seulement comme ​exemple de métier encadré) ; la ressource à jour est sur le site de l'ANSSI.

## Partie A

| # | Problème | Exigence | Demande |
|---|---|---|---|
| 1 | « Réseau de l'entreprise » : périmètre **non défini** | Périmètre précis | ​Liste des adresses, sites, applications |
| 2 | « Si nécessaire » : tests d'intrusion **sans limites** | Règles d'engagement, interdits | Objectifs précis, techniques **autorisées et interdites**, validation préalable de chaque test |
| 3 | « Quand cela vous arrange » : pas de **dates ni d'horaires** | Dates et horaires | ​Fenêtres fixées avec le dirigeant, hors production |
| 4 | Logiciel **hébergé chez un prestataire** | Accord des tiers | Autorisation **écrite du prestataire** ou exclusion du périmètre |
| 5 | Signataire : un responsable qui consacre deux heures par ​semaine à l'informatique | Signataire **habilité** | Signature du **dirigeant** ou délégation écrite |
| 6 | Absents : contact d'urgence, confidentialité, responsabilités, sort des preuves | Contenu minimal du cadrage | Les ​ajouter |

Autres éléments acceptables : « accéder à **tous** les systèmes, y compris les messageries » (accès aux courriers des salariés : vie privée, S04) ; « rapport remis au responsable administratif » (le dirigeant doit le ​recevoir).

**Réponse attendue** : on **renvoie une demande de cadrage** ; on ne commence **pas** : l'autorisation est insuffisante et un accès au système du prestataire serait **non autorisé** (S04).

## Partie B

| Réf. | Preuve | Décision | Pour prouver |
|---|---|---|---|
| E1 | Solide | **Ferme** | (déjà ​prouvé) |
| E2 | Insuffisante (déclaratif) | **À confirmer** | Liste des comptes du groupe des administrateurs locaux sur un échantillon de postes |
| E3 | Partielle | **À confirmer** (ou ferme sur « non testée » : le journal ne montre ​aucune restauration) | Demander un **test de restauration** ou l'historique |
| E4 | Solide (inventaire + photo) | **Ferme** | (déjà prouvé) |
| E5 | Partielle (déclaration) | **À confirmer** | Date du dernier changement, appareils connectés |
| E6 | Insuffisante (rumeur) | **Exclu** tant que non vérifié | Examiner la configuration de la journalisation du serveur |
| E7 | Solide | **Ferme** | (déjà prouvé) |
| E8 | Solide | **Ferme** | (déjà prouvé) |

**E6 est dangereux** : une affirmation **fausse** ​discrédite tout le rapport. Il devient un constat utile en **vérifiant** : « La journalisation d'audit du serveur de fichiers n'est pas activée (capture de la configuration, date et heure) » **ou** « est activée, durée de conservation : … ».

## Partie C

Priorités attendues avec la règle de S13 : **E1 P1** (exposé à ​Internet, accès distant par mot de passe seul), **E4 P1** (machines de production sans correctif, **isolement** d'abord), **E8 P1 ou P2** (sensibilité des données du personnel : à argumenter ; la facilité est forte car le droit est « Tout le monde (comptes du bureau) »), **E7 P2** (messagerie sans deuxième facteur ; **P1** pour les comptes de direction, à argumenter), **E3** si confirmé : **P1** (sauvegarde non testée, S02).

Recommandation réécrite (exemple) : **« Fermer la ​redirection du port 3389 sur la box ; ouvrir à la place un accès par VPN avec authentification à deux facteurs, pour les deux commerciaux, avant la fin de la semaine. »**

Pour E8 : la fiche cite le **RGPD** (données de salariés, accès restreint, mesures de sécurité : S04) et **ne reproduit ​aucune donnée**.

## Partie D

Critères du résumé : bilan en deux phrases **avec un point positif réel** (par exemple : le serveur de fichiers existe et une copie nocturne est faite ; le dirigeant est prêt à fermer l'atelier un week-end, annexe 5 de S02) ; trois ​risques **en langage clair** (quelqu'un depuis Internet peut tenter d'ouvrir le poste de la comptable ; la copie de sauvegarde n'a jamais été testée ; des salariés peuvent lire les fiches de paie de tous) ; trois décisions (fermer l'accès distant, tester la ​restauration, restreindre le dossier du personnel) ; limites (tout ce qui est « à confirmer », l'ERP hébergé hors périmètre) ; date de revérification. Pénaliser : sigles, affirmations sans preuve, plus d'une page.

## Partie E

Réponse à « Et si on ne fait rien ? » : **conséquences concrètes pour l'entreprise** (arrêt de l'atelier ​plusieurs jours, comme l'entreprise voisine de l'annexe 4 de S02, fuite de données du personnel avec obligations de notification, S04), sans dramatiser et sans chiffres inventés.

## Partie F

| Situation | Réflexe |
|---|---|
| Dossier d'un ​client accessible depuis Internet | **Danger immédiat** : prévenir **tout de suite** le contact d'urgence, ne pas ouvrir les fichiers au-delà de la preuve minimale |
| Fichiers privés d'un collègue montrés par un salarié | **Ne pas les consulter** (ou refuser), minimiser, noter l'incident sans reproduire le ​contenu |
| Activité frauduleuse sans rapport avec la mission | **S'arrêter**, prévenir le donneur d'ordre, **avis juridique** |
| Demande orale d'« aller voir » chez le prestataire | **Refuser** sans autorisation écrite **du prestataire** ; demander la modification du cadrage |

## Pièges fréquents

- **Commencer** ​avant l'autorisation écrite.
- Mettre dans le rapport une **rumeur** ou un propos non vérifié.
- Recommandations **génériques**.
- **Jargon** dans le résumé managérial.
- **Reproduire des données personnelles** dans le rapport.
- Oublier les **limites** de la mission.
