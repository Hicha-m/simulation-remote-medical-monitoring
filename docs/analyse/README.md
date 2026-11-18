# Analyse du projet — Simulation d'un système de télésurveillance médicale

> **État :** étude préliminaire — aucune architecture, technologie ou fonctionnalité n'est arrêtée.  
> **Date de référence :** 18 novembre 2026.  
> **Périmètre :** comprendre le domaine, les usages, les acteurs, les solutions existantes, les contraintes et les échelles possibles avant toute implémentation.

## Pourquoi ce dossier existe

Ce répertoire conserve la trace structurée de l'analyse du sujet, des sources consultées, des questions encore ouvertes, des pistes de valeur ajoutée et des prompts utilisés pour reproduire la recherche.

Le dossier ne constitue ni une spécification finale, ni une recommandation médicale, ni une preuve de conformité réglementaire.

## Règles de lecture

Chaque information doit être interprétée selon son statut :

- **Fait sourcé** — information directement appuyée par une source identifiable.
- **Observation** — constat tiré de la comparaison de sources ou de projets.
- **Piste à étudier** — possibilité qui mérite une investigation, sans engagement.
- **Question ouverte** — information manquante qui nécessite une réponse ou une source.
- **Décision** — choix explicitement validé par l'équipe. Aucune décision de conception n'est prise dans cette première version.

Les informations commerciales publiées par les fournisseurs sont identifiées comme telles et ne sont pas assimilées à des évaluations indépendantes.

## Périmètre désormais confirmé

Le sujet est recentré sur le **monitorage hospitalier**. Le dossier de référence à jour est [monitorage-hospitalier](monitorage-hospitalier/README.md), organisé en sous-répertoires par environnement de soins, famille de systèmes, métier et besoins. Les anciens documents génériques ci-dessous conservent la trace de l'exploration initiale ; certaines parties concernent encore la télésurveillance à domicile et ne constituent plus le périmètre principal.

## Documents de cadrage initiaux

| Document | Objet |
|---|---|
| [00 — Cadrage et méthode](00-cadrage-et-methode.md) | Sujet reformulé, limites de l'analyse et méthode de travail |
| [01 — Glossaire et domaine](01-glossaire-et-domaine.md) | Définition des termes métier, médicaux et techniques |
| [02 — Acteurs, parcours et scénarios](02-acteurs-parcours-et-scenarios.md) | Rôles, cycle de vie des données et scénarios à examiner |
| [03 — Projets et briques existantes](03-projets-et-briques-existantes.md) | Benchmark open source et solutions techniques réutilisables |
| [04 — Marché et positionnement](04-marche-et-positionnement.md) | Écosystème français, fournisseurs, besoins et pistes de différenciation |
| [05 — Échelles et vision](05-echelles-et-vision.md) | Périmètres petit, moyen, large et vision théorique sans limite de moyens |
| [06 — Sécurité et cadre réglementaire](06-securite-et-cadre-reglementaire.md) | Données de santé, sécurité, hébergement et réglementation à surveiller |
| [07 — Questions ouvertes et décisions](07-questions-ouvertes-et-decisions.md) | Questions à poser, informations à obtenir et journal des décisions |
| [08 — Sources](08-sources.md) | Registre des sources et limites de chacune |

## Reproductibilité

Les prompts et instructions de recherche sont archivés dans le dossier [prompts](prompts/README.md). Ils servent à reproduire, compléter ou actualiser les investigations. Un prompt n'est pas une source et ne transforme pas une piste générée en fait établi.

## Principes de prudence

1. Ne pas utiliser de données réelles de patients dans le POC.
2. Ne pas connecter le projet à un dispositif médical réel ni à un système d'information hospitalier sans cadre et autorisation explicites.
3. Ne pas présenter une valeur simulée, une alerte ou un seuil comme un avis ou une recommandation médicale.
4. Distinguer la simulation logicielle d'un dispositif médical destiné à être utilisé en situation de soins.
5. Vérifier les textes et référentiels applicables à la date de toute décision de conception ou de déploiement.

## Historique

- **18/11/2026 — v0.1 :** création du dossier d'analyse initial ; cadrage, glossaire, benchmark, étude de marché préliminaire, scénarios, échelles, sécurité et questions ouvertes.
