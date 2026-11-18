# Besoins 02 — Scénarios et indicateurs à simuler

**Version :** 0.1 — **Date :** 18 novembre 2026  
**Statut :** bibliothèque initiale de scénarios ; aucun résultat clinique visé.

## 1. Pourquoi des scénarios reproductibles ?

Un POC réaliste doit pouvoir reproduire plus qu'une suite de constantes régulières. Les sources terrain décrivent des incidents d'association, de connexion, de transport, de configuration, d'alarmes et de communication.

Les scénarios doivent pouvoir être lancés plusieurs fois dans les mêmes conditions, avec un résultat observable et des journaux permettant de comprendre ce qui s'est passé.

## 2. Scénarios d'admission et d'affectation

| ID | Situation | Comportement à observer | Critère technique |
|---|---|---|---|
| SCN-ID-01 | Admission d'un patient | Création du contexte de suivi et de l'affectation. | Identité et session cohérentes. |
| SCN-ID-02 | Appareil déjà utilisé | Tentative d'association à une nouvelle session. | Détecter le conflit. |
| SCN-ID-03 | Patient transféré | Changement de lit et d'unité. | Pas de mélange de données entre patients. |
| SCN-ID-04 | Appareil remplacé | Fin de session ancienne et création de la nouvelle. | Historique des associations conservé. |
| SCN-ID-05 | Sortie du patient | Clôture de la session. | Plus aucune mesure attribuée à l'ancien séjour. |
| SCN-ID-06 | Mauvaise association | Appareil associé au mauvais patient. | Anomalie détectée ou processus de correction tracé. |

## 3. Scénarios de transmission et de réseau

| ID | Situation | Comportement à observer | Indicateur |
|---|---|---|---|
| SCN-NET-01 | Flux nominal | Mesures envoyées à intervalle contrôlé. | Latence et débit. |
| SCN-NET-02 | Plusieurs appareils simultanés | Arrivées concurrentes. | Débit en pic, erreurs, latence. |
| SCN-NET-03 | Déconnexion | Client perd le réseau. | Détection et durée d'indisponibilité. |
| SCN-NET-04 | Reconnexion | Le client revient sur le réseau. | Délai de reprise et rattrapage. |
| SCN-NET-05 | Message dupliqué | Même identifiant transmis deux fois. | Déduplication ou identification du doublon. |
| SCN-NET-06 | Message tardif | Une mesure ancienne arrive après une mesure plus récente. | Conservation des deux horodatages et ordre logique. |
| SCN-NET-07 | Horloge décalée | Horodatage client incohérent. | Détection et signalement. |
| SCN-NET-08 | Perte partielle | Certains paramètres arrivent, d'autres non. | Complétude des mesures. |

## 4. Scénarios de moniteur et de capteurs

| ID | Situation | Comportement à observer |
|---|---|---|
| SCN-DEV-01 | Électrode ECG retirée | Alarme technique et statut du signal. |
| SCN-DEV-02 | Capteur SpO₂ absent | Donnée indisponible et état du capteur. |
| SCN-DEV-03 | Batterie faible | Indication et événement technique. |
| SCN-DEV-04 | Moniteur hors ligne | Dernière donnée et état de connexion. |
| SCN-DEV-05 | Moniteur réinitialisé | Reprise de session et cohérence du contexte. |
| SCN-DEV-06 | Défaut d'un module | Paramètre correspondant indisponible sans fausse valeur. |

## 5. Scénarios d'alarmes et de traitement

| ID | Situation | Comportement à observer |
|---|---|---|
| SCN-ALM-01 | Condition d'alarme simulée | Création, affichage et traçabilité. |
| SCN-ALM-02 | Alarme technique | Distinction par rapport à une alarme physiologique. |
| SCN-ALM-03 | Alarme reportée à la centrale | Délai et résultat du report. |
| SCN-ALM-04 | Alarme non acquittée | Maintien en attente et signalement selon règles de démo. |
| SCN-ALM-05 | Acquittement | Auteur, heure et commentaire éventuel enregistrés. |
| SCN-ALM-06 | Transfert à une autre équipe | Nouvelle responsabilité visible et historique conservé. |
| SCN-ALM-07 | Plusieurs alarmes simultanées | Lisibilité, ordre de présentation et charge. |
| SCN-ALM-08 | Alarme répétitive | Statistiques de répétition et durée. |
| SCN-ALM-09 | Report d'alarme indisponible | Défaillance détectée et état visible. |
| SCN-ALM-10 | Relève d'équipe | Liste des événements non clos et transfert de responsabilité. |

Les conditions de déclenchement du POC sont des événements synthétiques ou des règles de démonstration. Elles ne doivent pas utiliser de seuils cliniques inventés ni être présentées comme des protocoles de soins.

## 6. Scénarios spécifiques aux soins critiques

| ID | Situation | Source de réalisme |
|---|---|---|
| SCN-ICU-01 | Vérification de centrale au changement d'équipe. | HAS attend une vérification à chaque prise de poste [H02]. |
| SCN-ICU-02 | Report d'alarme vers centrale et répétiteur. | Organisation décrite par la HAS [H02]. |
| SCN-ICU-03 | Absence de professionnel prévu près de la centrale. | Organisation de présence décrite par la HAS [H02]. |
| SCN-ICU-04 | Alarme provenant d'un appareil critique connecté. | Centrales pouvant intégrer ventilateurs et autres appareils [H08]. |

## 7. Scénarios spécifiques au transport

La HAS a documenté plusieurs événements indésirables graves lors de transports intrahospitaliers de patients de soins critiques [H19] :

- **SCN-TR-01 — Réserve d'oxygène épuisée :** une bouteille se vide pendant le transport ; l'affichage du ventilateur change mais les alarmes ne sont pas perçues.
- **SCN-TR-02 — Changement de système de monitorage :** lors de l'arrivée en imagerie, un changement de matériel prend du temps et crée une rupture potentielle dans le suivi.
- **SCN-TR-03 — Circuit mal monté :** un circuit de ventilation est incorrectement assemblé lors du transport.
- **SCN-TR-04 — Mauvaise reprise à l'arrivée :** le patient est raccordé à un ventilateur à l'arrêt après le retour dans l'unité.
- **SCN-TR-05 — Changement d'équipe pendant le transport :** l'équipe qui accueille le patient n'est pas celle qui l'a préparé au départ.

Le POC ne doit pas simuler les conséquences médicales réelles de ces incidents ; il peut reproduire la séquence technique et les défauts de coordination, les événements de surveillance et les vérifications manquantes.

## 8. Indicateurs techniques

| Indicateur | Définition à retenir |
|---|---|
| Latence mesure → réception | Heure de réception serveur moins heure de mesure client. |
| Latence réception → persistance | Temps entre acceptation du message et confirmation de stockage. |
| Latence réception → interface | Temps entre arrivée serveur et affichage visible sur la vue. |
| Débit | Messages ou mesures traités par seconde. |
| Pic de débit | Débit maximal sur une fenêtre de mesure définie. |
| Taux de perte | Messages attendus non retrouvés. |
| Taux de doublons | Messages répétés / messages transmis. |
| Taux de rejet | Messages refusés lors de la validation technique. |
| Temps de détection de panne | Délai entre la panne injectée et sa détection. |
| Temps de reprise | Délai entre rétablissement et retour à un état nominal. |
| Fraîcheur affichée | Écart entre l'heure courante et la dernière mesure reçue. |
| Complétude de l'historique | Proportion des mesures attendues retrouvées. |

Aucun objectif chiffré n'est défini dans cette version : les cibles doivent être choisies à partir du cas d'usage et mesurées sur une configuration documentée.

## 9. Indicateurs de workflow

- temps entre détection et affichage à la centrale ;
- temps entre affichage et prise de connaissance ;
- temps de traitement et clôture ;
- nombre d'événements ouverts par équipe ;
- nombre d'événements réassignés ;
- nombre d'événements non acquittés ;
- alarmes répétitives par appareil ;
- indisponibilités de source par période ;
- changements de configuration ;
- vérifications réalisées lors des admissions et relèves.

Ces indicateurs évaluent le workflow simulé et ne doivent pas servir à juger la performance individuelle d'un professionnel réel.

## 10. Méthode de test

Pour chaque scénario :
1. fixer l'état initial ;
2. fixer les identités patient, lit et appareil ;
3. générer un jeu de données synthétiques ;
4. injecter l'événement à un instant contrôlé ;
5. enregistrer les horodatages à chaque étape ;
6. observer serveur, stockage et interface ;
7. contrôler les journaux ;
8. répéter dans les mêmes conditions ;
9. comparer les résultats ;
10. consigner la configuration et les limites.

## 11. Sources

- **[H02]** HAS, Surveillance des patients en soins critiques : https://www.has-sante.fr/jcms/p_3511526/fr/flash-securite-patient-surveillance-des-patients-en-service-de-soins-critiques-une-veille-sans-faille-pour-qu-aucun-patient-ne-defaille
- **[H08]** Dräger, Infinity CentralStation Wide : https://www.draeger.com/fr_fr/Products/Infinity-CentralStation
- **[H19]** HAS, Transport intrahospitalier des patients de soins critiques : https://www.has-sante.fr/upload/docs/application/pdf/2024-03/flash_secrutie_patient_-transport_intrahospitalier_des_patients_de_soins_critiques_..._le_transport_lui_aussi_est_critique.pdf
- **[H22]** Simulation-Based Usability Testing of Physiologic Monitors : https://nursing.jmir.org/2021/1/e20584
