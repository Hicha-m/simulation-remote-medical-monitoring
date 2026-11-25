# 05 — Préparation du rapport et de la soutenance

**Version :** 1.0 — **Date :** 25 novembre 2026  
**Équipe :** Hicham, Omar et Nawfel.  
**Échéance projet actuellement connue :** 8 janvier 2027.  
**Statut :** plan de préparation prévisionnel ; modalités officielles de rendu et de soutenance non communiquées.

## 1. Objectif et hypothèses de préparation

Même si les modalités ne sont pas encore connues, l'équipe doit se préparer à pouvoir présenter un dossier écrit et un oral de qualité.

**Hypothèse prudente de travail :** préparer :
- un rapport technique structuré décrivant le besoin, les choix d'architecture, la conception, la réalisation et les validations ;
- un support de présentation orale ;
- une démonstration reproductible du système ;
- des éléments de secours si la démonstration en direct échoue (captures, résultats et éventuellement vidéo courte).

Ces éléments constituent une préparation interne. Ils ne préjugent pas des livrables effectivement exigés, du format, du nombre de pages, de la durée de l'oral ou de la date de soutenance. Il faudra remplacer ces hypothèses par les consignes officielles dès qu'elles seront disponibles.

**Point de calendrier :** le 8 janvier 2027 est l'échéance projet connue. La date de soutenance peut être différente et reste inconnue. Le rapport et un support oral de base doivent être prêts à cette échéance dans notre planning prévisionnel ; si l'oral a lieu plus tard, le calendrier de répétition sera recalé sur la date réelle.

## 2. Modalités à confirmer

Dès que l'information sera disponible, consigner :

| Point | Modalité officielle | Source / date de confirmation |
|---|---|---|
| Date et heure de remise du projet | À confirmer | |
| Date et heure de la soutenance | À confirmer | |
| Rapport obligatoire ? | À confirmer | |
| Format du rapport (PDF, dépôt, modèle) | À confirmer | |
| Longueur ou limite de pages | À confirmer | |
| Plan imposé ou libre | À confirmer | |
| Langue du rapport | À confirmer | |
| Durée de présentation | À confirmer | |
| Durée des questions | À confirmer | |
| Présentation individuelle ou collective | À confirmer | |
| Participation orale attendue de chaque membre | À confirmer | |
| Démonstration en direct obligatoire ? | À confirmer | |
| Support accepté (PDF, slides, autre) | À confirmer | |
| Modalité de dépôt / nommage des fichiers | À confirmer | |
| Grille d'évaluation / critères | À confirmer | |

Ne pas inventer une durée, une pagination ou une date. En attendant, préparer un contenu modulaire qui pourra être raccourci ou détaillé.

## 3. Rapport : plan de travail proposé

Le plan ci-dessous est un squelette adaptable, pas un plan imposé.

1. **Résumé exécutif** — besoin traité, solution construite, résultats principaux et limites.
2. **Contexte et problématique** — monitorage hospitalier, acteurs, environnement et enjeux.
3. **Objectifs et périmètre** — fonctions incluses, exclusions, hypothèses et exigences.
4. **Analyse fonctionnelle** — cas d'utilisation, scénarios, rôles, données et critères d'acceptation.
5. **Étude des architectures possibles** — options envisagées, critères de comparaison, raisons du choix et alternatives non retenues.
6. **Architecture retenue / System Design** — vues logiques, déploiement, réseau, composants, flux, protocoles et frontières de confiance.
7. **Conception des données** — modèle de domaine, schéma, index, stratégie de stockage, horodatages, qualité et provenance.
8. **Réalisation** — composants développés, programmation réseau en Java, interface, ingestion, simulateurs et intégration.
9. **Sécurité et résilience** — authentification, autorisations, segmentation de démonstration, journalisation, pannes, reprise et limites.
10. **Conteneurisation et déploiement** — Docker, réseaux, volumes, configuration et procédure d'installation.
11. **Tests et résultats** — scénarios, environnement, métriques, résultats bruts synthétisés, limites et corrections.
12. **Discussion** — compromis, difficultés, décisions révisées et ce qui reste à faire.
13. **Conclusion et perspectives** — bilan par rapport aux objectifs.
14. **Bibliographie et annexes** — sources, dictionnaire de données, diagrammes détaillés, contrats, procédures et résultats complémentaires.

Ne pas transformer le rapport en journal chronologique de commits. Il doit expliquer le problème, les décisions, les preuves et les résultats. Le journal de développement reste une source de traçabilité.

## 4. Rédaction progressive : ce qu'il faut conserver dès maintenant

Le rapport ne doit pas être commencé le 5 janvier. Chaque phase produit immédiatement les éléments qui alimenteront le rapport :

| Phase | Éléments à rédiger / archiver |
|---|---|
| Cadrage | Contexte, objectifs, périmètre, exigences, acteurs, glossaire et sources |
| System Design | Diagrammes d'architecture, alternatives, critères, décision retenue et compromis |
| DEV | Modèle de données, contrats, captures d'écran, scénarios, tests et difficultés |
| Docker | Topologie, fichiers de configuration non secrets, procédure de lancement, volumes et healthchecks |
| Metrics | Protocole, configuration, données brutes, graphiques, p50/p95/p99, pertes, ressources et analyse |
| Stabilisation | Limites connues, bilan, procédure de démonstration, conclusion et annexes |

### Registre des preuves

Chaque résultat important doit être reproductible et rattaché à une version.

| ID | Élément | Preuve / emplacement | Version / date | Réutilisation dans le rapport |
|---|---|---|---|---|
| PRF-01 | Décision d'architecture | Lien vers ADR / cahier de décisions | | |
| PRF-02 | Diagramme système | Fichier source du diagramme | | |
| PRF-03 | Modèle de données | Diagramme et migrations | | |
| PRF-04 | Interface | Captures datées / version | | |
| PRF-05 | Tests fonctionnels | Rapport automatisé | | |
| PRF-06 | Réseau Java | Contrat, protocole, tests client/serveur | | |
| PRF-07 | Docker | Compose, healthchecks, procédure | | |
| PRF-08 | Performance | Résultats bruts et graphiques | | |
| PRF-09 | Résilience | Scénarios de panne et résultats | | |
| PRF-10 | Livraison | Version taguée, instructions et artefacts | | |

À conserver systématiquement : les sources citées, les versions logicielles, les paramètres de test, les captures utiles, les résultats bruts et les limites observées. Les secrets et les données personnelles réelles ne doivent jamais être intégrés aux annexes.

## 5. Soutenance : fil narratif proposé

La présentation doit raconter une histoire cohérente plutôt que parcourir les dossiers du dépôt.

1. **Le problème** — pourquoi un système de monitorage hospitalier doit recevoir et présenter des données de manière fiable.
2. **Le besoin retenu** — quels utilisateurs, quels appareils, quel périmètre et quels scénarios.
3. **Les choix de conception** — quelles architectures ont été comparées et pourquoi celle retenue convient au besoin.
4. **Le fonctionnement** — comment une mesure traverse le réseau Java, l'application, le stockage et arrive à la centrale.
5. **La fiabilité** — comment le système traite les mesures anciennes, les pertes, les erreurs d'association, les alarmes et les interruptions.
6. **La réalisation** — ce qui fonctionne réellement et ce qui a été conteneurisé.
7. **Les résultats** — ce qui a été testé, mesuré et démontré, avec les limites.
8. **Le bilan** — objectifs atteints, compromis, limites et évolutions possibles.

Le nombre de diapositives et le temps par partie seront adaptés à la durée officielle lorsqu'elle sera connue. Prévoir une version courte et une version détaillée du fil conducteur.

## 6. Démonstration reproductible

La démonstration doit prouver un parcours complet, pas seulement montrer une interface.

### Scénario principal candidat

1. Charger un jeu de données fictives et un environnement propre.
2. Présenter un patient, son séjour, son lit et le moniteur simulé associé.
3. Démarrer le simulateur et montrer la réception des mesures via le composant réseau Java.
4. Montrer l'actualisation des valeurs et, si retenu, d'une courbe.
5. Déclencher un événement d'alarme de simulation et montrer ses états successifs.
6. Provoquer un défaut technique ou une coupure réseau contrôlée.
7. Montrer que les données indisponibles ou périmées ne sont pas présentées comme actuelles.
8. Rétablir le flux, vérifier la reprise et consulter l'historique.

Les événements, seuils et profils doivent être explicitement simulés et ne doivent pas être présentés comme une conduite clinique validée.

### Préparation de la démonstration

- Un script écrit avec les commandes exactes et les résultats attendus.
- Un jeu de données déterministe et réinitialisable.
- Une version taguée de l'application.
- Une répétition sur une machine ou un environnement aussi proche que possible du jour J.
- Une vérification des ports, services, comptes de démonstration, écrans et données.
- Une procédure de retour à l'état initial.
- Des captures et résultats de secours.
- Une courte vidéo de secours uniquement si son usage est autorisé et utile.

Le jour de la présentation, aucune donnée personnelle réelle ni aucun secret ne doivent être visibles.

## 7. Préparation aux questions

Chaque membre doit comprendre le système global, même s'il a développé une partie particulière.

Thèmes à préparer :
- pourquoi cette architecture plutôt qu'une autre ;
- pourquoi cette topologie de déploiement et de réseau ;
- comment fonctionne la programmation réseau en Java ;
- comment les messages sont authentifiés, validés, ordonnés et dédupliqués ;
- comment sont gérés les patients, séjours, lits, appareils et sessions ;
- pourquoi le stockage et les index sont conçus ainsi ;
- comment les alarmes et leurs états sont gérés ;
- ce qui se passe lors d'une panne réseau, serveur ou base ;
- comment les performances ont été mesurées ;
- quelles limites empêchent de qualifier le système de dispositif médical réel.

Répondre avec des preuves et des limites explicites. Ne pas annoncer une performance non mesurée ni revendiquer une validation clinique.

## 8. Calendrier de préparation intégré au Gantt

| Date cible | Travail | Résultat attendu |
|---|---|---|
| 25–30 novembre | Créer le squelette du rapport et relever les modalités manquantes | Plan du rapport, liste de questions et registre des preuves |
| 1–7 décembre | Rédiger contexte, périmètre, exigences et premières décisions d'architecture | Premiers chapitres versionnés |
| 8–20 décembre | Alimenter conception détaillée, réalisation, réseau Java, données et tests | Rapport intermédiaire cohérent avec la version DEV |
| 21–28 décembre | Ajouter conteneurisation, déploiement et procédure d'installation | Chapitre Docker documenté |
| 29 décembre–4 janvier | Ajouter les protocoles de mesure, résultats Metrics et analyses | Chapitre validation et résultats |
| 5–6 janvier | Finaliser le rapport, vérifier sources, figures, annexes et cohérence | Version candidate complète du rapport |
| 4–6 janvier | Construire le support oral et préparer le fil de démonstration | Slides et conducteur ajustables |
| 7 janvier | Répéter l'oral et la démonstration de bout en bout ; préparer les réponses | Répétition complète et liste des corrections |
| 8 janvier | Vérifier et remettre le paquet de livraison selon les consignes disponibles | Rapport et supports prêts ; application et preuves archivées |

Si la soutenance est programmée après le 8 janvier, réutiliser le rapport et le support gelés comme base, puis prévoir une répétition finale proche de la date officielle.

## 9. Répartition de la préparation

La répartition n'est pas imposée dans ce document. Hicham, Omar et Nawfel doivent décider ensemble :
- qui coordonne la compilation du rapport ;
- qui vérifie les références, figures et annexes ;
- qui prépare le support oral ;
- qui pilote la démonstration technique ;
- comment chaque membre présente sa contribution et répond aux questions.

Le rapport et la soutenance restent des productions collectives : une seule personne ne doit pas être la seule à connaître le contenu global.

## 10. Historique des modalités et versions

| Date | Information reçue | Décision de l'équipe | Impact sur rapport / oral / planning |
|---|---|---|---|
| 25 novembre 2026 | Modalités non encore communiquées | Préparer un rapport technique, un support oral et une démonstration, sans figer le format | Réserver des tâches progressives dans le Gantt |
