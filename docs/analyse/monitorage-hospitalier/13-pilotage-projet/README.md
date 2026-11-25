# Pilotage du projet — cadrage, organisation, planning et arbitrages

**Version :** 1.4 — **Date :** 25 novembre 2026  
**Échéance de livraison :** vendredi 8 janvier 2027.  
**Équipe :** Hicham, Omar et Nawfel (3 personnes).  
**Contrainte technique connue :** programmation réseau en Java ; autres choix libres.  
**État :** projet logiciel complet en cours de conception ; ce dossier reste un support de décisions de l'équipe.

## Objectif

Rendre les décisions explicites et faciles à faire évoluer. Le cahier de décisions constitue une baseline initiale, révisable au fil du projet ; le journal d'arbitrages conserve les versions précédentes et les raisons des changements. Ce dossier est conçu pour être mis à jour directement : chaque décision garde sa justification et les résultats des essais.

## Documents

1. [Cahier de décisions et questions de cadrage](01-questionnaire-tuteur.md) — périmètre clinique, fonctionnalités, données, architecture, choix technologiques et points à faire valider.
2. [Questionnaire d'organisation de l'équipe de trois](02-questionnaire-equipe.md) — compétences, disponibilité, responsabilités, méthode Git, décisions, réunions et règles d'intégration.
3. [Planning Gantt générique](03-gantt-generique.md) — séquence DEV → Docker → Metrics et échéance du 8 janvier 2027.
4. [Stratégies et arbitrages critiques](04-strategies-et-arbitrages-critiques.md) — orientations possibles, situations critiques, expérimentations, métriques et journal de décision.
5. [Préparation du rapport et de la soutenance](05-rapport-et-soutenance.md) — plan du rapport, preuves à conserver, fil oral, démonstration et modalités à confirmer.

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
- Les choix qui modifient la nature du produit (services, fonctionnalités, sources médicales, architecture, interface, données, sécurité) sont arbitrés explicitement par les trois membres. Le tuteur laisse ces choix ouverts, sauf la programmation réseau qui doit être en Java.
- Quand plusieurs approches sont plausibles, construire un essai comparatif avant de choisir.
- Définir les métriques et les critères de réussite avant de regarder les résultats.
- Conserver les résultats bruts des essais : charge, latence, pertes, volume, erreurs, temps d'intégration et limites observées.
- Le planning est une maquette macro, pas un engagement de charge déjà validé.
- Le rapport doit être alimenté pendant DEV, Docker et Metrics ; la période du 5 au 8 janvier est réservée à la finalisation et aux répétitions, pas au démarrage de la rédaction.
- La date et les modalités exactes de soutenance restent inconnues ; elles seront ajoutées dès confirmation.
- L'échéance du 8 janvier 2027 est une contrainte ferme à confirmer avec le tuteur (heure, format et contenu du rendu).

## Statut des décisions

| ID | Sujet | État |
|---|---|---|
| DIR-01 | Nature du système | Confirmé : monitorage hospitalier, moniteurs de chevet vers centrale(s). |
| DIR-02 | Services cliniques exacts | Première décision prise : réanimation adulte polyvalente comme service initial ; USC, cardiologie/télémétrie, urgences/SAUV et SSPI comme extensions possibles. |
| DIR-03 | Fonctionnalités fonctionnelles attendues | Décidé provisoirement : F-01 à F-06, F-08 à F-12 et F-16 à F-19 obligatoires ; F-07, F-13, F-14 et F-20 à F-22 souhaitées ; F-15 hors périmètre. Critères détaillés dans le cahier de décisions. Le top 3, le dimensionnement et la faisabilité restent à préciser. |
| DIR-04 | Niveau de réalisme médical et signaux | Ouvert : paramètres, courbes et données sources à sélectionner. |
| DIR-05 | Technologies | Partiellement confirmé : programmation réseau en Java ; technologies des autres composants libres. |
| DIR-06 | Architecture réseau et déploiement | Exigence fonctionnelle décidée : centrales locales par service et supervision transversale réelle ; topologie technique, hébergement et mécanismes réseau encore ouverts. |
| DIR-07 | Livrables et barème | À préciser par l'équipe et à faire valider si nécessaire. |
| DIR-08 | Répartition de l'équipe | À décider par Hicham, Omar et Nawfel. |
| DIR-09 | Séquence DEV → Docker → Metrics | Séquence retenue ; planning recalé au 25 novembre avec échéance au 8 janvier. |
| DIR-10 | CI/CD | À mettre en place dès DEV, puis enrichir avec Docker et Metrics. |
