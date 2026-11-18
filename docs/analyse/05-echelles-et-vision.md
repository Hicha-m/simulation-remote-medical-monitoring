# 05 — Échelles possibles et vision théorique

**Version :** 0.1 — **Date :** 18 novembre 2026  
**Statut :** scénarios de périmètre ; aucun dimensionnement ni choix d'architecture n'est arrêté.

## 1. Pourquoi réfléchir à plusieurs échelles ?

Le même sujet peut désigner :

- un prototype pédagogique avec quelques clients simulés ;
- un outil de démonstration couvrant le parcours d'un service hospitalier ;
- une plateforme multi-services ou multi-établissements ;
- un environnement de simulation très riche, conçu comme un laboratoire de validation technique et organisationnelle.

L'échelle ne se mesure pas uniquement au nombre de patients. Elle dépend aussi du débit de mesures, du nombre de sources, de la simultanéité, des équipes, des sites, des règles, de la continuité et du niveau de sécurité.

## 2. Les dimensions de capacité à mesurer

| Dimension | Unité ou indicateur à définir | Pourquoi elle compte |
|---|---|---|
| Patients suivis | Patients inscrits / patients actifs / patients simultanés | Charge des vues, des historiques et des relations. |
| Appareils | Appareils par patient, nombre total, types | Diversité de sources et association correcte. |
| Mesures | Mesures par appareil et par intervalle | Débit d'ingestion et volume de stockage. |
| Signaux | Fréquence d'échantillonnage, nombre de canaux, durée | Les signaux bruts peuvent être bien plus volumineux que des valeurs ponctuelles. |
| Messages simultanés | Événements/seconde en pic | Saturation et files d'attente. |
| Utilisateurs | Utilisateurs connectés simultanément | Capacité du serveur et diffusion en direct. |
| Alertes | Alertes générées, ouvertes et clôturées par période | Charge de traitement et risque de surcharge de l'interface. |
| Historique | Durée de conservation et granularité | Taille de stockage et coût des requêtes. |
| Sites | Services, unités, bâtiments, établissements | Isolation des données et gouvernance. |
| Disponibilité | Objectif de service et durée maximale d'interruption | Complexité de l'exploitation et de la reprise. |
| Latence | Mesure → serveur → traitement → interface | Vérification de l'objectif de rapidité. |
| Réseau | Latence, perte, gigue, coupures, bande passante | Comportement en conditions non idéales. |

Aucune valeur de dimensionnement n'est connue. Il faut recueillir les valeurs auprès des utilisateurs ou définir des hypothèses de test clairement identifiées comme telles.

## 3. Scénario petit — POC de laboratoire

### Objectif

Vérifier rapidement la faisabilité du parcours essentiel et des échanges entre composants dans un environnement contrôlé.

### Périmètre envisageable

- un seul environnement de démonstration ;
- un périmètre métier très limité ;
- un ensemble restreint de patients fictifs ;
- un ou plusieurs clients simulateurs ;
- quelques types de mesures choisis après clarification ;
- un serveur central ;
- un stockage persistant ou temporaire à déterminer ;
- un dashboard avec historique et indication de fraîcheur ;
- des utilisateurs fictifs avec droits différenciés ;
- des scénarios normaux et quelques cas de panne.

### Ce qui doit être démontré

- un client peut émettre des mesures ;
- le serveur peut les recevoir et les identifier ;
- les mesures peuvent être stockées ;
- le dashboard peut les rendre visibles avec un délai mesurable ;
- les erreurs de transmission sont observables ;
- les utilisateurs ne voient que les ressources autorisées dans le scénario.

### Ce que ce scénario ne permet pas de prétendre

- déploiement hospitalier opérationnel ;
- fiabilité clinique ;
- conformité d'un dispositif médical ;
- résistance à une forte charge non testée ;
- haute disponibilité ;
- interopérabilité avec un SIH réel ;
- sécurité d'un service en production.

## 4. Scénario moyen — périmètre d'un service

### Objectif

Étudier un fonctionnement organisé autour d'une unité ou d'un service médical, avec plusieurs rôles, plusieurs sources et un flux de travail d'alertes.

### Périmètre envisageable

- plusieurs groupes de patients ;
- plusieurs familles de simulateurs ou d'appareils ;
- plusieurs utilisateurs connectés ;
- rôles soignant, médecin, coordination, administration ;
- historique consultable et filtres ;
- workflow d'alerte avec statut, acquittement, commentaire, transfert et clôture ;
- gestion de données manquantes, retardées et dupliquées ;
- authentification et habilitations ;
- journalisation des actions sensibles ;
- tests de charge reproductibles ;
- sauvegarde et procédure de reprise.

### Questions supplémentaires

- Comment les responsabilités sont-elles distribuées ?
- Quelle est l'organisation de relève ?
- Quelles vues sont réellement utiles à chaque rôle ?
- Quelles données doivent être disponibles immédiatement ?
- Comment traiter un appareil déconnecté ?
- Quelle quantité de données et quelle durée d'historique sont nécessaires ?
- Quel est le coût humain et informatique du fonctionnement ?

## 5. Scénario large — multi-services ou multi-établissements

### Objectif

Explorer les problèmes d'un système distribué et multi-organisations.

### Périmètre envisageable

- plusieurs services et établissements ;
- plusieurs réseaux et environnements techniques ;
- isolation des organisations et des patients ;
- plusieurs instances d'ingestion ;
- files de messages ou broker distribué selon les résultats de l'étude ;
- stockage adapté aux différents types de données ;
- authentification fédérée ou gestion centralisée des identités ;
- intégration de référentiels et systèmes externes ;
- supervision de l'infrastructure ;
- haute disponibilité et reprise après sinistre ;
- gouvernance des données et des accès ;
- audits, procédures d'incident et gestion des mises à jour.

### Difficultés supplémentaires

- cohérence des identités patient et appareil ;
- synchronisation et décalage d'horloge ;
- réseau intermittent ;
- duplication et ordre des messages ;
- isolation entre établissements ;
- gouvernance des rôles ;
- interopérabilité et gestion des versions ;
- maintien en conditions opérationnelles ;
- réglementation, contrats, hébergement et responsabilités.

## 6. Vision théorique sans limite de temps ni de budget

Ce scénario est un horizon d'exploration, et non une feuille de route réaliste ni une promesse de résultat.

Un système de cette ambition pourrait couvrir :

### Acquisition et appareils

- catalogue de sources hétérogènes ;
- intégration avec plusieurs familles d'appareils ;
- simulateurs numériques de dispositifs ;
- passerelles locales ;
- gestion de l'identité, de l'étalonnage et de l'état des équipements ;
- collecte de signaux bruts, mesures structurées et questionnaires.

### Réseau et transport

- plusieurs modes de transport ;
- communication sécurisée ;
- gestion des déconnexions ;
- file locale et reprise après coupure ;
- mécanismes de déduplication ;
- horodatage et synchronisation ;
- validation de l'origine et de l'intégrité des messages.

### Traitement et stockage

- pipeline d'ingestion distribué ;
- validation technique et traçabilité ;
- stockage de séries temporelles et dossiers structurés ;
- archivage selon des règles définies ;
- versionnement des modèles de données ;
- export et interopérabilité par standards ;
- recherche historique et analyse de tendances.

### Workflow et interface

- vues adaptées aux rôles ;
- tri des événements ;
- gestion des alertes et escalades ;
- historique de chaque événement ;
- tableaux de bord multi-services ;
- accès patient et aidant si le parcours le demande ;
- accessibilité et prise en compte des difficultés numériques ;
- journal de relève et continuité d'équipe.

### Sécurité et exploitation

- identité forte et gestion centralisée des accès ;
- séparation stricte des responsabilités ;
- chiffrement et gestion des secrets ;
- journalisation protégée ;
- détection d'incidents ;
- sauvegardes testées ;
- haute disponibilité ;
- plan de reprise ;
- supervision technique et tableaux de bord opérationnels ;
- gestion de vulnérabilités et des mises à jour ;
- audits indépendants et gouvernance.

### Validation et recherche

- bibliothèque de scénarios reproductibles ;
- injection de pannes réseau, matériel, stockage et sécurité ;
- rejeu de campagnes de mesures ;
- générateur de populations synthétiques ;
- mesure des performances et de la charge ;
- évaluation de la charge d'alertes ;
- tests de robustesse et d'interopérabilité ;
- validation clinique si une finalité clinique est réellement poursuivie.

Une telle plateforme ne deviendrait pas automatiquement un dispositif médical certifié parce qu'elle serait techniquement sophistiquée. La finalité prévue, le rôle des composants, les responsabilités et les usages devraient être analysés.

## 7. Comparaison qualitative des échelles

| Dimension | Petit POC | Service | Multi-établissements | Vision théorique |
|---|---|---|---|---|
| Déploiement | Local | Service | Plusieurs sites | Réseau d'organisations |
| Sources | Simulateurs limités | Plusieurs familles | Hétérogènes et réelles ou simulées | Écosystème complet |
| Utilisateurs | Quelques comptes fictifs | Plusieurs rôles | Organisations séparées | Identité et gouvernance centralisées |
| Données | Synthétiques | Synthétiques | Synthétiques et éventuellement données autorisées | Données multi-sources encadrées |
| Flux | Contrôlés | Concurrents | Distribués | Très grande diversité de flux |
| Alertes | Règles de démonstration | Workflow complet | Coordination inter-équipes | Gestion avancée, évaluation et audit |
| Sécurité | Socle démonstratif | Contrôle d'accès et audit | Segmentation et exploitation sécurisée | Programme de sécurité complet |
| Disponibilité | Pas d'engagement de production | Reprise testée | Haute disponibilité à étudier | Résilience avancée |
| Interopérabilité | Formats internes | Modèle et API documentés | Standards et intégrations | Interopérabilité multi-systèmes |
| Validation | Tests de scénarios | Tests de charge et d'usage | Tests d'intégration et de reprise | Validation indépendante et clinique si nécessaire |

## 8. Architecture fonctionnelle à comparer (sans décision)

Le système peut être étudié comme une chaîne de responsabilités :

1. **Sources** — appareil réel, client simulateur, saisie ou générateur de données.
2. **Transport** — protocole, authentification et gestion des coupures.
3. **Réception** — point d'entrée et identification de l'émetteur.
4. **Validation technique** — structure, unité, horodatage, déduplication et qualité.
5. **Traitement** — règles, transformations et création d'événements.
6. **Stockage** — données courantes, historiques, audit et configuration.
7. **Diffusion** — actualisation des interfaces.
8. **Workflow** — tri, acquittement, transfert et clôture.
9. **Interface** — vues selon les rôles.
10. **Sécurité et supervision** — identités, droits, journaux, métriques et incidents.

Pour chaque bloc, il faudra comparer les alternatives techniques, les coûts, les avantages, les limites et la complexité opérationnelle avant de sélectionner une solution.

## 9. Architecture technique : familles d'options à étudier

| Problème | Options à étudier | Critères de comparaison |
|---|---|---|
| Communication client-serveur | HTTP/REST, MQTT, TCP personnalisé | Simplicité, fréquence, gestion des coupures, sécurité et extensibilité. |
| Diffusion dashboard | Polling, SSE, WebSocket | Latence, nombre de clients, sens des échanges et complexité. |
| Traitement | Synchrone, asynchrone, files de messages | Ordonnancement, résilience et capacité de reprise. |
| Stockage | SQL relationnel, base temporelle, stockage de fichiers | Requêtes, historique, volumes, cohérence et exploitation. |
| Modélisation | Modèle interne, FHIR, formats spécialisés | Interopérabilité, complexité, maturité et besoin réel. |
| Simulation | Générateur déterministe, scénarios, rejeu | Reproductibilité, contrôle et réalisme. |
| Déploiement | Monolithe modulaire, services séparés | Simplicité du POC, déploiement, évolutivité et diagnostic. |

Aucune de ces options n'est recommandée à ce stade. Un POC rapide peut justifier une solution simple, mais la décision doit être distinguée de ce qui serait nécessaire pour un système réellement exploité en milieu de soins.

## 10. Critères de comparaison des scénarios

La comparaison finale devra porter au minimum sur :

- faisabilité académique ;
- valeur démonstrative ;
- fidélité au parcours choisi ;
- complexité de développement ;
- complexité d'exploitation ;
- coût matériel et logiciel ;
- facilité de génération de données ;
- difficulté d'intégration ;
- sécurité ;
- qualité de la simulation des pannes ;
- mesure de performance ;
- possibilités d'évolution ;
- capacité à démontrer une valeur ajoutée identifiable.

## 11. Décision attendue

Avant de dimensionner le système, il faut répondre à trois questions :

1. Quel contexte est simulé : lit hospitalier, domicile ou hybride ?
2. Quel parcours et quelle équipe sont représentés ?
3. Quel niveau de réalisme est nécessaire pour démontrer la valeur du POC ?

Les paramètres chiffrés seront définis ensuite ; ils ne doivent pas être inventés pour donner artificiellement une apparence de précision.
