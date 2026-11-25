# CI/CD — Intégration et livraison continues

**Portée :** transversale à DEV, Docker et Metrics.  
**Principe :** l'automatisation est construite progressivement dès le début du développement.

## 1. Objectifs

La CI/CD doit garantir que les changements intégrés :
- compilent et respectent les conventions du projet ;
- passent les tests unitaires et d'intégration ;
- ne cassent pas les contrats de données ;
- ne réintroduisent pas de régression sur les parcours essentiels ;
- ne contiennent pas de secrets ou de vulnérabilités connues non traitées ;
- peuvent être construits et livrés de façon reproductible.

CI signifie vérifier automatiquement chaque changement. CD signifie préparer puis livrer une version contrôlée dans un environnement autorisé. Le déploiement automatique en environnement clinique réel n'est ni supposé ni prévu par ce document.

## 2. Stratégie de branches et intégration

Proposition à confirmer par l'équipe :
- branche principale protégée ;
- branche courte par fonctionnalité ou correction ;
- Pull Request obligatoire vers la branche principale ;
- tests automatiques obligatoires avant fusion ;
- revue par au moins un autre membre ;
- petites PR centrées sur un objectif ;
- versions ou tags pour les jalons de livraison.

Éviter les branches de longue durée et les intégrations massives en fin de phase.

## 3. Pipeline CI dès DEV

À chaque Pull Request :

1. vérification du formatage et du style ;
2. compilation ;
3. tests unitaires ;
4. tests de contrat des API et messages ;
5. tests du modèle et des migrations de base ;
6. tests d'intégration avec données synthétiques ;
7. analyse statique ;
8. vérification des dépendances et licences ;
9. détection de secrets ;
10. rapport de couverture et publication des journaux de tests.

Les tests utilisent uniquement des données fictives et des datasets dont l'usage est autorisé. Aucun identifiant, secret ou fichier contenant des données personnelles ne doit être committé.

## 4. Évolution du pipeline pendant Docker

Une fois les Dockerfiles et Compose établis :

- construire les images sur CI ;
- fixer les versions de base ;
- lancer l'environnement Compose dans le runner ;
- attendre les healthchecks ;
- exécuter les tests de bout en bout ;
- vérifier les ports publiés et la configuration réseau ;
- tester la persistance et les migrations ;
- scanner les images et dépendances ;
- produire un SBOM lorsque l'outillage le permet ;
- publier les images versionnées sur le registre choisi.

Les images doivent être identifiées par tag de version et/ou SHA de commit. Un tag flottant ne doit pas être la seule référence d'une recette.

## 5. Pipeline de livraison

Proposition :
- Pull Request : tests et contrôles, aucune publication de version stable ;
- fusion sur la branche principale : construction et publication d'une image de développement identifiée par commit ;
- création d'un tag de version : génération de la version candidate, notes de version, artefacts et rapport de tests ;
- déploiement démo : manuel ou approbation explicite sur un environnement de démonstration ;
- retour arrière : possibilité de redéployer l'image précédente et de restaurer les données selon la procédure validée.

La méthode de publication et le registre (par exemple GHCR) sont à confirmer avec l'équipe et les contraintes du dépôt.

## 6. Intégrer Metrics sans rendre la CI instable

Toutes les campagnes de charge ne doivent pas tourner à chaque Pull Request : les runners partagés ne sont pas suffisamment déterministes pour des comparaisons fines.

Séparer :
- **smoke tests** : très courts, à chaque PR, vérifier que le parcours principal fonctionne ;
- **tests de performance légers** : exécution planifiée ou à la demande, détection de régression grossière ;
- **campagnes de référence** : manuelles ou sur runner contrôlé, avec ressources réservées, version et configuration figées ;
- **tests de durée** : planifiés, hors du cycle normal des PR.

Toute régression de performance doit être interprétée avec la charge, le runner et les conditions consignés. Ne pas bloquer une fusion sur un écart mineur mesuré dans un environnement bruyant sans confirmation.

## 7. Sécurité du pipeline

- utiliser les secrets du gestionnaire CI, jamais des fichiers committés ;
- appliquer le moindre privilège aux tokens ;
- limiter les permissions d'écriture des jobs qui n'en ont pas besoin ;
- analyser les dépendances et images ;
- ne pas exécuter de données ou scripts externes non fiables avec des secrets ;
- séparer les environnements de test et de démonstration ;
- garder un historique des artefacts publiés ;
- documenter la rotation et la révocation des secrets.

## 8. Pipeline cible par phase

| Phase | Contrôles automatisés attendus |
|---|---|
| DEV | Format, build, tests unitaires, contrats, migrations, tests métier, analyse statique et secrets |
| Docker | Build images, Compose up, healthchecks, tests end-to-end, persistance, scan et publication |
| Metrics | Smoke tests, campagnes contrôlées, génération des résultats et archivage des rapports |
| Livraison | Version taguée, artefacts identifiés, procédure de déploiement et possibilité de retour arrière |

## 9. Livrables CI/CD

- workflows versionnés ;
- documentation des jobs et déclencheurs ;
- règles de protection de la branche principale ;
- configuration de qualité et sécurité ;
- images et artefacts identifiables ;
- rapports de tests associés aux commits ;
- procédure de publication et de retour arrière.

## 10. Critère de sortie

La CI/CD est considérée opérationnelle lorsque chaque Pull Request exécute des contrôles utiles, la branche principale produit un artefact identifié, le déploiement Compose peut être testé automatiquement et la livraison de démonstration est reproductible.

L'automatisation doit rester proportionnée au projet : un pipeline maintenable et fiable vaut mieux qu'une chaîne complexe qui ne peut pas être comprise ou réparée par les trois membres.
