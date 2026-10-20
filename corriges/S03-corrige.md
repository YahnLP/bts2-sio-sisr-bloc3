# Corrigé – S03 : Référentiels, normes et PSSI

*Réservé à l'enseignant. La séance se corrige par la **cohérence** (risque → famille → mesure → référence relue) et la **vérifiabilité** des ​règles, non par une liste unique.*

## Partie A

| Référentiel | Attendu |
|---|---|
| Guide d'hygiène de l'ANSSI | Publié par l'ANSSI ; gratuit ; **non certifiable** ; relever la version de la page de garde |
| ISO/IEC 27001 | Publié par l'ISO et la commission électrotechnique internationale ; **norme payante** ; **certifiable** |
| CIS Controls | Publié par le Center for Internet Security ; gratuit à lire (inscription possible) ; **non certifiable** |

Éléments de A2 : voir les ​blocs « Éléments de réponse » du TP.

## Partie B – Réponses de référence

| Risque | Famille | Mesure précise | 
|---|---|---|
| S1 | Sauvegarder et reprendre ; Sécuriser les postes | Sauvegarde hors ligne ou non modifiable, restauration testée chaque trimestre ; retrait des droits d'administrateur ; mises à jour mensuelles |
| S2 | Gérer le nomadisme ; ​Authentifier | Fermeture du port 3389 ; accès par VPN avec second facteur |
| S3 | Sécuriser le réseau | Réseau séparé pour les PC des machines, flux autorisés listés ; plan de ​remplacement |
| S4 | Authentifier et contrôler les accès | Authentification multifacteur sur toutes les boîtes ; sensibilisation à l'hameçonnage |
| S5 | (Hors référentiel général) | Clauses du contrat : fréquence de sauvegarde, durée de restauration, notification d'incident, réversibilité |

**La référence relue est vérifiée à la source** : l'étudiant cite le guide et l'intitulé qu'il lit. Un ​numéro de mesure absent du guide, ou recopié de mémoire, est refusé.

**Exemple d'exigence vérifiable** : « L'administrateur teste le premier lundi de chaque trimestre la restauration d'un dossier du serveur depuis le NAS et envoie le résultat à la direction. »

Sûreté (B2) : accepter par exemple incendie (poussière de bois, local technique proche de l'atelier : détection, extinction adaptée, copie de sauvegarde hors du bâtiment) et coupure ou surtension électrique sur les machines et le serveur (onduleur, ​parafoudre). Les événements doivent être ​plausibles pour une menuiserie.

**B2** : risque sur mesure = le **tiers** (prestataire de l'ERP) ; les référentiels généraux traitent peu le ​contrat avec un fournisseur précis : exiger des garanties écrites.

## Partie C – Critères d'une bonne PSSI d'une page

- Les **cinq rubriques** sont présentes ; la direction est nommée comme signataire ;
- Au moins **quatre principes** en lien avec les risques de S02 ;
- Des **règles vérifiables** (qui, quoi, quand), pas des vœux (« les mots de passe sont solides » → « douze caractères minimum, gestionnaire de mots de passe fourni ») ;
- Une **révision** ​datée ;
- Une organisation réaliste pour une structure de 35 personnes (le responsable administratif et le prestataire, pas un « comité de sécurité »).

**C2 – exemple**

| Niveau | Rédaction |
|---|---|
| ​Politique | Les données sont sauvegardées et la restauration est testée régulièrement. |
| Procédure | Chaque trimestre, l'administrateur restaure un dossier test depuis le NAS, note la durée et le résultat, et en rend compte à la direction. |
| Mode opératoire | 1. Choisir un dossier. 2. Le restaurer dans un emplacement de test. 3. Comparer avec l'original. 4. ​Noter la durée. 5. Archiver le compte rendu. |

## Partie D – Critères de la charte

- Langage simple, une demi-page ;
- Cinq règles concrètes ;
- **Contrôle et finalité annoncés** (journalisation, filtrage) : l'employeur informe les salariés ;
- Qui prévenir et sous quel ​délai en cas d'incident.

Opposabilité : renvoyer à la séance S04 et à un juriste ; ne pas trancher en séance.

## Pièges fréquents

- Citer un **numéro de mesure** non relu.
- Confondre **27001** (certifiable) et **27002** (guide).
- Écrire une politique de **vœux** non vérifiables.
- Oublier la **signature de la direction**.
- Copier une PSSI de grande entreprise (comités, classification) inadaptée à 35 personnes.

## Vérification

Chiffres et intitulés des référentiels (nombre de mesures, version en vigueur de ​chaque guide) **non repris dans le cours à dessein** : à relire à la source par l'enseignant avant d'en parler. Le cours ne cite que la nature de chaque ​document (certifiable ou non, publié par qui), à confirmer sur les sites des éditeurs.
