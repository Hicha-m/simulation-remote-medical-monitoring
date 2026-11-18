# Couverture 03 — Couverture intégrale du projet de monitorage hospitalier

**Version :** 0.1 — **Date :** 18 novembre 2026  
**Objectif :** vérifier que tous les points du sujet initial et les besoins découverts sont traités avant toute conception.

## 1. Statuts de couverture

- **Documenté** : le thème est décrit et sourcé dans le dossier.
- **Partiel** : les premières sources et besoins sont identifiés, mais le contexte exact ou les critères restent à confirmer.
- **Ouvert** : aucune décision n'est encore prise ou la recherche terrain manque.
- **Hors périmètre provisoire** : ne sera pas implémenté dans le POC tant que l'objectif n'est pas explicitement modifié.

## 2. Matrice fonctionnelle et technique

| Domaine | Points à traiter | État actuel | Documents / sources | Livrable à produire avant codage |
|---|---|---|---|---|
| 01. Contexte de soins | Service cible, type de patients, niveau de surveillance, organisation, locaux, horaires. | Partiel | [Contextes](../01-contextes/README.md), HAS [H93–H94]. | Contexte métier principal choisi, description du service et limites. |
| 02. Acteurs et rôles | IDE, médecin, observateur central, cadre, biomédical, DSI, administrateur, prestataire. | Partiel | [Métiers](../03-metiers/README.md). | Cartographie des acteurs et matrice des responsabilités. |
| 03. Parcours patient | Admission, séjour, unité, chambre, lit, transfert, transport, sortie. | Partiel | [Cycle patient/lit/appareil](../03-metiers/02-cycle-patient-lit-appareil.md). | Diagrammes de séquence et états du patient. |
| 04. Equipements | Moniteurs de chevet, transport, télémétrie, capteurs, appareils périphériques. | Documenté en panorama, périmètre ouvert | [Systèmes](../02-systemes/README.md), standards produit [H66–H72]. | Fiche des types d'appareils simulés et de leurs capacités. |
| 05. Paramètres physiologiques | ECG, FC, PA, SpO₂, FR, température, CO₂, pression invasive, courbes. | Partiel | [Glossaire](../01-glossaire-et-domaine.md), normes produit [H69–H72]. | Dictionnaire de données avec unité, fréquence, source et qualité. |
| 06. Clients simulateurs | Identité appareil, cadence, génération, états, déconnexion, batterie, capteur, horloge. | Ouvert | [Scénarios](../04-besoins/02-scenarios-et-indicateurs.md). | Contrat du simulateur et catalogue de profils d'appareils. |
| 07. Réseau | Topologie, segmentation, protocoles, flux, qualité de service, perte, latence, reconnexion. | Partiel | [Architecture](../06-architecture-technique/README.md), IEC 80001-1 [H76]. | Diagramme de flux et tableau des interfaces. |
| 08. Serveur d'ingestion | Réception, authentification, validation, normalisation, ordre, déduplication, erreurs. | Ouvert | [Architectures de référence](../06-architecture-technique/01-architectures-de-reference.md). | Spécification des messages et des traitements. |
| 09. Traitement métier | Associations, tendances, événements, règles de démonstration, statuts d'alarme. | Partiel | [Alarmes](../03-metiers/03-alarmes-et-traitement.md). | Catalogue des événements et workflow. |
| 10. Persistance et base de données | Patients, séjours, lits, appareils, observations, courbes, événements, alarmes, audit, archivage. | Partiel | [Données et intégration](../06-architecture-technique/04-donnees-et-integration-sih.md). | Modèle conceptuel et politique de rétention. |
| 11. Tableau de bord | Vue multi-patients, vue patient, courbes, tendances, fraîcheur, filtres, navigation. | Partiel | [Centrales](../02-systemes/02-centrales-de-surveillance.md). | Maquettes et tests de tâches utilisateur. |
| 12. Gestion des alarmes | Types, priorité, report, réception, acquittement, escalade, clôture, relève. | Documenté métier, règles de simulation ouvertes | [Alarmes](../03-metiers/03-alarmes-et-traitement.md), IEC 60601-1-8 [H67], HAS [H93–H95]. | Diagramme d'états d'une alarme et tests. |
| 13. Temps réel | Définition, latence de bout en bout, débit, concurrence, fraîcheur, perte et rattrapage. | Ouvert | [Scénarios et indicateurs](../04-besoins/02-scenarios-et-indicateurs.md). | SLO de démonstration et protocole de benchmark. |
| 14. Sécurité et confidentialité | Identités, rôles, authentification appareil, chiffrement, logs, secrets, sauvegardes, vulnérabilités. | Documenté en panorama, exigences POC ouvertes | [Cybersécurité](../07-cybersecurite/README.md), PGSSI-S, CNIL [H87, H92]. | Modèle de menace et checklist de contrôle. |
| 15. Disponibilité et continuité | Panne de client, réseau, serveur, base, centrale ; fonctionnement dégradé et restauration. | Partiel | [Prévention et continuité](../07-cybersecurite/03-prevention-detection-reponse-continuite.md), HAS/CaRE [H93, H96]. | Scénarios de panne et critères de reprise. |
| 16. Interopérabilité | ADT, DPI, HL7, FHIR, IHE PCD, terminologies, export/import. | Partiel | [Interopérabilité](../06-architecture-technique/04-donnees-et-integration-sih.md), CI-SIS [H88]. | Décision sur les interfaces réellement nécessaires. |
| 17. Infrastructure | Déploiement local, serveurs, sauvegarde, supervision, réseau et environnement. | Partiel | [Infrastructure](../06-architecture-technique/03-infrastructure-serveurs-et-deploiement.md). | Schéma de déploiement et prérequis d'exécution. |
| 18. Maintenance et matériel | Inventaire, configuration, maintenance, mise à jour, cycles de vie, retrait. | Ouvert | Marchés publics et documentations fabricants. | Cycle de vie d'un équipement simulé. |
| 19. Ergonomie et usage | Lisibilité, erreurs, alarmes, accessibilité, formation, fatigue. | Partiel | IEC 62366-1 [H75], HAS/ANSM [H93–H95]. | Scénarios d'utilisation et tests d'interface. |
| 20. Vérification et validation | Tests unitaires, intégration, bout en bout, charge, sécurité, restauration, reproductibilité. | Ouvert | IEC 62304/ISO 14971 comme références [H73–H74]. | Stratégie de test, critères d'acceptation et preuves. |
| 21. Réglementation | Finalité du logiciel, MDR, RGPD, HDS, PGSSI-S, responsabilités. | Partiel | [Registre des normes](01-registre-normes-et-reglementation.md). | Note de périmètre réglementaire validée pour le POC. |
| 22. Documentation et reproductibilité | Architecture, décisions, sources, prompts, installation, scénario de démonstration. | Documenté, à maintenir | README, prompts et journal des décisions. | Dossier de conception et guide de démonstration. |
| 23. Java et outillage | Version du JDK, bibliothèques réseau, framework serveur et GUI, outillage de build, tests, packaging et documentation. | Ouvert | Sujet initial (Java) et contraintes académiques à confirmer. | Version Java, contraintes de langage, framework autorisé et procédure d'exécution. |
| 24. Périmètre et critères de réussite | Objectif du POC, fonctions prioritaires, fonctions exclues, scénarios de démonstration et indicateurs de succès. | Ouvert | Cadrage général et scénarios initiaux. | Note de périmètre, backlog priorisé et critères d'acceptation. |

## 3. Matrice de traçabilité exigences → scénarios

Les familles de scénarios ci-dessous doivent être transformées en fiches numérotées lorsque le service cible est confirmé.

| ID | Exigence / capacité à démontrer | Scénario attendu | Critère de réussite |
|---|---|---|---|
| COV-01 | Un appareil est identifié et associé au bon patient. | Admission et association. | Le lien patient-séjour-lit-appareil est unique et historisé. |
| COV-02 | Le serveur reçoit une mesure. | Émission d'une mesure nominale. | La mesure est validée et visible avec son origine et son horodatage. |
| COV-03 | La mesure est persistée. | Arrivée d'un message valide. | La donnée est retrouvée après redémarrage contrôlé. |
| COV-04 | L'interface se met à jour. | Mesure nominale. | Latence mesurée selon le protocole de benchmark défini. |
| COV-05 | Une source se déconnecte. | Perte réseau d'un appareil. | L'état hors ligne et la dernière mesure connue sont visibles. |
| COV-06 | Une alarme est transmise et suivie. | Événement de démonstration. | Détection, affichage, réception, acquittement et clôture sont distincts et tracés. |
| COV-07 | Plusieurs patients sont surveillés. | Flux simultanés. | Chaque mesure reste associée au bon patient et l'écran est exploitable. |
| COV-08 | Le patient est transféré. | Changement de lit/unité. | Pas de mélange de mesures et historique des associations conservé. |
| COV-09 | La centrale devient indisponible. | Arrêt de service. | La défaillance est visible et le mode dégradé simulé est activé. |
| COV-10 | Un client non autorisé tente de transmettre. | Client inconnu. | Connexion ou message refusé et journalisé. |
| COV-11 | Un rôle essaie d'accéder à un secteur interdit. | Accès hors habilitation. | Accès refusé côté serveur et trace créée. |
| COV-12 | Les messages sont répétés ou désordonnés. | Doublon / message tardif. | Déduplication et ordre temporel explicites. |
| COV-13 | Le serveur ou la base tombe puis reprend. | Panne et restauration. | Cohérence et complétude contrôlées après reprise. |
| COV-14 | Les performances sont mesurées. | Campagne de charge. | Latence, débit, perte et utilisation des ressources sont documentés. |
| COV-15 | La configuration peut changer. | Modification de règle ou d'affectation par rôle habilité. | Auteur, date, ancienne et nouvelle valeur sont tracés. |
| COV-16 | La simulation est reproductible. | Rejeu d'un même scénario. | Même graine et même configuration produisent la même séquence déterministe. |

## 4. Ce qui est déjà couvert et ce qui reste à faire

### Déjà bien documenté

- environnements hospitaliers possibles ;
- familles de moniteurs et centrales ;
- quatre écosystèmes fabricants ;
- plusieurs marchés publics et retours d'expérience ;
- grandes architectures réseau et principes d'intégration ;
- incidents cyber et vulnérabilités ;
- organisation des alarmes et responsabilités ;
- panorama initial des normes.

### Partiellement documenté

- processus précis d'un service français donné ;
- architecture et protocole exacts de chaque modèle de moniteur ;
- gestion de la centrale durant les pauses et la nuit dans un établissement concret ;
- interactions exactes avec ADT et DPI ;
- critères d'alarme définis par spécialité ;
- exigences de capacité et de temps réel.

### Toujours ouvert

- le service hospitalier de référence ;
- la liste exacte d'équipements et paramètres simulés ;
- le nombre de patients, appareils et utilisateurs ;
- le protocole réseau du POC ;
- les technologies Java et le type d'interface ;
- le modèle et les volumes de base de données ;
- les seuils de performance de démonstration ;
- le niveau de sécurité fonctionnel exigé ;
- les scénarios d'évaluation prioritaires ;
- les critères qui rendront le POC concluant.

## 5. Points qui doivent impérativement être traités avant la conception

1. Choisir un service de référence (par exemple soins critiques) et décrire son organisation avec des sources et, si possible, un entretien.
2. Identifier les utilisateurs, leurs responsabilités et les moments où ils utilisent la centrale.
3. Définir le parcours d'un patient, d'un appareil et d'une alarme.
4. Sélectionner les paramètres et les appareils que le POC représente réellement.
5. Décrire les flux de données et les événements techniques.
6. Définir les règles de qualité, de fraîcheur, d'ordre et de persistance.
7. Définir les vues du dashboard et les interactions.
8. Définir les objectifs de performance et comment ils sont mesurés.
9. Réaliser le modèle de menace et sélectionner les protections du POC.
10. Écrire les scénarios nominaux, dégradés, d'erreur et de reprise.
11. Définir les critères d'acceptation et les preuves attendues.
12. Documenter les limites du simulateur et l'absence d'usage clinique.

Aucune décision de technologie ne doit précéder la clarification des flux, rôles, données et résultats attendus.
