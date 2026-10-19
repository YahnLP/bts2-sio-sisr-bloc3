# Bloc 3 · SISR – BTS SIO 2e année

Cours, TP et aide-mémoire du **bloc 3 (cybersécurité des services informatiques)** du BTS SIO option SISR, 2e année : **19 séances de 4 h** pour 19 semaines d'alternance réparties sur l'année. Auteur : Yahn LE PRETTRE - Formateur – licence CC BY-NC-SA 4.0.

**Site (GitHub Pages) :** <https://yahnlp.github.io/bts2-sio-sisr-bloc3/>

Ce dépôt fait suite à [`bts1-sio-sisr-bloc3`](https://github.com/YahnLP/bts1-sio-sisr-bloc3). La séance S01 révise l'essentiel de la première année ; les séances suivantes approfondissent la justification, le déploiement et la supervision des mesures, et préparent l'épreuve écrite E7.

## Contenu

| Dossier | Contenu |
|---|---|
| [`docs/phase-1-reprendre-cadrer`](docs/phase-1-reprendre-cadrer/README.md) | S01 à S05 : révisions, analyse de risques, référentiels et PSSI, cadre juridique, filtrage avancé |
| [`docs/phase-2-securiser-acces-services`](docs/phase-2-securiser-acces-services/README.md) | S06 à S10 : annuaire sécurisé, 802.1X et Wi-Fi, services web, messagerie et DNS, durcissement |
| [`docs/phase-3-detecter-reagir`](docs/phase-3-detecter-reagir/README.md) | S11 à S15 : journaux et SIEM, détection d'intrusion, vulnérabilités, audit, réponse à incident |
| [`docs/phase-4-resilience-e7`](docs/phase-4-resilience-e7/README.md) | S16 à S19 : continuité face à une cyberattaque, sécurité de projet, méthode E7, épreuve blanche |
| [`docs/ressources`](docs/ressources/README.md) | Référentiel, épreuve E7, outils, glossaire, licences |
| [`corriges`](corriges/) | Corrigés **réservés à l'enseignant** (non publiés sur le site, mais visibles dans ce dépôt) |
| [`tools`](tools/CONVENTIONS.md) | Conventions de rédaction du site |

## Avancement

| Séances | État |
|---|---|
| S01 à S05 (phase 1) | Rédigées (fiche, cours, TP, aide-mémoire, corrigé) |
| S06 à S10 (phase 2) | Rédigées (fiche, cours, TP, aide-mémoire, corrigé) |
| S11 à S15 (phase 3) | Rédigées (fiche, cours, TP, aide-mémoire, corrigé) |
| S16 à S19 (phase 4) | Rédigées (fiche, cours, TP, aide-mémoire, corrigé) |

## Cadre d'examen

Toutes les épreuves sont **ponctuelles** (pas de contrôle en cours de formation). Ce bloc prépare l'épreuve **E7** (cybersécurité des services informatiques : écrit de 4 h, coefficient 4). Voir [`docs/ressources/epreuve-e7.md`](docs/ressources/epreuve-e7.md).

## Travailler en local

```bash
pip install -r requirements.txt
mkdocs serve        # http://127.0.0.1:8000
mkdocs build --strict
```

## Licence

Contenus : **CC BY-NC-SA 4.0**. Détail : [`docs/ressources/licences.md`](docs/ressources/licences.md).
