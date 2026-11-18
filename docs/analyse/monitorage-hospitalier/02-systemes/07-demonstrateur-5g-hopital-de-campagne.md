# Retour d'expérience 02 — Démonstrateur 5G de réanimation éphémère et d'hôpital de campagne

**Version :** 0.1  
**Date de la source :** rapport moral Images & Réseaux 2025, publié en 2026.  
**Type :** démonstrateur technologique / expérimentation, pas une unité clinique exploitant des patients réels.

## 1. Pourquoi ce cas est particulièrement pertinent

Le rapport moral 2025 du pôle de compétitivité Images & Réseaux décrit, dans le cadre du projet **Engage 5G & Beyond**, un démonstrateur santé nommé « réanimation éphémère et hôpital de campagne ».

Le système est intéressant car il décrit explicitement comment plusieurs appareils de monitorage et de ventilation peuvent être reliés par une infrastructure de communication vers un poste central. Il ressemble à un laboratoire de simulation d'une unité de soins critiques.

## 2. Architecture physique du démonstrateur

Le rapport décrit quatre lits équipés de mannequins. Chaque lit comprend :
- un moniteur patient Philips MP60 ;
- un respirateur Dräger Evita XL ou Getinge Servo-I ;
- un routeur 5G Teltonika permettant la remontée d'informations vers un poste central Philips PIC iX ;
- pour trois lits sur quatre, une caméra de surveillance via un terminal Crosscall 5G, avec restitution au poste central [H39].

Il s'agit donc d'un montage multi-équipements :
- moniteur patient ;
- ventilateur ;
- routeur / liaison 5G ;
- centrale de surveillance ;
- caméra et terminal mobile sur certains lits.

## 3. Chaîne logique visible dans le cas

Le rapport ne fournit pas le détail des protocoles ni des formats utilisés. La chaîne fonctionnelle que l'on peut en tirer est :

1. Les appareils au lit du mannequin produisent des données et événements.
2. Un routeur 5G fournit la connectivité de remontée.
3. Les informations sont acheminées vers un poste central Philips PIC iX.
4. Une caméra associée à un terminal 5G fournit une vue vidéo depuis trois lits.
5. Le système central permet de rassembler les éléments de surveillance du démonstrateur.

Ce schéma est une reformulation fonctionnelle du montage documenté, et non une description du protocole réseau interne.

## 4. Partenaires et contexte

Le projet Engage 5G & Beyond est décrit comme une initiative de plateformes 5G privées et multi-sites. Le consortium mentionné dans le rapport comprend notamment Orange, Nokia, Eurecom, EDF, le CHU de Rennes et Images & Réseaux. Le projet est indiqué comme achevé en janvier 2025 [H39].

Le démonstrateur santé fait partie des cas d'expérimentation du projet. Le rapport mentionne que ces expérimentations ont permis de valider les apports de la 5G en termes de performance, de fiabilité et de nouveaux usages métiers, sans fournir dans cette section de mesures détaillées propres aux flux de monitorage [H39].

## 5. Ce que ce cas permet d'affirmer

- Un démonstrateur hospitalier de quatre lits avec mannequins a été réalisé.
- Les lits utilisaient des moniteurs Philips MP60 et des respirateurs Dräger ou Getinge.
- La remontée vers un poste central Philips PIC iX passait par des routeurs 5G Teltonika.
- Trois des quatre lits disposaient d'une caméra via un terminal 5G.
- Le démonstrateur s'inscrivait dans un programme d'expérimentation de 5G privée [H39].

## 6. Ce que ce cas ne démontre pas

- Que les quatre lits étaient utilisés pour soigner de vrais patients.
- Que le système était un environnement de production hospitalier.
- Que la 5G est nécessaire ou supérieure à Ethernet, Wi-Fi ou aux réseaux spécialisés pour tous les déploiements.
- La latence, le débit, la disponibilité ou les pertes de données observés.
- Les protocoles exacts entre moniteurs, routeur et PIC iX.
- La compatibilité avec tous les fabricants.
- La façon dont les alarmes étaient distribuées aux professionnels.
- Les performances cliniques ou la conformité réglementaire du démonstrateur.

La mention « démonstrateur » est essentielle : ce cas prouve l'existence d'une expérimentation technique reproductible, pas un mode de déploiement clinique standard.

## 7. Besoins métiers et techniques associés

| ID candidat | Besoin à étudier | Élément observé dans le démonstrateur |
|---|---|---|
| DEMO-5G-01 | Simuler plusieurs lits équipés en parallèle. | Quatre lits avec mannequins. |
| DEMO-5G-02 | Relier des dispositifs de fabricants différents. | Philips, Dräger et Getinge dans le même démonstrateur. |
| DEMO-5G-03 | Remonter les données vers une centrale. | Routeur 5G Teltonika vers Philips PIC iX. |
| DEMO-5G-04 | Ajouter d'autres flux que les constantes. | Caméra sur trois lits. |
| DEMO-5G-05 | Étudier l'effet de l'infrastructure réseau. | 5G privée / routeurs de remontée. |
| DEMO-5G-06 | Reproduire un environnement de soins critiques sans patient réel. | Mannequins utilisés sur les quatre lits. |

## 8. Conséquences pour notre POC

Ce démonstrateur donne un modèle d'environnement expérimental intéressant :
- plusieurs lits et mannequins ;
- des appareils hétérogènes ;
- un réseau configurable ;
- un poste central ;
- plusieurs flux par lit ;
- une distinction claire entre les données physiologiques et la vidéo.

Il pourrait inspirer la description de notre environnement de test même si le POC ne reproduit ni le matériel, ni la 5G, ni les dispositifs médicaux réels.

Une version purement logicielle pourrait simuler chaque appareil et la disponibilité du réseau, puis comparer les résultats selon plusieurs scénarios. Cela restera une piste à évaluer, pas une architecture choisie.

## 9. Source

- **[H39]** Pôle Images & Réseaux, *Rapport moral 2025*, section « Engage 5G & Beyond : un levier pour l'appropriation de la 5G privée par les filières », pages 26–27 (rapport mis en ligne en 2026) : https://www.images-et-reseaux.com/voy_content/uploads/2026/06/ir_rm_2025-def.pdf
