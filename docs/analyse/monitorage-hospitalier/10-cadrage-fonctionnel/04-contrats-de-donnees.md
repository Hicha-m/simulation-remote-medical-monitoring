# Contrats de données proposés

**Date :** 18 novembre 2026  
**Statut :** contrat logique de départ ; ce n'est pas encore un schéma technique final ni une implémentation.

## 1. Faut-il un format différent pour chaque appareil ?

Pas entièrement.

Un format différent pour chaque fabricant rendrait le serveur difficile à maintenir. À l'inverse, un format unique qui efface les différences entre appareils ferait perdre des informations essentielles.

La proposition est donc :

- une **enveloppe commune** pour l'identité, la source, le contexte et les horodatages ;
- des **types de messages communs** : observation, alarme, état technique et événement de localisation ;
- des **données métier spécifiques** à chaque famille d'appareils ;
- un dictionnaire de paramètres pour les codes, unités et significations.

Le serveur peut ainsi traiter plusieurs familles d'appareils sans prétendre que leurs mesures sont identiques.

## 2. Identifiants nécessaires

| Identifiant | Rôle |
|---|---|
| patientId | Identifie le patient dans la simulation ; pseudonyme, jamais un nom réel. |
| encounterId | Identifie l'épisode d'hospitalisation ou le passage. |
| unitStayId | Identifie le passage dans une unité précise. |
| unitId | Identifie le service ou l'unité. |
| bedId | Identifie le lit ou le poste. |
| deviceId | Identifie l'appareil physique simulé. |
| monitoringSessionId | Identifie la période pendant laquelle cet appareil surveille ce patient. |
| messageId | Identifiant unique du message pour détecter les doublons. |
| sequenceNumber | Numéro de séquence par appareil/session pour analyser l'ordre des messages. |

Il faut conserver séparément patient, hospitalisation, séjour d'unité, lit, appareil et session. Ils n'ont pas le même cycle de vie.

## 3. Enveloppe commune proposée

Tous les types de messages doivent partager au minimum :

| Champ | Sens | Pourquoi |
|---|---|---|
| schemaVersion | Version du contrat. | Faire évoluer les formats sans ambiguïté. |
| messageId | Identifiant unique. | Déduplication et audit technique. |
| messageType | observation, alarm, device_status, location_event. | Router le traitement approprié. |
| deviceId | Appareil source. | Provenance des données. |
| patientId | Patient associé, si connu. | Contexte patient. |
| encounterId | Épisode hospitalier, si connu. | Éviter de mélanger deux séjours. |
| unitStayId | Séjour dans l'unité, si connu. | Gérer les transferts. |
| unitId / bedId | Localisation au moment de la mesure. | Vérifier l'affectation. |
| monitoringSessionId | Session d'association active. | Éviter les données orphelines ou croisées. |
| observedAt | Heure à laquelle la mesure ou l'événement a eu lieu sur l'appareil. | Chronologie réelle de l'événement. |
| sentAt | Heure d'émission par le simulateur. | Détecter un retard avant réception. |
| receivedAt | Heure de réception par le serveur, ajoutée côté serveur. | Mesurer la latence et les retards réseau. |
| sequenceNumber | Position dans le flux. | Détecter pertes, répétitions et désordre. |
| source | Capteur, module ou sous-système de l'appareil. | Identifier l'origine précise. |

Les dates doivent être représentées dans un format non ambigu, par exemple ISO 8601 avec fuseau explicite. Le serveur ne doit jamais remplacer l'heure d'observation par l'heure de réception.

## 4. Contrat d'une observation

Une observation contient une ou plusieurs mesures. Chaque mesure porte son propre code, sa valeur, son unité, son horodatage et son état de qualité.

Exemple illustratif, sans valeur médicale de référence :

    {
      "schemaVersion": "1.0",
      "messageId": "msg-000104",
      "messageType": "observation",
      "deviceId": "MON-ICU-01",
      "patientId": "PAT-SYN-001",
      "encounterId": "ENC-001",
      "unitStayId": "STAY-ICU-001",
      "unitId": "ICU-A",
      "bedId": "BED-01",
      "monitoringSessionId": "SESSION-001",
      "observedAt": "2026-11-18T10:14:20Z",
      "sentAt": "2026-11-18T10:14:21Z",
      "sequenceNumber": 104,
      "measurements": [
        {
          "code": "heart-rate",
          "value": 86,
          "unit": "/min",
          "quality": "valid",
          "measuredAt": "2026-11-18T10:14:20Z",
          "source": "ecg-module"
        },
        {
          "code": "spo2",
          "value": 97,
          "unit": "%",
          "quality": "valid",
          "measuredAt": "2026-11-18T10:14:20Z",
          "source": "pulse-oximeter"
        }
      ]
    }

## 5. Paramètres à cataloguer

| Code logique initial | Signification | Unité indicative |
|---|---|---|
| heart-rate | Fréquence cardiaque | /min |
| spo2 | Saturation pulsée en oxygène | % |
| respiratory-rate | Fréquence respiratoire | /min |
| nibp-systolic | Pression systolique non invasive | mm[Hg] |
| nibp-diastolic | Pression diastolique non invasive | mm[Hg] |
| nibp-mean | Pression artérielle moyenne non invasive | mm[Hg] |
| temperature | Température | Cel |
| etco2 | CO₂ télé-expiratoire | unité à confirmer selon équipement |
| ibp-systolic | Pression invasive systolique | mm[Hg] |

Ces codes sont des identifiants internes provisoires. Une future interopérabilité devra les mapper vers des terminologies reconnues telles que LOINC et UCUM, ou des ressources HL7 FHIR adaptées. Le POC n'a pas besoin de mettre en œuvre tout FHIR pour commencer.

## 6. Qualité et absence de données

Une mesure doit pouvoir être marquée comme :

- valid : mesure exploitable dans la simulation ;
- suspect : mesure reçue mais qualité incertaine ;
- invalid : mesure rejetée ou non exploitable ;
- not_measured : aucune mesure produite pour cette période ;
- sensor_off : capteur non connecté ;
- signal_lost : qualité de signal insuffisante ou perdue.

Une donnée absente ne doit jamais être transformée en zéro. Une donnée ancienne ne doit jamais être présentée comme une valeur instantanée.

La fraîcheur doit pouvoir être calculée à partir de observedAt et comparée à la cadence attendue définie par le profil de l'appareil. La durée maximale autorisée sans nouvelle mesure reste à définir.

## 7. Contrat d'une alarme

Une alarme est un événement distinct d'une mesure. Le message peut provenir directement d'un appareil ou d'un moteur de règles simulé ; cette provenance doit être visible.

Champs proposés :

| Champ | Sens |
|---|---|
| alarmId | Identifiant unique de l'alarme. |
| alarmKind | physiological ou technical. |
| origin | device ou simulation_rule. |
| parameterCode | Paramètre concerné, si applicable. |
| priority | Priorité fournie par le profil simulé ou l'appareil ; ne pas déduire une priorité clinique universelle. |
| state | active, acknowledged, resolved, cancelled. |
| startedAt | Début de l'alarme. |
| acknowledgedAt / acknowledgedBy | Acquittement et acteur. |
| resolvedAt / resolvedBy | Fin et acteur, si la résolution est opérateur-dépendante. |
| deviceId et contexte patient | Appareil, patient, séjour, unité, lit et session concernés. |
| description | Texte descriptif de l'événement. |

**Règle fondamentale : acquittement ≠ résolution.** Un professionnel peut avoir pris connaissance d'une alarme alors que la condition simulée ou le défaut technique est toujours présent.

## 8. Contrat d'état d'un appareil

Exemples d'événements techniques :

- connected / disconnected ;
- sensor_connected / sensor_disconnected ;
- low_battery ;
- poor_signal ;
- maintenance_required ;
- out_of_service ;
- patient_assigned / patient_unassigned.

Les événements d'un appareil ne remplacent pas les observations physiologiques. Une perte réseau n'est pas la même chose qu'une mesure physiologique anormale.

## 9. Données spécifiques par famille

| Famille | Payload propre | Points particuliers |
|---|---|---|
| Moniteur multiparamétrique | Tableau de mesures et événements par module. | Plusieurs paramètres, courbes éventuelles, état de chaque capteur. |
| Télémétrie portable | ECG / fréquence, signal, batterie, couverture. | Patient mobile et perte de liaison radio. |
| Moniteur de transport | Sous-ensemble des paramètres et état sur batterie. | Changement de lieu et continuité de session. |
| Respirateur | Mesures, réglages et alarmes ventilatoires. | Source indépendante du moniteur patient. |
| Pompe | Débit, volume, état et alarmes propres à la pompe. | Ne pas mélanger les données de traitement aux constantes physiologiques. |

## 10. Contrôles à appliquer côté serveur

1. Vérifier la version et la structure du message.
2. Authentifier l'appareil ou le client simulateur.
3. Vérifier que la session et l'affectation sont cohérentes.
4. Vérifier la valeur, l'unité, le code et l'horodatage.
5. Détecter doublons et numéros de séquence incohérents.
6. Conserver la provenance et les horodatages d'origine.
7. Stocker l'événement et publier la mise à jour de l'interface.
8. Marquer explicitement les données rejetées ou mises en quarantaine.

Un message qui ne peut pas être associé sans ambiguïté à un patient ne doit pas apparaître silencieusement sur la fiche d'un autre patient.

## 11. Fréquences et courbes : ne pas les figer trop tôt

Il faut distinguer :

- la fréquence d'acquisition du capteur ;
- la fréquence de calcul d'une valeur dérivée ;
- la fréquence d'émission sur le réseau ;
- la fréquence d'actualisation de l'interface ;
- la fréquence de persistance dans la base.

Ces cadences peuvent être différentes. Les jeux de données de soins intensifs montrent des résolutions variables ; HiRID publie notamment des mesures de monitorage souvent enregistrées toutes les deux minutes [H102]. Ce chiffre n'est pas une cadence universelle de moniteur et ne doit pas être repris comme exigence du POC.

Pour le premier POC, proposer des mesures numériques périodiques configurables. Les courbes ECG brutes ou les signaux continus haute fréquence seront une extension distincte.

## 12. Références de standardisation

- HL7 FHIR Observation : https://www.hl7.org/fhir/observation.html
- IHE Devices : https://profiles.ihe.net/DEV/
- ISO/IEEE 11073 : https://www.iso.org/standard/88167.html
- CI-SIS / doctrine d'interopérabilité : https://esante.gouv.fr/doctrine/interoperabilite

Ces références servent à orienter le vocabulaire et l'interopérabilité ; elles n'imposent pas une implémentation complète dans ce POC.
