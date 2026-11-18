# 08 — Prompt : établir la couverture intégrale d'un projet

## Prompt réutilisable

À partir du sujet initial et de tous les documents d'analyse existants, construis une matrice de couverture complète du projet.

Le but est de vérifier qu'aucune partie fonctionnelle, métier, technique, réglementaire, sécurité ou qualité n'est oubliée avant de commencer la conception et le développement.

## Entrées

- Sujet initial : [coller le texte exact].
- Périmètre confirmé : [contexte hospitalier précis].
- Dossier documentaire : [liste des index et dossiers].
- Contraintes académiques : [langages, calendrier, taille d'équipe, livrables].

## Dimensions obligatoires

1. Environnement métier et acteurs.
2. Parcours patient, admission, lit, appareil, transfert, sortie.
3. Equipements, capteurs et mesures physiologiques.
4. Clients simulateurs et scénarios reproductibles.
5. Réseau, protocoles et qualité de service.
6. Serveur d'ingestion et traitement des messages.
7. Données, base de données, historique et archivage.
8. Alarmes, priorités, report et workflow.
9. Tableau de bord et ergonomie.
10. Performance, temps réel et montée en charge.
11. Cybersécurité et protection des données.
12. Disponibilité, sauvegarde et reprise.
13. Intégration et interopérabilité.
14. Maintenance, exploitation et supervision.
15. Langages, frameworks et outillage.
16. Normes, réglementation et recommandations.
17. Tests, validation et critères d'acceptation.
18. Documentation et reproductibilité.

## Statuts

- Documenté : thème couvert par des éléments vérifiables.
- Partiel : éléments présents mais contexte, exigences ou preuves à compléter.
- Ouvert : aucune décision ou validation suffisante.
- Hors périmètre provisoire : explicitement exclu du POC.

Ne pas marquer un thème « documenté » simplement parce qu'il a été mentionné. Vérifier la présence d'une source, d'une exigence ou d'une décision.

## Pour chaque domaine

Produire :
- besoin métier ;
- exigences fonctionnelles ;
- contraintes non fonctionnelles ;
- acteurs ;
- données ;
- risques ;
- dépendances ;
- normes et recommandations ;
- sources ;
- scénarios de test ;
- critères d'acceptation ;
- questions ouvertes ;
- livrables nécessaires.

## Règles

- Préserver les décisions déjà explicitement validées.
- Ne pas convertir une hypothèse en décision.
- Ne pas déduire une exigence clinique sans source ou validation professionnelle.
- Ne pas imposer une technologie avant de décrire le besoin.
- Associer chaque exigence importante à une source, un entretien ou une décision.
- Faire apparaître les lacunes et contradictions.
- Conserver la traçabilité sujet → besoin → risque → exigence → scénario → test.

## Sortie attendue

1. Matrice de couverture complète.
2. Tableau de maturité et lacunes.
3. Carte des dépendances entre domaines.
4. Liste des décisions bloquantes.
5. Checklist de sortie d'analyse.
6. Proposition d'ordre de travail, sans commencer à coder.

## Paramètres

- Date de mise à jour : [à compléter]
- Version du dossier : [à compléter]
- État du projet : analyse / conception / POC / validation
