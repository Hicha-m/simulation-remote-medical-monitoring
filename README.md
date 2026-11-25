# Projet de monitorage hospitalier

Projet académique de conception et de développement d'un système logiciel complet de monitorage hospitalier multiparamétrique.

## État du projet

**Phase actuelle :** analyse du domaine, cadrage médical et fonctionnel, préparation de l'architecture et des arbitrages. Le développement applicatif n'a pas encore commencé.

**Nature du système confirmée :** des moniteurs de chevet transmettent des mesures et des événements vers des centrales locales et une supervision transversale.  
**Premier service retenu :** réanimation adulte polyvalente ; les autres services sont des extensions progressives.  
**Équipe :** Hicham, Omar et Nawfel (3 personnes).  
**Contrainte technique confirmée :** la programmation réseau doit être réalisée en Java ; les autres technologies sont libres.  
**Planning recalé :** à partir du 25 novembre 2026, avec livraison le **8 janvier 2027**.

Le service initial, la cible multi-services et une première priorisation des fonctionnalités ont été retenus provisoirement par l'équipe. Les profils d'accès sont également cadrés dans une première version de TUT-06. Les paramètres médicaux, les choix techniques détaillés et les fonctionnalités souhaitées restent à arbitrer. Le cahier de décisions forme une baseline évolutive, avec un historique des arbitrages conservé. Le tuteur laisse le périmètre et les choix technologiques libres, sous réserve de la contrainte Java pour le réseau.

## Méthode de réalisation

Le développement suivra trois phases successives, inspirées des consignes du projet Intern :
1. [DEV](docs/consignes/DEV.md) — analyse, maquettes, données, ingestion/métier, interface et recette locale ;
2. [Docker](docs/consignes/Docker.md) — images, réseaux, volumes, composition et déploiement reproductible ;
3. [Metrics](docs/consignes/Metrics.md) — instrumentation, campagnes de mesure, charge, intégrité et analyse.

La [CI/CD](docs/consignes/CI-CD.md) sera mise en place dès DEV et enrichie à chaque phase.

## Documentation médicale et fonctionnelle

Le dossier de référence est [docs/analyse/monitorage-hospitalier](docs/analyse/monitorage-hospitalier/README.md).

Il est organisé par thèmes :
- environnements hospitaliers et équipements ;
- acteurs, métiers, processus et besoins ;
- architecture technique, cybersécurité et interopérabilité ;
- cadrage fonctionnel, parcours patient, appareils, données et tests ;
- maquette d'établissement ;
- domaines médicaux approfondis : dictionnaire des paramètres, courbes et données brutes, qualité des mesures, alarmes, contexte patient et pratiques françaises ;
- pilotage : cahier de décisions, organisation de Hicham, Omar et Nawfel, Gantt recalé et arbitrages mesurés.

**Accès directs :**
- [Dossier médical approfondi](docs/analyse/monitorage-hospitalier/12-domaines-medicaux-approfondis/README.md)
- [Pilotage et cadrage du projet](docs/analyse/monitorage-hospitalier/13-pilotage-projet/README.md)
- [Cahier de décisions à compléter par l'équipe](docs/analyse/monitorage-hospitalier/13-pilotage-projet/01-questionnaire-tuteur.md)
- [Planning Gantt recalé au 25 novembre — livraison le 8 janvier 2027](docs/analyse/monitorage-hospitalier/13-pilotage-projet/03-gantt-generique.md)
- [Stratégies et arbitrages critiques](docs/analyse/monitorage-hospitalier/13-pilotage-projet/04-strategies-et-arbitrages-critiques.md)
- [Préparation du rapport et de la soutenance](docs/analyse/monitorage-hospitalier/13-pilotage-projet/05-rapport-et-soutenance.md)
- [Méthode DEV → Docker → Metrics](docs/consignes/README.md)

Les documents de cadrage initiaux sont conservés dans [docs/analyse](docs/analyse/README.md).

## Principes

- Distinguer faits sourcés, fonctions annoncées par les fabricants, observations et hypothèses.
- Citer et versionner les sources utilisées.
- Ne pas inventer de seuils, de protocoles ou de conduites médicales.
- Préserver la provenance, la qualité et les horodatages des mesures.
- Utiliser des données de recherche dé-identifiées uniquement dans le respect de leurs conditions d'accès et de réutilisation ; compléter avec des données synthétiques clairement identifiées.
- Ne pas connecter le système à un dispositif médical réel ou à un SIH sans autorisation, validation de sécurité et clarification réglementaire.
- Documenter les décisions et comparer les choix structurants à l'aide de mesures reproductibles.
