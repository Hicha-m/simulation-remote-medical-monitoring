# Pilotage du projet — cadrage, organisation, planning et arbitrages

**Version :** 1.1 — **Date :** 18 novembre 2026  
**Échéance de livraison :** vendredi 8 janvier 2027.  
**État :** projet logiciel complet en cours de cadrage ; ce dossier n'est pas un cahier des charges validé.

## Objectif

Rendre les décisions explicites et faciles à faire évoluer. Ce dossier est conçu pour être utilisé en réunion puis mis à jour directement : chaque question possède une zone de réponse, chaque décision garde sa justification et les résultats des essais.

## Documents

1. [Questionnaire à faire remplir par le tuteur](01-questionnaire-tuteur.md) — périmètre clinique, services, fonctionnalités, réalisme médical, technologie, livrables et évaluation.
2. [Questionnaire d'organisation de l'équipe de quatre](02-questionnaire-equipe.md) — compétences, disponibilité, responsabilités, méthode Git, décisions, réunions et règles d'intégration.
3. [Planning Gantt générique](03-gantt-generique.md) — séquence DEV → Docker → Metrics et échéance du 8 janvier 2027.
4. [Stratégies et arbitrages critiques](04-strategies-et-arbitrages-critiques.md) — orientations possibles, situations critiques, expérimentations, métriques et journal de décision.

## Méthode de réalisation retenue

Le travail est organisé en trois phases principales :
1. **DEV** : analyse, maquettes, données, ingestion/métier, interface et recette locale ;
2. **Docker** : images, réseaux, volumes, composition, santé et reproduction de l'environnement ;
3. **Metrics** : instrumentation, étalonnage, campagnes et analyse.

La **CI/CD est transversale** et commence dès DEV. Les consignes détaillées sont dans [docs/consignes](../../../consignes/README.md).

La référence Intern inclut une phase VM intermédiaire ; elle n'est pas obligatoire dans le planning actuel. Elle pourra être ajoutée si le tuteur demande explicitement une comparaison VM/Docker.

## Règles de pilotage

- Une question n'est pas une décision tant qu'une réponse n'est pas obtenue et enregistrée.
- Une proposition de l'équipe reste une hypothèse tant qu'elle n'est pas validée.
- Les choix qui modifient la nature du produit (services, fonctionnalités, sources médicales, architecture, interface, données, sécurité) sont arbitrés explicitement.
- Quand plusieurs approches sont plausibles, construire un essai comparatif avant de choisir.
- Définir les métriques et les critères de réussite avant de regarder les résultats.
- Conserver les résultats bruts des essais : charge, latence, pertes, volume, erreurs, temps d'intégration et limites observées.
- Le planning est une maquette macro, pas un engagement de charge déjà validé.
- L'échéance du 8 janvier 2027 est une contrainte ferme à confirmer avec le tuteur (heure, format et contenu du rendu).

## Statut des décisions

| ID | Sujet | État |
|---|---|---|
| DIR-01 | Nature du système | Confirmé : monitorage hospitalier, moniteurs de chevet vers centrale(s). |
| DIR-02 | Services cliniques exacts | Ouvert : service principal et extensions à préciser. |
| DIR-03 | Fonctionnalités fonctionnelles attendues | Ouvert : liste à faire valider. |
| DIR-04 | Niveau de réalisme médical et signaux | Ouvert : paramètres, courbes et données sources à sélectionner. |
| DIR-05 | Langages, frameworks, UI et stockage | Ouvert : à comparer, Java reste à faire préciser. |
| DIR-06 | Architecture réseau et déploiement | Ouvert : à choisir après les besoins et essais. |
| DIR-07 | Livrables et barème | Ouvert : à confirmer. |
| DIR-08 | Répartition de l'équipe | Ouvert : à décider en réunion à quatre. |
| DIR-09 | Séquence DEV → Docker → Metrics | Proposition de travail retenue ; dates à confirmer avec les disponibilités. |
| DIR-10 | CI/CD | À mettre en place dès DEV, puis enrichir avec Docker et Metrics. |
