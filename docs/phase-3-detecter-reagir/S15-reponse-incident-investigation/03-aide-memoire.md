# Aide-mémoire – Le premier quart d'heure et l'investigation

*BTS SIO SISR 2e année – Bloc 3 – S15*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## Les phases

Préparer → détecter et qualifier → **contenir** → éradiquer → reprendre → retour d'expérience.

**Contenir avant d'éradiquer** : ne pas réinstaller avant d'avoir compris et conservé.

## Check-list du premier quart d'heure

- [ ] Noter l'**heure**, photographier l'écran
- [ ] **Isoler du réseau** la machine touchée
- [ ] **Ne rien effacer**, ne pas « nettoyer »
- [ ] **Alerter** la chaîne prévue (direction, prestataire)
- [ ] **Ne pas utiliser** la machine ni les comptes touchés
- [ ] **Préserver** journaux et sauvegardes encore saines
- [ ] Changer les mots de passe concernés **depuis une machine saine**
- [ ] **Décider avec la personne compétente** : éteindre ou laisser allumé

| Éteindre | Laisser allumé |
|---|---|
| Arrête le chiffrement en cours | Conserve la mémoire (traces, parfois la clé) |
| Perd la mémoire | Le chiffrement peut continuer |

## Preuves

| Règle | Commande ou geste |
|---|---|
| Copier, ne pas toucher l'original | `cp originaux/* copies/` |
| Empreinte | `sha256sum fichier > empreintes.sha256` |
| Vérifier | `sha256sum -c empreintes.sha256` (**dans le bon dossier**) |
| Conserver l'empreinte **à part** | Support séparé |
| Tracer | Fiche : qui, quoi, quand, où, accès |

Ordre de volatilité : mémoire et connexions → fichiers temporaires → disque → **journaux distants** → sauvegardes.

## Analyser des journaux

| Besoin | Commande |
|---|---|
| Échecs par adresse | `grep echec log \| grep -o 'source=[^ ]*' \| sort \| uniq -c \| sort -rn` |
| Une adresse | `grep 'source=203.0.113.77' log` |
| Fusionner par heure | `cat a.log b.log c.log \| sort` |
| Compter | `grep -c motif log` |
| Première, dernière ligne | `head -1`, `tail -1` |

## Chronologie

| Heure | Source | Événement | Interprétation | Certitude |
|---|---|---|---|---|

On distingue **établi** (cité d'une ligne) et **supposé**.

## Questions à poser

Entrée ? · Progression ? · Actions de l'attaquant ? · **Vol** avant chiffrement ? · Périmètre (touché, menacé, sain) ? · Attaquant encore présent ?

## Obligations

| Sujet | Repère |
|---|---|
| Données personnelles | Notification **CNIL sous 72 h** après connaissance, si risque ; information des personnes si risque élevé (S04) |
| Plainte, assurance | Conserver les preuves, respecter les délais du contrat |
| Rançon | Recommandation des autorités : **ne pas payer** |

## Communication

| Public | Contenu |
|---|---|
| Direction | Faits, hypothèses, décisions, **prochain point** daté |
| Salariés | Quoi faire, quoi ne pas faire |
| Externes | Validé par la direction, **sans supposition** |

## Reprendre

Sauvegarde **saine** ? Cause **fermée** ? Mots de passe **changés** ? Surveillance **renforcée** ? Retour d'expérience daté.
