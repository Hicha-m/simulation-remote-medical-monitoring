# Couverture 01 — Matrice du sujet initial

**Version :** 0.1 — **Date :** 18 novembre 2026

## 1. Sujet fourni

Le sujet demande une application simulant un système de surveillance médicale. Plusieurs données physiologiques de patients arrivent régulièrement sur un serveur, qui les traite et les stocke dans une base de données. Les appareils émetteurs sont simulés par des programmes clients. Un tableau de bord présente les données au personnel hospitalier à distance et en direct. La sécurité des données sensibles constitue un enjeu important.

Mots-clés : Java, réseau, sécurité, interface graphique, base de données.

## 2. Matrice de couverture

| Élément du sujet | Ce qu'il signifie dans le contexte hospitalier | Étude déjà réalisée | Ce qui reste à préciser |
|---|---|---|---|
| Système de monitorage hospitalier | Ensemble d'équipements, réseaux, centrales, utilisateurs et processus. | Contextes, systèmes et métiers. | Quel service hospitalier et quel parcours principal ? |
| Patients | Identité, séjour, localisation, état d'affectation. | Cycle patient/lit/appareil. | Référentiel patient simulé, séjour et transferts. |
| Paramètres physiologiques | FC, ECG, PA, SpO₂, FR, température, CO₂ et autres selon service. | Glossaire et moniteurs. | Liste exacte des mesures du POC et leurs unités. |
| Appareils | Moniteurs de chevet, transport, télémétrie et capteurs. | Familles de fabricants et produits. | Quels équipements reproduire dans la simulation ? |
| Clients simulateurs | Programmes qui reproduisent les émissions et états d'appareils. | Scénarios préliminaires. | Nombre, comportement, fréquence, identités, pannes et rejeu. |
| Serveur de réception | Point d'entrée des flux, authentification, validation et rattachement aux patients. | Architecture fonctionnelle et systèmes fabricants. | Traitement synchrone/asynchrone, files, erreurs et reprise. |
| Traitement des données | Normalisation, validation technique, calculs, événements et règles. | Glossaire, qualité et alarmes. | Quelles règles sont purement techniques et lesquelles sont hors périmètre clinique ? |
| Base de données | Données patients fictives, affectations, mesures, alarmes, états, audit et configuration. | Données et intégration SIH. | Modèle, volumes, rétention, requêtes et archivage des courbes. |
| Tableau de bord | Vue multi-patients, détail patient, courbes, tendances, alarmes et disponibilité. | Centrales et besoins métier. | Desktop ou web, rôles, ergonomie, affichage multi-écran. |
| Direct / rapidement possible | Latence de bout en bout et fraîcheur visible des données. | Scénarios de performance et centrales. | Objectifs chiffrés, percentiles, nombre d'appareils et débit. |
| Personnel hospitalier | IDE, médecin, personnel de surveillance centrale, biomédical et DSI selon le scénario. | Cartographie des acteurs. | Qui surveille, qui reçoit, qui acquitte et qui répond ? |
| Sécurité | Confidentialité, intégrité, disponibilité, authenticité, contrôle d'accès et audit. | Dossier cybersécurité. | Niveau de sécurité attendu pour le POC et limites explicites. |
| Java | Langage cité dans le sujet. | Pas de décision technologique. | Version Java, composants concernés, frameworks autorisés et interface. |
| Réseau | Topologie, segmentation, transport, protocoles, pertes et reconnexion. | Architectures GE/Philips/Dräger/Mindray. | Protocole de démonstration et comportement lors des pannes. |
| Interface graphique | Interface de surveillance et administration éventuelle. | Besoins et centrales actuelles. | Liste des vues, tâches utilisateurs et navigation. |
| Exploitation | Disponibilité, maintenance, mises à jour, sauvegardes et fonctionnement dégradé. | Architecture et cybersécurité. | Ce qui doit être simulé et ce qui est hors périmètre. |

## 3. Détail par mot-clé du sujet

### 3.1 Java

Java est explicitement cité, mais le sujet ne dit pas nécessairement que chaque composant doit être écrit en Java. Il faut déterminer si l'obligation s'applique :
- au serveur ;
- aux clients simulateurs ;
- au dashboard ;
- à tous les composants ;
- ou seulement à une partie de l'application.

Questions à trancher :
- version du JDK ;
- bibliothèque réseau ;
- framework serveur ;
- interface desktop ou web ;
- choix de persistance ;
- gestion des threads, événements et concurrence ;
- outillage de test et de packaging.

Aucune technologie Java n'est choisie dans cette phase.

### 3.2 Réseau

L'étude montre plusieurs réseaux dédiés, VLAN, passerelles et protocoles selon les fabricants. Il faut définir :
- les liaisons entre clients et serveur ;
- le type de flux (mesures, courbes, alarmes, états techniques) ;
- le transport et la fiabilité attendue ;
- l'authentification des clients ;
- l'horodatage ;
- la perte, le retard, les doublons et les reconnexions ;
- les objectifs de latence.

La simulation doit permettre de mesurer le comportement du système sous conditions normales et dégradées.

### 3.3 Sécurité

Les menaces sont techniques et organisationnelles :
- appareil ou utilisateur non autorisé ;
- compromission de comptes ;
- modification ou rejeu de mesures ;
- interception de flux ;
- exploitation d'une vulnérabilité d'appareil ;
- ransomware ou indisponibilité du SI ;
- accès prestataire mal maîtrisé ;
- fuite de données ;
- perte d'une centrale ou d'une passerelle.

Les mécanismes de sécurité doivent être reliés à un scénario de menace et à une vérification.

### 3.4 Interface graphique

Le besoin ne se réduit pas à afficher des valeurs. Une interface de centrale peut devoir :
- afficher plusieurs patients ;
- indiquer lit, appareil et unité ;
- afficher la dernière donnée et sa fraîcheur ;
- distinguer les alarmes physiologiques et techniques ;
- ouvrir une vue détaillée ;
- afficher des courbes et tendances ;
- montrer les appareils hors ligne ;
- présenter les événements en attente ;
- conserver l'historique des actions autorisées.

La hiérarchie visuelle et le workflow doivent être étudiés avec les utilisateurs du contexte retenu.

### 3.5 Base de données

Le modèle pourrait distinguer :
- Patient ;
- Séjour ;
- Unité et lit ;
- Appareil et capteur ;
- Session de surveillance ;
- Observation ;
- Échantillon ou segment de courbe ;
- Événement ;
- Alarme ;
- Acquittement / action / clôture ;
- Configuration ;
- Utilisateur et rôle ;
- Journal d'audit ;
- état de connectivité et maintenance.

La liste est un modèle conceptuel à vérifier, pas un schéma choisi. Les courbes brutes peuvent avoir des exigences de volume, de rétention et d'accès différentes des valeurs ponctuelles.

## 4. Besoins hospitaliers supplémentaires découverts

Le sujet académique initial ne détaille pas explicitement, mais le terrain hospitalier ajoute plusieurs sujets qui conditionnent le réalisme :

1. Admission et identification du patient.
2. Affectation au lit et à l'unité.
3. Association et remplacement d'appareils.
4. Transfert et transport intrahospitalier.
5. Report des alarmes locales vers une centrale.
6. Rôles d'observateur et de répondant.
7. Acquittement, escalade, transmission et clôture d'événement.
8. Relève d'équipe.
9. Gestion des capteurs déconnectés et données manquantes.
10. Fonctionnement dégradé de la centrale ou du réseau.
11. Maintenance, nettoyage, recharge et réaffectation des appareils.
12. Interopérabilité avec ADT, DPI et autres systèmes cliniques.
13. Formation et accompagnement des professionnels.
14. Cybersécurité du dispositif médical lui-même et de l'infrastructure hospitalière.

## 5. Traçabilité avec les autres dossiers

- Contextes : [01-contextes](../01-contextes/README.md)
- Systèmes : [02-systemes](../02-systemes/README.md)
- Métiers : [03-metiers](../03-metiers/README.md)
- Besoins et scénarios : [04-besoins](../04-besoins/README.md)
- Architecture : [06-architecture-technique](../06-architecture-technique/README.md)
- Cybersécurité : [07-cybersecurite](../07-cybersecurite/README.md)
