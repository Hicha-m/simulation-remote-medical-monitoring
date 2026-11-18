# Architecture technique 01 — Architectures de référence des systèmes de monitorage

**Version :** 0.1 — **Date :** 18 novembre 2026

## 1. Vue fonctionnelle générale

Les documentations des constructeurs font apparaître une architecture qui comprend généralement plusieurs niveaux logiques :

1. **Dispositifs de chevet** : moniteurs physiologiques, capteurs, modules et parfois équipements périphériques.
2. **Réseau de dispositifs** : Ethernet, réseau sans fil ou infrastructure spécifique au système de monitorage.
3. **Passerelle ou couche d'intégration** : échange contrôlé entre le réseau médical et le SI hospitalier.
4. **Centrale de surveillance** : réception, affichage multi-patients, alarmes, courbes et tendances.
5. **Services annexes** : archivage, viewers distants, rapports, notifications, maintenance et gestion du parc.
6. **Systèmes hospitaliers** : admission, transfert, sortie, dossier patient informatisé et systèmes cliniques.

Cette architecture est une synthèse fonctionnelle. Les produits ne regroupent pas toujours les fonctions de la même façon et les interfaces ne sont pas nécessairement compatibles entre fabricants.

## 2. GE HealthCare CARESCAPE

Le livre blanc du fabricant décrit explicitement trois éléments :
- CARESCAPE Mission Critical (MC) Network ;
- CARESCAPE Information Exchange (IX) Network ;
- CARESCAPE Gateway.

### Réseau MC

Le réseau MC relie les moniteurs, les centrales et la passerelle. Le fabricant indique qu'il transporte les données de monitorage en temps réel : paramètres, courbes, canaux de contrôle, tendances, historiques d'alarmes et découverte des dispositifs.

### Réseau IX

Le réseau IX transporte des données non temps réel, des fichiers et certaines données de maintenance. Il sert aussi à connecter le système au réseau d'entreprise et aux applications cliniques de l'hôpital.

### CARESCAPE Gateway

La passerelle sert de pont contrôlé entre le réseau MC, le réseau IX et les applications hospitalières. Le fabricant documente :
- export de constantes vers les systèmes hospitaliers au format HL7 ;
- import des informations ADT du SIH vers les dispositifs ;
- synchronisation horaire par NTP ;
- flux de données et courbes proche temps réel au format XML pour certaines interfaces.

### Sécurité documentée

GE décrit un réseau MC isolé et non routable, séparé du réseau d'entreprise. Le réseau IX est séparé du réseau hospitalier par un routeur/pare-feu de couche 3. Des ACL, un pare-feu hôte, une liste blanche d'applications et des mises à jour signées sont également documentés.

**Point critique :** le livre blanc GE précise que certaines données de monitorage sur le réseau MC et certains flux HL7 d'interface ne sont pas chiffrés ; leur protection repose notamment sur l'isolation du réseau, le contrôle des destinations et les mécanismes propres au protocole. Cette description doit être vérifiée avec la documentation correspondant au produit, à la version et à la configuration actuellement étudiés. Elle ne permet pas de conclure que toutes les solutions GE actuelles fonctionnent de cette manière.

Sources : [H40].

## 3. Philips IntelliVue / PIC iX

La documentation Philips décrit une architecture de réseau de monitorage IntelliVue qui peut utiliser un réseau logique isolé (LAN ou VLAN) réservé aux équipements concernés.

Les documents indiquent :
- segmentation physique ou logique du trafic ;
- interconnexion des réseaux au moyen de routeurs et pare-feu ;
- protection antivirus pour les plateformes informatiques classiques ;
- possibilité d'authentification réseau des moniteurs par une autorité de certification ;
- vérification de la conformité aux spécifications réseau avec le client avant mise en service.

Les documents publics n'exposent pas l'intégralité des protocoles propriétaires et paramètres de configuration de chaque version PIC iX. Certaines informations complètes sont accessibles via la documentation produit réservée aux clients et partenaires.

Sources : [H41, H42].

## 4. Dräger Infinity

La notice technique Infinity CentralStation VG6.0 décrit plusieurs sous-réseaux :
- réseau Infinity pour les moniteurs et la centrale ;
- réseau M300 pour certains dispositifs de télémétrie ;
- réseau hospitalier, raccordé selon les règles et interfaces autorisées ;
- passerelle Infinity et outils de maintenance.

La notice donne un exemple d'architecture en étoile reposant sur des commutateurs et VLAN séparés. Elle décrit des communications multicast pour certains flux de données patient.

Le système propose un mode Legacy et un mode Secure :
- Legacy : absence d'authentification et de chiffrement entre appareils ;
- Secure : authentification mutuelle, intégrité et chiffrement entre appareils compatibles, avec PSK/MCK.

La documentation avertit que les modifications réseau peuvent affecter les performances, les alarmes et la sécurité du patient. Elle recommande notamment une QoS pour les équipements concernés.

Sources : [H43, H44].

## 5. Mindray BeneVision CMS

La brochure publiée en septembre 2026 décrit les niveaux suivants :

- **Hospital Network** : HIS, EMR, CIS et eGateway.
- **Department Network** : CentralStation, ViewStation, WorkStation, CMS Viewer, Mobile Viewer, AlarmGUARD et Archive Server.
- **Bedside Network** : moniteurs, ventilateurs, pompes, systèmes d'anesthésie, échographes et appareils périphériques.
- **Passerelles** : X-Link et BeneLink selon les interconnexions présentées.

La documentation annonce une compatibilité avec des réseaux filaires et sans fil, des dispositifs de télémétrie WMTS, des communications unicast et multicast, et une sortie IHE HL7 via eGateway.

Le fabricant annonce aussi TLS, LDAP, whitelisting, RAID1, QoS et backfilling de données. Il présente la possibilité d'une virtualisation du système sur une infrastructure VMware du client.

Ces éléments proviennent de la documentation Mindray et ne sont pas une analyse indépendante de son efficacité.

Sources : [H45].

## 6. Comparaison fonctionnelle

| Composant | GE CARESCAPE | Philips | Dräger Infinity | Mindray BeneVision |
|---|---|---|---|---|
| Moniteurs de chevet | Oui | Oui | Oui | Oui |
| Centrale multi-patients | Oui | PIC iX | Infinity CentralStation | BeneVision CMS |
| Réseau isolé / VLAN | MC dédié, IX séparé | LAN/VLAN isolé | VLAN séparés | Architecture à plusieurs niveaux |
| Passerelle SIH | CARESCAPE Gateway | Interfaces et PIC iX | Infinity Gateway | eGateway |
| ADT | Import documenté | À vérifier par système | Selon interfaces/configuration | Selon interfaces/configuration |
| HL7 | Oui, documenté | À vérifier selon solution | À vérifier selon solution | IHE HL7 via eGateway annoncé |
| Historique / archivage | Selon options et produits | PIC iX / solutions associées | Selon produits et options | Archive Server annoncé |
| Maintenance distante | Selon architecture et autorisation | Selon contrat et solution | Selon accès autorisé | Services distants sous autorisation |

Cette comparaison ne signifie pas que les quatre systèmes ont la même couverture fonctionnelle ou la même sécurité.

## 7. Architecture de référence à retenir pour les études futures

Pour modéliser les besoins sans copier un fabricant, on peut représenter les responsabilités suivantes :

- sources physiologiques ;
- acquisition et identité des dispositifs ;
- réseau clinique du monitorage ;
- centrale de réception ;
- traitement des données et événements ;
- archivage ;
- passerelle SIH ;
- interface de supervision ;
- contrôle d'accès et audit ;
- maintenance et supervision technique.

Il faudra décider ultérieurement quelles fonctions sont indispensables au scénario choisi et lesquelles peuvent être simulées ou laissées hors périmètre.

## 8. Sources

- [H40] GE HealthCare — CARESCAPE Network and Gateway, Cybersecurity Fundamentals : https://www.gehealthcare.com/-/media/86efd534d0c94edb831beacde0c0f7eb.pdf
- [H41] Philips — IntelliVue MX400/MX450/MX500/MX550 Instructions for Use, Security Information : https://www.documents.philips.com/assets/Instruction%20for%20Use/20241010/7d137e87854a40a5b843b205009e75dc.pdf
- [H42] Philips — Network security requirements for connectivity to Philips systems : https://www.documents.philips.com/assets/Instruction%20for%20Use/20220912/198affb31877429695abaf0e00a3a901.pdf
- [H43] Dräger — Infinity CentralStation Wide VG6.0, notice française : https://www.draeger.com/Content/Documents/Products/ics-ifu-3736474-fr.pdf
- [H44] Dräger — Infinity CentralStation Wide VG4.0, release notes : https://www.draeger.com/Content/Documents/Products/ics-ifusp-3720573-en.pdf
- [H45] Mindray — BeneVision Central Monitoring System brochure, 28/09/2026 : https://www.mindray.com/content/dam/xpace/en/resources/brochure/BeneVision_CMS.pdf
