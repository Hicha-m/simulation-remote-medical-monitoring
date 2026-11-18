# 08 — Registre des sources

**Date de consultation de référence :** 18 novembre 2026  
**But :** conserver les sources utilisées, les faits qu'elles appuient et leurs limites.

## A. Projets open source et outils

| ID | Source | Ce qu'elle documente | Limites |
|---|---|---|---|
| S01 | [Code for Japan — API](https://github.com/codeforjapan/remote-patient-monitoring-api) | Contexte, chronologie, fonctions, spécification et architecture du serveur. | Déclarations du dépôt ; projet lié au contexte COVID-19 au Japon. |
| S02 | [Code for Japan — Dashboard](https://github.com/codeforjapan/remote-patient-monitoring-dashboard) | Interface de suivi destinée aux professionnels ; Nuxt.js dans le README. | README et documentation, pas audit du code ou de l'usage actuel. |
| S03 | [Code for Japan — Client](https://github.com/codeforjapan/remote-patient-monitoring-client) | Client patient ; configuration et technologie Vue CLI mentionnées. | Pas d'audit du code actuel. |
| S04 | [HomeICU](https://github.com/iozwang/homeicu) | Moniteur portable, BLE, application base-station, flux de données et fonctionnalités annoncées. | Les fonctions « en développement » et revendications de qualité ne sont pas des certifications. |
| S05 | [Synthea](https://github.com/synthetichealth/synthea) | Génération de patients et dossiers synthétiques, formats d'export dont FHIR et CSV. | Ne fournit pas une plateforme de surveillance en direct. |
| S06 | [HAPI FHIR JPA Server Starter](https://github.com/hapifhir/hapi-fhir-jpaserver-starter) | Serveur FHIR Java avec persistance ; avertissements sur sécurité et logs absents par défaut. | Starter d'implémentation, pas une solution clinique complète. |
| S07 | [HL7 FHIR — Observation R5](https://www.hl7.org/fhir/observation.html) | Définition de la ressource Observation et exemples de mesures et constantes. | La version FHIR adaptée au périmètre doit être choisie. |
| S10 | [Open mHealth — Schemas](https://github.com/openmhealth/schemas) | Schémas, données d'essai, validation et SDK. | SDK Java déprécié ; dépôt en évolution. |
| S11 | [Mirth Connect](https://github.com/nextgenhealthcare/connect) | Intégration, filtrage, transformation et routage de messages de santé. | Pas une application de télésurveillance clé en main. |
| S23 | [Documentation HAPI FHIR](https://hapifhir.io/hapi-fhir/docs/server_jpa/get_started.html) | Démarrage d'un serveur FHIR JPA et options de persistance. | La documentation technique ne garantit pas une mise en conformité de l'application résultante. |

## B. Sources institutionnelles et réglementaires

| ID | Source | Ce qu'elle documente | Limites |
|---|---|---|---|
| S08 | [Ministère de la Santé — Vos questions, nos réponses sur la télésurveillance](https://sante.gouv.fr/soins-et-maladies/prises-en-charge-specialisees/telesante-pour-l-acces-de-tous-a-des-soins-a-distance/la-telesurveillance-11332/article/vos-questions-nos-reponses) | Types d'alertes, organisation et modalités de tri. | Le détail dépend des textes spécifiques et du contexte clinique. |
| S09 | [Code de la sécurité sociale — Section télésurveillance médicale](https://www.legifrance.gouv.fr/codes/id/LEGISCTA000044565906) | Articles L.162-48 à L.162-57, dont définition légale de l'activité. | Vérifier la version en vigueur au moment de toute décision. |
| S17 | [ANS — Champ d'application HDS](https://esante.gouv.fr/faq/quel-est-le-champ-dapplication-de-la-legislation-relative-lhebergement-de-donnees-de-sante-caractere-personnel) | Conditions cumulatives de l'obligation d'hébergement certifié HDS et appréciation au cas par cas. | Une analyse juridique et technique du cas concret reste nécessaire. |
| S18 | [ANS — Comité ENS du 30 septembre 2026, support HDS v2.1](https://esante.gouv.fr/sites/default/files/media/document/ComiteENS_30092026.pdf) | Calendrier prévisionnel actualisé de la version HDS v2.1, publication attendue à horizon décembre 2026. | Support de présentation et calendrier prévisionnel, à revérifier avant usage. |
| S19 | [CNIL — Sécurité : tracer les opérations](https://www.cnil.fr/fr/securite-tracer-les-operations) | Journalisation des opérations, accès, actions et incidents ; protection des traces. | Les recommandations doivent être adaptées au contexte et aux obligations applicables. |
| S20 | [CNIL — Sécurité : gérer les habilitations](https://www.cnil.fr/fr/securite-gerer-les-habilitations) | Gestion des profils et principe de moindre privilège. | À compléter par les politiques de l'organisation concernée. |
| S21 | [RGPD — Règlement (UE) 2016/679](https://eur-lex.europa.eu/legal-content/FR/TXT/?uri=CELEX:32016R0679) | Cadre européen de protection des données personnelles, article 9 et catégories particulières. | Le fondement juridique dépend du traitement réel. |
| S22 | [Règlement (UE) 2017/745 relatif aux dispositifs médicaux](https://eur-lex.europa.eu/legal-content/FR/TXT/?uri=CELEX:32017R0745) | Définitions et cadre des dispositifs médicaux, y compris logiciels selon leur destination. | La qualification dépend de la finalité prévue et des fonctionnalités. |
| S25 | [Légifrance — Arrêté du 3 mars 2026, télésurveillance](https://www.legifrance.gouv.fr/eli/arrete/2026/3/3/SFHS2606147A/jo/article_snum1) | Exemple récent d'organisation de l'opérateur, rôles et continuité des soins. | Texte associé à une activité/pathologie et à lire dans son contexte. |

## C. Marché et retours d'expérience

| ID | Source | Ce qu'elle documente | Limites |
|---|---|---|---|
| S12 | [Resilience — Retour d'expérience à l'Hôpital Européen Marseille](https://www.resilience.care/fr/ressources/favoriser-ladhesion-des-patients-et-des-professionnels-de-sante-a-la-telesurveillance-medicale) | Déploiement en oncologie, équipe, inclusion, consentement, traitement des alertes et accompagnement patient. | Source fournisseur relatant une expérience partenaire ; pas une étude indépendante. |
| S13 | [Resilience Care — Solutions](https://www.resilience.care/fr) | Positionnement produit et spécialités annoncées, statut de produits présenté par le fournisseur. | Déclarations commerciales ; notices et bases officielles à vérifier. |
| S14 | [BIOTRONIK — Home Monitoring](https://www.biotronik.com/en-int/managing-af) | Flux du dispositif implanté vers passerelle et plateforme distante, alertes et absence de transmission. | Documentation du fabricant ; périmètre centré sur ses dispositifs et indications. |
| S15 | [Implicity](https://implicity.com/) | Plateforme multi-constructeurs de suivi à distance des dispositifs cardiaques implantables. | Documentation commerciale ; preuves et indications doivent être vérifiées. |
| S16 | [Semeia — MedicWise](https://www.semeia.io/notre-solution) | Collecte, analyse, alertes et plans personnalisés annoncés pour maladies chroniques. | Documentation fournisseur ; informations à confronter aux notices et données indépendantes. |
| S24 | [UniHA — Marché télésurveillance médicale M_2941](https://www.uniha.org/marche/telesurveillance-medicale-m-2941) | Marché actif 2023–2029, périmètre du SAD et liste de candidats admis mise à jour août 2026. | La liste ne mesure pas les ventes, parts de marché ni le nombre de déploiements par fournisseur. |

## D. Notes de lecture

1. Les pages de produits et les retours d'expérience publiés par un fournisseur doivent être considérés comme des sources commerciales ou partenaires.
2. Un dépôt GitHub public ne prouve ni la qualité clinique, ni la sécurité, ni la conformité d'une solution.
3. La présence d'un fournisseur dans un marché public ne prouve pas qu'il est utilisé dans chaque établissement.
4. Un standard décrit un format ou un mécanisme ; il ne définit pas à lui seul l'organisation du soin.
5. Les règles réglementaires doivent être réexaminées à la date de tout changement de périmètre ou de déploiement.
6. Cette liste constitue la base initiale de recherche, et non une bibliographie exhaustive.
