# Modèle d'organisation, objets et relations

**Date :** 18 novembre 2026  
**Objectif :** définir une structure métier indépendante de la future technologie de base de données.

## 1. Deux hiérarchies différentes

La carte de l'hôpital doit séparer :

### Hiérarchie physique

Site → Bâtiment → Étage → Zone → Chambre / salle → Lit / poste.

Cette hiérarchie répond à la question : où se trouve le patient, le lit, l'appareil ou la centrale ?

### Hiérarchie organisationnelle

Établissement → Pôle / département → Service → Unité de soins → Équipe.

Cette hiérarchie répond à la question : de quelle organisation médicale ou opérationnelle dépend cette prise en charge ?

Une unité organisationnelle peut occuper plusieurs zones physiques. Une zone physique peut accueillir plusieurs fonctions. Il faut donc une relation entre les deux, pas les confondre dans un seul arbre.

## 2. Entités principales

| Objet | Identifiant | Attributs principaux | Rôle |
|---|---|---|---|
| Site | siteId | nom, version de carte | Établissement / campus. |
| Building | buildingId | code, nom | Bâtiment. |
| Floor | floorId | bâtiment, niveau | Niveau physique. |
| Zone | zoneId | étage, type, coordonnées de plan | Zone, secteur ou local. |
| Room | roomId | zone, numéro, type | Chambre, box, poste ou salle. |
| CareService | serviceId | nom, spécialité, pôle | Service organisationnel. |
| CareUnit | unitId | service, zone principale, profil | Unité de soins représentée par la simulation. |
| BedPosition | bedId | chambre, code, type, état | Lit, place de SSPI ou poste patient. |
| Patient | patientId | identifiant synthétique, attributs pseudonymisés | Personne suivie dans la simulation. |
| Encounter | encounterId | patient, admission, sortie, source | Séjour hospitalier. |
| UnitMovement | movementId | encounter, unité, début, fin, source | Segment de présence dans une unité. |
| PatientLocation | locationId | patient, lit, début, fin, source | Affectation physique à un lit. |
| Device | deviceId | famille, profil, état | Appareil simulé. |
| DeviceAssignment | assignmentId | appareil, patient, lit, début, fin | Historique d'association. |
| MonitoringSession | sessionId | patient, unité, appareil, début, fin | Période de surveillance. |
| Observation | observationId | session, paramètre, valeur, unité, horodatage | Mesure reçue. |
| AlarmEvent | alarmId | appareil/session, origine, priorité, cycle de vie | Événement d'alarme. |
| InfrastructureNode | nodeId | type, zone, alimentation, réseau | Centrale, switch, serveur, UPS ou groupe simulé. |

## 3. Relations cardinales

- Un site contient plusieurs bâtiments.
- Un bâtiment contient plusieurs étages.
- Un étage contient plusieurs zones.
- Une zone contient plusieurs chambres ou locaux.
- Une chambre contient une ou plusieurs positions de soin.
- Un service peut regrouper plusieurs unités.
- Une unité est rattachée à une zone principale, mais peut avoir d'autres zones associées.
- Un patient peut posséder plusieurs séjours au cours de la simulation.
- Un séjour comporte plusieurs segments de mouvement.
- Un segment de mouvement peut avoir une affectation de lit synthétique.
- Un patient peut être relié à plusieurs appareils au fil du temps.
- Un appareil ne peut avoir qu'une association patient active à un instant, sauf si son profil définit explicitement un usage différent.
- Une session de surveillance regroupe les observations et événements concernés.

## 4. Modèle relationnel logique

    Site 1 ── * Building 1 ── * Floor 1 ── * Zone
                                                    │
                                                    * Room 1 ── * BedPosition

    CareService 1 ── * CareUnit * ── * Zone

    Patient 1 ── * Encounter 1 ── * UnitMovement
       │                              │
       │                              * ── 0..1 PatientLocation ── 1 BedPosition
       │
       * ── * MonitoringSession * ── 1 Device
                                     │
                                     ├── * Observation
                                     └── * AlarmEvent

    InfrastructureNode * ── 1 Zone

Le schéma sera ajusté lors du modèle conceptuel détaillé ; il définit les relations utiles à la maquette sans imposer SQL, NoSQL ou un framework.

## 5. Historisation obligatoire

Pour les objets suivants, privilégier des relations datées plutôt qu'une simple colonne currentBed ou currentPatient :

- PatientLocation : validFrom, validTo.
- DeviceAssignment : validFrom, validTo.
- MonitoringSession : startedAt, endedAt.
- InfrastructureState : observedAt, state, sourceIncidentId.

La localisation courante est calculée à partir de l'affectation active. L'historique reste disponible après un transfert.

## 6. Identifiants source et identifiants cibles

Pour un rejeu MIMIC, conserver deux ensembles :

- identifiants source : sourceSubjectId, sourceHadmId, sourceTransferId ;
- identifiants internes de simulation : patientId, encounterId, movementId, targetUnitId, targetRoomId, targetBedId.

Cette séparation permet de rejouer le même dataset avec une autre version de la carte sans modifier les données source.

## 7. Coordonnées de plan

Chaque zone et chaque chambre peuvent disposer de coordonnées schématiques :

- x, y : position dans le dessin de l'étage ;
- width, height : taille visuelle ;
- floorId : étage ;
- shapeType : room, corridor, nurse_station, technical_room, operating_room.

Ce sont des coordonnées d'affichage relatives. Elles ne sont pas des mesures architecturales.

## 8. États séparés

Ne pas réunir tous les états dans un unique statut patient.

| Domaine | Exemples d'états |
|---|---|
| Patient / séjour | admitted, in_unit, transferred, discharged |
| Lit | free, occupied, reserved, unavailable |
| Appareil | connected, on_battery, offline, maintenance |
| Réseau | connected, degraded, unavailable |
| Surveillance | active, local_only, central_lost, ended |
| Alarme | active, acknowledged, resolved, cancelled |
| Énergie | normal, on_ups, generator_supply, failed |

Un patient peut être in_unit, son lit occupied, son moniteur on_battery, le réseau unavailable et la session local_only au même moment.

## 9. Conséquence pour la carte

La carte est une vue dérivée des objets et de leurs relations. Elle n'est pas une base de vérité autonome. Lorsqu'un transfert est enregistré, le mouvement, l'affectation physique et les associations d'appareils sont modifiés dans les entités métiers, puis le plan est mis à jour.
