# Domaines médicaux approfondis — référence de travail

**Version :** 1.0  
**Date :** 18 novembre 2026  
**Périmètre confirmé :** système de monitorage hospitalier reliant des moniteurs de chevet à une ou plusieurs centrales de surveillance.  
**Statut :** référentiel documentaire à faire valider par le tuteur et, si possible, par un professionnel de santé.

## Objectif

Passer d'un panorama hospitalier à une description exploitable par l'équipe de développement : contenu médical des mesures, signaux physiologiques, données brutes, qualité des mesures, cycle humain des alarmes, informations patient et pratiques françaises.

Ce dossier décrit ce qu'un système de monitorage peut recevoir, conserver et présenter. Il ne définit pas de seuils cliniques universels, de diagnostic ni de conduite thérapeutique. Les profils, règles et seuils propres à une unité devront être validés par une source clinique compétente.

## Documents

1. [Dictionnaire médical des paramètres](01-dictionnaire-medical-parametres.md) — mesure, unité, origine, signal, cadence et statut.
2. [Courbes physiologiques et données brutes](02-courbes-et-donnees-brutes.md) — signaux, formats, fréquences observées et bases ouvertes.
3. [Qualité et fiabilité des mesures](03-qualite-et-fiabilite-mesures.md) — artefacts, indicateurs qualité, fraîcheur et règles d'intégrité.
4. [Gestion des alarmes par les soignants](04-gestion-alarmes-et-workflow-soignant.md) — détection, diffusion, prise en compte, intervention, escalade et relève.
5. [Informations médicales associées au patient](05-contexte-medical-patient.md) — patient, séjour, unité, lit, session, identité et minimisation.
6. [Pratiques françaises et environnement hospitalier](06-pratiques-francaises-etablissement.md) — identitovigilance, responsabilités, procédures, organisation et précautions réglementaires.

## Règles de lecture

- Une mesure numérique, une courbe brute, une alarme et un événement technique sont quatre objets différents.
- La fréquence d'échantillonnage d'un signal ne doit pas être confondue avec la fréquence de publication d'une valeur numérique.
- Les valeurs documentées dans une base de recherche ne sont pas nécessairement des mesures brutes ni des valeurs validées par un soignant.
- La qualité technique d'un signal et la signification clinique de la valeur doivent être stockées séparément.
- Une valeur physiologiquement inhabituelle n'est pas automatiquement une mesure techniquement invalide.
- L'acquittement d'une alarme ne signifie pas que sa cause a disparu.
- Les exemples de données réelles sont dé-identifiés et soumis aux conditions d'accès et de réutilisation de leur source.
- Le modèle de données du projet doit être suffisamment riche pour conserver la provenance, mais le produit ne doit pas collecter des informations médicales sans besoin fonctionnel identifié.

## Référence d'autorité

Les fréquences citées sont celles des jeux de données nommés, et non des cadences universelles imposées aux moniteurs. Les pratiques de service sont variables ; la procédure réelle de l'établissement et la validation des professionnels priment sur une reconstruction documentaire.

## Décisions encore ouvertes

- Service clinique prioritaire et autres services nécessaires.
- Population : adultes, pédiatrie, néonatologie.
- Paramètres et courbes obligatoires.
- Usage de données réelles de recherche, de données synthétiques ou d'un mélange.
- Profondeur de l'intégration au dossier patient.
- Modèle d'alarme et rôles de réception.
- Finalité prévue du logiciel et éventuelle qualification réglementaire.
