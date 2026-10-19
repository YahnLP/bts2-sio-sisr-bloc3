# Corrigé – S09 : Messagerie et DNS

*Réservé à l'enseignant.*

## Vérification

Exécuté dans un laboratoire Ubuntu 24.04 de l'auteur (BIND 9.18, mise en place **sur la disposition Debian** `/etc/bind` avec `named.conf.local`) :

| Test | Résultat constaté |
|---|---|
| `named-checkzone`, `named-checkconf` | `OK` |
| `dig` MX, TXT (SPF), `_dmarc`, `sel1._domainkey` | Les enregistrements attendus |
| `dig … AXFR` sur la configuration par défaut | **Transfert de toute la zone accepté** |
| Avec `allow-transfer { none; };` | `Transfer failed` |
| `version.bind` avant | La version de BIND est annoncée |
| Avec `version "non communiquee";` | `"non communiquee"` |
| Signature (`dnssec-keygen`, `dnssec-signzone`), `dig +dnssec` | `RRSIG` présent |
| `delv` avec l'ancre construite à partir du fichier `dsset-` | `; fully validated` |
| Après modification de l'adresse dans le fichier signé | `dig` renvoie la **fausse** adresse ; `delv` : `no valid signature found` / `RRSIG failed to verify` |

**Non vérifié** : le nom du service sous Debian (`bind9`, ici `systemctl restart bind9`) et son comportement avec AppArmor (le fichier signé se lit dans `/etc/bind`, ce qui est permis par défaut) ; le comportement sous la version de BIND de la salle ; la durée de validité des signatures par défaut (environ un mois dans le laboratoire de l'auteur : la lecture du champ d'expiration du `RRSIG` le confirme, mais à confirmer sur la machine de la salle).

## Partie A

| Message | SPF | DKIM | DMARC | Verdict |
|---|---|---|---|---|
| 1 | pass | pass | pass | **Légitime** |
| 2 | pass (mais pour `promo-rapide.example`) | aucun | **fail** | **Usurpation** : `From:` = `verdier.example`, enveloppe d'un autre domaine, `Reply-To` vers un tiers, demande de virement urgent |
| 3 | **fail** | pass (aligné) | pass | **Légitime** : relais de liste de diffusion ; SPF casse au transfert, DKIM sauve |
| 4 | pass | pass | pass | **Hameçonnage par domaine ressemblant** (`verdler`) : les trois contrôles passent pour **son** domaine ; demande de changement de RIB |

**A2** : le message 4 réussit parce que l'attaquant **possède** le domaine `verdler.example` et le configure correctement. Protection manquante : **surveillance de noms de domaine proches** (enregistrement défensif des variantes), **procédure de vérification par un second canal** pour tout changement de RIB (séance S01), sensibilisation, marquage des expéditeurs externes.

## Partie B

- Enregistrement MX : `mail.lab.local` (priorité 10) ; liste des expéditeurs autorisés : le TXT SPF du domaine ; politique en cas d'échec : le TXT `_dmarc`.
- B2 : les résultats de `dig` reprennent les enregistrements de la zone.
- « Un message depuis `192.0.2.99` avec une enveloppe `@lab.local` » : **échec** SPF (réponse en C).

## Partie C

| Envoi | SPF | Pourquoi |
|---|---|---|
| `192.0.2.25` | pass | Adresse listée |
| `192.0.2.99` | **fail** | Absente de la liste, `-all` |
| Outil de newsletters non déclaré | **fail** | Absent de la liste ; il faut ajouter `include:` ; si l'outil signe en DKIM avec le domaine, DMARC peut tout de même passer |

C2 : `v=spf1 ip4:192.0.2.25 include:spf.prestataire.example -all`.

| Étape | On observe | On risque |
|---|---|---|
| `p=none` | Les rapports agrégés : qui envoie pour mon domaine | Rien, mais **aucune protection** |
| `p=quarantine` | Les messages en échec vont en spam | Mettre en spam des envois **légitimes** oubliés |
| `p=reject` | Les messages en échec sont refusés | **Bloquer** des envois légitimes si l'inventaire est incomplet |

## Partie D

- D1 : par défaut, la zone est **transférable à tous** ; l'attaquant récupère **tous les noms** (serveurs de messagerie, d'administration, postes), une **carte** du domaine. Après `allow-transfer { none; }` : `Transfer failed`.
- D2 : la version de BIND est annoncée par défaut ; masquée ensuite.

## Partie E

E2 : un `RRSIG` apparaît. E3 : `fully validated`. E4 : voir les éléments de réponse du TP.

**Limites de DNSSEC (au choix, deux)** : pas de **confidentialité** des requêtes ; ne protège pas du **détournement du compte chez le bureau d'enregistrement** (l'attaquant publie un DS valide) ; demande de l'**exploitation** (signatures qui expirent, rotation des clés) et une erreur rend le domaine injoignable ; ne sert que si le **résolveur valide** et si la zone parente publie le **DS**.

## Pièges fréquents

- Confondre l'adresse **d'enveloppe** et l'adresse **visible** : SPF « pass » ne signifie pas que le `From:` est vrai.
- Passer DMARC en `reject` d'emblée.
- Oublier l'**alignement**.
- Croire que DNSSEC chiffre.
- Laisser le **transfert de zone** ouvert (défaut).
- Éditer le **fichier signé** sans le re-signer (ici, voulu pour le test ; hors test, on **re-signe** après chaque changement).
