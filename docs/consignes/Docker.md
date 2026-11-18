# Docker — Conteneurisation et infrastructure reproductible

**Périmètre :** étapes 7 à 10.  
**Prérequis :** phase DEV terminée, application locale fonctionnelle, tests P0 passants et configuration externalisée.

## 1. Contexte et objectif

La phase Docker ne doit pas modifier le comportement métier de l'application. Elle doit fournir une manière reproductible de construire, démarrer, arrêter, mettre à jour et inspecter le système complet.

L'objectif est de passer d'une installation locale dépendante des postes des développeurs à un environnement décrit par des fichiers versionnés.

Docker n'est pas une correction du code : si une application ne démarre pas correctement localement ou dépend d'adresses codées en dur, la conteneurisation exposera ces défauts au lieu de les résoudre.

## 2. Topologie logique à conteneuriser

La composition exacte dépend de l'architecture retenue après DEV. Les services candidats sont :

| Service logique | Responsabilité | Publication réseau |
|---|---|---|
| Point d'entrée / proxy | Servir la centrale, router les API et appliquer les règles de point d'entrée | Seul point public par défaut |
| Interface centrale | Fichiers de l'application web si séparée du backend | Réseau frontal |
| Backend / services métier | Patients, sessions, appareils, alarmes, autorisations et API | Réseaux applicatifs privés |
| Ingestion temps réel | Recevoir les messages de moniteurs et les flux de données | Réseau privé, sauf si l'architecture impose un point d'accès dédié |
| Simulateurs de moniteurs | Générer ou rejouer des données et événements | Réseau privé |
| Base de données | Métadonnées, observations, alarmes, utilisateurs et configuration | Aucun port publié par défaut |
| Stockage de waveforms | Données de signaux volumineuses si un stockage séparé est retenu | Réseau privé |
| Collecteur de métriques | Collecter les métriques des services | Accès réservé à l'environnement d'exploitation |
| Visualisation | Tableaux de bord techniques et résultats de campagnes | Accès contrôlé, non exposé publiquement par défaut |

Ces composants sont des responsabilités logiques, pas un nombre imposé de conteneurs. Plusieurs responsabilités peuvent rester dans un même service si cela respecte les frontières de sécurité et de maintenance.

## 3. Principes d'infrastructure

### 3.1 Images et reproductibilité

- choisir une image de base officielle et épingler une version ;
- construire l'image applicative à partir du dépôt ;
- utiliser un fichier d'exclusion pour ne pas embarquer caches, secrets, fichiers temporaires et données locales ;
- séparer les dépendances du code afin de bénéficier du cache de construction ;
- exécuter les processus avec un utilisateur non privilégié lorsque possible ;
- minimiser les paquets présents dans les images ;
- documenter l'architecture CPU et les versions des images ;
- enregistrer l'identifiant de l'image utilisée pour chaque recette ou mesure.

Éviter les tags flottants comme latest pour les versions de référence et les campagnes de mesure.

### 3.2 Réseaux et exposition

- créer des réseaux dédiés aux flux nécessaires ;
- n'exposer que le point d'entrée requis par l'utilisateur ;
- ne pas publier directement la base de données sur l'hôte ;
- ne pas donner au proxy un accès réseau à la base si le proxy n'en a pas besoin ;
- séparer les flux d'administration, de mesure et de monitorage lorsque le besoin le justifie ;
- vérifier les communications autorisées et interdites depuis chaque conteneur.

La topologie doit être une décision documentée, pas un simple réseau unique par défaut.

### 3.3 Persistance

Les données qui doivent survivre au remplacement d'un conteneur ne doivent pas être stockées uniquement dans sa couche inscriptible.

Identifier séparément :
- base relationnelle ;
- fichiers ou blocs waveform ;
- configuration persistante si nécessaire ;
- résultats de campagnes Metrics ;
- sauvegardes.

Les volumes de données de test doivent être réinitialisables de manière explicite. Les commandes destructives doivent être documentées.

### 3.4 Configuration et secrets

- fournir un fichier exemple de variables sans secret réel ;
- ne jamais committer de mots de passe, jetons ou clés privées ;
- documenter les variables obligatoires et leurs valeurs de démonstration ;
- utiliser les mécanismes adaptés de secrets au déploiement ;
- différencier configuration de développement, test et démonstration.

### 3.5 Santé et dépendances

Chaque service doit pouvoir signaler s'il est vivant et s'il est prêt à traiter les requêtes. Le simple démarrage d'un conteneur ne prouve pas que sa base ou son broker accepte les connexions.

- healthcheck adapté à chaque composant ;
- délais de reprise et reconnexion ;
- politique de redémarrage raisonnable ;
- gestion des dépendances circulaires ;
- absence de boucle de redémarrage silencieuse ;
- logs explicites lors d'une indisponibilité.

## 4. Déroulement du travail

### Étape 7 — Conteneuriser la persistance

**Objectif :** démarrer la base et le stockage persistant sans dépendre d'une installation manuelle.

**Travail à faire :**
- écrire la déclaration du service de base ;
- fixer une version d'image ;
- externaliser les identifiants ;
- définir les volumes ;
- brancher les migrations ou scripts d'initialisation de manière contrôlée ;
- ajouter healthcheck ;
- vérifier sauvegarde, restauration et réinitialisation.

**Vérifications :**
- la base survit à la suppression/recréation du conteneur ;
- le volume n'est pas supprimé par un simple arrêt ;
- une base neuve peut être initialisée ;
- une mise à jour de schéma est gérée par migration et non par un script supposé rejoué à chaque démarrage ;
- aucun port non requis n'est publié.

**Livrables :** déclaration du service, volumes, procédure d'initialisation, rapport de sauvegarde/restauration et preuve de persistance.

### Étape 8 — Construire les images applicatives

**Objectif :** produire les images de la centrale, du backend, de l'ingestion et des simulateurs selon le découpage réellement retenu.

**Travail à faire :**
- écrire les fichiers de construction ;
- épingler les images de base ;
- utiliser un ordre efficace des instructions ;
- exclure les fichiers inutiles ;
- démarrer en utilisateur non root ;
- injecter la configuration par environnement ;
- s'assurer que les logs vont vers la sortie standard ;
- faire écouter les services sur les interfaces accessibles dans leurs réseaux de conteneurs.

**Vérifications :**
- image construite depuis un environnement propre ;
- aucun secret ni donnée patient réelle dans l'image ;
- taille et contenu relevés ;
- démarrage en tant qu'utilisateur non privilégié ;
- l'application rejoint ses dépendances par nom de service et non par adresse IP fixe ;
- aucune dépendance au répertoire personnel d'un développeur.

**Livrables :** fichiers de construction, fichiers d'exclusion, inventaire des images et procédure de lancement isolé.

### Étape 9 — Composer l'infrastructure

**Objectif :** démarrer l'ensemble par une commande reproductible.

**Travail à faire :**
- écrire le fichier Compose ;
- déclarer les services, réseaux et volumes ;
- définir les dépendances de santé ;
- limiter les ressources si nécessaire ;
- ajouter les profils de simulation et de démonstration ;
- documenter les commandes de démarrage, arrêt, logs et remise à zéro ;
- intégrer les collecteurs de métriques uniquement si le périmètre d'exploitation les retient.

**Vérifications :**
- démarrage depuis une machine préparée ;
- arrêt et redémarrage sans perte des données persistées ;
- panne puis redémarrage d'un service ;
- aucun port inattendu publié ;
- accès réseau conforme à la matrice ;
- scénario médical de démonstration exécutable ;
- configuration identique à travers le dépôt, sans modification de code.

**Livrables :** fichier Compose, configurations, procédure d'installation et matrice de connectivité.

### Étape 10 — Vérifier l'infrastructure et préparer Metrics

**Objectif :** prouver que le déploiement est stable et établir sa configuration de référence.

**Travail à faire :**
- vérifier chaque healthcheck ;
- vérifier les réseaux autorisés et les interdictions ;
- mesurer temps de démarrage ;
- relever mémoire, CPU, stockage et consommation au repos ;
- rejouer les scénarios DEV ;
- vérifier persistance et reprise ;
- enregistrer les versions, images, volumes, limites et paramètres ;
- conserver un jeu de données identique pour les futures campagnes.

**Livrables :**
- matrice de connectivité remplie ;
- résultats des scénarios d'intégration ;
- fiche de configuration de référence ;
- mesures de base au repos ;
- procédure de reproduction.

## 5. Matrice de connectivité à remplir

| Depuis | Destination | Attendu | Résultat observé | Statut |
|---|---|---|---|---|
| Hôte | Point d'entrée | Autorisé sur le port prévu | À relever | |
| Hôte | Base de données | Refusé par défaut | À relever | |
| Proxy | Backend/API | Autorisé | À relever | |
| Proxy | Base de données | Refusé | À relever | |
| Backend | Base de données | Autorisé | À relever | |
| Simulateur | Ingestion | Autorisé | À relever | |
| Simulateur | Base de données | Refusé | À relever | |
| Collecteur metrics | Endpoints métriques | Autorisé selon le réseau de supervision | À relever | |

Adapter les lignes si le découpage final diffère. Une tentative interdite doit échouer parce que la route ou la règle réseau est absente, pas parce que le service cible est arrêté.

## 6. Erreurs à éviter

| Symptôme | Cause probable |
|---|---|
| Les mesures disparaissent après recréation | Stockage non monté sur un volume persistant |
| La base est accessible depuis l'hôte | Port publié inutilement |
| Le backend démarre puis s'arrête | Dépendance non prête ou stratégie de reconnexion absente |
| Les migrations ne sont pas exécutées | Confusion entre scripts d'initialisation et migrations versionnées |
| L'image contient des fichiers personnels | Fichier d'exclusion incomplet |
| L'image ne démarre pas sur une autre machine | Version d'image, architecture, secret ou variable implicite |
| Les mesures ne sont pas comparables | Images, paramètres ou données de départ non enregistrés |

## 7. Critères de sortie Docker

Docker est terminé lorsque :
- l'environnement peut être construit depuis le dépôt ;
- l'ensemble démarre et s'arrête par une procédure documentée ;
- les données persistantes survivent à la recréation des conteneurs ;
- les ports et réseaux respectent la topologie décidée ;
- les scénarios DEV passent dans Compose ;
- les versions et paramètres sont enregistrés ;
- la configuration de référence peut être restaurée pour Metrics.

La phase suivante est [Metrics.md](Metrics.md).
