# Monitorage hospitalier — dossier de référence

**Version :** 0.1  
**Date de mise à jour :** 25 novembre 2026  
**Périmètre confirmé :** monitorage hospitalier.  
**Statut :** analyse, cadrage médical et fonctionnel ; les choix de services, fonctionnalités et technologies restent à valider.

**Nature confirmée :** système de monitorage hospitalier reliant des moniteurs de chevet à une ou plusieurs centrales de surveillance. **Échéance de livraison : 8 janvier 2027.** Il s'agit du projet logiciel complet, et non d'une simple preuve de concept.

## Objectif

Décrire la réalité du monitorage dans les établissements de santé : environnements de soins, équipements, systèmes centralisés, métiers, parcours opérationnels, données, alarmes, intégration informatique et besoins.

Ce dossier est volontairement découpé par thème. Chaque document traite un sujet défini et possède ses propres sources. Il ne faut pas fusionner tous les résultats dans un fichier unique.

## Lire dans cet ordre

### 1. Comprendre les environnements de soins

- [Réanimation et soins critiques](01-contextes/01-reanimation-soins-critiques.md)
- [Bloc opératoire et SSPI](01-contextes/02-bloc-operatoire-sspi.md)
- [Cardiologie et télémétrie hospitalière](01-contextes/03-cardiologie-telemetrie.md)
- [Unités de soins conventionnelles](01-contextes/04-unites-conventionnelles.md)
- [Urgences et transport intrahospitalier](01-contextes/05-urgences-et-transport.md)

- [Néonatologie et pédiatrie](01-contextes/06-neonatologie-et-pediatrie.md) — surveillance cardiorespiratoire néonatale, alarmes et profils pédiatriques.

### 2. Comprendre les équipements et systèmes actuels

- [Moniteurs de chevet et moniteurs de transport](02-systemes/01-moniteurs-de-chevet.md)
- [Centrales de surveillance et systèmes centralisés](02-systemes/02-centrales-de-surveillance.md)
- [Télémétrie hospitalière sans fil](02-systemes/03-telemetrie-hospitaliere.md)
- [Intégration et interopérabilité](02-systemes/04-integration-et-interoperabilite.md)
- [Écosystème et marchés publics en France](02-systemes/05-ecosysteme-et-marches-publics-france.md) — enquête ANSM, achats hospitaliers récents et familles de systèmes référencées.
- [Retour d'expérience CHU de Toulouse / BeneVision](02-systemes/06-retour-experience-chu-toulouse-benevision.md) — cas hospitalier décrit par Mindray.
- [Démonstrateur 5G de réanimation éphémère](02-systemes/07-demonstrateur-5g-hopital-de-campagne.md) — quatre lits de mannequins, moniteurs, respirateurs, routeurs 5G et centrale.

### 3. Comprendre les métiers et opérations

- [Acteurs et responsabilités](03-metiers/01-acteurs-et-responsabilites.md)
- [Cycle de vie patient, lit et appareil](03-metiers/02-cycle-patient-lit-appareil.md)
- [Alarmes, événements et traitement](03-metiers/03-alarmes-et-traitement.md)
- [Organisation du poste central et relèves](03-metiers/04-organisation-poste-central-et-releves.md)

### 4. Transformer le terrain en besoins testables

- [Catalogue des besoins métiers](04-besoins/01-catalogue-besoins-metiers.md)
- [Scénarios et indicateurs à simuler](04-besoins/02-scenarios-et-indicateurs.md)

### 5. Sources

- [Registre des sources hospitalières](05-sources/README.md)

## Ce que le dossier établit déjà

1. En soins critiques, la surveillance continue des paramètres physiologiques est une exigence explicitement mentionnée dans le cadre français des soins critiques. La HAS détaille en outre les conditions organisationnelles de la surveillance et des alarmes [H01, H02].
2. En salle de surveillance postinterventionnelle (SSPI), le Code de la santé publique décrit les fonctions de surveillance instrumentale par poste et la continuité pendant le transfert [H03].
3. Des systèmes commerciaux de surveillance centralisée existent chez plusieurs fabricants : Philips, GE HealthCare, Dräger et Mindray. Leurs fonctions et capacités annoncées ne sont pas identiques [H06–H09].
4. La télémétrie hospitalière désigne notamment le suivi sans fil de patients mobiles, avec des mesures transmises vers une infrastructure centrale. Les pratiques d'organisation et de surveillance humaine varient selon les établissements [H10, H11].
5. En unités conventionnelles, le monitorage continu portable constitue une évolution et/ou une modalité sélective ; il ne faut pas le confondre avec les contrôles intermittents habituels [H12, H13].
6. L'enquête ANSM réalisée en 2017 auprès de 631 services a documenté les modes de report d'alarmes et leurs difficultés ; cette photographie est historique et ne doit pas être présentée comme une mesure de 2026 [H33].
7. Des marchés publics français 2023–2029 détaillent les moniteurs, centrales, logiciels, alarmes, intégration, maintenance et formation recherchés par les établissements [H34–H37].
8. Des retours d'expérience documentent un système BeneVision au CHU de Toulouse et un démonstrateur 5G à quatre lits de mannequins ; ces deux cas sont de nature différente et ne doivent pas être confondus avec une installation clinique standard [H38, H39].


### 6. Comprendre l'architecture technique

- [Architectures de référence](06-architecture-technique/01-architectures-de-reference.md) — GE, Philips, Dräger et Mindray.
- [Technologies et protocoles](06-architecture-technique/02-technologies-et-protocoles.md) — Ethernet, VLAN, TCP/IP, HL7, IHE PCD, NTP, TLS et flux propriétaires.
- [Infrastructure, serveurs et déploiement](06-architecture-technique/03-infrastructure-serveurs-et-deploiement.md) — centrales, passerelles, virtualisation, disponibilité et maintenance.
- [Données et intégration SIH](06-architecture-technique/04-donnees-et-integration-sih.md) — identité, ADT, observations, archives et provenance.
- [Informations publiques et privées](06-architecture-technique/05-limites-documentaires-et-informations-privees.md) — limites des détails d'implémentation accessibles.

### 7. Comprendre la cybersécurité

- [Sécurité des dispositifs et des réseaux](07-cybersecurite/01-securite-dispositifs-reseaux.md) — protections documentées par les fabricants.
- [Incidents, vulnérabilités et fuites](07-cybersecurite/02-incidents-vulnerabilites-et-fuites.md) — cas documentés des équipements et établissements.
- [Prévention, détection, réponse et continuité](07-cybersecurite/03-prevention-detection-reponse-continuite.md) — pratiques organisationnelles et techniques.
- [Modèle de menace et matrice](07-cybersecurite/04-modele-de-menace-et-matrice.md) — menaces et scénarios non destructifs pour le projet.



### 8. Vérifier la couverture du sujet initial

- [Matrice de couverture](08-couverture-du-sujet/01-matrice-de-couverture.md) — lien entre la consigne, les mots-clés et les domaines étudiés.
- [Questions et arbitrages](08-couverture-du-sujet/02-questions-et-arbitrages.md) — éléments à résoudre avant la conception.

### 9. Cadrer le fonctionnement réel du projet

- [Comparaison des services et choix de référence](10-cadrage-fonctionnel/01-choix-service-reference.md) — différences entre réanimation, USC, cardiologie, SSPI, urgences et unités conventionnelles.
- [Parcours et personas](10-cadrage-fonctionnel/02-parcours-et-personas.md) — parcours composites, événements et bases de données hospitalières de recherche.
- [Appareils et profils par service](10-cadrage-fonctionnel/03-appareils-et-profils-par-service.md) — socle commun et équipements spécifiques aux unités.
- [Contrats de données](10-cadrage-fonctionnel/04-contrats-de-donnees.md) — enveloppe commune, observations, alarmes et états techniques.
- [Workflows métier](10-cadrage-fonctionnel/05-workflows-metier.md) — admission, mesure, alarme, transfert, déconnexion et sortie.
- [Points critiques et critères d'acceptation](10-cadrage-fonctionnel/06-points-critiques-et-criteres-acceptation.md) — risques P0/P1/P2 et tests de bout en bout.
- [Cartographie hospitalière et architecture du SI](10-cadrage-fonctionnel/07-cartographie-hospitaliere-et-architecture-du-si.md) — bâtiments, étages, services, lits, centrales, réseau et systèmes partagés.
- [Continuité électrique et fonctionnement dégradé](10-cadrage-fonctionnel/08-continuite-electrique-et-mode-degrade.md) — coupure de courant, batteries, onduleurs, groupe électrogène, panne réseau et tests PWR-01 à PWR-10.

La proposition actuelle est de prendre une réanimation adulte polyvalente comme référence de travail, mais ce choix n'est pas encore validé.

### 10. Stabiliser la maquette de l'établissement

- [Index de la maquette](11-maquette-etablissement/README.md) — bâtiments, étages, unités et statut des données réelles / fictives.
- [Plan physique et unités](11-maquette-etablissement/01-plan-physique-et-unites.md) — structure du site, services, centrales et zone technique.
- [Inventaire des chambres et lits](11-maquette-etablissement/02-inventaire-chambres-lits-postes.md) — identifiants stables de chaque chambre, lit et poste.
- [Correspondance MIMIC vers la maquette](11-maquette-etablissement/03-correspondance-mimic-vers-maquette.md) — parcours réellement enregistrés et affectations physiques synthétiques.
- [Modèle d'organisation et relations](11-maquette-etablissement/04-modele-organisation-et-relations.md) — distinction entre hiérarchie physique et organisationnelle.
- [Scénarios rejouables](11-maquette-etablissement/05-scenarios-rejouables.md) — deux parcours de référence et critères MAP-01 à MAP-10.
- [Configuration de la carte](11-maquette-etablissement/facility-map-v1.json) — source JSON versionnée pour le futur plan interactif.
- [Mapping MIMIC versionné](11-maquette-etablissement/mimic-transfer-mapping-v1.json) — unités, parcours réels et lits fictifs.

La maquette est fictive et versionnée. Elle ne prétend pas reproduire le plan d'un hôpital français précis.

### 11. Normes, recommandations et couverture intégrale

- [Registre des normes et textes](09-normes-et-recommandations/01-registre-normes-et-reglementation.md) — IEC/ISO, MDR, RGPD, HDS, PGSSI-S, CI-SIS et HAS.
- [Recommandations](09-normes-et-recommandations/02-recommandations.md) — exigences métier, sécurité, ergonomie et continuité.
- [Couverture intégrale du projet](09-normes-et-recommandations/03-couverture-integrale-du-projet.md) — 24 domaines du sujet et 16 scénarios de traçabilité.
- [Checklist avant conception](09-normes-et-recommandations/04-checklist-avant-conception.md) — critères de sortie de l'analyse.

Le registre note aussi le projet de loi français de transposition NIS2, adopté en première lecture à l'Assemblée nationale le 17 novembre 2026, mais non promulgué au 18 novembre 2026.

### 12. Approfondir les domaines médicaux essentiels

- [Dictionnaire médical des paramètres](12-domaines-medicaux-approfondis/01-dictionnaire-medical-parametres.md) — ECG, FC, SpO₂, PPG, PANI, PAI, respiration, CO₂, température et métadonnées.
- [Courbes et données brutes](12-domaines-medicaux-approfondis/02-courbes-et-donnees-brutes.md) — WFDB, MIMIC-IV Waveform, VitalDB, Barcelona SICU Signals et données haute résolution.
- [Qualité et fiabilité des mesures](12-domaines-medicaux-approfondis/03-qualite-et-fiabilite-mesures.md) — artefacts, valeurs périmées, qualité source et indicateurs calculés.
- [Gestion des alarmes par les soignants](12-domaines-medicaux-approfondis/04-gestion-alarmes-et-workflow-soignant.md) — circuit humain, prise de connaissance, intervention, escalade et relève.
- [Informations médicales associées au patient](12-domaines-medicaux-approfondis/05-contexte-medical-patient.md) — patient, séjour, affectation, identité et minimisation.
- [Pratiques françaises](12-domaines-medicaux-approfondis/06-pratiques-francaises-etablissement.md) — organisation hospitalière, identitovigilance, interopérabilité et limites réglementaires.

### 13. Piloter le projet à trois jusqu'au 8 janvier 2027

- [Cahier de décisions et questions de cadrage](13-pilotage-projet/01-questionnaire-tuteur.md) — questions à trancher par l'équipe ; programmation réseau en Java, autres choix libres.
- [Questionnaire d'organisation de l'équipe de trois](13-pilotage-projet/02-questionnaire-equipe.md) — disponibilités, compétences, responsabilités, Git, intégration et décisions.
- [Gantt](13-pilotage-projet/03-gantt-generique.md) — planning recalé du 25 novembre 2026 au 8 janvier 2027 pour trois personnes.
- [Stratégies et arbitrages critiques](13-pilotage-projet/04-strategies-et-arbitrages-critiques.md) — options d'architecture, scénarios de panne et mesures comparatives.

### 14. Méthode de réalisation et livraison

Le développement suivra les trois phases définies dans [docs/consignes](../consignes/README.md) :

- [DEV](../consignes/DEV.md) — analyse, prototype d'interface, données, ingestion, backend, centrale et recette locale.
- [Docker](../consignes/Docker.md) — construction des images, réseaux, volumes, Compose, santé et installation reproductible.
- [Metrics](../consignes/Metrics.md) — instrumentation, plan de test, étalonnage, campagnes et analyse.
- [CI/CD](../consignes/CI-CD.md) — intégration, contrôles qualité, construction et livraison continues, transversalement aux trois phases.

La séquence VM intermédiaire présente dans le projet de référence n'est pas retenue comme une phase obligatoire à ce stade. La date de livraison est le 8 janvier 2027 ; le [Gantt](13-pilotage-projet/03-gantt-generique.md) est recalé au 25 novembre et devra être ajusté après saisie des disponibilités des trois membres.

## Règles de preuve

Chaque document distingue :
- **Fait réglementaire ou institutionnel** : texte ou recommandation officielle.
- **Fonction produit documentée** : caractéristique décrite par le fabricant ; cela ne prouve pas le déploiement dans un hôpital particulier.
- **Résultat d'étude** : résultat publié dans la littérature ; préciser population, contexte et limites.
- **Besoin métier déduit** : exigence candidate déduite d'un processus documenté ; elle doit être validée avec les professionnels.
- **Question ouverte** : information qui n'a pas encore été confirmée.

Ne jamais extrapoler une caractéristique produit à l'ensemble des hôpitaux. Ne jamais présenter un seuil ou un comportement simulé comme une règle clinique.

## Hors périmètre provisoire

- Télésurveillance de patients à domicile.
- Remplacement d'une centrale clinique ou d'un moniteur certifié.
- Décision ou diagnostic médical automatisé.
- Connexion à un réseau hospitalier réel.
- Utilisation de données patient réelles.

Ces limites pourront être réexaminées si le sujet académique l'exige explicitement.
