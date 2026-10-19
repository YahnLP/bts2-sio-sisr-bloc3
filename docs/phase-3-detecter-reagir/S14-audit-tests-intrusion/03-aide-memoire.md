# Aide-mémoire – Audit : cadre et rapport

*BTS SIO SISR 2e année – Bloc 3 – S14*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## Avant de commencer (check-list)

- [ ] **Autorisation écrite**, signée par une personne **habilitée**
- [ ] **Périmètre précis** (adresses, applications, locaux) : ce qui n'est pas écrit est **hors périmètre**
- [ ] **Accord des tiers** (hébergeur, prestataire) pour leurs systèmes
- [ ] **Dates et horaires**
- [ ] **Interdits** (saturation, destruction, copie de données…)
- [ ] **Contact d'urgence** joignable
- [ ] **Confidentialité** et sort des preuves
- [ ] Responsabilités en cas d'incident

## Types d'audit

| Type | Question |
|---|---|
| Organisationnel | Les règles sont-elles appliquées ? |
| Configuration | Conforme à la référence ? |
| Architecture | Découpage et flux cohérents ? |
| Vulnérabilités | Quelles failles connues ? |
| Test d'intrusion | Un attaquant réaliste atteint-il un objectif ? |
| Ingénierie sociale | Le personnel résiste-t-il ? |

## La démarche

Cadrer → collecter → analyser → **qualifier** → rédiger → restituer → suivre.

## Niveaux de preuve

| Niveau | Décision |
|---|---|
| Solide (capture datée, extrait) | Constat **ferme** |
| Partielle (déclaratif, incomplète) | Constat **à confirmer** |
| Insuffisante (rumeur) | **Exclu** tant que non vérifié |

## Fiche de constat

Identifiant · description factuelle · **preuve** · risque (valeur métier) · gravité et facilité · **recommandation précise** · priorité.

| Mauvais | Bon |
|---|---|
| « Améliorer la sécurité » | « Fermer la redirection du port 3389 et ouvrir un accès par VPN avec authentification forte » |

## Structure du rapport

1. **Résumé managérial** (une page, sans jargon)
2. Contexte, méthode, **limites**
3. Constats (une fiche chacun)
4. Plan d'action priorisé
5. Annexes (preuves)

## Restituer en cinq minutes

Ce qui va bien · trois risques · décisions à prendre · coût (temps, argent) · quand on revérifie.

## Imprévus

| Situation | Réflexe |
|---|---|
| Danger immédiat | **Prévenir tout de suite** le contact d'urgence |
| Données personnelles | **Ne pas copier**, minimiser, signaler sans reproduire |
| Activité illicite hors sujet | S'arrêter, prévenir le donneur d'ordre, avis juridique |
| Système hors périmètre accessible | **Ne pas y toucher**, signaler |
