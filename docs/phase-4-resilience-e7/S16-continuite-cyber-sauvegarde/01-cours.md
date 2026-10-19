# Cours – Continuité d'activité face à une cyberattaque

*BTS SIO SISR 2e année – Bloc 3 – S16*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

Dans la séance S15, l'attaquant a **supprimé les quatorze sauvegardes** avant de chiffrer le serveur. Cette séance répond à la question suivante : **comment concevoir une reprise qui survit à une attaque qui la vise ?**

---

## 1. Continuité et reprise : deux plans

| | Plan de **continuité** d'activité (PCA) | Plan de **reprise** d'activité (PRA) |
|---|---|---|
| **Objectif** | Maintenir **un service minimal** pendant l'incident | **Redémarrer** le système après l'incident |
| **Quand** | Pendant | Après |
| **Exemples** | Travailler sur papier, sur un poste de secours, une solution dégradée | Restaurer le serveur, reconstruire l'annuaire |

Les deux partent d'un **bilan d'impact sur l'activité** (BIA) : pour chaque activité, que se passe-t-il si elle s'arrête une heure, un jour, une semaine ? On le relie à l'analyse de risques de la séance S02 (valeurs métier).

### Les objectifs de reprise

| Objectif | Question | Sigle usuel |
|---|---|---|
| **Durée maximale d'interruption admissible** | Combien de temps l'activité peut-elle s'arrêter ? | DMIA |
| **Perte de données maximale admissible** | Jusqu'à quand accepte-t-on de perdre des données ? | PDMA |
| **Temps de reprise visé** | En combien de temps **vise-t-on** la remise en service ? | RTO (*recovery time objective*) |
| **Point de reprise visé** | À quel moment des données revient-on ? | RPO (*recovery point objective*) |

La DMIA et la PDMA sont des **limites métier** (qu'est-ce qui est tolérable ?). Le RTO et le RPO sont des **objectifs techniques** choisis **en dessous** de ces limites. Un RPO de 24 heures signifie : une sauvegarde par nuit, donc **jusqu'à une journée de travail perdue**.

> [!NOTE]
> Ces objectifs sont une **décision de la direction**, éclairée par le coût : un RPO de quelques minutes ou un RTO d'une heure demandent une infrastructure bien plus coûteuse qu'un RPO de 24 heures et un RTO de plusieurs jours.

---

## 2. Pourquoi une sauvegarde ordinaire ne suffit plus

Dans les attaques par rançongiciel (S01, S15), les attaquants **cherchent et détruisent les sauvegardes** avant de chiffrer. Une sauvegarde est inutile si elle est :

| Faiblesse | Exemple |
|---|---|
| **Accessible en écriture** depuis les machines attaquées | Partage réseau monté en permanence |
| **Administrée avec les mêmes comptes** que le reste | Compte administrateur de l'annuaire qui administre aussi le NAS |
| **Identifiants par défaut** | Interface d'administration du NAS (séance S13) |
| **Jamais testée** | La restauration échoue le jour J |
| **Conservée trop peu de temps** | Les copies saines sont déjà écrasées par des copies déjà chiffrées |
| **Dans le même lieu** | Incendie, inondation, vol |

---

## 3. Une sauvegarde résistante

### La règle 3-2-1 et ses prolongements

| Règle | Sens |
|---|---|
| **3** copies des données (l'original compte) | Une panne n'est pas fatale |
| **2** supports ou technologies différents | Une même défaillance ne touche pas tout |
| **1** copie **hors site** | Sinistre local |
| **+ 1 copie hors ligne ou non modifiable** | **Résiste** au rançongiciel |
| **+ 0 erreur** : restauration **vérifiée** | Une sauvegarde non testée n'existe pas |

### Rendre une copie inaccessible à l'attaquant

| Moyen | Principe | Limite |
|---|---|---|
| **Compte séparé** | La sauvegarde est écrite par un compte que la production **ne connaît pas** | Si l'attaquant est administrateur de la machine de sauvegarde, c'est perdu |
| **Sauvegarde « tirée »** (*pull*) | C'est le **serveur de sauvegarde** qui va chercher les données ; la production n'a **aucun accès** en écriture à la sauvegarde | Le serveur de sauvegarde devient une cible : à isoler et durcir |
| **Administration séparée** | Le serveur de sauvegarde n'est **pas** dans l'annuaire de production ; accès par un compte et une authentification forte dédiés (S06) | Procédures plus lourdes |
| **Copie hors ligne** | Disque ou bande **déconnectés** : seule une copie **physiquement débranchée** est certaine | Rotation manuelle, rigueur |
| **Stockage non modifiable** (écriture unique, verrouillage d'objet) | Les copies **ne peuvent pas être effacées** avant une date | Coût, configuration à soigner |
| **Versions et rétention** | Plusieurs **dates** de copie : on peut revenir **avant** la compromission | Il faut que la rétention dépasse le **temps de présence** de l'attaquant |

> [!WARNING]
> **Rétention et temps de présence.** Dans le scénario de la séance S15, l'attaquant est entré environ **52 heures** avant la détection. Si l'on ne garde que les trois dernières nuits, **toutes** les copies peuvent être postérieures à l'intrusion, donc déjà **piégées**. La rétention se choisit en fonction du **délai de détection** réaliste, pas de l'espace disque disponible.

### Une restauration propre

| Étape | Pourquoi |
|---|---|
| **Éradiquer d'abord** (séance S15) | Restaurer sur une machine encore compromise est inutile |
| Restaurer dans un **réseau isolé** | Évite de réinfecter |
| **Vérifier** les données restaurées | Échantillon, comptes, dates |
| Respecter l'**ordre de dépendance** | Annuaire et noms (DNS) avant les serveurs qui en dépendent |
| **Changer les secrets** | Mots de passe et clés présents dans les données restaurées |

---

## 4. Tester : sans test, pas de plan

| Test | Contenu | Fréquence usuelle |
|---|---|---|
| **Vérification d'intégrité** | La sauvegarde est lisible, sans corruption | Automatique, à chaque sauvegarde |
| **Restauration d'un fichier** | Retrouver un document précis | Régulier |
| **Restauration complète chronométrée** | Reconstruire un serveur et **mesurer** le temps réel | Au moins annuel |
| **Exercice de crise** | Scénario joué par l'équipe, avec communication (S15) | Annuel |

Le temps **mesuré** remplace l'estimation : un RTO annoncé de « une journée » devient **faux** si la restauration de 400 Go prend trois jours.

### Estimer un temps de reprise

`durée ≈ volume à restaurer ÷ débit réel de restauration`

Le **débit réel** dépend du disque, du réseau et du logiciel. On le **mesure** sur un échantillon, puis on **extrapole avec prudence** : un petit essai donne un débit souvent plus favorable que celui d'un gros volume. On ajoute le temps de **reconstruction** de la machine, de **vérification** et de **remise en service**.

**Test flash.** L'Atelier Verdier fait une sauvegarde chaque nuit sur un NAS branché en permanence, jamais testée. Cite **trois** faiblesses face à un rançongiciel.

<details markdown="1">
<summary>Voir la réponse</summary>

1. NAS **toujours branché** et accessible depuis le réseau (donc supprimable par l'attaquant) ; 2. **jamais testée** : on ignore si la restauration marche et combien de temps elle prend ; 3. **pas de copie hors ligne ni hors site** ni de rétention pensée par rapport au délai de détection ; on peut ajouter les **identifiants par défaut** d'administration du NAS et l'**absence d'objectifs** (RPO, RTO) validés par la direction.

</details>
