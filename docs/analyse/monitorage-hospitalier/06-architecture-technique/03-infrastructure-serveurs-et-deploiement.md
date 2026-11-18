# Architecture technique 03 — Infrastructure, serveurs et déploiement

**Version :** 0.1 — **Date :** 18 novembre 2026

## 1. Composants physiques et logiques

Une installation hospitalière peut comporter :
- moniteurs et transmetteurs patients ;
- commutateurs réseau d'accès et de distribution ;
- points d'accès radio ou récepteurs de télémétrie ;
- routeurs et pare-feu ;
- centrale de surveillance ;
- serveurs d'intégration ;
- serveurs d'archivage ;
- postes clients et écrans déportés ;
- système d'alimentation secourue selon l'infrastructure ;
- consoles de maintenance et outils biomédicaux.

La configuration exacte est propre à l'établissement.

## 2. Topologie réseau

La documentation Dräger donne un exemple de réseau en étoile construit avec des commutateurs de couche 2 ou 3. Les dispositifs sont séparés du trafic informatique général par plusieurs VLAN.

La documentation GE donne un exemple de séparation en réseau critique MC et réseau IX, avec passerelle et routeur/pare-feu.

La brochure Mindray présente une architecture à trois niveaux : réseau hospitalier, réseau du service et réseau au chevet.

Ces documents montrent qu'un système de monitorage est généralement intégré à une architecture réseau organisée ; il ne faut pas supposer que tous les composants partagent un même sous-réseau.

## 3. Serveurs et virtualisation

Mindray annonce que BeneVision CMS peut être virtualisé sur une infrastructure VMware fournie par le client et qu'il peut utiliser des mécanismes de clustering selon l'installation.

La même brochure évoque un serveur d'archivage distinct. GE documente une passerelle fournie sur matériel dédié.

**À ne pas généraliser :** tous les fabricants et tous les hôpitaux ne virtualisent pas les mêmes composants. Certains appareils nécessitent un serveur physique ou une configuration validée par le constructeur.

## 4. Stockage

Les données à stocker peuvent inclure :
- mesures et tendances ;
- courbes physiologiques ;
- événements et alarmes ;
- informations patient et mouvements ;
- association moniteur / patient / lit ;
- état et historique des appareils ;
- traces d'administration ;
- journaux de maintenance.

Il faut distinguer le stockage opérationnel des données de monitorage, l'archive clinique, le dossier patient et les logs techniques. Ils ne répondent pas aux mêmes besoins, n'ont pas nécessairement la même durée de conservation et ne sont pas forcément gérés par le même système.

Le RAID1 annoncé par Mindray est un mécanisme de tolérance à la panne de disque. Il ne remplace ni une sauvegarde indépendante, ni une réplication adaptée, ni un test de restauration.

## 5. Continuité et disponibilité

Les questions d'infrastructure à examiner :
- alimentation électrique secourue ;
- redondance des chemins réseau ;
- redondance des serveurs ;
- comportement de la centrale en cas de perte de serveur ;
- conservation locale des mesures ;
- rattrapage après coupure ;
- bascule vers un moniteur local ;
- procédure en cas d'indisponibilité de la centrale ;
- reprise après incident de cybersécurité.

Les mécanismes exacts doivent être confirmés avec la documentation du produit et l'établissement.

## 6. Maintenance et accès distant

La maintenance implique souvent plusieurs acteurs : biomédical, DSI, fournisseur et mainteneur.

Les points à documenter :
- compte nominatif et durée d'accès ;
- validation par l'établissement ;
- accès VPN ou bastion ;
- authentification multi-facteur ;
- fenêtres de maintenance autorisées ;
- journalisation des opérations ;
- contrôle des transferts de fichiers ;
- procédure de retrait des accès après intervention ;
- validation des mises à jour ;
- gestion des vulnérabilités et versions en fin de support.

Le CERT Santé a documenté plusieurs incidents français liés à des accès VPN ou comptes prestataires compromis. L'accès distant est donc un sujet majeur de maîtrise des risques [H49, H50].

## 7. Sources

- [H43] Dräger Infinity CentralStation VG6.0 : https://www.draeger.com/Content/Documents/Products/ics-ifu-3736474-fr.pdf
- [H40] GE CARESCAPE Cybersecurity Fundamentals : https://www.gehealthcare.com/-/media/86efd534d0c94edb831beacde0c0f7eb.pdf
- [H45] Mindray BeneVision CMS brochure : https://www.mindray.com/content/dam/xpace/en/resources/brochure/BeneVision_CMS.pdf
- [H49] CERT Santé — groupement hospitalier, compromission après fuite d'identifiants VPN : https://cyberveille.esante.gouv.fr/retours-d-experience/un-groupement-hospitalier-victime-dune-compromission-de-son-si-suite-une-fuite
- [H50] CERT Santé — CHD Stell, compromission et rançongiciel, 2025 : https://cyberveille.esante.gouv.fr/retours-d-experience/compromission-du-si-et-ransomware-au-chd-stell-2025-10-14
