# Environnement 03 — Cardiologie et télémétrie hospitalière

**Version :** 0.1 — **Date :** 18 novembre 2026

## 1. Ce que signifie la télémétrie hospitalière

Dans un contexte hospitalier, la télémétrie désigne ici le suivi sans fil de patients qui ne restent pas nécessairement au lit. Un transmetteur porté par le patient mesure et transmet des paramètres, souvent l'ECG et la fréquence cardiaque, vers une infrastructure de réception et une centrale de surveillance.

Il faut distinguer cette télémétrie hospitalière de la télésurveillance à domicile.

Une publication sur la télémétrie hospitalière décrit les unités non-ICU dans lesquelles les patients portent un émetteur ECG portable qui transmet les courbes vers une banque centrale de moniteurs [H11].

## 2. Exemple de système actuel : Mindray BeneVision TM80

La page française du fabricant présente le TM80 comme un moniteur de télémétrie destiné aux patients mobiles en environnement hospitalier.

Les fonctions mentionnées comprennent :

- transmission sans fil ;
- ECG, respiration, SpO₂ et PNI selon modules et configuration ;
- usage au cours des déplacements et hors de la chambre ;
- communication bidirectionnelle avec la station centrale ;
- alarme lorsque le patient quitte la zone réseau configurée ;
- fonction de localisation du dispositif ;
- autonomie annoncée jusqu'à 40 heures ;
- association possible avec certains moniteurs BeneVision de chevet [H09].

Ces informations sont celles du fabricant et ne constituent pas une mesure indépendante de la fiabilité radio ni une preuve de bénéfice clinique.

## 3. Le rôle de la centrale de télémétrie

La centrale permet d'afficher les ECG et événements transmis par plusieurs patients. Selon l'organisation, les personnes qui surveillent les écrans peuvent être :

- les infirmiers de l'unité, en parallèle des soins ;
- des personnels spécifiquement affectés à la lecture des moniteurs ;
- une équipe de surveillance centralisée ;
- une organisation mixte.

Une étude sur les monitor watchers montre que les modèles de responsabilité varient selon les hôpitaux : certains ne disposent pas de personnel dédié à la surveillance des écrans, tandis que d'autres utilisent des observateurs dédiés qui alertent les équipes au lit du patient [H11].

Une autre étude décrit la centralisation de la surveillance dans une unité centrale, avec des enjeux de formation, de compétences, de communication en boucle fermée et de volume élevé d'alarmes [H14].

**Conséquence : ne pas supposer qu'il existe partout un poste dédié avec un technicien qui surveille tous les écrans.** L'organisation doit être explicitement documentée dans le scénario.

## 4. Besoins métiers candidats

| ID | Besoin | Explication |
|---|---|---|
| TEL-01 | Associer un transmetteur à un patient. | L'ECG reçu doit être attribué au bon dossier. |
| TEL-02 | Suivre plusieurs patients mobiles. | L'équipement ne reste pas attaché à un lit fixe. |
| TEL-03 | Maintenir une transmission sans fil. | La couverture radio et les zones de l'établissement sont importantes. |
| TEL-04 | Détecter une perte de liaison. | Un patient qui sort de la couverture ne doit pas être confondu avec un patient stable. |
| TEL-05 | Gérer l'autonomie et l'état du dispositif. | Batterie et disponibilité influencent la continuité. |
| TEL-06 | Visualiser ECG et événements. | La centrale doit rendre les événements consultables par les personnes habilitées. |
| TEL-07 | Définir qui observe et qui intervient. | Les rôles entre personnel de centrale et infirmier au chevet doivent être non ambigus. |
| TEL-08 | Transmettre une alerte à la bonne équipe. | L'événement doit être orienté vers l'équipe responsable du patient. |
| TEL-09 | Conserver les traces et bandes ECG pertinentes. | La relecture des événements peut être utile au suivi et au dossier. |
| TEL-10 | Gérer les changements d'unité et la sortie du dispositif. | Éviter que l'ancien patient reste associé à l'équipement. |

## 5. Scénarios représentatifs

1. Patient admis dans l'unité et équipé d'un transmetteur.
2. Transmetteur remplacé ou batterie faible.
3. Patient mobile se déplace dans l'unité.
4. Perte de couverture radio.
5. Retour de couverture et reprise de transmission.
6. Événement ECG détecté par le système.
7. Alarme reçue par la centrale.
8. Personnel de surveillance contacte l'infirmier responsable.
9. L'équipe au chevet évalue la situation et répond.
10. Transfert de patient vers une autre unité.
11. Sortie du patient et libération du transmetteur.
12. Mauvaise association entre patient et transmetteur.

Les scénarios d'événement ECG sont des scénarios de démonstration technique ; aucune interprétation médicale automatique ne doit être revendiquée.

## 6. Risques organisationnels importants

Les recherches sur la télémétrie décrivent plusieurs problèmes :

- volume d'alarmes et alarmes non actionnables ;
- fatigue liée aux alarmes ;
- variation des compétences entre observateurs ;
- manque de clarté sur les responsabilités ;
- communication incomplète entre la surveillance centrale et le personnel au chevet ;
- surveillance continue parfois prescrite ou utilisée sans indication réévaluée [H11, H14].

Une intervention technologique dans une unité de télémétrie a étudié l'identification des patients générant un nombre très élevé d'alarmes et l'envoi de rappels aux infirmiers pour revoir les limites d'alarme ; l'étude rapporte une réduction de la durée moyenne des alarmes après intervention [H15]. Cela illustre un besoin possible de pilotage et d'analyse de la charge d'alarmes, sans prouver qu'une approche unique s'applique à tous les services.

## 7. Sources

- **[H09]** Mindray France, BeneVision TM80 : https://www.mindray.com/fr/products/patient-monitoring/telemetry-monitoring/benevision-tm80
- **[H11]** Monitor-watcher use, nurses’ knowledge of electrocardiographic monitoring, and arrhythmia detection, 2021 : https://pmc.ncbi.nlm.nih.gov/articles/PMC8246648/
- **[H14]** Strengthening Telemetry Safety Through Standardized Physiological Parameter Monitor Technician Education, 2026 : https://pmc.ncbi.nlm.nih.gov/articles/PMC13680767/
- **[H15]** Technological Intervention to Improve Alarm Management in Acute Care Telemetry Units, 2023 : https://pubmed.ncbi.nlm.nih.gov/37343111/

## 8. Questions ouvertes

- Une unité de cardiologie donnée dispose-t-elle d'une centrale dédiée ?
- L'observation des écrans est-elle assurée par les infirmiers ou des moniteurs techniciens ?
- Quels critères définissent l'indication et la durée de la télémétrie ?
- Quelle organisation assure le contact entre observateur et soignant au chevet ?
- Comment la couverture radio de l'établissement est-elle testée ?
- Quelles informations sont transmises vers le dossier patient ?
