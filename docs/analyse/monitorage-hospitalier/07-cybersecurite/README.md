# Cybersécurité — dossier d'étude

**Version :** 0.1 — **Date :** 18 novembre 2026  
**Statut :** état des pratiques documentées et retours d'expérience publics ; aucune certification ou conformité revendiquée.

## Objectif

Étudier les protections réellement documentées dans les systèmes de monitorage, les attaques et fuites connues dans les établissements et chez les fournisseurs, puis traduire ces constats en besoins de sécurité pour le projet.

## Documents

1. [Sécurité des dispositifs, réseaux et centrales](01-securite-dispositifs-reseaux.md) — mécanismes décrits par GE, Philips, Dräger et Mindray.
2. [Vulnérabilités, attaques et fuites documentées](02-incidents-vulnerabilites-et-fuites.md) — cas Contec, Philips, hôpitaux français et fournisseur.
3. [Prévention, détection, réponse et continuité](03-prevention-detection-reponse-continuite.md) — contrôles et organisation à étudier.
4. [Modèle de menace et matrice de risques](04-modele-de-menace-et-matrice.md) — scénarios, impacts et besoins de test du POC.

## Principes

- Distinguer une vulnérabilité publiée d'une exploitation confirmée.
- Distinguer une attaque contre le SI général d'une attaque contre un moniteur.
- Ne pas attribuer un incident à un fabricant ou à un protocole sans preuve.
- Décrire les attaques à un niveau permettant de comprendre le risque et la prévention, sans reproduire de procédure d'intrusion.
- Utiliser uniquement des données fictives et des scénarios de sécurité contrôlés dans le POC.
- Ne jamais connecter les simulateurs à un réseau hospitalier réel sans autorisation.

## Repères institutionnels

- PGSSI-S : référentiels et guides de sécurité des systèmes d'information de santé [H48].
- Observatoire CERT Santé : données annuelles sur les incidents déclarés et retours d'expérience [H51].
- Guides et alertes du CERT Santé : confinement, analyse, correction et surveillance [H49–H51].


Les cadres de sécurité applicables et recommandations françaises sont regroupés dans le [registre Normes et réglementation](../09-normes-et-recommandations/01-registre-normes-et-reglementation.md) et les [recommandations](../09-normes-et-recommandations/02-recommandations.md).
