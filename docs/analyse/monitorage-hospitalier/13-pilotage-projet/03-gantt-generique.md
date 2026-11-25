# 03 — Planning Gantt — DEV → Docker → Metrics

**Version :** 2.1 — **Date de mise à jour :** 25 novembre 2026  
**Équipe :** Hicham, Omar et Nawfel (3 personnes).  
**Début du planning recalé :** mercredi 25 novembre 2026.  
**Livraison :** vendredi 8 janvier 2027.  
**Statut :** planning de référence révisé ; charge individuelle et modalités de soutenance encore à confirmer.

## 1. Hypothèses de planification

- Le projet est une réalisation logicielle complète de monitorage hospitalier.
- Le flux fonctionnel cible relie des moniteurs de chevet à une ou plusieurs centrales de surveillance.
- L'équipe est composée de trois personnes : Hicham, Omar et Nawfel.
- Le tuteur laisse le choix du périmètre fonctionnel et des technologies à l'équipe, sans autre limite communiquée à ce stade.
- **La programmation réseau doit être réalisée en Java.** Cela n'impose pas Java à toute l'application : les autres composants restent libres, sous réserve d'interfaces compatibles et documentées.
- La méthode est organisée en trois phases principales successives : DEV, Docker, Metrics.
- La CI/CD est transversale et commence dès DEV.
- La période des fêtes (notamment du 21 décembre au 4 janvier) est un risque de disponibilité ; chaque membre doit renseigner ses disponibilités.
- Le 8 janvier est réservé au paquet de livraison du projet (rapport préparé, application, preuves et support oral de base), pas au développement majeur.
- Les modalités et la date exacte de la soutenance ne sont pas encore connues ; le support et la démonstration sont préparés par précaution. Si l'oral a lieu après le 8 janvier, les répétitions seront recalées.
- Le planning ne présume pas de la répartition individuelle des tâches. Les responsabilités seront décidées par les trois membres.

La référence Intern comporte aussi une phase de déploiement sur machines virtuelles entre DEV et Docker. Elle n'est pas incluse comme phase obligatoire dans notre organisation actuelle.

## 2. Phases et échéances

| Phase | Période cible | Résultat attendu |
|---|---|---|
| **DEV** | 25 novembre – 20 décembre 2026 | Cadrage décidé par l'équipe, prototype, modèle de données, communication réseau Java, backend, interface et recette locale intégrée |
| **Docker** | 21 – 28 décembre 2026 | Application conteneurisée, réseaux et volumes vérifiés, installation reproductible |
| **Metrics** | 29 décembre 2026 – 4 janvier 2027 | Instrumentation, étalonnage, campagnes de charge/reprise et analyse |
| **Stabilisation, rapport et préparation orale** | 5 – 8 janvier 2027 | Corrections critiques, rapport final, support oral, répétition et paquet de livraison |

Ces dates constituent un calendrier cible resserré pour trois personnes. Elles devront être réévaluées après saisie des disponibilités, notamment pendant les fêtes. Avec trois personnes, il faut limiter le périmètre initial et éviter le travail en silos, sans retirer les étapes d'intégration ou de test.

## 3. Gantt macro

| Phase / activité | 25–30 nov. | 1–7 déc. | 8–14 déc. | 15–20 déc. | 21–27 déc. | 28 déc.–3 janv. | 4–8 janv. |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **DEV** — cadrage et exigences | █ | | | | | | |
| DEV — architecture, prototype et contrats | █ | █ | | | | | |
| DEV — modèle de données et persistance | | █ | █ | | | | |
| DEV — communication réseau Java, ingestion et backend | | ░ | █ | █ | | | |
| DEV — interface centrale | | | █ | █ | | | |
| DEV — intégration et recette locale | | | ░ | █ | | | |
| **Docker** — images, volumes et réseaux | | | | | █ | ░ | |
| Docker — Compose, santé et installation | | | | | █ | ░ | |
| Docker — vérification et référence | | | | | | █ | |
| Instrumentation élémentaire (préparée pendant DEV) | ░ | ░ | ░ | ░ | ░ | ░ | ░ |
| **Metrics** — plan de test et étalonnage | | | | | | █ | |
| Metrics — campagnes de charge et de reprise | | | | | | █ | █ |
| Metrics — analyse et rapport | | | | | | ░ | █ |
| **CI/CD** — tests et qualité à chaque PR | █ | █ | █ | █ | █ | █ | █ |
| CI/CD — build images, scan et publication | | | | ░ | █ | █ | █ |
| **Rapport** — plan et modalités à confirmer | █ | | | | | | |
| Rapport — rédaction progressive des chapitres | ░ | █ | █ | █ | █ | █ | |
| Rapport — compilation des résultats Docker / Metrics | | | | | ░ | █ | |
| Rapport — finalisation, sources et annexes | | | | | | | █ |
| **Oral** — conducteur, supports et trame de démo | | | | | | █ | █ |
| Oral — répétition complète et corrections | | | | | | | █ |
| **Livraison** — gel, documentation et démonstration | | | | | | ░ | █ |

L'instrumentation élémentaire (horodatages, logs structurés, compteurs) commence pendant DEV. La phase Metrics correspond à la préparation des campagnes, à leur étalonnage, à leur exécution et à l'analyse.

## 4. Diagramme Mermaid modifiable

Les dates sont indicatives. Les dépendances entre phases sont volontairement séquentielles : Docker ne commence qu'après la sortie de DEV ; Metrics ne commence qu'après la validation de l'environnement Docker.

~~~mermaid
gantt
    title Monitorage hospitalier — livraison du 8 janvier 2027
    dateFormat YYYY-MM-DD
    axisFormat %d/%m

    section DEV
    Cadrage et exigences                  :a1, 2026-11-25, 6d
    Architecture, prototype et contrats  :a2, 2026-11-28, 10d
    Modèle de données et persistance      :a3, 2026-12-01, 12d
    Réseau Java, ingestion et backend     :a4, 2026-12-08, 10d
    Interface centrale                    :a5, 2026-12-08, 10d
    Intégration et recette locale         :a6, 2026-12-15, 6d

    section Docker
    Images et volumes                     :b1, 2026-12-21, 3d
    Réseaux et Compose                    :b2, 2026-12-24, 3d
    Vérification et installation          :b3, 2026-12-27, 2d

    section Metrics
    Plan de test et étalonnage            :c1, 2026-12-29, 2d
    Campagnes de charge et de reprise     :c2, 2026-12-31, 3d
    Analyse et rapport                    :c3, 2027-01-03, 2d

    section CI CD transversal
    CI tests et qualité                   :d1, 2026-11-25, 2027-01-08
    Build, scan et publication Docker     :d2, 2026-12-21, 18d

    section Rapport et soutenance
    Squelette du rapport et modalités      :r1, 2026-11-25, 6d
    Rédaction progressive                 :r2, 2026-11-30, 36d
    Collecte de preuves et illustrations  :r3, 2026-11-25, 44d
    Finalisation du rapport                :r4, 2027-01-05, 2d
    Support oral et conducteur             :r5, 2027-01-04, 3d
    Répétition orale et démonstration       :r6, 2027-01-07, 1d

    section Livraison
    Gel et validation finale              :e1, 2027-01-05, 3d
    Paquet de livraison prêt               :milestone, e2, 2027-01-08, 0d
~~~

## 5. Jalons et conditions de passage

| Jalon | Date cible | Résultat attendu | Condition de passage |
|---|---|---|---|
| M0 — Organisation | 27 novembre 2026 | Disponibilités, règles d'équipe, responsables et contraintes connues | Les trois membres ont renseigné leur disponibilité et choisi une organisation |
| M1 — Cadrage v1 | 30 novembre 2026 | Périmètre, utilisateurs, fonctionnalités prioritaires et scénarios | Le périmètre initial est explicite et réalisable |
| M2 — Conception v1 | 7 décembre 2026 | Architecture, maquettes, contrats réseau et données | Les interfaces entre les composants sont documentées |
| M3 — Premier flux intégré | 13 décembre 2026 | Un simulateur transmet un flux via le composant réseau Java jusqu'au backend et au stockage | Source, patient/session, séquence et horodatages sont préservés |
| M4 — DEV terminé | 20 décembre 2026 | Application locale intégrée et recette fonctionnelle | Tests P0 passants, parcours principal démontrable |
| M5 — Docker terminé | 28 décembre 2026 | Compose reproductible, volumes et réseaux vérifiés | Le même scénario DEV passe dans l'environnement conteneurisé |
| M6 — Metrics terminé | 4 janvier 2027 | Campagnes principales, résultats et analyse | Résultats reproductibles et limites identifiées |
| M7 — Rapport candidat | 6 janvier 2027 | Rapport complet relu, figures, sources et annexes vérifiées | Cohérence entre rapport, dépôt et résultats |
| M8 — Répétition | 7 janvier 2027 | Oral et démonstration intégrale répétés | Conducteur chronométré, scénario reproductible et solution de secours prête |
| M9 — Paquet de livraison | **8 janvier 2027** | Application, rapport et support oral de base prêts selon les modalités connues | Tous les livrables confirmés sont présents ; la date réelle d'oral reste à intégrer si différente |

## 6. Organisation du travail à trois

Les chantiers fonctionnels restent séparés pour clarifier les responsabilités, mais leur attribution doit être faite par Hicham, Omar et Nawfel. Une personne peut porter plusieurs chantiers ; chaque chantier doit avoir un relecteur différent lorsque c'est possible.

| Chantier | Périmètre | Responsable | Relecteur |
|---|---|---|---|
| Domaine médical, données et simulateurs | Paramètres, sources, qualité, rejeu et scénarios | À décider | À décider |
| Communication réseau Java et backend | Clients/serveur réseau, protocoles, ingestion, sessions, événements et API | À décider | À décider |
| Persistance et sécurité | Modèle, migrations, droits, audit, sauvegarde et intégrité | À décider | À décider |
| Interface centrale et intégration | Multi-patients, vues patient, courbes, alarmes et intégration bout en bout | À décider | À décider |

Cette grille ne suppose pas quatre responsables : elle décompose le travail en quatre domaines pour que les trois membres puissent se les répartir sans perdre de responsabilités. La revue croisée, les tests et la documentation restent collectifs.

## 7. CI/CD transversal par niveau de maturité

| Période | Ce qui doit être automatisé |
|---|---|
| Dès le début de DEV | Format, compilation, tests unitaires, analyse statique, secrets et dépendances |
| Fin DEV | Tests API, contrats réseau Java, migrations et scénario d'intégration |
| Docker | Construction des images, Compose, healthchecks, tests de bout en bout et scan d'images |
| Metrics | Smoke tests de non-régression ; campagnes de charge contrôlées séparées |
| Livraison | Artefact versionné, rapport de tests, documentation et procédure de retour arrière |

## 8. Chemin critique et risques

Chemin critique : cadrage → architecture et contrats → premier flux réseau Java → persistance et centrale intégrées → recette locale → conteneurisation → scénario conteneurisé → campagnes Metrics → rapport final et support oral → répétition → paquet de livraison.

Risques prioritaires :
- disponibilité réelle des trois membres pendant les fêtes ;
- périmètre trop large pour trois personnes ;
- contrat réseau Java et format des messages stabilisés trop tard ;
- intégration tardive entre serveur, base et interface ;
- données waveform trop volumineuses pour le stockage ou le rendu retenu ;
- campagnes Metrics trop courtes ou mal étalonnées ;
- absence de procédure de livraison reproductible.
- rapport commencé trop tard ou rédigé sans preuves vérifiables ;
- modalités de soutenance communiquées tardivement ;
- démonstration dépendante d'un réseau ou service externe non maîtrisé.

## 9. Règles de pilotage

- Mettre à jour le planning chaque semaine.
- Affecter un responsable et un livrable vérifiable à chaque tâche.
- Faire une démonstration intégrée chaque semaine.
- Ne pas commencer Docker tant que la recette locale DEV n'est pas satisfaisante.
- Ne pas tirer de conclusion de performance avant d'avoir étalonné le protocole.
- Définir les seuils d'acceptation avant les campagnes.
- Geler les nouvelles fonctionnalités après le passage M4, sauf correction nécessaire.
- Réserver les 5 à 8 janvier à la stabilisation, à la finalisation du rapport, à la répétition et à la livraison ; la rédaction du rapport et la collecte de preuves commencent dès le cadrage.
- Ne pas attendre les modalités officielles pour préparer le contenu ; adapter ensuite durée, format et pagination.

**À compléter :** disponibilités hebdomadaires de Hicham, Omar et Nawfel, notamment du 21 décembre au 4 janvier. Les dates ci-dessus sont un calendrier cible ; les charges individuelles seront ajustées après ces réponses.
