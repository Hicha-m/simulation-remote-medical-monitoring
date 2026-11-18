# 03 — Planning Gantt générique — DEV → Docker → Metrics

**Version :** 2.0 — **Date de préparation :** 18 novembre 2026  
**Début :** 18 novembre 2026  
**Livraison :** vendredi 8 janvier 2027  
**Statut :** macro-planning générique, à réviser après le rendez-vous tuteur et la réunion des quatre membres.

## 1. Hypothèses de planification

- Le projet est une réalisation logicielle complète de monitorage hospitalier.
- Le flux fonctionnel cible relie des moniteurs de chevet à une ou plusieurs centrales de surveillance.
- La méthode est organisée en trois phases principales successives : DEV, Docker, Metrics.
- La CI/CD est transversale et commence dès DEV.
- Les choix précis de service, de charge et de technologies restent à valider.
- La période du 21 décembre au 4 janvier comprend les fêtes : les disponibilités doivent être recueillies et le planning révisé en conséquence.
- Le 8 janvier est réservé au rendu et à la démonstration, pas à du développement majeur.

Le planning de référence d'Intern comporte aussi un déploiement sur machines virtuelles entre DEV et Docker. Cette étape VM n'est pas incluse comme phase obligatoire dans notre organisation actuelle.

## 2. Gantt macro par phases

| Phase / activité | 18–29 nov. | 30 nov.–6 déc. | 7–13 déc. | 14–20 déc. | 21–27 déc. | 28 déc.–3 janv. | 4–8 janv. |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **DEV** — exigences, services et scénarios | █ | | | | | | |
| DEV — prototype d'interface et contrats | █ | █ | | | | | |
| DEV — données, modèle et persistance | ░ | █ | █ | | | | |
| DEV — ingestion, simulateurs et backend | | ░ | █ | █ | | | |
| DEV — interface centrale | | | █ | █ | | | |
| DEV — intégration et recette locale | | | ░ | █ | | | |
| **Docker** — images, volumes, réseaux | | | | ░ | █ | | |
| Docker — Compose, santé et installation | | | | ░ | █ | ░ | |
| Docker — vérification et référence | | | | | ░ | █ | |
| **Metrics** — instrumentation et plan de test | ░ | ░ | ░ | ░ | ░ | █ | |
| Metrics — étalonnage et campagnes | | | | | | █ | █ |
| Metrics — analyse et rapport | | | | | | ░ | █ |
| **CI/CD** — tests et qualité à chaque PR | █ | █ | █ | █ | █ | █ | █ |
| CI/CD — build images, scan et publication | | | | ░ | █ | █ | █ |
| **Livraison** — gel, documentation, démo | | | | | | ░ | █ |

L'instrumentation élémentaire (horodatages, logs structurés, compteurs) commence pendant DEV. La phase Metrics correspond à la préparation des campagnes, à leur étalonnage, à leur exécution et à l'analyse, pas au premier ajout de logs dans le code.

## 3. Diagramme Mermaid modifiable

Les dates sont indicatives. Les tâches sont volontairement regroupées à un niveau macro pour pouvoir les déplacer après validation du tuteur.

~~~mermaid
gantt
    title Monitorage hospitalier — livraison du 8 janvier 2027
    dateFormat YYYY-MM-DD
    axisFormat %d/%m

    section DEV
    Cadrage et exigences                  :a1, 2026-11-18, 2026-11-29
    Prototype UI et contrats              :a2, 2026-11-23, 2026-12-06
    Modèle de données et persistance      :a3, 2026-11-30, 2026-12-13
    Ingestion, simulateurs et backend     :a4, 2026-12-07, 2026-12-17
    Interface centrale                    :a5, 2026-12-07, 2026-12-17
    Intégration et recette locale         :a6, 2026-12-14, 2026-12-20

    section Docker
    Images et volumes                     :b1, 2026-12-18, 2026-12-23
    Réseaux et Compose                    :b2, 2026-12-21, 2026-12-26
    Vérification et installation          :b3, 2026-12-26, 2026-12-28

    section Metrics
    Plan de test et étalonnage            :c1, 2026-12-28, 2026-12-30
    Campagnes de charge et de reprise     :c2, 2026-12-30, 2027-01-03
    Analyse et rapport                    :c3, 2027-01-02, 2027-01-05

    section CI CD transversal
    CI tests et qualité                   :d1, 2026-11-18, 2027-01-08
    Build, scan et publication Docker     :d2, 2026-12-18, 2027-01-08

    section Livraison
    Gel et validation finale              :e1, 2027-01-05, 2027-01-07
    Rendu final                           :milestone, e2, 2027-01-08, 0d
~~~

## 4. Jalons et conditions de passage

| Jalon | Date cible | Résultat attendu | Condition de passage |
|---|---|---|---|
| M0 — Cadrage de départ | 22 nov. 2026 | Réponses du tuteur, disponibilités, responsabilités | Les contraintes bloquantes sont identifiées |
| M1 — Exigences v1 | 29 nov. 2026 | Services, population, fonctionnalités, données et parcours | Les fonctions obligatoires sont séparées des extensions |
| M2 — Conception v1 | 6 déc. 2026 | Maquettes, contrats de données, modèle métier et architecture | Interfaces entre les quatre chantiers validées |
| M3 — Socle intégré | 13 déc. 2026 | Base, backend et simulateur échangent un premier flux | Le flux conserve identité, provenance et horodatage |
| M4 — DEV terminé | 20 déc. 2026 | Application locale intégrée et recette fonctionnelle | Tests P0 passants, parcours principal démontrable |
| M5 — Docker terminé | 28 déc. 2026 | Compose reproductible, volumes et réseaux vérifiés | Même scénario DEV passe dans l'environnement conteneurisé |
| M6 — Metrics terminé | 5 janv. 2027 | Campagnes principales, résultats et analyse | Résultats reproductibles et limites identifiées |
| M7 — Gel final | 7 janv. 2027 | Version candidate, documentation, installation | Livraison répétée avec procédure vérifiée |
| M8 — Livraison | **8 janv. 2027** | Dépôt, application et démonstration | Tous les livrables demandés par le tuteur sont présents |

## 5. CI/CD transversal par niveau de maturité

| Période | Ce qui doit être automatisé |
|---|---|
| Dès le début de DEV | Format, compilation, tests unitaires, analyse statique, secrets et dépendances |
| Fin DEV | Tests API, contrats, migrations et scénario d'intégration |
| Docker | Construction des images, Compose up, healthchecks, tests de bout en bout et scan d'images |
| Metrics | Smoke tests automatiques ; campagnes de charge contrôlées séparées |
| Livraison | Artefact versionné, rapport de tests, documentation et procédure de retour arrière |

## 6. Répartition en quatre chantiers

| Chantier | Responsabilité dominante | Collaboration obligatoire |
|---|---|---|
| Domaine médical, données et simulateurs | Profils de mesures, datasets, waveforms, qualité et scénarios | Contrats avec backend, vérification de provenance |
| Backend, ingestion et réseau | Réception, sessions, traitement, événements, API | Modèle de données, tests et métriques |
| Base de données et sécurité | Persistance, migrations, identité, rôles, audit et sauvegarde | Contrats, backend et exploitation Docker |
| Interface centrale | Multi-patients, patient, courbes, alarmes et états système | Prototype, API et validation utilisateur |

Une responsabilité principale ne dispense pas de contribuer à l'intégration et à la revue de code.

## 7. Chemin critique

Validation périmètre → contrats métier et données → premier flux moniteur → centrale intégrée → recette locale → images et Compose → scénario conteneurisé → campagnes Metrics → livraison.

Les risques les plus importants sont :
- retard de validation du service et des fonctions ;
- contrats de données non stabilisés ;
- intégration tardive entre ingestion et interface ;
- indisponibilité de l'équipe pendant les fêtes ;
- données waveform trop volumineuses pour le stockage ou le rendu retenu ;
- campagnes Metrics non étalonnées ;
- absence de procédure de livraison reproductible.

## 8. Règles de pilotage

- Mettre à jour le planning chaque semaine.
- Affecter un responsable et un livrable vérifiable à chaque tâche.
- Faire une démonstration intégrée chaque semaine.
- Ne pas commencer Docker tant que la recette locale DEV n'est pas satisfaisante.
- Ne pas tirer de conclusion de performance avant d'avoir étalonné le protocole.
- Définir les seuils d'acceptation avant les campagnes, après validation de la charge cible.
- Geler les nouvelles fonctionnalités après le passage M4, sauf correction nécessaire.
- Réserver les 5 à 8 janvier à la stabilisation, la documentation et la livraison.

Les dates sont un mockup. Les durées doivent être recalculées avec la disponibilité réelle des quatre membres et la portée finale confirmée par le tuteur.
