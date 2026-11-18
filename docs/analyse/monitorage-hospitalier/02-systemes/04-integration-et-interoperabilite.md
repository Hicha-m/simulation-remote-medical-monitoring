# Système 04 — Intégration, interopérabilité et systèmes hospitaliers

**Version :** 0.1 — **Date :** 18 novembre 2026

## 1. Pourquoi un système de monitorage est rarement isolé

Un équipement de monitorage peut devoir échanger des informations avec :
- le système d'identification et de gestion des mouvements des patients (admission, sortie, transfert) ;
- le dossier patient informatisé (DPI) ;
- le système d'information clinique ;
- le système d'information de cardiologie et de gestion ECG ;
- les centrales et moniteurs de différents fabricants ;
- les ventilateurs, appareils d'anesthésie et pompes selon le niveau d'intégration ;
- des systèmes de gestion des alarmes ;
- des systèmes de supervision et de gestion du parc biomédical.

L'intégration permet de limiter les doubles saisies et de rendre les données disponibles aux bons professionnels. Elle introduit cependant des dépendances supplémentaires : réseau, identités, correspondance des données, versions, habilitations et disponibilité des interfaces.

## 2. Exemples d'intégration documentés par les fabricants

| Fabricant / système | Fonction décrite | Source |
|---|---|---|
| Philips PIC iX | Collecte de données de monitorage et transmission au DPI, y compris pendant le transport, selon la solution décrite. | [H23] |
| GE CARESCAPE Gateway | Transfert bidirectionnel de données entre le système d'information hospitalier / clinique et les moniteurs, via HL7 selon la documentation GE. | [H24] |
| Mindray eGateway | Communication avec systèmes ADT/EMR et export centralisé HL7 IHE-PCD mentionné dans la présentation de BeneVision CMS. | [H05] |
| GE CARESCAPE Central Station | Import de données de systèmes ECG GE et export de rapports vers des destinations telles que DME, imprimante et serveur SFTP, selon options. | [H04] |
| Dräger Infinity CentralStation | Intégration de données de surveillance provenant de moniteurs, ventilateurs et dispositifs d'anesthésie Dräger. | [H08] |

Ce tableau décrit des capacités annoncées par les fournisseurs et leurs propres écosystèmes. Il ne démontre pas une interopérabilité universelle entre tous les équipements de tous les fabricants.

## 3. Standards et profils à connaître

### HL7 v2

Famille de messages largement utilisée pour les échanges entre systèmes hospitaliers, notamment autour des mouvements des patients et de la transmission d'observations. Plusieurs fabricants annoncent des interfaces HL7 dans leurs solutions.

### IHE Patient Care Devices (PCD)

Le domaine IHE Devices publie des profils pour l'échange entre dispositifs de soins et systèmes d'information. Au 18 novembre 2026, la page officielle IHE affiche la révision 11.0 du cadre technique, publiée le 12 novembre 2026, avec notamment :
- Device Enterprise Communication (DEC) ;
- Alert Communication Management (ACM) ;
- Implantable Device – Cardiac Observation (IDCO) ;
- Infusion Pump Event Communication (IPEC) ;
- Medical Equipment Management Device Management Communication (MEMDMC) ;
- Medical Equipment Management Location Services (MEMLS) [H25].

Ces profils décrivent des scénarios et transactions d'intégration. Leur présence dans un standard ne signifie pas que deux produits sont automatiquement compatibles : il faut vérifier les profils et options effectivement implémentés et testés.

### IEEE 11073

La famille IEEE 11073 couvre des aspects de communication et de modélisation des dispositifs médicaux au point de soin. IEEE présente notamment un projet de révision du profil 11073-20702 pour les communications de dispositifs médicaux distribués par services Web, dont le statut affiché en 2026 est un projet actif [H26].

Il faut vérifier précisément les parties de la famille 11073 et leur statut avant de les retenir pour une implémentation.

### SDC — Service-oriented Device Connectivity

Philips indique promouvoir une approche SDC pour permettre à des dispositifs compatibles de partager leurs données et services dans un environnement connecté. Cette mention doit être étudiée comme une piste d'interopérabilité avancée ; elle ne doit pas être confondue avec une compatibilité générique de tous les moniteurs [H23].

### FHIR

FHIR est pertinent pour représenter et échanger des informations de santé structurées (patient, appareil, observations, provenance, etc.). Il ne faut pas supposer qu'une API FHIR est à elle seule un protocole de diffusion temps réel de toutes les courbes physiologiques.

## 4. Identité et contexte : la partie souvent sous-estimée

Une mesure doit être rattachée sans ambiguïté :
- à un patient ;
- à un appareil ou capteur ;
- à une localisation de soins, si elle est pertinente ;
- à un paramètre et une unité ;
- à une heure de production ;
- à une heure de réception ;
- à une session ou période de surveillance ;
- à une source et une configuration.

Les systèmes d'admission, de sortie et de transfert sont donc très importants. Une mesure techniquement valide mais rattachée au mauvais patient reste un problème majeur de qualité.

## 5. Besoins métiers candidats

- rapprocher les identités patient, lit et dispositif ;
- importer les mouvements du patient ;
- transmettre des observations vers le DPI ;
- éviter les doubles saisies ;
- distinguer la valeur brute, la valeur calculée et la valeur documentée ;
- assurer la provenance et la traçabilité ;
- gérer les interfaces indisponibles et les reprises ;
- contrôler les droits d'accès aux données échangées ;
- gérer les changements de format et de version ;
- identifier les dispositifs et capacités réellement compatibles.

## 6. Sources

- **[H04]** GE HealthCare, CARESCAPE Central Station : https://www.gehealthcare.com/fr-fr/products/patient-monitoring/patient-monitors/carescape-central-station
- **[H05]** Mindray France, BeneVision CMS : https://www.mindray.com/fr/products/patient-monitoring/centralized-monitoring/benevision-cms
- **[H08]** Dräger, Infinity CentralStation : https://www.draeger.com/fr_fr/Products/Infinity-CentralStation
- **[H23]** Philips France, systèmes de monitorage centralisé : https://www.philips.fr/healthcare/patient-monitoring/enterprise-monitoring/central-patient-monitoring-systems
- **[H24]** GE HealthCare, connectivité et réseau de monitorage : https://www.gehealthcare.com/fr-fr/products/patient-monitoring/networking
- **[H25]** IHE Devices Domain, Technical Framework Rev. 11.0 : https://profiles.ihe.net/DEV/index.html
- **[H26]** IEEE 11073-20702 project page : https://standards.ieee.org/ieee/11073-20702/12539/
- **[H27]** HL7 FHIR R5 — Observation : https://www.hl7.org/fhir/observation.html

## 7. Questions ouvertes

- Quel standard est effectivement utilisé par les systèmes du service que nous voulons modéliser ?
- Les événements sont-ils transmis à une centrale propriétaire ou à un serveur d'intégration ?
- Les courbes brutes et les valeurs numériques empruntent-elles les mêmes interfaces ?
- Le DPI reçoit-il toutes les mesures ou seulement des snapshots / résultats sélectionnés ?
- Comment la gestion ADT est-elle connectée aux moniteurs ?
- Quelles interfaces de test ou environnements de démonstration sont accessibles ?
