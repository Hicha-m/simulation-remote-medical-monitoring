# 04 — Prompt : auditer les sources et les affirmations

## Prompt réutilisable

Effectue un audit de traçabilité sur un dossier d'analyse concernant un système de télésurveillance ou de monitorage médical.

### Objectif

Vérifier qu'aucun document ne présente une hypothèse comme un fait, qu'aucune citation ne soutient une affirmation qu'elle ne contient pas et que les sources sont suffisamment fiables et actuelles.

### Contrôles

1. Pour chaque affirmation importante, retrouver une source exacte.
2. Identifier l'auteur : organisme public, éditeur, fournisseur, chercheur, communauté ou contributeur individuel.
3. Vérifier la date de publication et la date de l'événement décrit.
4. Vérifier la version des textes et standards cités.
5. Contrôler que les chiffres sont bien présents dans la source et que leur périmètre est compris.
6. Identifier les formulations commerciales ou déclaratives.
7. Séparer fait, observation, interprétation, piste et décision.
8. Rechercher les contradictions entre sources.
9. Identifier les pages obsolètes, calendriers prévisionnels et informations non confirmées.
10. Proposer une correction lorsqu'une affirmation est trop catégorique.

### Règles strictes

- Ne jamais inventer une URL, une certification, un déploiement ou une statistique.
- Ne pas supposer qu'un projet open source est actif ou sécurisé sans preuve.
- Ne pas supposer qu'une présence dans un marché public signifie une adoption effective.
- Ne pas extrapoler un retour d'expérience d'un service à tous les hôpitaux.
- Ne pas qualifier une fonctionnalité de « temps réel » sans métrique.
- Ne pas confondre une alerte technique et une décision clinique.
- Indiquer clairement lorsqu'une information n'a pas pu être vérifiée.

### Format de sortie

| ID | Affirmation examinée | Source | Preuve exacte | Fiabilité | Limite | Action |
|---|---|---|---|---|---|---|

Terminer par :
- affirmations confirmées ;
- affirmations à reformuler ;
- affirmations non sourcées à supprimer ;
- sources à actualiser ;
- questions encore ouvertes.
