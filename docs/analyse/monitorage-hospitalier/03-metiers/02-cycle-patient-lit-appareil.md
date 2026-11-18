# Métier 02 — Cycle de vie du patient, du lit et de l'appareil

**Version :** 0.1 — **Date :** 18 novembre 2026

## 1. Pourquoi ce cycle est critique

Le moniteur mesure un phénomène ; le système hospitalier doit aussi savoir **à quel patient**, **à quel moment**, **dans quel lieu de soins** et **avec quel dispositif** la donnée correspond.

Une donnée physiologique peut être techniquement correcte et pourtant devenir dangereuse si elle est associée au mauvais patient ou au mauvais séjour.

Les systèmes centraux décrits par GE permettent notamment d'admettre, de sortir et de déplacer des patients sur les moniteurs et dispositifs de télémétrie [H04]. L'étude d'utilisabilité des moniteurs inclut elle aussi les opérations d'admission, transport et sortie [H22].

## 2. Objets à distinguer

| Objet | Description |
|---|---|
| Patient | Personne prise en charge dans l'établissement. |
| Identité patient | Identifiant et informations démographiques provenant du système de référence de l'établissement. |
| Séjour / épisode de soins | Période de prise en charge dans l'établissement ou l'unité. |
| Unité | Service ou secteur de soins. |
| Chambre | Espace physique dans l'unité. |
| Lit / emplacement | Place attribuée au patient. |
| Dispositif / moniteur | Équipement technique identifié par le système et/ou le parc biomédical. |
| Capteur / module | Élément connecté au moniteur qui acquiert un paramètre. |
| Session de surveillance | Période pendant laquelle un patient est associé à un dispositif ou à un ensemble d'équipements. |
| Observation | Mesure physiologique, événement ou donnée associée à un instant et à une source. |

## 3. Cycle de vie à modéliser

### A. Préparation

- vérifier que le lit et le dispositif sont disponibles ;
- vérifier l'état technique de l'appareil ;
- préparer les capteurs et accessoires ;
- charger ou vérifier l'autonomie si le dispositif est mobile ;
- s'assurer de la configuration utilisée.

### B. Admission et association

- identifier le patient ;
- choisir le séjour et le lieu de soins ;
- associer patient, lit et dispositif ;
- vérifier que l'association est correcte ;
- connecter les capteurs ;
- vérifier les données visibles au chevet et, le cas échéant, à la centrale.

### C. Surveillance

- recevoir et afficher les mesures ;
- conserver les observations et événements ;
- suivre l'état de connexion et les défauts techniques ;
- gérer les alarmes et les changements autorisés de configuration.

### D. Transfert

- préparer la destination ;
- maintenir la surveillance avec un dispositif adapté ;
- changer l'association au lieu de soins ;
- préserver l'historique du déplacement ;
- effectuer la transmission à l'équipe d'accueil.

### E. Sortie / fin de surveillance

- terminer la session de surveillance ;
- supprimer ou clôturer l'association patient-appareil ;
- vérifier que le dispositif ne transmet plus au dossier de l'ancien patient ;
- rendre l'appareil disponible après les opérations de nettoyage et de maintenance requises ;
- conserver les données selon les règles applicables.

Cette description est un modèle de cycle de vie pour l'analyse. Les procédures réelles sont propres aux établissements et aux dispositifs.

## 4. Événements métier à distinguer

| Événement | Exemple de signification |
|---|---|
| Patient admis | Le patient entre dans un séjour ou une unité. |
| Patient affecté à un lit | L'emplacement physique devient le lieu de soins courant. |
| Moniteur associé | Une session de surveillance est ouverte. |
| Capteur connecté | Une source de mesure devient active. |
| Moniteur déconnecté | La liaison au réseau ou à la centrale est rompue ; cela ne veut pas forcément dire que la mesure locale s'arrête. |
| Patient transféré | Le patient change de chambre, d'unité ou de dispositif. |
| Session terminée | Le suivi sur ce dispositif prend fin. |
| Appareil rendu disponible | L'appareil peut être préparé pour une autre utilisation selon les procédures. |

## 5. Cas limites essentiels

- deux patients avec des noms proches ;
- association de l'appareil au mauvais patient ;
- appareil déjà associé à une autre session ;
- patient transféré mais ancienne affectation non clôturée ;
- patient temporairement hors de sa chambre ;
- moniteur changé au cours du séjour ;
- patient transféré sans données récupérées ;
- appareil sorti du service pour maintenance ;
- retour d'un appareil sans nettoyage ou vérification documentée ;
- session ancienne toujours active après la sortie du patient.

## 6. Besoins pour la simulation

- identifiant unique patient, séjour, lit et dispositif ;
- historique des associations et désassociations ;
- contrôle de cohérence des affectations ;
- gestion des transferts sans mélanger les mesures ;
- état technique du matériel ;
- session de surveillance explicite ;
- horodatage des changements ;
- journalisation des actions d'association et de sortie ;
- affichage explicite du patient et du lieu courant ;
- mécanisme de blocage ou d'alerte en cas d'association incohérente.

## 7. Sources

- **[H04]** GE HealthCare, CARESCAPE Central Station — admission, sortie et déplacement de patients : https://www.gehealthcare.com/fr-fr/products/patient-monitoring/patient-monitors/carescape-central-station
- **[H22]** Simulation-Based Usability Testing of Physiologic Monitors, 2021 — tâches d'admission, transport, sortie et configuration : https://nursing.jmir.org/2021/1/e20584
- **[H23]** Philips PIC iX — données et continuité de l'admission à la sortie : https://www.philips.fr/healthcare/patient-monitoring/enterprise-monitoring/central-patient-monitoring-systems
