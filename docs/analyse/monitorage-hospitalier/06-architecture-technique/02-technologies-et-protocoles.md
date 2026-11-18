# Architecture technique 02 — Technologies et protocoles

**Version :** 0.1 — **Date :** 18 novembre 2026

## 1. Réseau physique et liaison

| Technologie | Usage possible dans un système de monitorage | Preuve / limite |
|---|---|---|
| Ethernet IEEE 802.3 | Connexion des moniteurs, centrales, serveurs et passerelles. | GE et Dräger décrivent des réseaux Ethernet/LAN. |
| Wi-Fi IEEE 802.11 | Connexion de certains dispositifs mobiles et points d'accès. | Les notices Dräger donnent des exigences réseau sans fil selon produit ; le Wi-Fi n'est pas universel. |
| WMTS | Bande et infrastructure radio utilisées par certains systèmes de télémétrie médicale. | Mindray annonce la compatibilité WMTS pour BeneVision CMS ; à vérifier pour chaque région et produit. |
| Multicast IP | Distribution de flux à plusieurs destinataires, notamment dans certains réseaux de monitorage. | Dräger documente l'usage de multicast sur Infinity ; cela impose une configuration réseau adaptée. |
| Unicast IP | Échange point à point entre dispositifs, stations et serveurs. | Mindray annonce la prise en charge unicast et multicast. |
| VLAN | Séparation logique des réseaux et des flux. | Philips, GE et Dräger documentent des réseaux dédiés ou VLAN séparés. |

Ne pas présumer que Bluetooth, Wi-Fi grand public, MQTT ou Internet sont utilisés par tous les moniteurs hospitaliers. Les interfaces sont spécifiques aux familles de produits et à leurs configurations.

## 2. Protocoles et standards d'échange

| Protocole / standard | Rôle possible | Ce que cela ne garantit pas |
|---|---|---|
| TCP/IP | Transport de données entre composants. | Ne définit pas le modèle métier des mesures. |
| HL7 v2 | Échange d'observations et d'informations patient, notamment vers les systèmes hospitaliers. | Ne décrit pas tous les flux bruts propriétaires entre moniteur et centrale. |
| IHE PCD | Profils d'interopérabilité pour dispositifs de soins et systèmes d'information. | La compatibilité dépend des profils effectivement implémentés. |
| XML | Encodage de certains flux d'intégration. | Ce n'est pas un protocole réseau à lui seul. |
| NTP | Synchronisation des horloges. | Ne garantit pas la qualité de l'horodatage du capteur lui-même. |
| TLS | Chiffrement et authentification de connexions selon version et configuration. | Ne chiffre pas automatiquement tous les flux d'un produit. |
| LDAP | Référentiel ou protocole d'annuaire pour l'identité et les autorisations. | Ne remplace pas une politique d'habilitation complète. |
| PSK/MCK | Clés partagées pour établir une communication sécurisée entre appareils compatibles Dräger. | La gestion et la rotation des clés sont des points à organiser. |
| Protocoles propriétaires | Échanges temps réel entre équipements d'un fabricant. | Interopérabilité et documentation peuvent être restreintes. |

## 3. Temps réel et flux de monitorage

Les appareils peuvent transmettre :
- valeurs numériques ponctuelles ou périodiques ;
- courbes physiologiques échantillonnées ;
- événements et alarmes ;
- tendances et données historiques ;
- états techniques (connexion, batterie, capteur, défaut) ;
- informations de contexte (patient, lit, appareil, session).

Les débits et fréquences d'émission diffèrent fortement entre une mesure de pression artérielle périodique, une fréquence cardiaque actualisée régulièrement et un signal ECG échantillonné.

Il faut séparer les objectifs de transport :
- continuité et faible latence pour les données de surveillance ;
- fiabilité et rattrapage pour les données historiques ;
- sécurité et disponibilité pour les alarmes ;
- cohérence pour les identités et mouvements patients.

## 4. Réseau et qualité de service

La QoS peut aider à préserver la qualité de transmission de certains flux lorsque le réseau est congestionné. Mindray la cite pour BeneVision CMS et Dräger l'exige pour certains équipements M300/M300+.

La QoS ne remplace pas :
- une segmentation correcte ;
- la capacité suffisante des commutateurs et liens ;
- la surveillance des pertes et retards ;
- la redondance quand elle est nécessaire ;
- des tests de charge et de panne.

Le multicast doit être pris en charge et contrôlé par l'infrastructure réseau ; il ne doit pas être activé ou propagé sans règles explicites.

## 5. Points techniques à documenter pour chaque flux

Pour chaque type d'équipement, collecter :
- source et destination ;
- protocole et port ;
- unicast ou multicast ;
- flux entrant ou sortant ;
- données transportées ;
- fréquence et débit ;
- exigences de latence ;
- chiffrement et authentification ;
- identité de l'équipement ;
- comportement en cas de perte ;
- reprise après coupure ;
- mécanismes de synchronisation ;
- logs et métriques disponibles.

Ces détails sont parfois dans des manuels de réseau et des documents réservés aux intégrateurs. Ils ne doivent être collectés que via les canaux autorisés du fabricant ou de l'établissement.

## 6. Sources

- [H40] GE CARESCAPE Cybersecurity Fundamentals : https://www.gehealthcare.com/-/media/86efd534d0c94edb831beacde0c0f7eb.pdf
- [H41] Philips IntelliVue MX400/MX450/MX500/MX550 Instructions for Use : https://www.documents.philips.com/assets/Instruction%20for%20Use/20241010/7d137e87854a40a5b843b205009e75dc.pdf
- [H43] Dräger Infinity CentralStation VG6.0 : https://www.draeger.com/Content/Documents/Products/ics-ifu-3736474-fr.pdf
- [H45] Mindray BeneVision CMS brochure : https://www.mindray.com/content/dam/xpace/en/resources/brochure/BeneVision_CMS.pdf
- [H46] IHE Devices Technical Framework, Rev. 11.0 : https://profiles.ihe.net/DEV/index.html
