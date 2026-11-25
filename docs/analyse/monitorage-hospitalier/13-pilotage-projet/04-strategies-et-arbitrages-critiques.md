# 04 — Stratégies et arbitrages critiques

**Version :** 1.1 — **Date :** 25 novembre 2026  
**Objectif :** lister les décisions qui peuvent modifier profondément la direction du projet et imposer une méthode mesurable pour les trancher.

## 1. Principe d'arbitrage

Quand plusieurs options sont raisonnables, l'équipe ne doit pas choisir uniquement par préférence personnelle ou familiarité avec une technologie.

Pour chaque décision :
1. Formuler le problème et les conséquences de chaque direction.
2. Éliminer les options interdites par le tuteur, la consigne ou la sécurité.
3. Définir un jeu de test représentatif.
4. Définir les métriques et leur méthode de calcul **avant** l'expérience.
5. Faire un essai comparable sur le même matériel et les mêmes entrées.
6. Relever les résultats bruts, les limites et le temps d'implémentation.
7. Choisir en fonction des critères pondérés et des exigences non négociables.
8. Enregistrer la décision et les raisons de ne pas choisir les autres options.

Une option qui échoue à un critère bloquant de sûreté ou d'intégrité ne doit pas être sauvée par une bonne note sur la vitesse ou la facilité de développement.

## 2. Matrice des décisions qui orientent le projet

| ID | Situation à décider | Direction A | Direction B | Direction C | Ce que ce choix change |
|---|---|---|---|---|---|
| DEC-01 | Périmètre des services | Un service complet | Deux ou trois services reliés | Plusieurs services de l'établissement | Profils médicaux, modèle d'organisation, nombre de centrales, charge, workflows |
| DEC-02 | Nature des données | Valeurs numériques | Valeurs + quelques courbes | Flux multiparamétriques haute résolution | Réseau, stockage, rendu, synchronisation, charge et compétences requises |
| DEC-03 | Source des données | Synthétiques | Datasets réels rejoués | Hybride réel + scénarios synthétiques | Fidélité, droits d'accès, variabilité, reproductibilité, scénarios de panne |
| DEC-04 | Répartition des langages | Java partout | Réseau Java + backend/UI dans un autre langage | Réseau Java + architecture multi-langages | Compétences, intégration, contrats inter-langages, maintenance, déploiement et performance |
| DEC-05 | Architecture logicielle | Monolithe modulaire | Services séparés | Architecture distribuée événementielle | Déploiement, complexité réseau, robustesse, intégration |
| DEC-06 | Interface | Desktop | Web | Hybride / plusieurs clients | Accessibilité, distribution, multi-postes, latence d'affichage |
| DEC-07 | Communication | TCP/WebSocket direct | Broker MQTT/AMQP | gRPC / flux spécialisés | Latence, débit, garantie de livraison, reprise, observabilité |
| DEC-08 | Stockage | SQL relationnel | Base temporelle/document | Hybride SQL + stockage waveform | Requêtes métier, ingestion, volume, historique, cohérence |
| DEC-09 | Calcul des alarmes | Au moniteur simulé | Centralisé au serveur | Hybride | Provenance, cohérence, disponibilité, charge, fidélité au workflow |
| DEC-10 | Gestion qualité | Flags source uniquement | Indicateur qualité dérivé | Source + qualité calculée et versionnée | Fidélité, complexité, faux classement et explicabilité |
| DEC-11 | Gestion des pannes | Détection seule | Buffer local puis rejeu | Redondance / mécanisme distribué | Perte, doublons, délai de reprise, complexité |
| DEC-12 | Données patient | Contexte minimal | Contexte clinique de scénario | Intégration simulée de type DPI/ADT | Modèle, identitovigilance, sécurité, périmètre réglementaire |

Ces options ne sont pas toutes mutuellement exclusives. La décision doit être prise pour un cas d'usage défini.

## 3. Protocole comparatif : métriques communes

| Dimension | Mesure | Comment calculer |
|---|---|---|
| Latence de mesure | Latence source → affichage | `displayedAt - observedAt`, distribution médiane/p95/p99 |
| Latence d'alarme | Source → notification | `notifiedAt - alarmCreatedAt` |
| Débit | Messages/s, échantillons/s et octets/s | Compteur reçu sur fenêtre temporelle, en distinguant valeurs et samples |
| Pertes | Taux de messages/samples manquants | Séquences attendues non reçues / séquences attendues |
| Doublons | Taux de messages dupliqués | MessageId déjà traité / messages reçus |
| Désordre | Événements reçus hors ordre | Écart entre séquence source et ordre d'arrivée |
| Reprise | Délai de récupération | Retour à un flux nominal après restauration du composant |
| Fidélité waveform | Écart source ↔ signal relu | Nombre d'échantillons, checksum, erreur numérique et alignement |
| Stockage | Volume par patient-heure | Octets persistés / durée de monitorage |
| Ressources | CPU, mémoire, I/O | Mesures système durant le même scénario |
| Interface | Fluidité et délai rendu | Temps de rendu, taux de rafraîchissement, blocages observés |
| Développement | Temps d'intégration | Heures entre début de tâche et intégration testée |
| Maintenabilité | Couplage et changements | Nombre de modules touchés pour une évolution et temps de changement |
| Fiabilité métier | Résultat des scénarios P0 | Tests réussis / tests P0, avec liste des échecs |

Les valeurs cibles ne sont pas inventées dans ce document. Elles seront proposées par l'équipe, justifiées par les besoins, puis confrontées à une mesure de référence.

## 4. Arbitrages de direction détaillés

### DEC-01 — Un service ou plusieurs services ?

**Question :** faut-il livrer un service de référence complet ou une petite architecture multi-services ?

- A : un service unique en profondeur. On couvre admission, affectation, surveillance, alarme, relève, transfert et sortie dans un service.
- B : deux services liés par un transfert et des centrales distinctes ou partagées.
- C : établissement multi-services avec plusieurs profils.

**Essai à réaliser :**
- implémenter sur maquette les parcours d'un service ;
- ajouter un second profil de service et un transfert ;
- mesurer l'effort d'ajout et les différences de configuration.

**Métriques :** nombre de cas métier couverts, nombre de règles spécifiques par service, temps d'ajout d'un service, réutilisation du modèle, erreurs d'affectation, complexité de test.

**Bascule de direction :** si ajouter un second service impose de modifier les objets centraux ou de dupliquer la logique, le modèle initial n'est pas suffisamment extensible. Ne pas conclure qu'il faut développer tous les services : choisir la profondeur exigée au rendu.

### DEC-02 — Valeurs numériques ou courbes haute résolution ?

- A : valeurs numériques et tendances uniquement.
- B : quelques courbes représentatives (ECG et PPG, par exemple).
- C : plusieurs flux haute résolution simultanés.

**Essai :** rejouer le même patient et la même période avec un, puis plusieurs signaux ; mesurer les performances sur une machine de référence.

**Métriques :** samples/s, octets/s, volume patient-heure, CPU, mémoire, pertes, latence p95, temps de rendu et fidélité du signal.

**Bascule :** si le système ne tient pas la charge, tester d'abord l'envoi par blocs, le tampon circulaire, la fenêtre d'affichage et le stockage séparé des signaux avant d'abandonner les courbes.

### DEC-03 — Génération ou rejeu de données réelles ?

- A : génération synthétique déterministe.
- B : rejeu de bases de recherche publiques dé-identifiées.
- C : hybride : rejeu réel pour la physiologie et événements synthétiques pour les scénarios/artefacts/pannes.

**Essai :** même scénario fonctionnel alimenté par les trois approches, avec un jeu de cas documenté.

**Métriques :** diversité des formes observées, reproductibilité, couverture des situations limites, temps de préparation, facilité d'annotation, respect des licences et capacité à injecter des événements contrôlés.

**Bascule :** si un dataset ne permet pas de créer une condition précise ou si ses conditions de réutilisation ne conviennent pas, le garder comme source de référence et créer un scénario synthétique clairement identifié. Ne jamais modifier la source réelle sans conserver la version originale.

### DEC-04 — Programmation réseau Java et liberté technologique du reste

**Options :**
Contrainte non négociable : la programmation réseau est réalisée en Java. Les choix suivants concernent le reste de l'application :
- A : Java pour la majorité des composants, y compris backend et interface JavaFX.
- B : composant réseau Java, backend métier Java, interface web TypeScript.
- C : composant réseau Java, backend métier dans un autre langage, outils de rejeu/traitement Python, interface web.
- D : architecture multi-langages, avec contrats/API documentés autour du composant réseau Java.

**Essai :** réaliser le même vertical slice minimal : un client émet une mesure, serveur reçoit et persiste, UI affiche.

**Métriques :** délai de développement, latence p95, débit, consommation, simplicité de déploiement, couverture de tests, intégration entre langages et facilité de reprise par les trois membres.

**Bascule :** une stack plus rapide à prototyper n'est pas forcément meilleure si elle complique les tests ou la livraison. Une contrainte académique de Java prévaut sur le benchmark.

### DEC-05 — Monolithe modulaire ou services distribués ?

- A : monolithe modulaire avec composants séparés par interfaces.
- B : backend découpé en services indépendants.
- C : architecture orientée événements avec broker et services spécialisés.

**Essai :** comparer un même scénario multi-moniteurs avec démarrage, panne, redémarrage et évolution d'un module.

**Métriques :** temps de déploiement, latence, nombre de dépendances opérationnelles, comportement en cas de panne, facilité de test, temps de diagnostic, ressources consommées.

**Bascule :** si les services distribués ajoutent davantage de configuration et de pannes qu'ils n'en résolvent sur la charge cible, privilégier un monolithe modulaire ; garder les contrats d'événements pour une évolution future.

### DEC-06 — Desktop ou interface web ?

- A : application desktop (JavaFX/Swing ou équivalent).
- B : interface web servie par le backend.
- C : application web avec vues distinctes pour centrale et administration.

**Essai :** implémenter le même écran multi-lits et le même panneau de courbe sur une machine cible.

**Métriques :** délai de rendu, fluidité lors des mises à jour, temps d'installation, nombre de postes supportés, accès simultané, ergonomie clavier/souris et temps de déploiement.

**Bascule :** si plusieurs postes doivent consulter simultanément la centrale, mesurer le coût de déploiement d'une UI web ; si l'interface doit fonctionner hors navigateur ou sur machine dédiée, vérifier le besoin desktop.

### DEC-07 — Protocole direct ou broker ?

- A : TCP/WebSocket entre simulateurs et serveur.
- B : MQTT ou broker de messages.
- C : gRPC ou protocole spécialisé pour flux structurés.
- D : séparation : REST pour administration, flux temps réel dédié pour monitorage.

**Essai :** injecter exactement le même débit et les mêmes coupures pour chaque protocole candidat.

**Métriques :** latence p95/p99, throughput, CPU, pertes, doublons, ordre, reconnexion, backpressure, complexité d'authentification et facilité de diagnostic.

**Bascule :** le meilleur protocole n'est pas seulement celui avec la latence la plus faible : il doit assurer l'intégrité et la reprise nécessaires au scénario.

### DEC-08 — Stockage relationnel, temporel ou hybride ?

- A : base relationnelle pour tout.
- B : base temporelle pour mesures + relationnel pour patients et appareils.
- C : relationnel pour métier et alarmes + fichiers/blocs dédiés aux waveforms.

**Essai :** charger le même jeu de données, puis exécuter les mêmes requêtes : patient, période, paramètre, alarmes, dernières valeurs, transfert et affichage de courbe.

**Métriques :** temps d'ingestion, p95 des requêtes, volume patient-heure, coût des index, CPU, mémoire, sauvegarde/restauration et complexité des migrations.

**Bascule :** choisir le plus simple qui atteint les volumes et requêtes du cahier des charges. Un stockage hybride n'est retenu que si le benchmark justifie la séparation.

### DEC-09 — Où créer les alarmes ?

- A : le moniteur simulé crée et transmet les alarmes, la centrale les affiche et les route.
- B : le serveur calcule les alarmes à partir des observations.
- C : hybride : alarmes natives simulées côté moniteur et alarmes système côté serveur.

**Essai :** rejouer une trace annotée avec plusieurs défauts de signal, plusieurs moniteurs et une coupure réseau.

**Métriques :** délai de détection, délai d'affichage, duplications, pertes, traçabilité de la source, comportement lors d'une panne serveur et cohérence des états.

**Bascule :** aucune règle centrale ne doit être présentée comme une règle clinique validée si elle est construite pour la simulation. La provenance de chaque alarme doit rester visible.

### DEC-10 — Qualité source ou indicateur calculé ?

- A : conserver uniquement le flag qualité de la source.
- B : calculer un indicateur de qualité à partir du signal.
- C : conserver les deux et afficher la provenance de l'indice calculé.

**Essai :** utiliser des segments avec et sans artefacts et, lorsqu'ils existent, des annotations de référence.

**Métriques :** taux de fausse classification GOOD, sensibilité de détection, faux rejets, latence de calcul, coût CPU et explicabilité.

**Bascule :** sans vérité terrain annotée, ne pas prétendre qu'un SQI calcule la qualité clinique ; le présenter comme expérimental et non décisionnel.

### DEC-11 — Perte réseau, panne serveur ou base indisponible

Stratégies possibles :
- A : détection seule, données manquantes signalées.
- B : buffer local et retransmission après reconnexion.
- C : persistance locale durable puis rattrapage avec déduplication.
- D : redondance de composants, si le périmètre la justifie.

**Essais séparés :** couper le réseau, arrêter le serveur, arrêter la base, redémarrer un client, saturer le buffer, renvoyer des messages retardés.

**Métriques :** données perdues, doublons, retard de rattrapage, durée de panne visible, mémoire occupée, ordre restauré, temps de reprise et cohérence des alarmes.

**Bascule :** si le buffer en mémoire perd des données au redémarrage, tester un spool durable. Si la reprise crée des doublons, renforcer les identifiants idempotents et les séquences. Ne pas afficher « nominal » tant que le flux n'est pas effectivement rétabli.

### DEC-12 — Données patient minimales ou intégration plus riche ?

- A : patient fictif + séjour + unité + lit + session.
- B : ajouter contexte clinique minimal pour les profils/scénarios.
- C : simuler une intégration ADT/DPI et des identités selon les concepts INS/RNIV.

**Essai :** créer plusieurs séjours, transferts, collisions d'identité et changements d'unité.

**Métriques :** taux d'association correcte, erreurs de patient, temps de création/affectation, champs indispensables réellement utilisés, complexité de sécurité et nombre de flux externes.

**Bascule :** si les fonctions de monitorage n'ont pas besoin des données cliniques détaillées, ne pas construire un DPI miniature. Garder le contexte nécessaire au bon patient, bon séjour, bon lit, bon appareil et bon profil.

## 5. Stratégies face aux situations critiques

| Situation critique | Stratégie A | Stratégie B | Stratégie C | Mesures qui départagent |
|---|---|---|---|---|
| Mauvaise association patient/appareil | Refuser toute donnée incohérente | Quarantaine et résolution manuelle | Validation à deux étapes avant activation | Faux rattachements (objectif : zéro), taux de quarantaine, temps de résolution, erreurs de transfert |
| Appareil silencieux | Détection par timeout fixe | Timeout spécifique par profil | Heartbeat + état de session + qualité de flux | Délai de détection, faux hors-ligne, coût trafic, robustesse aux cadences variables |
| Mesure ancienne reçue après une nouvelle | Rejeter pour mise à jour courante, conserver l'historique | Mettre en file et ordonner par temps source | Fenêtre de réordonnancement bornée | Valeur courante correcte, latence ajoutée, retard accepté, événements perdus |
| Signal de mauvaise qualité | Afficher la valeur avec avertissement | Marquer suspect/invalide selon flags source | Ajouter un SQI versionné | Faux GOOD, faux rejet, coût CPU, explicabilité |
| Rafale d'alarmes | Afficher toutes, triées par priorité | Agréger visuellement sans supprimer l'historique | Regrouper les répétitions avec lien vers les événements source | Alarmes critiques visibles, temps de perception simulé, nombre de notifications, événements perdus |
| Alarme non acquittée | Persistance visuelle | Escalade temporisée | Escalade selon affectation/équipe et calendrier | Délai d'escalade, livraison, doublons, alarmes orphelines |
| Centrale indisponible | État dégradé visible, surveillance locale simulée | Seconde centrale de relève | Buffer et rattrapage après reprise | Continuité locale, délai de reprise, perte, cohérence des alarmes |
| Base indisponible | Mise en échec explicite | File en mémoire | Journal local durable puis reprise | Perte au redémarrage, taille file, retard de rattrapage, doublons |
| Transfert pendant une alarme | Maintenir alarme liée au patient | Transfert de session et de routage | Transition coordonnée avec double visibilité temporaire | Alarme non perdue, absence d'ancien rattachement, durée transition |
| Charge waveform trop élevée | Réduire fréquence d'affichage, pas le brut stocké | Stocker par blocs et lire à la demande | Séparer flux temps réel et archive | Échantillons perdus, latence d'écran, volume, mémoire, erreur du signal affiché |
| Identité inconnue ou ambiguë | Rejeter du flux patient | Quarantaine d'identité | Procédure de rapprochement manuelle auditée | Zéro association arbitraire, délai résolution, qualité de traçabilité |
| Utilisateur sans habilitation | Refus côté serveur | Refus + journalisation + alerte sécurité | Limitation/révocation après tentatives répétées | Requêtes non autorisées réussies (objectif : zéro), faux blocages, qualité des logs |

Le choix doit aussi intégrer la réalité métier et la validation du tuteur. Les métriques de performance ne remplacent jamais les critères P0 d'intégrité et de sûreté.

## 6. Méthode de scoring avant choix

L'équipe et le tuteur fixent les poids avant le comparatif.

| Critère | Poids (à fixer) | Note option A (1–5) | Note option B (1–5) | Note option C (1–5) | Preuve / mesure |
|---|---:|---:|---:|---:|---|
| Réponse au besoin métier | | | | | |
| Intégrité et sûreté | | | | | |
| Latence / débit | | | | | |
| Fiabilité / reprise | | | | | |
| Facilité d'intégration à trois | | | | | |
| Simplicité de déploiement | | | | | |
| Maintenabilité / évolution | | | | | |
| Coût de réalisation dans le délai | | | | | |

Une note élevée n'annule pas un échec à une exigence bloquante.

## 7. Fiche de décision à copier pour chaque arbitrage

### [DEC-XX] — [Titre de la décision]

- **Date :**
- **Responsable de l'étude :**
- **Décideurs / validation :**
- **Question exacte :**
- **Pourquoi cette décision change la direction du projet :**
- **Options comparées :**
- **Contraintes non négociables :**
- **Jeu de test / scénario utilisé :**
- **Configuration matérielle et logicielle :**
- **Métriques choisies avant test :**
- **Résultats bruts (lien vers logs/rapport) :**
- **Limites et biais de l'expérience :**
- **Option retenue :**
- **Justification mesurée :**
- **Compromis acceptés :**
- **Options rejetées et raisons :**
- **Conséquences sur planning, données, API et équipe :**
- **Date de réévaluation si hypothèse invalidée :**

## 8. Ordre de priorité des arbitrages

| Ordre | Décision | Date cible du Gantt | Pourquoi |
|---|---|---|---|
| 1 | Services, population, fonctionnalités | 29 nov. 2026 | Fixe le domaine métier et la charge. |
| 2 | Paramètres, courbes, sources de données | 29 nov. 2026 | Fixe les débits, le stockage et les simulateurs. |
| 3 | Contrats patient/appareil/observation/alarme | 6 déc. 2026 | Bloque ou débloque tous les développements parallèles. |
| 4 | Java, UI, protocole et architecture | 6 déc. 2026 | Oriente les compétences, les outils et le déploiement. |
| 5 | Stockage et stratégie qualité | 13 déc. 2026 | Détermine les performances et la fidélité des données. |
| 6 | Routage, escalade et mode dégradé | 13 déc. 2026 | Détermine le workflow humain et les tests critiques. |

