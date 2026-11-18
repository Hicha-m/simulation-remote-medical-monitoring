# 05 — Prompt : analyser l'architecture technique des systèmes de monitorage hospitalier

## Prompt réutilisable

Tu es chargé de conduire une étude technique et documentaire des systèmes de monitorage hospitalier réellement utilisés ou commercialisés : moniteurs de chevet, moniteurs de transport, télémétrie hospitalière, centrales de surveillance, passerelles, systèmes d'intégration et serveurs.

Le projet cible est un POC académique de simulation logicielle. Aucune architecture cible ne doit être décidée pendant la recherche.

## Objectifs

Pour chaque fabricant, système et version étudiés :
- reconstituer les composants physiques et logiciels ;
- décrire les réseaux et leur segmentation ;
- identifier les protocoles et interfaces ;
- distinguer flux de mesures, courbes, alarmes, événements, ADT et maintenance ;
- décrire les passerelles et le rôle du SIH ;
- identifier les formes de stockage et d'archivage documentées ;
- décrire les modes de disponibilité et de reprise ;
- relever les mécanismes de sécurité ;
- distinguer ce qui est public, accessible sous contrat et privé.

## Sources à privilégier

1. Manuels d'installation et notices d'utilisation du modèle exact.
2. Security guides, hardening guides et security advisories du fabricant.
3. Marchés publics, CCTP et documentation des centrales d'achat.
4. Profils IHE, HL7, IEEE, IEC et référentiels ANS.
5. Retours d'expérience d'établissements et études évaluées par les pairs.
6. Documents marketing, uniquement comme déclaration du fabricant.

## Pour chaque système

Produire une fiche contenant :
- fabricant, gamme, modèle, version et date de la documentation ;
- contexte de soins et destination ;
- composants et topologie logique ;
- réseaux, VLAN, interfaces, protocoles et ports si publics ;
- données transportées et sens des flux ;
- comportement temps réel et historique ;
- ADT, DPI, HL7, IHE, FHIR ou interfaces propriétaires ;
- stockage, archivage, sauvegarde ;
- disponibilité, redondance, rattrapage ;
- authentification, chiffrement, certificats et contrôle d'accès ;
- maintenance distante et mise à jour ;
- contraintes et dépendances ;
- informations manquantes ou confidentielles.

## Règles strictes

- Ne jamais inventer un protocole, un port, une architecture ou une configuration.
- Ne pas supposer que les quatre fabricants utilisent les mêmes principes.
- Distinguer les capacités commerciales des performances mesurées.
- Ne pas présenter une brochure comme une preuve de déploiement.
- Ne pas déduire la configuration réelle d'un hôpital à partir d'une documentation générale.
- Ne pas rechercher, publier ni reconstituer les secrets, IP, VLAN, règles firewall ou accès privés d'un établissement réel.
- Distinguer architecture de référence, installation client et déploiement réel.

## Format de sortie

1. Fiche de chaque fournisseur.
2. Schémas fonctionnels basés sur les sources.
3. Tableau comparatif des réseaux et protocoles.
4. Flux de données détaillés.
5. Points d'intégration SIH.
6. Sécurité par flux et par composant.
7. Informations privées / non documentées.
8. Questions à poser à un intégrateur, biomédical et DSI.
9. Sources avec pages, versions et limites.

## Paramètres

- Date de recherche : [à compléter]
- Fabricants : Philips, GE HealthCare, Dräger, Mindray, Nihon Kohden, Spacelabs et autres systèmes pertinents.
- Pays : France en priorité.
- Contexte : monitorage hospitalier, pas télésurveillance à domicile.
