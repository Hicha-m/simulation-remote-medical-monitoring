# 03 — Projets et briques existantes

**Version :** 0.1 — **Date :** 18 novembre 2026  
**Méthode :** benchmark documentaire initial à partir des dépôts publics et documentations des éditeurs. Ce n'est pas un audit de code, de sécurité, de qualité clinique ou de conformité.

## 1. Résumé comparatif

| Projet / solution | Nature | Proximité avec le sujet | Apport à étudier |
|---|---|---|---|
| Code for Japan — Remote Patient Monitoring | Application open source composée d'une API, d'un dashboard soignant et d'un client patient. | **Très forte** sur le suivi distant et le traitement de données patients. | Parcours patient, rôles, absence de données, tableau de suivi, découpage des composants. |
| HomeICU | Projet open source de moniteur portable et de station de base mobile. | **Forte** sur l'acquisition de constantes et la transmission distante. | Modèle appareil–passerelle–serveur, mesure multi-paramètres, déconnexion et simulation matérielle. |
| Synthea | Générateur de population et dossiers médicaux synthétiques. | **Complémentaire** ; ne fournit pas une plateforme de surveillance en direct. | Production de patients et d'observations fictifs, scénarios reproductibles, formats FHIR. |
| HAPI FHIR | Bibliothèque et serveur Java pour le standard FHIR. | **Complémentaire** ; pas un produit complet de télésurveillance. | Interopérabilité, API, stockage structuré et intégration Java. |
| Open mHealth Schemas | Modèles de données et outils de validation pour mesures de santé. | **Complémentaire** ; pas de tableau de bord clinique complet. | Représentation structurée des mesures et métadonnées. |
| Mirth Connect | Moteur d'intégration et de transformation de messages de santé. | **Complémentaire** ; pas une application de surveillance patient. | Routage, filtrage et transformation de messages HL7 et d'autres formats. |

## 2. Code for Japan — Remote Patient Monitoring

- Dépôt API : https://github.com/codeforjapan/remote-patient-monitoring-api
- Dashboard soignant : https://github.com/codeforjapan/remote-patient-monitoring-dashboard
- Client patient : https://github.com/codeforjapan/remote-patient-monitoring-client

### Contexte et objectif documentés

Le README de l'API présente un système destiné aux personnes en convalescence à domicile ou en hébergement, avec saisie d'informations de santé depuis un smartphone et consultation par les services de santé publique. Le projet est lié au contexte de la pandémie de COVID-19 au Japon [S01].

Le README fournit une chronologie : conception des cas d'usage et wireframes en décembre 2020, début du développement, première implémentation en avril 2021 et test dans un centre de santé publique d'Hokkaido. Ce sont des éléments déclarés dans le dépôt du projet, pas une évaluation indépendante [S01].

### Fonctionnalités figurant dans la spécification

- saisie périodique de données par le patient ;
- mesures de saturation en oxygène, de pouls, de température et de symptômes ;
- possibilité étudiée d'une collecte Bluetooth via un oxymètre ;
- tableau de bord destiné aux personnels de santé ;
- classement des patients par centre ;
- identifiant anonymisé et nom d'affichage ;
- signalement de mesures hors plage et d'absence de transmission ;
- historique graphique de température [S01].

### Architecture documentée

Le projet est divisé en trois dépôts : API, dashboard destiné aux infirmiers et client destiné aux patients. La documentation de développement de l'API décrit un environnement Serverless sur AWS, avec API Gateway, fonctions Lambda et DynamoDB. Les README des interfaces mentionnent respectivement Nuxt.js et Vue CLI [S01, S02].

Le dépôt API annonce la licence GNU AGPL v3. Les licences et obligations de réutilisation de chaque dépôt doivent être vérifiées séparément avant toute reprise de code [S01, S02, S03].

### Ce que ce projet permet d'apprendre

1. Un système de télésurveillance peut être conçu autour de rôles séparés patient / soignant / administrateur.
2. L'absence de mesure et les mesures hors d'une zone configurée sont des événements distincts.
3. Le suivi à distance peut combiner données manuelles, capteurs et questionnaire.
4. Le tableau de bord doit refléter une organisation de prise en charge, pas seulement afficher une liste de valeurs.

### Limites de la comparaison

Le contexte est celui du suivi de personnes en isolement à domicile, et non nécessairement celui du monitorage continu de patients hospitalisés. Le code, les dépendances, l'état de maintenance et la conformité actuels n'ont pas fait l'objet d'un audit complet.

## 3. HomeICU — moniteur portable open source

Dépôt : https://github.com/iozwang/homeicu

Le README décrit un système de capteur porté par le patient, relié à une application mobile jouant le rôle de station de base. Le matériel communique avec la station par Bluetooth Low Energy ; les données sont ensuite envoyées vers un serveur distant consultable par les médecins [S04].

Les paramètres cités par le projet comprennent la température, la SpO₂, la fréquence cardiaque, la fréquence respiratoire, l'ECG et des mesures de mouvement ou de toux. Le README présente plusieurs fonctionnalités comme réalisées et d'autres comme étant en développement, dont certaines autour de MQTT [S04].

Le dépôt est utile pour comprendre une chaîne appareil → Bluetooth → application passerelle → service distant. En revanche, les affirmations du README relatives à une qualité « medical-grade » sont des déclarations du projet ; elles ne sont pas ici considérées comme une certification ou une preuve de conformité réglementaire.

## 4. Synthea — données de patients fictifs

Dépôt : https://github.com/synthetichealth/synthea

Synthea est un simulateur de population et un générateur de dossiers de santé synthétiques. Sa documentation mentionne notamment patients fictifs, consultations, observations, constantes, traitements et plans de soins. Les exports incluent plusieurs versions de FHIR ainsi que CSV [S05].

**Intérêt pour le projet :** produire des identités et histoires fictives cohérentes, constituer un jeu de test réutilisable et éviter d'utiliser des données réelles.

**Limite :** Synthea génère principalement des dossiers et événements de santé ; il ne reproduit pas à lui seul un réseau de moniteurs, les contraintes d'ingestion en flux, le traitement opérationnel des alarmes et un dashboard de surveillance.

## 5. HAPI FHIR — interopérabilité Java

- Projet : https://github.com/hapifhir/hapi-fhir
- Starter serveur : https://github.com/hapifhir/hapi-fhir-jpaserver-starter
- Documentation : https://hapifhir.io/hapi-fhir/docs/

HAPI FHIR est une implémentation Java de l'API FHIR. Le projet de démarrage JPA permet de lancer un serveur FHIR avec persistance relationnelle [S06, S23].

Point de vigilance important : le README du starter indique explicitement que l'implémentation de sécurité et les logs d'entreprise ne sont pas fournis par défaut. Le starter ne doit donc pas être considéré comme une plateforme sécurisée et prête à être exploitée en santé sans conception complémentaire [S06].

**Intérêt :** étudier la modélisation des patients, appareils et observations et la possibilité d'exposer une API compatible avec les systèmes de santé.

## 6. Open mHealth — schémas de données

Dépôt : https://github.com/openmhealth/schemas

Le dépôt contient des schémas, des données de test, un validateur et un SDK. Le README courant indique que le SDK Java historique est déprécié et remplacé par un SDK Kotlin utilisable depuis Java, Groovy et Scala. Le dépôt évolue également vers les schémas IEEE 1752.1 pour certains domaines [S10].

**Intérêt :** étudier la façon de représenter les mesures et leurs métadonnées de manière structurée.

**Limite :** un schéma de mesure ne résout pas les questions d'identité, de transport, d'autorisation, de workflow ou de présentation.

## 7. Mirth Connect — intégration des systèmes de santé

- Projet : https://github.com/nextgenhealthcare/connect
- Exemples : https://github.com/nextgenhealthcare/connect-examples

Mirth Connect se présente comme un moteur d'intégration capable de filtrer, transformer et router des messages entre systèmes. La documentation explique notamment la conversion de formats tels que HL7 vers XML et les échanges avec des bases de données [S11].

**Intérêt :** comprendre les systèmes hospitaliers existants, l'hétérogénéité des formats et la nécessité d'une couche d'intégration.

**Limite :** ce n'est pas un moteur de télésurveillance patient prêt à l'emploi.

## 8. Solutions commerciales à comparer

Ces solutions sont des références de marché et des objets d'étude, pas des composants open source.

### Resilience

La documentation commerciale présente des solutions de télésurveillance pour l'oncologie, la gastro-entérologie et la psychiatrie. Resilience PRO est présenté comme un dispositif médical numérique de classe IIa marqué CE [S13].

Le retour d'expérience publié sur l'Hôpital Européen Marseille donne des informations particulièrement utiles sur le déploiement dans un service d'oncologie : inclusion, consentement, accompagnement, traitement des alertes, rôles infirmiers et coordination [S12].

### BIOTRONIK Home Monitoring

Le fournisseur décrit un flux automatique depuis un dispositif cardiaque implanté, vers un transmetteur à domicile, puis vers un serveur sécurisé consulté par les médecins. Des alertes sont configurables, y compris sur l'absence de transmission pendant plusieurs jours [S14].

### Implicity

Le fournisseur présente une plateforme de télésurveillance de dispositifs cardiaques implantables multi-constructeurs, avec regroupement de données, gestion d'alertes et intégration annoncée aux systèmes de dossiers patients [S15].

### Semeia — MedicWise

Le fournisseur présente MedicWise comme une plateforme de télésurveillance pour maladies chroniques, avec collecte automatisée, analyse, restitution, alertes et plans de suivi personnalisés. Il annonce plusieurs déclinaisons par spécialité [S16].

## 9. Synthèse des enseignements

Le benchmark révèle plusieurs niveaux de solutions :

- des applications complètes de suivi patient et de coordination, comme Code for Japan ;
- des chaînes d'acquisition connectée et de transmission, comme HomeICU ;
- des outils de génération de données fictives, comme Synthea ;
- des standards et serveurs d'interopérabilité, comme FHIR et HAPI FHIR ;
- des outils de validation de modèles de données, comme Open mHealth ;
- des moteurs d'intégration, comme Mirth Connect ;
- des produits commerciaux spécialisés par pathologie ou famille de dispositifs.

Il serait donc réducteur de comparer uniquement le projet à une application de dashboard. La comparaison devra couvrir la chaîne complète : source, transport, traitement, stockage, présentation, alerte, intervention humaine et interopérabilité.

## 10. Points à approfondir

1. Vérifier l'état de maintenance et les licences exactes des trois dépôts Code for Japan.
2. Examiner le code de HomeICU et de sa station de base pour comprendre le protocole et le format réellement implémentés, et non uniquement le README.
3. Examiner les exemples FHIR Observation, Device, Patient et Provenance.
4. Comparer les pratiques d'alerting et de gestion des accusés de réception des produits commerciaux.
5. Rechercher des études indépendantes sur la charge d'alertes et le temps réellement passé par les équipes.
6. Rechercher des projets spécifiquement dédiés au monitorage central hospitalier, distincts de la télésurveillance à domicile.
