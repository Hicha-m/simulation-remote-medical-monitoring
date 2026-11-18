# Système 03 — Télémétrie hospitalière sans fil

**Version :** 0.1 — **Date :** 18 novembre 2026

## 1. Définition opérationnelle

Dans cette étude, la télémétrie hospitalière décrit les équipements portés par le patient qui envoient des données physiologiques sans fil vers une infrastructure de monitorage pendant que le patient peut se déplacer dans une zone de couverture définie.

Elle est différente :
- d'un moniteur fixe relié par câbles au chevet ;
- d'un appareil de mesures ponctuelles utilisé pendant une tournée ;
- de la télésurveillance médicale à domicile.

## 2. Chaîne technique habituelle

La chaîne peut comporter :

1. un patient équipé d'un transmetteur ou d'un moniteur compact ;
2. des électrodes, capteurs ou modules physiologiques ;
3. une liaison radio entre le patient et les points d'accès / récepteurs ;
4. une infrastructure réseau ;
5. une centrale ou un serveur de monitorage ;
6. un poste central ou des postes de consultation déportés ;
7. une organisation de professionnels chargés de surveiller et de traiter les alertes.

La technologie radio, l'architecture réseau et les comportements de reconnexion dépendent du fabricant et de l'établissement. Ne pas supposer que le système fonctionne nécessairement en Wi-Fi standard ou en Bluetooth.

## 3. Exemple actuel documenté : Mindray BeneVision TM80

Le TM80 est présenté sur le site français de Mindray comme un moniteur de télémétrie portable pour patients mobiles à l'hôpital. Le fabricant décrit ECG, respiration, SpO₂ et PNI selon configuration, une communication bidirectionnelle avec la centrale, une alerte en cas de sortie de la zone réseau et une autonomie annoncée jusqu'à 40 heures [H09].

Ces fonctions sont utiles pour comprendre les états de fonctionnement à simuler :
- transmetteur associé ;
- transmission active ;
- perte de couverture ;
- retour dans une zone couverte ;
- batterie faible ;
- alarme remontée ;
- patient en déplacement ;
- dispositif localisé ou manquant.

## 4. Problématiques métier spécifiques

| ID | Besoin | Description |
|---|---|---|
| TELE-01 | Localiser le patient ou l'équipement dans les limites prévues par le système. | Retrouver un patient mobile ou un transmetteur égaré. |
| TELE-02 | Surveiller la couverture réseau. | Distinguer une situation physiologique d'une interruption technique. |
| TELE-03 | Gérer la batterie. | Éviter qu'un transmetteur s'arrête sans que le service ne le sache. |
| TELE-04 | Associer le transmetteur à un patient. | Une transmission ne doit pas être attribuée au mauvais dossier. |
| TELE-05 | Gérer les zones autorisées. | Signaler une sortie de la zone de couverture configurée. |
| TELE-06 | Avertir le personnel responsable. | L'alerte doit atteindre la bonne équipe. |
| TELE-07 | Continuer le suivi lors de déplacements. | Maintenir la surveillance sans immobiliser le patient au lit. |
| TELE-08 | Reprendre le suivi après une perte radio. | Gérer la reconnexion, le trou de données et l'historique. |
| TELE-09 | Nettoyer, recharger et réaffecter les appareils. | Le cycle de vie du matériel fait partie de l'exploitation. |
| TELE-10 | Définir l'observateur et le répondant. | La centrale et l'infirmier au chevet n'ont pas nécessairement la même responsabilité. |

## 5. Organisation humaine : variation entre établissements

Une publication sur les moniteurs ECG et les « monitor watchers » décrit plusieurs modèles : observation par les infirmiers eux-mêmes, surveillance par des personnels dédiés, ou organisation hybride. Elle souligne la nécessité d'une communication en boucle fermée entre la personne qui observe l'écran et celle qui prend en charge le patient [H11].

Une publication de 2026 portant sur la formation des techniciens de surveillance physiologique en unité centrale décrit également le rôle d'observateurs centralisés, les besoins de formation, le risque d'alarmes non actionnables et l'importance de procédures d'escalade [H14].

Ces descriptions sont issues de la littérature anglophone et ne doivent pas être considérées comme l'organisation de tous les hôpitaux français.

## 6. Scénarios de test à prévoir

- patient associé à un transmetteur ;
- transmetteur non associé ou mal associé ;
- sortie de la zone couverte ;
- perte de liaison de plusieurs secondes ou minutes ;
- reconnexion avec ou sans rattrapage de données ;
- batterie faible ;
- appareil retrouvé après perte ;
- alarmes simultanées de plusieurs patients ;
- transfert de patient dans une autre unité ;
- changement d'équipe ;
- absence d'observateur ou de répondant désigné.

## 7. Sources

- **[H09]** Mindray France, BeneVision TM80 : https://www.mindray.com/fr/products/patient-monitoring/telemetry-monitoring/benevision-tm80
- **[H11]** Monitor-watcher use, nurses’ knowledge of electrocardiographic monitoring, and arrhythmia detection, 2021 : https://pmc.ncbi.nlm.nih.gov/articles/PMC8246648/
- **[H14]** Strengthening Telemetry Safety Through Standardized Physiological Parameter Monitor Technician Education, 2026 : https://pmc.ncbi.nlm.nih.gov/articles/PMC13680767/
