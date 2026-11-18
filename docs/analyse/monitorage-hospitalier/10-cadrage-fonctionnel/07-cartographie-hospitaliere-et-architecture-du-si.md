# Cartographie hospitalière et architecture du système d'information

**Date :** 18 novembre 2026  
**Statut :** architecture fonctionnelle de référence proposée pour le POC. Le plan décrit ci-dessous est une maquette fictive et configurable, pas le plan d'un hôpital réel.

## 1. Oui : le POC doit posséder une carte de l'hôpital

La carte doit permettre de répondre à quatre questions :

1. Où se trouve le patient ?
2. Dans quelle unité, chambre et sur quel lit est-il installé ?
3. Quel appareil lui est associé et où se trouve cet appareil ?
4. Par quel poste ou quelle centrale ses données et alarmes sont-elles surveillées ?

Ce ne doit pas être une carte GPS. C'est un plan d'établissement composé de bâtiments, d'étages, d'unités, de chambres et de lits, avec des informations opérationnelles superposées.

Les plans publics d'hôpitaux servent souvent à orienter les visiteurs. Ils ne donnent pas nécessairement la disposition opérationnelle des lits, les réseaux médicaux, les locaux techniques ou les affectations courantes. Le POC doit donc utiliser une maquette propre à la simulation.

## 2. Ne pas confondre organisation médicale et géographie

Un service est une unité organisationnelle et médicale. Une chambre ou un lit est un emplacement physique.

Ces deux structures doivent être séparées dans le modèle. Un service peut occuper plusieurs zones physiques ; un même bâtiment peut héberger plusieurs services ; un patient peut changer de lit sans changer de séjour ; un appareil peut être déplacé d'un lit à l'autre.

### Structure physique

- Site hospitalier
- Bâtiment
- Étage
- Zone ou secteur
- Chambre ou emplacement
- Lit ou poste de surveillance

### Structure organisationnelle

- Établissement
- Pôle ou département
- Service
- Unité de soins
- Équipe ou secteur fonctionnel

### Objets opérationnels placés sur la carte

- Patient actuellement affecté à un lit
- Moniteur ou appareil mobile
- Poste de soins
- Centrale de surveillance
- Récepteur de télémétrie
- Passerelle ou baie réseau, si connue
- Tableau électrique ou local technique, selon le niveau de détail autorisé

Un lit n'est pas un patient. Une chambre n'est pas un service. Un moniteur n'est pas attaché définitivement à un lit.

## 3. Exemple de maquette hospitalière pour la démonstration

La structure suivante sert uniquement à créer un environnement cohérent et testable. Les capacités, nombres de lits et relations physiques sont des paramètres de démonstration, pas des standards hospitaliers.

### Site HOSP-01 — Hôpital de démonstration

| Bâtiment / étage | Zone de soins | Fonction dans les scénarios | Éléments à afficher |
|---|---|---|---|
| Bâtiment A — RDC | Urgences et SAUV | Admissions, triage, premiers monitorages, orientation. | Box, places SAUV, appareils d'accueil, poste infirmier. |
| Bâtiment A — RDC | Imagerie | Destination de transfert d'un patient hospitalisé. | Salles d'examen et zone d'attente ; pas nécessairement un flux continu. |
| Bâtiment A — R+1 | Réanimation adulte | Service de référence provisoire du POC. | Chambres, lits monitorés, poste de soins, centrale et appareils. |
| Bâtiment A — R+1 | USC | Étape de transfert après soins critiques ou surveillance renforcée. | Lits, moniteurs selon profil, poste de soins. |
| Bâtiment A — R+2 | Cardiologie / télémétrie | Patients mobiles suivis par transmetteurs. | Chambres, lits, zones de déplacement, récepteur de télémétrie et centrale. |
| Bâtiment A — R+2 | Médecine conventionnelle | Mesures ponctuelles et éventuelle dégradation. | Chambres, lits, postes de mesure ; tous les lits ne sont pas supposés monitorés en continu. |
| Bâtiment B — RDC | Bloc opératoire et SSPI | Parcours chirurgical et réveil. | Salles opératoires, postes de SSPI, zone de transfert. |
| Zone technique | Informatique et énergie | Hébergement des composants locaux et secours électriques. | Baie réseau, serveurs ou équipements de communication, UPS, tableau de secours, groupe électrogène. |

La carte doit permettre d'afficher seulement les bâtiments et unités, puis de descendre jusqu'à une chambre et un lit. Il n'est pas nécessaire de dessiner chaque couloir au premier POC.

## 4. Ce que l'utilisateur doit voir

### Vue 1 — Hôpital entier

- Liste des bâtiments et niveaux.
- Nombre de lits occupés, libres, bloqués ou en transfert par unité.
- État général des centrales et de la connectivité.
- Alertes techniques et zones affectées par un incident.

### Vue 2 — Étage

- Plan schématique des unités et secteurs.
- Chambres, postes de soins, centrales et zones techniques.
- Nombre et état des lits de chaque unité.

### Vue 3 — Service

- Tous les lits de l'unité.
- Patient pseudonymisé et identifiant de séjour.
- Appareil associé.
- État de la session de surveillance.
- Dernière mesure reçue et ancienneté de cette mesure.
- Alarmes actives et états techniques.

### Vue 4 — Chambre et lit

- Détail de l'affectation patient / séjour / lit / appareil.
- Historique des changements d'appareil et de lit.
- Mesures, courbes éventuelles, alarmes et événements techniques.
- Historique de l'état électrique et réseau simulé.

La carte doit utiliser des libellés textuels en plus des couleurs. Une chambre ne doit jamais être interprétée comme surveillée simplement parce qu'elle est coloriée en vert.

## 5. États visuels proposés

### État du lit

- Libre
- Occupé
- Réservé
- En préparation
- Indisponible

### État du dispositif

- Connecté
- Fonctionnement sur batterie
- Liaison centrale perdue
- Capteur déconnecté
- Hors service
- Maintenance

### État de la surveillance

- Session active et données fraîches
- Session active mais données périmées
- Surveillance locale sans report central
- Session terminée
- État inconnu

Il faut dissocier l'état du lit, celui de l'appareil et celui de la session de surveillance. Un patient peut être toujours présent alors que son appareil ou la centrale est indisponible.

## 6. Modèle logique à prévoir

| Entité | Champs importants | Rôle |
|---|---|---|
| Site | siteId, nom, adresse fictive | Regroupe un établissement ou un campus. |
| Building | buildingId, siteId, nom | Décrit un bâtiment. |
| Floor | floorId, buildingId, niveau | Décrit un étage. |
| PhysicalZone | zoneId, floorId, type, coordonnées | Décrit une zone ou un secteur physique. |
| Room | roomId, zoneId, numéro, type | Décrit une chambre, un box ou une salle. |
| Bed | bedId, roomId, numéro, status | Représente un lit ou poste de surveillance. |
| CareService | serviceId, nom, spécialité | Décrit le service organisationnel. |
| CareUnit | unitId, serviceId, zoneId | Relie une unité à son organisation et à sa zone habituelle. |
| PatientLocation | patientId, encounterId, bedId, startAt, endAt | Historise la localisation du patient. |
| Device | deviceId, family, modelProfile, status | Référence un appareil simulé. |
| DeviceAssignment | deviceId, patientId, bedId, sessionId, startAt, endAt | Historise son association. |
| MonitoringSession | sessionId, patientId, unitId, startAt, endAt | Décrit une période de surveillance. |

Les coordonnées x/y servent à dessiner le plan schématique. Elles ne sont pas des coordonnées GPS et ne prétendent pas reproduire les distances ou dimensions architecturales exactes.

## 7. Comment le système informatique est-il organisé ?

La réponse réaliste est : **un système hybride, avec des équipements et des centrales proches des services, reliés à une infrastructure et à des services informatiques partagés au niveau de l'établissement.**

Il n'est généralement ni constitué d'une application totalement isolée par service, ni d'un seul serveur central qui ferait tout.

### Niveau A — Au chevet et dans le service

- Moniteurs de chevet.
- Transmetteurs de télémétrie.
- Respirateurs et autres dispositifs connectés.
- Points d'accès Wi-Fi, commutateurs et récepteurs radio.
- Centrale ou poste de surveillance de l'unité.
- Poste de soins et éventuels répétiteurs.

La centrale du service reçoit les données de plusieurs patients. Une architecture fabricant documente des réseaux de dispositifs au chevet et un réseau de centrales, avec des connexions Ethernet, Wi-Fi et télémétriques ; plusieurs centrales peuvent être interconnectées [H117].

### Niveau B — Réseau partagé de l'établissement

- Cœur de réseau et commutateurs de distribution.
- Réseaux filaires et Wi-Fi.
- Segmentation logique des équipements médicaux et des autres systèmes.
- Pare-feu et filtrage entre zones.
- Passerelles d'intégration des dispositifs.
- Supervision et journalisation des équipements réseau.

L'ANSM décrivait en 2019 que le report d'alarmes sur centrale était le modèle le plus répandu dans les unités de soins intensifs et réanimations étudiées ; le réseau était souvent intégré au réseau hospitalier, avec une séparation virtuelle plutôt que physique. Le rapport signalait qu'une intervention réseau pouvait perturber le système d'alarme. C'est une observation historique, pas une règle universelle en 2026 [H95].

### Niveau C — Systèmes partagés de l'hôpital

- Identité et annuaire des patients.
- Admission, mouvements et sorties (ADT).
- Dossier patient informatisé (DPI).
- Gestion des utilisateurs et des habilitations.
- Moteur d'interopérabilité et passerelles.
- Bases de données des applications.
- Sauvegardes, supervision et cybersécurité.
- Archivage des données selon les applications.

Les données des dispositifs peuvent être agrégées puis partagées avec le DPI, les systèmes cliniques, des outils de visualisation ou des archives. La documentation Philips Medical Device Integration illustre ce type de chaîne d'intégration ; c'est une architecture fournisseur, pas un schéma imposé à tous les hôpitaux [H118].

### Niveau D — Échelle du GHT

Dans un groupement hospitalier de territoire, certaines fonctions du système d'information peuvent converger ou être mutualisées sous la responsabilité de l'établissement support. Cela ne signifie pas que les équipements de chaque unité disparaissent ou que tous les établissements ont exactement le même système [H119].

## 8. Schéma logique du système

    DISPOSITIFS DU SERVICE
    Moniteurs / télémétrie / respirateurs / autres appareils
                       |
                       v
    RÉSEAU DES DISPOSITIFS
    Ethernet / Wi-Fi / récepteur radio / segmentation
                       |
                       v
    CENTRALE LOCALE DU SERVICE
    Vue multi-patients / alarmes / postes de visualisation
                       |
                       v
    PASSERELLE D'INTÉGRATION ET RÉSEAU HOSPITALIER
                       |
              +--------+---------+
              |                  |
              v                  v
       DPI / ADT / SIH       Archivage / analyse
       Patient / séjour     Données / historiques
              |
              v
       Annuaire / droits / identité / audit
              |
              v
       Services partagés de l'établissement ou du GHT

Le chemin de l'alarme locale et le chemin d'intégration vers le DPI ne doivent pas être confondus. Une défaillance d'une application de dossier patient ne doit pas être supposée identique à une défaillance de la centrale de surveillance. Chaque chaîne doit avoir ses états, ses dépendances et ses procédures dégradées.

## 9. Conséquence pour notre POC

Le POC doit simuler :

1. Plusieurs services et étages dans une même carte.
2. Plusieurs lits et chambres, avec des patients qui changent de place.
3. Un poste ou une centrale par unité de référence.
4. Une infrastructure réseau partagée.
5. Des composants informatiques communs : identité, mouvements, serveur de données et journal d'audit.
6. Des pannes ciblées : un appareil, une unité, un étage ou le réseau général.

Le système doit donc être organisé à la fois par service pour l'affichage et les workflows locaux, et par établissement pour les identités, les données partagées, la sécurité, l'intégration et la supervision.

## Sources

- [H95] ANSM — Gestion des alarmes des dispositifs médicaux, septembre 2019.
- [H114] Ministère de la Santé — Guide d'aide à la préparation au volet numérique du Plan blanc, 2023.
- [H117] Mindray — BeneVision Central Monitoring System, Operator's Manual, réseau des dispositifs et centrales.
- [H118] Philips — Medical Device Integration.
- [H119] Ministère de la Santé — Système d'information convergent du GHT.
