# Architecture technique — dossier d'étude

**Version :** 0.1 — **Date :** 18 novembre 2026  
**Statut :** architectures publiquement documentées et options à étudier ; aucune architecture cible choisie.

## Objectif

Comprendre les technologies qui composent les systèmes hospitaliers actuels, leur organisation réseau, leurs protocoles, les composants serveurs et les frontières avec le système informatique hospitalier.

## Documents

1. [Architecture de référence et variantes](01-architectures-de-reference.md) — composants, flux et comparaison GE, Philips, Dräger, Mindray.
2. [Technologies et protocoles](02-technologies-et-protocoles.md) — réseaux, transports, interfaces, formats et limites d'interopérabilité.
3. [Infrastructure, serveurs et déploiement](03-infrastructure-serveurs-et-deploiement.md) — LAN/VLAN, centrales, virtualisation, postes, disponibilité et maintenance.
4. [Données et intégration au SIH](04-donnees-et-integration-sih.md) — identité patient, ADT, HL7, archivage et traçabilité.
5. [Public, privé et inconnues](05-limites-documentaires-et-informations-privees.md) — ce que l'on sait, ce qu'on ignore et comment obtenir les informations.

## Règles

- Les documents fabricants sont des sources primaires sur les produits qu'ils décrivent, pas des preuves de leur déploiement dans tous les hôpitaux.
- Les protocoles propriétaires et configurations exactes peuvent être couverts par des manuels réservés aux clients ou aux mainteneurs.
- Les architectures proposées dans ces documents ne sont pas des architectures de production validées.
- Les détails sensibles d'infrastructures réelles ne doivent pas être recherchés ni reproduits sans autorisation.


Les normes liées au monitorage, aux réseaux, au logiciel et à la sécurité sont regroupées dans le [registre Normes et réglementation](../09-normes-et-recommandations/01-registre-normes-et-reglementation.md).
