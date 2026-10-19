# S08 – Sécuriser les services web : reverse proxy, en-têtes et OWASP

> [!WARNING]
> **Séance à rédiger.** Cette page donne le cadre prévu (objectifs, compétences, contenu). Le cours, le TP et l'aide-mémoire arrivent avec la phase 2.

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 2e année – bloc 3 |
| **Séance** | S08 (séance 8 sur 19) – Phase 2 |
| **Durée** | 4 heures |
| **Prérequis** | S05 |
| **Matériel** | VirtualBox : un reverse proxy et une application web de laboratoire |
| **Compétences travaillées** | B3.4 · B3.5A (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Comment exposer une application sans exposer ses faiblesses ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. Placer un reverse proxy avec TLS devant une application ;
2. Appliquer des en-têtes de sécurité et limiter les méthodes et les débits ;
3. Situer les familles de failles web les plus fréquentes (liste de l'OWASP) ;
4. Vérifier la configuration et lire les journaux d'accès.

## Contenu prévu

- Cours : reverse proxy, TLS, en-têtes de sécurité, pare-feu applicatif, familles de failles
- TP : nginx en reverse proxy HTTPS devant une application volontairement simple ; tests avec curl
- Aide-mémoire : en-têtes et directives utiles

## Évaluation

- Compte rendu avec captures d'écran datées, nommé `RENDU-B3A2-S08-NOM.pdf`.
- Bilan de compétences rempli en fin de séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)) ; le choix des compétences pour cette séance est une proposition à valider.
- **Programme :** cette séance fait partie d'un programme proposé, à valider avant rédaction.
- Liste OWASP et versions des en-têtes à relire à la source. Prolonge S12 de la première année (mini-PKI et HTTPS).

</details>
