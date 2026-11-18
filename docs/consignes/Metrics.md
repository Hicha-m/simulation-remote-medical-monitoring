# METRICS — Instrumentation, campagnes et analyse du monitorage

**Périmètre :** étapes 11 à 14.  
**Prérequis :** application conteneurisée, scénarios reproductibles, données de référence et configuration Docker enregistrées.

## 1. Contexte et objectif

Cette phase ne doit pas seulement répondre à « combien de requêtes par seconde le serveur accepte-t-il ? ». Pour un système de monitorage, elle doit établir jusqu'à quelle charge les mesures et les alarmes restent reçues, associées, persistées et affichées correctement.

La mesure doit couvrir quatre dimensions complémentaires :
1. performance applicative et réseau ;
2. fidélité et intégrité des données physiologiques ;
3. continuité du workflow d'alarme ;
4. ressources et disponibilité de l'infrastructure.

Une interface rapide qui perd des échantillons ou mélange deux patients n'est pas performante. Les critères d'intégrité et de sûreté sont des conditions bloquantes indépendantes du débit.

## 2. Familles de mesures

### 2.1 Latence de bout en bout

Conserver les horodatages nécessaires pour mesurer :

- observation source → réception de l'ingestion ;
- réception → persistance ;
- réception → publication vers la centrale ;
- source → affichage ;
- création d'alarme → réception par la centrale ;
- création d'alarme → notification du destinataire ;
- prise de connaissance simulée → affichage du nouvel état.

Pour chaque mesure, relever médiane, p90, p95 et p99, pas uniquement moyenne. Vérifier la synchronisation des horloges entre les composants ; à défaut, mesurer les durées avec une horloge monotone locale et documenter les limites de comparaison inter-machines.

### 2.2 Débit

Ne pas confondre les unités :
- observations numériques par seconde ;
- échantillons waveform par seconde ;
- messages par seconde ;
- événements d'alarme par seconde ;
- octets entrants/sortants par seconde ;
- patients et appareils actifs simultanément.

Le débit dépend fortement du nombre de canaux, de leur fréquence d'échantillonnage, du format et du regroupement des échantillons par message.

### 2.3 Intégrité et fidélité

Mesurer au minimum :
- messages reçus, acceptés, rejetés et mis en quarantaine ;
- messages perdus, dupliqués et reçus hors ordre ;
- séquences d'échantillons manquantes ;
- écart entre nombre d'échantillons émis et persistés ;
- checksums des fichiers/segments source et archivés lorsque la conservation binaire est attendue ;
- erreur numérique de reconstruction lorsqu'une conversion ou un rééchantillonnage est effectué ;
- association correcte patient / séjour / lit / appareil / session ;
- valeurs anciennes qui auraient remplacé la dernière valeur connue ;
- données passées à STALE sans être présentées comme actuelles.

Ne jamais conclure à la fidélité d'une waveform à partir d'une simple capture graphique.

### 2.4 Workflow d'alarme

Mesurer :
- alarmes générées, reçues et affichées ;
- taux de livraison des notifications ;
- latence source → centrale et source → destinataire ;
- alarmes non acquittées ;
- temps simulé avant acquittement ;
- nombre et latence des escalades ;
- alarmes acquittées mais encore actives ;
- erreurs de rattachement à un patient ou un lit ;
- doublons et pertes de transitions d'état.

Les délais de réaction simulés servent à mesurer le logiciel et le scénario, pas à définir un délai de soin réel.

### 2.5 Infrastructure

Mesurer par composant :
- CPU ;
- mémoire ;
- entrées/sorties et latence disque ;
- volume de stockage et croissance par patient-heure ;
- nombre de connexions à la base ;
- taille des files et retard de consommation ;
- redémarrages ;
- durée de disponibilité ;
- temps de démarrage et de restauration.

Les métriques métier et les métriques d'infrastructure doivent être alignées temporellement afin d'identifier le composant qui devient le goulot.

## 3. Outils possibles

Le choix dépend des flux réellement retenus ; aucun outil ne doit être sélectionné uniquement parce qu'il est déjà connu.

| Besoin | Outils candidats | Particularité |
|---|---|---|
| Injection de requêtes HTTP | Apache JMeter, k6, Gatling | Adaptés aux API et parcours HTTP ; assertions nécessaires sur contenu et résultat fonctionnel. |
| Rejeu de waveforms | Adaptateur/replayer dédié au dataset, client simulateur | Doit respecter cadence, nombre d'échantillons, horodatages et canaux ; une charge HTTP générique ne suffit pas. |
| Métriques techniques | Prometheus, OpenTelemetry, métriques du moteur de conteneurs | Collecter les services et l'infrastructure avec des labels maîtrisés. |
| Visualisation | Grafana ou rapports générés | Aligner la fenêtre de charge avec les métriques et événements. |
| Traces distribuées | OpenTelemetry et backend compatible | Utile pour relier ingestion, traitement, base et publication. |
| Analyse waveform | Python/NumPy/SciPy ou outils du format source | Comparaison numérique des signaux, pas seulement visuelle. |

Le protocole définit d'abord la charge et les mesures ; l'outil est choisi ensuite. JMeter peut tester les parcours API et les actions de gestion, mais un injecteur de waveforms doit préserver la cadence et le format des données.

## 4. Scénarios de campagnes

| ID | Campagne | Objectif |
|---|---|---|
| MET-01 | Référence faible charge | Vérifier les latences et ressources de base avec peu de patients. |
| MET-02 | Charge nominale | Représenter le nombre de patients, moniteurs, utilisateurs et canaux validé par le tuteur. |
| MET-03 | Montée progressive | Identifier le point où le débit n'augmente plus ou la latence se dégrade. |
| MET-04 | Pic d'activité | Simuler démarrages simultanés, nombreuses mesures ou rafale d'alarmes. |
| MET-05 | Longue durée | Détecter fuite mémoire, croissance de stockage et dérive des files. |
| MET-06 | Reconnexion après panne réseau | Mesurer perte, rattrapage, doublons et temps de retour à un état nominal. |
| MET-07 | Redémarrage d'un service | Vérifier reprise des flux et continuité des données persistées. |
| MET-08 | Base indisponible | Mesurer comportement, buffer, erreurs et reprise après restauration. |
| MET-09 | Charge waveform | Tester échantillons/s, débit binaire, rendu et persistance. |
| MET-10 | Alarmes simultanées | Tester affichage, routage, ordonnancement et transitions d'état. |
| MET-11 | Plusieurs services / centrales | Mesurer isolation et agrégation si le périmètre multi-services est retenu. |
| MET-12 | Campagne de sécurité contrôlée | Vérifier refus d'identifiants inconnus et absence d'accès non autorisé sous charge. |

Le nombre de patients, de moniteurs, de canaux, les cadences et les durées doivent venir de la réponse du tuteur ou d'une hypothèse explicitement écrite. Ne pas inventer une charge clinique de référence.

## 5. Protocole de mesure reproductible

### Étape 11 — Préparer le plan de test

**Objectif :** construire un scénario qui exerce l'application et détecte ses propres erreurs.

**Travail à faire :**
- figer le dataset ou la graine de génération ;
- définir le nombre de patients, moniteurs, canaux et utilisateurs ;
- préciser la cadence de chaque paramètre ;
- décrire le scénario nominal et les événements injectés ;
- ajouter des assertions sur les réponses et sur les données finales ;
- enregistrer les identifiants de campagne et de scénario ;
- vérifier qu'un scénario attendu en échec est bien détecté.

**Livrables :** plans de test, manifests de données, paramètres de charge et validation d'une exécution simple.

### Étape 12 — Étalonner l'instrument et le protocole

**Objectif :** s'assurer que l'injecteur, les horloges et les collecteurs ne deviennent pas eux-mêmes le facteur limitant.

**Travail à faire :**
- mesurer la capacité de l'injecteur sur une cible simple ;
- vérifier CPU et mémoire de l'injecteur ;
- vérifier la synchronisation temporelle des hôtes ;
- fixer les paliers, la rampe et la durée des fenêtres stables ;
- faire au moins deux exécutions de contrôle avec paramètres identiques ;
- mesurer la variabilité entre exécutions ;
- documenter les outils, versions, machines et tâches de fond.

**Livrables :** rapport d'étalonnage, paliers retenus, fenêtres de mesure, variabilité et limites.

### Étape 13 — Exécuter les campagnes

**Objectif :** obtenir les résultats clients, métiers et infrastructures sur des scénarios identiques.

**Travail à faire :**
- démarrer une configuration de référence ;
- réinitialiser le dataset et les files selon une procédure maîtrisée ;
- vérifier la santé des composants ;
- lancer les paliers et campagnes ;
- relever en parallèle les métriques de chaque composant ;
- conserver les événements d'injection de panne ;
- enregistrer les fichiers bruts, logs et configuration ;
- répéter les essais représentatifs.

**Livrables :** fichiers de résultats bruts, tableaux de métriques, journaux, configuration complète et incidents observés.

### Étape 14 — Analyser et conclure

**Objectif :** identifier les limites, les goulots d'étranglement et les compromis.

**Travail à faire :**
- tracer débit en fonction de la charge ;
- tracer p50/p95/p99 ;
- tracer taux de perte, doublons et erreurs ;
- rapprocher les courbes des ressources CPU, mémoire, disque et files ;
- identifier le premier composant saturé ;
- comparer la charge nominale à la capacité observée ;
- vérifier les résultats anormalement bons ou mauvais ;
- expliquer ce que les mesures ne permettent pas de conclure.

**Livrables :** tableaux et graphiques, rapport comparatif, goulots d'étranglement identifiés et plan d'amélioration priorisé.

## 6. Conditions équitables de comparaison

Comparer deux campagnes seulement si :
- même version applicative ;
- même dataset, mêmes graines et scénarios ;
- mêmes nombres de patients, moniteurs, canaux et utilisateurs ;
- mêmes cadences et durées ;
- même configuration de ressources, ou différence explicitement étudiée ;
- mêmes versions et paramètres pertinents ;
- même protocole de remise à zéro ;
- injecteur non saturé ;
- résultats bruts conservés.

Une différence de configuration volontaire doit être le sujet de l'expérience, et pas une variable oubliée.

## 7. Tableaux à remplir

### Résumé par palier

| Campagne | Patients | Moniteurs | Débit observations/s | Débit samples/s | Latence p95 affichage | Perte samples | CPU max | RAM max | Statut |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---|
| MET-01 | | | | | | | | | |
| MET-02 | | | | | | | | | |
| MET-03 | | | | | | | | | |

### Résumé alarmes

| Campagne | Alarmes émises | Reçues | Affichées | Perdues | Latence p95 source→centrale | Escalades | Erreurs d'association |
|---|---:|---:|---:|---:|---:|---:|---:|
| MET-10 | | | | | | | |

### Résumé reprise

| Incident | Données perdues | Doublons | Durée indisponible | Temps de rattrapage | Retour nominal vérifié |
|---|---:|---:|---:|---:|---|
| Réseau coupé | | | | | |
| Backend redémarré | | | | | |
| Base indisponible | | | | | |

## 8. Critères de validité des campagnes

Une campagne n'est pas exploitable si :
- l'injecteur est saturé ;
- le dataset ou la configuration ne sont pas connus ;
- les compteurs d'émission et de réception sont incohérents sans explication ;
- les assertions ne détectent pas les erreurs fonctionnelles ;
- la fenêtre de montée est mélangée à la fenêtre stable sans distinction ;
- les ressources mesurées ne correspondent pas à la période de charge ;
- les résultats bruts manquent ;
- le même scénario ne peut pas être rejoué.

Les seuils d'acceptation seront définis après le dimensionnement et les premières mesures de référence. Les tests d'intégrité critiques (zéro mélange de patients, absence de fausse valeur actuelle, aucune alarme perdue dans les scénarios retenus) sont des exigences métier à part entière et ne se négocient pas contre un gain de débit.

## 9. Structure conseillée pour les résultats

Créer un répertoire séparé des sources de données et du code applicatif :

- plans ;
- manifests de campagnes ;
- données d'entrée ou références de dataset ;
- résultats bruts ;
- métriques d'infrastructure ;
- journaux ;
- graphiques ;
- rapports et conclusions.

Chaque nom de fichier doit indiquer l'identifiant de campagne, le scénario, le nombre de sources et la date. Les données brutes ne doivent pas être remplacées par un tableau de synthèse.

## 10. Critères de sortie Metrics

La phase est terminée lorsque :
- les campagnes principales sont reproductibles ;
- les résultats bruts sont conservés ;
- la capacité à charge nominale est décrite ;
- les latences p50/p95/p99 sont calculées ;
- pertes, doublons, désordre et erreurs d'association sont mesurés ;
- les alarmes et leurs délais de transmission sont évalués ;
- les scénarios de panne et de reprise ont des résultats ;
- les ressources et goulots d'étranglement sont identifiés ;
- les limites de l'expérience sont explicites.

Metrics ne démontre pas une aptitude à l'usage clinique ni une disponibilité hospitalière certifiée : il documente les performances du logiciel et de l'environnement évalués.
