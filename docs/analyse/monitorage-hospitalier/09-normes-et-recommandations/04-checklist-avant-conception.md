# Checklist 04 — Livrables à obtenir avant de commencer le développement

**Version :** 0.1 — **Date :** 18 novembre 2026

Cette checklist est une porte de sortie de la phase d'analyse. Elle ne signifie pas que chaque document doit faire des dizaines de pages : chaque point doit avoir une réponse documentée, même courte.

## A. Domaine et métier

- [ ] Un service hospitalier de référence est choisi.
- [ ] Le contexte (réanimation, cardiologie, SSPI, unité conventionnelle, urgences) est expliqué.
- [ ] Les rôles utilisateurs sont définis.
- [ ] Le circuit d'une admission et d'une sortie est décrit.
- [ ] Le cycle lit / patient / moniteur est décrit.
- [ ] Le fonctionnement du poste central et des relèves est documenté.
- [ ] La gestion des alarmes est décrite sans inventer de seuil clinique.

## B. Équipements et données

- [ ] Les familles d'appareils simulées sont choisies.
- [ ] Les paramètres sont définis avec unités, fréquences et métadonnées.
- [ ] Les courbes ou valeurs seules sont arbitrées.
- [ ] Les états techniques des appareils sont listés.
- [ ] L'identité et l'association appareil-patient sont spécifiées.
- [ ] Les cas de remplacement et de transport sont définis.
- [ ] Les sources et limites des données synthétiques sont documentées.

## C. Réseau et serveur

- [ ] Les flux et leurs destinations sont dessinés.
- [ ] Le protocole et le format de messages sont spécifiés.
- [ ] L'authentification des clients est définie.
- [ ] Les règles de validation, d'ordre et de déduplication sont définies.
- [ ] La gestion des pertes et reconnexions est décrite.
- [ ] La latence et le débit sont mesurables.
- [ ] Les erreurs et comportements lors de panne sont spécifiés.

## D. Stockage et interface

- [ ] Le modèle de données conceptuel est dessiné.
- [ ] Les données historiques, courbes, alarmes et audits sont distingués.
- [ ] La durée de conservation du POC est fixée.
- [ ] Les vues multi-patients, patient, appareil et alarmes sont listées.
- [ ] L'état de fraîcheur et d'indisponibilité est visible.
- [ ] Les rôles et actions permis sont définis.
- [ ] Les tests d'ergonomie sont planifiés.

## E. Sécurité et continuité

- [ ] Le POC reste alimenté par des données synthétiques.
- [ ] Les limites d'usage clinique sont affichées.
- [ ] Le modèle de menace est validé.
- [ ] Les comptes, rôles et secrets sont gérés.
- [ ] Les flux réseau nécessaires sont listés.
- [ ] La journalisation des actions sensibles est spécifiée.
- [ ] La sauvegarde et la restauration sont prévues.
- [ ] Les scénarios d'accès interdit et de client inconnu sont prévus.
- [ ] Le fonctionnement dégradé est décrit.
- [ ] Aucun test n'est mené sur un système hospitalier réel sans autorisation.

## F. Tests et reproductibilité

- [ ] Les scénarios nominaux sont écrits.
- [ ] Les scénarios limites sont écrits.
- [ ] Les tests réseau et charge sont définis.
- [ ] Les tests de sécurité non destructifs sont définis.
- [ ] Les critères d'acceptation sont mesurables.
- [ ] Les paramètres de simulation sont versionnés.
- [ ] Les prompts de recherche sont archivés.
- [ ] Les décisions et alternatives sont conservées dans Git.

## G. Décision de sortie d'analyse

La phase d'analyse peut être considérée comme suffisante pour commencer un POC lorsque :
- le service de référence et le parcours principal sont compris ;
- les équipements, données, rôles et flux du POC sont définis ;
- les scénarios nominaux et les pannes essentielles sont spécifiés ;
- les objectifs de performance sont mesurables ;
- les protections de sécurité du POC sont décidées ;
- les critères de réussite et limites du POC sont explicites.

La sortie de l'analyse ne constitue pas une validation réglementaire ou clinique d'un dispositif médical.
