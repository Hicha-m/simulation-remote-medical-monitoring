# Système 02 — Centrales de surveillance et systèmes centralisés

**Version :** 0.1 — **Date :** 18 novembre 2026

## 1. Fonction d'une centrale de surveillance

Une centrale de surveillance (central station / central monitoring system) rassemble des informations issues de plusieurs moniteurs ou transmetteurs et les présente sur un ou plusieurs postes de travail.

Elle peut fournir :
- une vue multi-patients ;
- les paramètres numériques et courbes de chaque patient ;
- l'affichage d'une vue détaillée pour un patient sélectionné ;
- les alarmes et événements ;
- l'historique et les tendances ;
- le suivi de la télémétrie sans fil ;
- dans certains écosystèmes, des données provenant de ventilateurs, stations d'anesthésie ou autres équipements ;
- l'accès à des postes déportés et, selon les offres, à des terminaux mobiles ;
- une interface avec le dossier patient ou le système d'information.

Une centrale ne remplace pas automatiquement l'équipement au chevet : elle collecte, présente et diffuse une vue centrale selon les rôles et l'architecture installée.

## 2. Exemples de systèmes actuellement documentés sur le marché

Les capacités listées ci-dessous sont des caractéristiques annoncées par les fabricants sur leurs pages produit. Elles varient avec la version, les options, les licences et la configuration ; elles ne doivent pas être traitées comme des capacités garanties dans tout déploiement.

### Philips — Patient Information Center iX (PIC iX)

La page française présente PIC iX comme une solution de monitorage centralisé conçue pour collecter des données patient et les transmettre au dossier patient informatisé, de l'admission à la sortie, y compris pendant le transport. Philips met également en avant la visibilité distante pour les soignants, les alarmes et l'intégration avec des dispositifs de plusieurs fabricants via sa plateforme d'intégration [H23].

**À étudier :** collecte et continuité de données, intégration DPI, notification d'événements et vue centralisée.

### GE HealthCare — CARESCAPE Central Station

La documentation française décrit une surveillance centralisée de patients connectés à des moniteurs GE ou à des émetteurs de télémétrie. La page indique :
- jusqu'à 4 courbes en temps réel par patient pour un maximum de 16 patients sur la vue décrite ;
- jusqu'à 9 courbes pour un patient sélectionné ;
- affichage ECG, SpO₂, respiration, pression invasive et CO₂ ;
- gestion d'admission, sortie et déplacement des patients ;
- réglage à distance de paramètres de moniteur et de télémétrie ;
- alarmes secondaires des moniteurs de chevet et alarmes primaires pour les émetteurs de télémétrie ;
- historique Full Disclosure annoncé jusqu'à 144 heures selon options et modes [H04].

**À étudier :** gestion patient/lit, configuration distante, historique et différence entre alarmes primaires et secondaires.

### Dräger — Infinity CentralStation Wide

Dräger annonce :
- centralisation des données, alarmes et historiques en temps réel ;
- surveillance des alarmes de 32 ou 64 patients selon configuration ;
- archivage des enregistrements complets et événements sur 120 heures ;
- affichage des données et alarmes venant de ventilateurs et appareils d'anesthésie Dräger [H08].

**À étudier :** surveillance multi-patients, intégration d'équipements de soins et consultation rétrospective.

### Mindray — BeneVision CMS

La page française présente :
- réseau de surveillance évolutif ;
- connexion de moniteurs câblés, sans fil et émetteurs de télémétrie ;
- jusqu'à 1 200 appareils sur le réseau de l'établissement annoncé ;
- jusqu'à 64 lits gérés par station dans la configuration décrite ;
- affichage simultané des informations de 16 patients ;
- historique de courbes annoncé jusqu'à 240 heures ;
- base historique de patients sortis ;
- communication bidirectionnelle et intégration avec ADT/EMR par eGateway, avec export HL7 IHE-PCD mentionné [H05].

**À étudier :** architecture distribuée, multi-postes, communication bidirectionnelle, gestion des historiques et intégration.

## 3. Comparaison synthétique

| Solution | Éléments distinctifs annoncés | Questions à approfondir |
|---|---|---|
| Philips PIC iX | Intégration DPI, vues distantes, collecte patient et continuité durant le transport. | Quelles données sont réellement transférées, à quelle fréquence et avec quelle granularité ? |
| GE CARESCAPE Central Station | Vue multi-patients, contrôle distant, gestion admissions/transferts, historiques, télémétrie. | Comment les événements sont-ils priorisés et transmis aux soignants ? |
| Dräger Infinity CentralStation | Vues 32/64 patients, historique, données de ventilateurs et d'anesthésie. | Quelles interfaces et quelles limites entre dispositifs Dräger et tiers ? |
| Mindray BeneVision CMS | Réseau distribué à grande échelle, 1 200 appareils annoncés, multi-postes, eGateway. | Quelles exigences réseau, segmentation et gestion de la disponibilité ? |

## 4. Ce qu'il ne faut pas déduire

- Ces chiffres ne constituent pas une comparaison de performance indépendante.
- Un maximum de dispositifs annoncé ne dit rien à lui seul de la latence réelle sous charge.
- Une compatibilité annoncée ne signifie pas que toutes les combinaisons d'appareils sont interopérables.
- Une fonction d'affichage central ne dit pas qui est responsable de surveiller l'écran.
- Une transmission vers le DPI n'implique pas nécessairement une écriture de toutes les courbes brutes.
- Les pages produits ne prouvent pas qu'un hôpital français particulier utilise le système.

## 5. Besoins métiers que la centrale révèle

- tableau multi-patients et navigation vers un patient ;
- affectation patient / lit / moniteur ;
- admission, transfert et sortie ;
- affichage temps réel des mesures et courbes ;
- historique des tendances et événements ;
- centralisation et diffusion des alarmes ;
- gestion de l'état de connexion des appareils ;
- affichages ou postes de travail adaptés aux rôles ;
- report d'alarmes dans plusieurs zones ;
- intégration avec les équipements et logiciels environnants ;
- traçabilité des réglages, changements et actions.

## 6. Sources

- **[H04]** GE HealthCare, CARESCAPE Central Station : https://www.gehealthcare.com/fr-fr/products/patient-monitoring/patient-monitors/carescape-central-station
- **[H05]** Mindray France, BeneVision CMS : https://www.mindray.com/fr/products/patient-monitoring/centralized-monitoring/benevision-cms
- **[H08]** Dräger, Infinity CentralStation Wide : https://www.draeger.com/fr_fr/Products/Infinity-CentralStation
- **[H23]** Philips France, systèmes de monitorage patient centralisé : https://www.philips.fr/healthcare/patient-monitoring/enterprise-monitoring/central-patient-monitoring-systems
