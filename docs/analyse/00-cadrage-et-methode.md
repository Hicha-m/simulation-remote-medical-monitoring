# 00 — Cadrage et méthode d'analyse

**Version :** 0.1  
**Date :** 18 novembre 2026  
**Statut :** cadrage exploratoire — décisions ouvertes

## 1. Sujet transmis

> Simulation d'un système de télésurveillance médicale. Plusieurs données sur les patients (fréquence cardiaque, tension artérielle, saturation en oxygène, etc.) arrivent régulièrement au niveau d'un serveur qui les traite et les stocke dans une base de données. Les différents appareils envoyant les données sont simulés par des programmes clients. Un tableau de bord permet au personnel hospitalier de surveiller les patients à distance et en direct, avec un affichage des données reçues le plus rapidement possible. Les données étant sensibles, la sécurité est importante.

Mots-clés annoncés : Java, réseau, sécurité, interface graphique, base de données.

Cette reformulation conserve le sens du sujet sans lui attribuer de protocole réseau, de technologie de stockage, de contexte médical ou de seuil clinique qui ne serait pas précisé.

## 2. Ce qui est explicitement demandé

- Simuler plusieurs sources de données représentant des appareils associés à des patients.
- Faire parvenir régulièrement des mesures à un serveur.
- Traiter et conserver les mesures reçues dans une base de données.
- Présenter les données à distance sur un tableau de bord destiné à du personnel hospitalier.
- Réduire autant que possible le délai entre la réception d'une mesure et son affichage.
- Prendre en compte la sensibilité des données et la sécurité du système.

## 3. Ce qui n'est pas encore défini

Le sujet ne précise pas, à ce stade :

- si le patient est hospitalisé, à domicile ou dans les deux situations ;
- si les appareils représentent des moniteurs de chevet, des objets connectés ou des dispositifs médicaux de télésurveillance ;
- si la fréquence d'émission est continue, périodique, déclenchée par un événement ou variable selon l'appareil ;
- quels paramètres physiologiques sont obligatoires ;
- si les mesures sont des valeurs ponctuelles, des séries temporelles, des signaux bruts ou un mélange ;
- le nombre de patients, d'appareils, de services et d'utilisateurs ;
- les rôles exacts et les responsabilités du personnel ;
- ce qui déclenche une alerte, qui la reçoit et comment elle est clôturée ;
- le délai maximal acceptable entre mesure, serveur et affichage ;
- la disponibilité attendue, la durée de conservation et les règles d'archivage ;
- le niveau d'interopérabilité avec des systèmes hospitaliers existants ;
- le périmètre exact de la sécurité attendue ;
- si le système est seulement pédagogique ou s'il est envisagé comme une démonstration proche d'un produit de santé.

Ces points sont des questions à instruire, pas des lacunes à combler arbitrairement.

## 4. Trois interprétations à départager

### A — Monitorage de patients hospitalisés

Le patient se trouve dans un établissement. Des moniteurs ou capteurs présents au lit transmettent des données vers une station ou un système central. L'étude doit alors regarder les unités de soins, les lits, les transferts de patients, la continuité des mesures, les alarmes et les transmissions entre équipes.

### B — Télésurveillance de patients à distance ou à domicile

Le patient se trouve en dehors de l'établissement. Il transmet des mesures via un appareil, une application ou une passerelle. L'étude doit alors inclure l'inclusion du patient, l'association appareil-patient, l'observance, les absences de transmission, l'accompagnement et l'organisation de l'équipe de télésurveillance.

### C — Système hybride

Le système couvre plusieurs lieux et modalités de collecte : établissement, domicile, appareils médicaux, saisie patient et passerelles. Il faut alors étudier les frontières de confiance, les différences de fréquence, l'identité des appareils, les droits d'accès et la continuité du suivi.

**Aucune de ces interprétations n'est retenue dans cette version.** Le vocabulaire réglementaire français de « télésurveillance médicale » ne suffit pas à lui seul à déterminer le contexte opérationnel visé par le sujet. Voir les références [S08] et [S09].

## 5. Pourquoi cette distinction est structurante

Les trois interprétations changent notamment :

| Dimension | Monitorage hospitalier | Télésurveillance à domicile | Hybride |
|---|---|---|---|
| Localisation | Dans l'établissement | Hors établissement | Plusieurs lieux |
| Sources | Moniteurs et capteurs | Appareils, applications, saisie patient | Sources mixtes |
| Connectivité | Réseau de l'établissement et réseaux spécialisés | Internet, réseau mobile, Bluetooth, passerelle | Plusieurs réseaux |
| Organisation | Service, unité, lit, équipe de garde | Opérateur, médecin, infirmier, patient | Organisation combinée |
| Événements à considérer | Transfert de lit, changement d'unité, alarmes | Non-transmission, oubli, connexion interrompue | Les deux familles |
| Intégration | Système d'information hospitalier et équipements | Plateforme de télésurveillance et parcours de soins | Plusieurs systèmes |

Ce tableau est une grille de comparaison, pas une description universelle de tous les établissements.

## 6. Méthode d'analyse

1. **Définir le domaine :** glossaire, données, objets, acteurs et frontières du système.
2. **Comprendre les usages :** reconstituer des parcours documentés et identifier les événements opérationnels.
3. **Étudier l'existant :** projets open source, solutions commerciales et standards.
4. **Comparer les échelles :** démonstrateur local, périmètre de service, périmètre multi-établissements et vision théorique.
5. **Identifier les contraintes :** sécurité, confidentialité, continuité, interopérabilité, réglementation et exploitation.
6. **Formuler des pistes de différenciation :** chaque piste doit être confrontée à des solutions existantes et à un besoin réel.
7. **Décider seulement après validation :** les décisions seront consignées dans le journal de décisions.

## 7. Qualité des preuves

Ordre de préférence pour les recherches futures :

1. textes réglementaires, autorités publiques, référentiels et normes ;
2. documentations officielles et dépôts des projets étudiés ;
3. retours d'expérience d'établissements et publications scientifiques ;
4. documents fournisseurs, clairement identifiés comme sources commerciales ;
5. discussions communautaires et témoignages, utilisés comme pistes de vérification.

Toute affirmation importante doit avoir une source, une date et une limite d'interprétation.

## 8. Livrable attendu à la fin de l'analyse

La phase d'analyse devra permettre de produire, sans imposer prématurément une technologie :

- un périmètre fonctionnel validé ;
- une liste d'acteurs et de responsabilités ;
- des parcours d'utilisation et scénarios ;
- des exigences qualitatives et des métriques à mesurer ;
- une comparaison des options techniques ;
- une première analyse de risques ;
- plusieurs scénarios d'échelle ;
- un positionnement et une proposition de valeur argumentés ;
- une liste des points volontairement hors périmètre ;
- un backlog de questions et de décisions.

**État actuel :** aucune architecture, pile technique, base de données, technologie de transport, règle clinique ou taille de déploiement n'est validée.
