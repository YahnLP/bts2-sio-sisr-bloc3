# Corrigé – S02 : Analyse de risques (Atelier Verdier)

*Réservé à l'enseignant. Il n'y a pas une réponse unique : on évalue la **justification par le dossier**, la cohérence des échelles et le réalisme du plan. Ce corrigé propose une analyse de référence.*

## Partie A – Cadrer

| Valeur métier | Biens supports |
|---|---|
| Fabriquer et livrer dans les délais | Machines à commande numérique et leurs PC Windows 7 (annexe 2), serveur de fichiers, réseau, ERP |
| Garder confidentiels les plans des clients et les gabarits maison | Serveur de fichiers (dossier `Plans`), postes du bureau d'études, messagerie |
| Gérer les clients et la facturation | ERP hébergé, serveur de fichiers (tableur clients), messagerie |
| Respecter les obligations envers le personnel (paie) | Dossier `RH` du serveur, postes administratifs |

| Événement redouté | Critère | Gravité | Justification |
|---|---|---|---|
| Atelier à l'arrêt plus d'une semaine | D | 3 | Délais de chantier manqués, pénalités contractuelles (annexe 1) |
| Plans de clients publiés ou revendus | C | 3 | Plans de bâtiments publics, confiance de l'architecte (annexe 4) |
| Gabarits maison copiés par un concurrent | C | 2 | Savoir-faire, perte d'avantage, mais pas d'arrêt d'activité |
| Fiches de paie et dossiers du personnel divulgués | C | 3 | Données personnelles sensibles, notification possible, atteinte aux salariés |
| Programmes de découpe modifiés | I | 3 | Pièces défectueuses, risque pour la sécurité des personnes sur machines |
| ERP indisponible plusieurs jours | D | 2 | Facturation retardée, activité de fabrication maintenue |

(La gravité 4 peut être défendue pour l'arrêt prolongé si on estime la survie menacée ; accepter l'argument.)

## Partie B – Sources et scénarios

| Source | Objectif | Pertinence |
|---|---|---|
| Cybercriminel opportuniste | Rançon (chiffrer et monnayer) | **Très pertinente** : voisin déjà touché (annexe 4), protections faibles |
| Concurrent | Copier plans et gabarits | Pertinente mais moins probable : demande des moyens ciblés |
| Salarié ou ancien salarié mécontent | Nuire, emporter des données | Pertinente : tout le monde accède à tout (annexe 2) |
| Hacktiviste | Message politique | Écartée : rien dans le dossier ne désigne l'atelier comme cible |

Scénarios de référence :

| N° | Chaîne | Événement redouté | Bien visé |
|---|---|---|---|
| S1 | Message piégé → clic d'un salarié → poste (droits d'administrateur) infecté → déplacement vers le serveur de fichiers → chiffrement du serveur **et du NAS** (branché en permanence) | Atelier à l'arrêt, données perdues | Serveur de fichiers, NAS |
| S2 | Accès distant (port 3389 ouvert, mot de passe seul) deviné ou volé → accès au poste d'un commercial → serveur de fichiers → chiffrement ou vol de données | Arrêt ou fuite de plans | Poste distant, serveur |
| S3 | Faille d'un PC Windows 7 non maintenu → ver ou intrusion → machines à commande numérique → modification ou arrêt des programmes de découpe | Pièces défectueuses, arrêt | Machines à commande numérique |
| S4 | Compte de messagerie volé (mot de passe seul, hameçonnage) → lecture des échanges et envoi de faux messages aux clients | Fuite de plans, fraude | Messagerie |
| S5 | **Prestataire de l'ERP** compromis ou incident chez lui, sans garantie de restauration → données clients indisponibles ou volées | ERP indisponible, fuite des coordonnées de 600 clients | ERP (tiers) |

Un scénario d'initié (salarié qui copie le dossier `RH` ou `Plans`) est accepté comme S6.

## Partie C – Évaluation

| Scénario | G | V | Produit | Niveau |
|---|---|---|---|---|
| S1 | 3 | 4 | 12 | **Élevé** (clic déjà arrivé, droits d'administrateur, NAS exposé) |
| S2 | 3 | 3 | 9 | **Élevé** (accès distant exposé, mot de passe seul) |
| S3 | 3 | 2 | 6 | Moyen (réseau non cloisonné, mais cible peu attrayante) |
| S4 | 2 | 3 | 6 | Moyen |
| S5 | 2 | 2 | 4 | Moyen (tiers, contrat flou) |

La vraisemblance est acceptée à ±1 niveau si elle est **justifiée** par le dossier. Une vraisemblance donnée sans justification perd les points de la colonne « Pourquoi ».

## Partie D – Traitement de référence

| Risque | Décision | Mesure | Coût (ordre de grandeur à justifier) | Délai | Résiduel |
|---|---|---|---|---|---|
| S1 | Réduire | Sauvegarde **isolée** (disque débranché ou copie non modifiable) et **test de restauration** ; retirer les droits d'administrateur aux utilisateurs ; mises à jour | Quelques centaines d'euros de matériel, quelques jours de travail | 1 mois | 3 × 2 = 6 |
| S2 | Éviter | Supprimer la redirection du port 3389, accès par **VPN** avec authentification multifacteur | Temps de prestataire | 2 semaines | 3 × 1 = 3 |
| S3 | Réduire | Isoler les PC des machines dans un **réseau séparé** (pare-feu entre bureau et atelier) ; remplacement progressif des PC non maintenus | Pare-feu et temps de configuration ; remplacement étalé | 3 mois | 3 × 1 = 3 |

Mesures transverses à citer : authentification multifacteur sur la messagerie (S4), exigences de sauvegarde et de sécurité dans le contrat du prestataire de l'ERP (S5), droits par dossier (RH, Compta), changement du mot de passe du Wi-Fi et séparation invité / personnel.

**La mesure la plus rentable** : la sauvegarde isolée testée, qui coupe S1, S2 (en partie), S3 et l'initié. L'accepter comme réponse si elle est argumentée.

> [!NOTE]
> Les coûts ne sont pas des prix de marché vérifiés : accepter tout ordre de grandeur **cohérent avec le budget de 8 000 €** et justifié (temps, matériel, licence). Un plan qui dépasse le budget sans expliquer ce qui est reporté perd les points de réalisme.

**Risque accepté, exemple :** S5 (prestataire) partiellement, tant que le contrat n'est pas renégocié, avec décision écrite du dirigeant.

## Partie E – Note au dirigeant : critères

- Pas de jargon (pas de « 3389 » ni « MFA » sans explication) ;
- Trois risques, trois mesures, **un coût et un effet** pour chacune ;
- Le risque accepté et son sens sont écrits ;
- **Une décision demandée** : valider le budget, la fermeture d'un week-end, la renégociation avec le prestataire.

## Pièges fréquents

- Lister des **failles** (« Windows 7 est vulnérable ») sans scénario ni événement redouté.
- Estimer la gravité d'après la **technique** (« le serveur est important ») et non d'après la **valeur métier**.
- Mettre une vraisemblance basse « parce que ça n'est jamais arrivé » alors que le dossier cite un voisin touché.
- Proposer six mesures sans hiérarchie ni coût.
- Oublier que le **NAS branché en permanence** est chiffré avec le reste.
- Oublier le **tiers** (S5).
