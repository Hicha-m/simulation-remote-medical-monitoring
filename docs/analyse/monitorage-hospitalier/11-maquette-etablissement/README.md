# Maquette fonctionnelle de l'établissement

**Version :** 0.1  
**Date :** 18 novembre 2026  
**Statut :** maquette de référence proposée pour le projet. Les bâtiments, étages, chambres et lits sont fictifs ; les parcours MIMIC restent des données de recherche réelles et dé-identifiées.

## Objectif

Fixer un environnement spatial et organisationnel assez précis pour relier les admissions et mouvements MIMIC-IV, les services de la simulation, les chambres et lits fictifs, les appareils simulés, les centrales et l'infrastructure informatique.

La maquette est volontairement petite. Elle doit soutenir une démonstration complète et des tests de transfert, pas reproduire la capacité d'un grand CHU.

## Décisions de modélisation

1. Un site, deux bâtiments cliniques et une zone technique.
2. Cinq niveaux physiques : bâtiment A RDC, R+1, R+2 ; bâtiment B RDC, R+1 ; plus un sous-sol technique dans A.
3. Les services et les emplacements physiques sont deux objets séparés.
4. Les lits et postes possèdent des identifiants stables.
5. Un mouvement MIMIC est relié à une unité cible, puis à un lit fictif ; le lit n'est jamais déduit du dataset.
6. Les appareils et leur emplacement sont historisés et indépendants de l'affectation du patient.
7. La réanimation adulte polyvalente est le service de référence du premier projet ; la CVICU et les autres secteurs servent à tester des extensions de parcours.

## Documents

- [01 — Plan physique et unités](01-plan-physique-et-unites.md)
- [02 — Inventaire des chambres, lits et postes](02-inventaire-chambres-lits-postes.md)
- [03 — Correspondance MIMIC-IV vers la maquette](03-correspondance-mimic-vers-maquette.md)
- [04 — Modèle d'organisation, objets et relations](04-modele-organisation-et-relations.md)
- [05 — Scénarios de rejeu reproductibles](05-scenarios-rejouables.md)
- [Configuration machine-readable de l'établissement](facility-map-v1.json) — bâtiments, étages, zones, unités, chambres et positions avec coordonnées relatives.
- [Mapping machine-readable MIMIC → maquette](mimic-transfer-mapping-v1.json) — correspondances, parcours exemples, affectations de lits et politique déterministe.

## Configuration utilisable par un futur plan interactif

Les deux fichiers JSON ci-dessus constituent la configuration versionnée à charger pour rendre la carte. Les coordonnées sont relatives au plan de chaque étage ; les chambres disposent de positions de grille dans leur zone. La carte est une vue de ces données, pas la source de vérité du parcours.

## Réel et fictif : séparation obligatoire

| Élément | Statut |
|---|---|
| subject_id, hadm_id, transfer_id, careunit, eventtype, intime, outtime | Champs issus de la table MIMIC-IV transfers. |
| Horaires et unités des deux parcours exemples | Données MIMIC-IV Demo 2.2, dates décalées pour anonymisation. |
| Bâtiments, étages, chambres, lits et coordonnées du plan | Maquette fictive du projet. |
| Affectation d'un parcours MIMIC à un lit donné | Règle de simulation déterministe, pas une donnée de soin observée. |
| Identifiants et profils de moniteurs | Appareils virtuels du projet. |
| Alarmes, coupures réseau et pannes électriques | Scénarios synthétiques, sauf lorsque la source apporte explicitement un événement correspondant. |

## Règle essentielle

La table MIMIC-IV transfers décrit des localisations physiques et des périodes, mais ne fournit pas le numéro de chambre ou le numéro de lit. Le système doit donc préserver le transfer_id source et stocker séparément l'emplacement synthétique alloué par la maquette [H111].
