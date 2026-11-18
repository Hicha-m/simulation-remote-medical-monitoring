# Cadrage fonctionnel — services, parcours, appareils et tests

**Date :** 18 novembre 2026  
**Statut :** proposition issue de la recherche documentaire ; aucun service ni protocole clinique n'est encore validé par un établissement partenaire.

Ce dossier transforme l'analyse hospitalière en scénarios compréhensibles et testables. Il ne constitue ni un protocole de soins, ni un cahier des charges clinique.

## Documents

1. [Comparer les services et choisir une référence](01-choix-service-reference.md)
2. [Parcours hospitaliers et personas](02-parcours-et-personas.md)
3. [Appareils et profils par service](03-appareils-et-profils-par-service.md)
4. [Contrats de données proposés](04-contrats-de-donnees.md)
5. [Workflows métier expliqués](05-workflows-metier.md)
6. [Points critiques, stratégie de test et acceptation](06-points-critiques-et-criteres-acceptation.md)
7. [Cartographie hospitalière et architecture du SI](07-cartographie-hospitaliere-et-architecture-du-si.md)
8. [Continuité électrique et fonctionnement dégradé](08-continuite-electrique-et-mode-degrade.md)

## Proposition de lecture

- Commencer par la comparaison des services. La réanimation adulte est recommandée comme référence de travail, mais le choix reste à valider.
- Lire les personas pour comprendre que le patient peut traverser plusieurs services et changer plusieurs fois d'appareils.
- Définir ensuite les appareils et les contrats logiques de données.
- Formaliser les workflows avant de choisir le découpage technique.
- Utiliser les points critiques comme base de la stratégie de test.

## Principes de prudence

- Les personas sont fictifs et composites ; ils ne reproduisent pas un dossier réel.
- Les données doivent être synthétiques dans le POC.
- Les seuils, alarmes et conduites à tenir médicales ne sont pas définis ici.
- Une fonction décrite par un fabricant n'est pas nécessairement déployée dans tous les hôpitaux.
- Un flux simulé n'est pas un dispositif de surveillance clinique et ne doit jamais être connecté à un patient réel.
