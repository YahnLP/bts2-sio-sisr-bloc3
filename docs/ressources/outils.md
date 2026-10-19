# Outils et laboratoires

| Outil | Usage dans la formation | Accès |
|---|---|---|
| **VirtualBox** | Machines virtuelles Debian, Windows et Windows Server : l'**environnement de laboratoire** de tous les TP de sécurité. | Installé sur les postes de la salle |
| **OpenSSH** | Administration à distance, durcissement de la configuration (S01, S06). | Paquet Debian |
| **nftables** | Pare-feu à politique restrictive, journalisation, zones (S01, S05). | Paquet Debian |
| **Wireshark** | Capture et analyse de trames : voir ce qui circule en clair et ce qui est chiffré. | Installé sur les postes de la salle |
| **Nmap** | Découverte et vérification de ports et de services (S05, S13, S14), uniquement sur le laboratoire. | Paquet Debian |
| **FreeRADIUS** | Authentification des équipements et du Wi-Fi d'entreprise (S07). | Paquet Debian |
| **nginx** | Reverse proxy, TLS, en-têtes de sécurité (S08). | Paquet Debian |
| **Lynis, OpenSCAP** | Audit local de conformité et de durcissement (S10). | Paquets Debian |
| **Wazuh, rsyslog** | Journalisation centralisée et supervision de sécurité (S11). | Machines virtuelles du laboratoire |
| **Suricata** | Détection d'intrusion (S12). | Paquet Debian |
| **Scanneur de vulnérabilités** | Découverte et tri des vulnérabilités du laboratoire (S13). Outil à valider. | Machine virtuelle du laboratoire |
| **restic** | Sauvegarde chiffrée et isolée (S16). | Paquet Debian |
| **Simulateur réseau, Cisco Packet Tracer** | Comprendre la segmentation et le filtrage. Ils servent à comprendre et s'entraîner. | [Simulateur du bloc 2](https://yahnlp.github.io/bts1-sio-sisr-bloc2/simulateur/simulateur-reseau.html) · compte Networking Academy pour Packet Tracer |

> [!NOTE]
> Les outils des séances S06 à S19 sont ceux **prévus** : le choix définitif est validé séance par séance avant rédaction.

## Règles de laboratoire

> [!WARNING]
> - Les **identifiants communs d'un TP** (par exemple `etudiant` / `Lab-2026`) sont des **identifiants de laboratoire** : ils sont identiques pour toute la classe afin que chacun fasse la même chose dans un environnement contrôlé. **Ils ne sont jamais repris** dans une réalisation, un dossier d'épreuve ou un vrai système.
> - **On n'attaque que le laboratoire.** Les outils d'audit (Nmap, scanners de vulnérabilités) ne se lancent que sur les machines virtuelles du TP, isolées du réseau de l'établissement.
> - **Le laboratoire sert à comprendre et s'entraîner.** L'épreuve E7 est écrite : ce que tu manipules ici te donne les faits et les exemples dont tu argumenteras à l'écrit.
