# Cybersécurité 01 — Sécurité des dispositifs, réseaux et centrales

**Version :** 0.1 — **Date :** 18 novembre 2026

## 1. Le périmètre à protéger

Un système de monitorage comprend plusieurs actifs :

- moniteurs de chevet et moniteurs de transport ;
- capteurs et modules ;
- transmetteurs de télémétrie ;
- stations centrales ;
- serveurs d'archivage et d'intégration ;
- passerelles vers le SIH ;
- postes de consultation ;
- comptes utilisateurs et comptes techniques ;
- réseaux et équipements d'infrastructure ;
- accès distants de maintenance ;
- configurations, certificats, clés et mises à jour ;
- journaux et sauvegardes.

Il faut protéger à la fois la confidentialité, l'intégrité, la disponibilité et la sûreté de fonctionnement.

## 2. Mesures publiquement décrites chez les fabricants

### GE CARESCAPE

Le livre blanc GE décrit :
- réseau MC isolé et non routable ;
- réseau IX distinct ;
- passerelle entre les deux réseaux ;
- routeur/pare-feu entre réseau IX et SI de l'hôpital ;
- listes de contrôle d'accès ;
- whitelisting des applications autorisées ;
- vérification d'intégrité logicielle ;
- pare-feu hôte ;
- limitation des ports nécessaires ;
- mises à jour logicielles signées ;
- processus de développement incluant analyse de risques, threat modeling, analyse d'impact sur la vie privée et analyses statiques/dynamiques ;
- limitation des données personnelles dans certains échanges et dé-identification des logs exportés ;
- journal d'audit des activités utilisateur [H40].

**Point de prudence :** ce même livre blanc précise que certaines données sur le réseau MC et certains flux HL7 vers les systèmes hospitaliers ne sont pas chiffrés. Il décrit une protection par isolement, protocoles et contrôles d'accès. La portée de ces informations dépend du produit et de la version étudiés ; il faudra demander au fabricant une documentation à jour et vérifier les flux exacts [H40].

### Philips IntelliVue / PIC iX

La documentation Philips recommande :
- réseau logique ou physique isolé ;
- VLAN dédiés ;
- interconnexion avec d'autres réseaux via pare-feu ;
- protection antivirus des plateformes classiques ;
- contrôle de l'identité des moniteurs par autorité de certification lorsque l'authentification réseau est configurée ;
- vérification de la configuration réseau avant mise en service [H41, H42].

Pour certaines versions PIC iX et Efficia, Philips a également recommandé le chiffrement BitLocker au repos, l'isolation du réseau de monitorage, et la limitation des connexions par ACL aux ports et adresses nécessaires [H54].

### Dräger Infinity

La notice française VG6.0 précise :
- segmentation par pare-feu ;
- fermeture des ports non utilisés ;
- limitation des autorisations ;
- restriction des accès tiers ;
- surveillance de l'activité réseau ;
- réseaux VLAN séparés et isolés ;
- ordinateur de maintenance dédié ;
- restriction de l'accès physique aux appareils et ports non utilisés ;
- mode Secure reposant sur PSK/MCK pour authentification, intégrité et chiffrement entre certains dispositifs compatibles ;
- collecte des logs lors d'un incident suspecté [H43].

La notice décrit aussi un mode Legacy sans authentification ni chiffrement entre les appareils. Le mode Secure est le mode préféré, mais sa disponibilité dépend des appareils et versions compatibles [H43, H44].

### Mindray BeneVision CMS

La brochure de septembre 2026 annonce :
- chiffrement TLS ;
- autorisation LDAP ;
- liste blanche logicielle ;
- stockage RAID1 ;
- QoS ;
- stratégie de backfilling des données ;
- virtualisation VMware possible ;
- collecte centralisée des informations et logs de maintenance ;
- configuration et mise à jour centralisées du firmware ;
- services distants avec autorisation [H45].

La brochure n'expose pas les détails de toutes les options cryptographiques, la gestion des certificats ou les ports utilisés. Ces points nécessiteraient les manuels d'intégration et de sécurité associés au déploiement réel.

## 3. Comparaison des mécanismes documentés

| Contrôle | GE CARESCAPE | Philips IntelliVue | Dräger Infinity | Mindray BeneVision |
|---|---|---|---|---|
| Segmentation réseau | MC / IX / SIH | LAN ou VLAN isolé | VLAN isolés | Architecture à plusieurs niveaux |
| Pare-feu / ACL | Documentés | Documentés | Recommandés | À confirmer par architecture installée |
| Authentification appareil | Mécanismes spécifiques | Certificats possibles | PSK/MCK selon appareils | Documentation de détail nécessaire |
| Chiffrement transport | Pas uniforme selon flux | À vérifier selon flux et version | Secure mode pour appareils compatibles | TLS annoncé pour CMS |
| Whitelisting | Documenté | À vérifier | À vérifier | Annoncé |
| Maintenance | VPN contrôlé / IX | Procédures fabricant | Accès tiers restreint | Service distant autorisé |
| Journalisation | Audit utilisateur | Logs produit et sécurité à confirmer | Logs et erreurs | Logs centralisés annoncés |

Ne pas interpréter une case « à vérifier » comme une absence de protection : cela signifie que la source publique consultée ne permet pas de confirmer le mécanisme pour le système et la version considérés.

## 4. Menaces à considérer

| Menace | Actif concerné | Conséquence possible |
|---|---|---|
| Compromission d'un compte soignant | Centrale, viewer, DPI | Consultation ou action non autorisée. |
| Compromission d'un compte technique | Serveurs, équipements, réseau | Modification de configuration ou accès étendu. |
| Appareil non autorisé | Réseau médical | Injection de données, perturbation ou usurpation d'identité appareil. |
| Flux intercepté ou modifié | Communication moniteur-centrale | Atteinte à la confidentialité ou à l'intégrité. |
| Déni de service / congestion | Réseau, moniteur, centrale | Retard ou absence d'informations et d'alarmes. |
| Firmware compromis | Moniteur ou passerelle | Comportement inattendu et risque sur la sûreté de fonctionnement. |
| Mise à jour mal maîtrisée | Équipement médical | Panne, incompatibilité ou interruption de surveillance. |
| Accès distant mal contrôlé | Maintenance | Compromission par prestataire ou compte oublié. |
| Rançongiciel | Serveurs, postes, annuaire | Indisponibilité des applications et données. |
| Exfiltration | SIH, partage de fichiers, archives | Fuite de données personnelles et de santé. |

## 5. Sécurité et sûreté clinique

Une défaillance cyber peut avoir plusieurs effets qui doivent être séparés :

1. **Confidentialité** : des données patient sont consultées ou divulguées.
2. **Intégrité** : une donnée ou une configuration est modifiée.
3. **Disponibilité** : le moniteur, la centrale ou l'interface n'est plus accessible.
4. **Sûreté de fonctionnement** : un professionnel ne reçoit plus les informations ou alarmes nécessaires au moment attendu.

Le risque n'est pas limité à la fuite de données. Une interruption du monitorage, une valeur fausse ou une alarme non transmise peut avoir une conséquence opérationnelle et potentiellement clinique.

## 8. Sources

- [H40] GE CARESCAPE Cybersecurity Fundamentals : https://www.gehealthcare.com/-/media/86efd534d0c94edb831beacde0c0f7eb.pdf
- [H41] Philips IntelliVue MX400/MX450/MX500/MX550 Instructions for Use : https://www.documents.philips.com/assets/Instruction%20for%20Use/20241010/7d137e87854a40a5b843b205009e75dc.pdf
- [H42] Philips Network Security Requirements : https://www.documents.philips.com/assets/Instruction%20for%20Use/20220912/198affb31877429695abaf0e00a3a901.pdf
- [H43] Dräger Infinity CentralStation Wide VG6.0 : https://www.draeger.com/Content/Documents/Products/ics-ifu-3736474-fr.pdf
- [H44] Dräger Infinity CentralStation Wide VG4.0 release notes : https://www.draeger.com/Content/Documents/Products/ics-ifusp-3720573-en.pdf
- [H45] Mindray BeneVision CMS brochure, 2026 : https://www.mindray.com/content/dam/xpace/en/resources/brochure/BeneVision_CMS.pdf
- [H64] IEC 80001-1:2021 : https://webstore.iec.ch/en/publication/34263
- [H54] NHS England — Philips PIC iX and Efficia cybersecurity vulnerabilities : https://digital.nhs.uk/cyber-alerts/2021/cc-3980
