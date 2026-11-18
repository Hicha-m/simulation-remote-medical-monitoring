# Normes 01 — Registre des normes et textes applicables au monitorage hospitalier

**Version :** 0.1  
**Date :** 18 novembre 2026  
**Attention :** cette liste est un registre de repérage. Elle ne remplace pas une analyse réglementaire, la consultation des textes complets ni la vérification des éditions harmonisées EN publiées au Journal officiel de l'Union européenne.

## 1. Comprendre les trois niveaux

| Niveau | Nature | Exemple | Rôle |
|---|---|---|---|
| Réglementation | Texte juridiquement contraignant dans son champ. | MDR 2017/745, RGPD, Code de la santé publique. | Définit les obligations des fabricants, organismes et traitements concernés. |
| Norme technique | Référentiel consensuel de conception, test, qualité ou sécurité. | IEC 60601-1, ISO 14971, IEC 62304. | Donne une manière structurée de démontrer certaines exigences. |
| Recommandation / référentiel métier | Guide, procédure, certification ou bonnes pratiques. | HAS, ANS PGSSI-S, CNIL, ANSM. | Décrit les pratiques attendues et les contrôles utiles. |

Une norme IEC/ISO n'est pas automatiquement une obligation légale pour notre POC. Pour un dispositif médical mis sur le marché dans l'Union européenne, il faut aussi vérifier les normes harmonisées applicables et leur publication au Journal officiel de l'Union européenne à la date concernée.

## 2. Normes de sécurité et performance des dispositifs de monitorage

| Référence | Domaine | Pertinence pour le sujet | Statut repéré au 18/11/2026 |
|---|---|---|---|
| IEC 60601-1:2005 + A1:2012 + A2:2020 | Sécurité de base et performances essentielles des appareils électromédicaux. | Socle des moniteurs et systèmes électromédicaux réels. | Version consolidée publiée par IEC. |
| IEC 60601-1-2:2014 + A1:2020 | Compatibilité électromagnétique (CEM), émissions et immunité. | Pertinent pour la coexistence des appareils, réseaux, radios et environnements hospitaliers. | Version consolidée publiée par IEC. |
| IEC 60601-1-8:2006 + A1:2012 + A2:2020 | Systèmes d'alarme des dispositifs électromédicaux : catégories de priorité, signaux, états de commande, essais et guidance. | Référence centrale pour l'étude des alarmes des moniteurs. Elle concerne le système d'alarme de l'appareil, pas à elle seule l'organisation humaine complète du service. | Version consolidée publiée ; stabilité IEC annoncée jusqu'en 2028. |
| IEC 80601-2-49:2018 + A1:2024 | Sécurité et performances essentielles des moniteurs multiparamétriques. | Référence particulièrement proche d'un moniteur de chevet regroupant plusieurs paramètres physiologiques. | Version consolidée 1.1 publiée en septembre 2024. |
| IEC 60601-2-27:2011 | Équipements de monitorage ECG. | À examiner si le POC simule ECG, rythme ou télémétrie ECG. | Édition IEC 2011 publiée ; vérifier les amendements et l'édition EN applicable. |
| IEC 80601-2-30:2018 | Sphygmomanomètres automatiques non invasifs. | À examiner pour la mesure périodique de pression artérielle par brassard. | Édition 2018 publiée, révision en cours (IEC/DIS annoncé). |
| ISO 80601-2-61:2026 | Équipement d'oxymétrie de pouls : moniteur, sonde et câble. | À examiner pour SpO₂ et mesure du pouls. | Nouvelle édition 3 publiée le 10 avril 2026 ; remplace l'édition 2011. |

Ces standards sont des références produit : ils concernent la sécurité et les performances essentielles de dispositifs médicaux réels, pas la simple simulation logicielle de valeurs.

### Autres normes produit éventuelles

Selon les paramètres et appareils retenus, une recherche complémentaire sera nécessaire pour :
- pression artérielle invasive ;
- température clinique ;
- gaz respiratoires et capnographie ;
- ventilateurs de soins critiques ;
- moniteurs spécialisés néonatals ou fœtaux ;
- appareils de transport et environnement électromagnétique particulier.

Il ne faut pas ajouter toutes ces normes au périmètre sans choisir d'abord les paramètres et familles d'équipements simulés.

## 3. Normes de cycle de vie logiciel, qualité et facteurs humains

| Référence | Domaine | Pertinence |
|---|---|---|
| ISO 14971:2019 | Gestion des risques des dispositifs médicaux sur tout le cycle de vie. | Structurer les dangers, situations dangereuses, contrôles et risques résiduels du système étudié. Version confirmée par ISO en 2025. |
| IEC 62304:2006 + A1:2015 | Processus du cycle de vie du logiciel de dispositif médical. | Exigences de développement, maintenance et maîtrise des changements si le logiciel relève d'un dispositif médical. Confirmée par ISO en 2023. |
| IEC 62366-1:2015 + A1:2020 | Ingénierie de l'aptitude à l'utilisation des dispositifs médicaux. | Étudier les erreurs d'utilisation, l'ergonomie de la centrale et les risques liés à l'interface. |
| IEC 81001-5-1:2021 | Activités de cybersécurité dans le cycle de vie du logiciel de santé. | Référence de sécurité dès la conception, pendant la maintenance et jusqu'à la fin de vie. Une révision est en développement ; vérifier le statut avant usage réglementaire. |
| ISO 13485:2016 | Système de management de la qualité pour les dispositifs médicaux. | Plutôt une norme de système qualité du fabricant et de ses processus que de l'application elle-même. Confirmée en 2025. |
| ISO 20417:2026 | Informations à fournir par le fabricant d'un dispositif médical. | Instructions, documentation, étiquetage, informations de sécurité et informations d'accompagnement. Édition 2026 publiée en mars 2026. |
| ISO 15223-1:2021 + A1:2025 | Symboles utilisés pour les informations fournies avec les dispositifs médicaux. | À considérer si le projet représente les étiquettes, états et symboles d'un vrai dispositif. |

## 4. Normes de réseau, cybersécurité et information de santé

| Référence | Domaine | Pertinence |
|---|---|---|
| IEC 80001-1:2021 | Gestion des risques des réseaux informatiques intégrant des dispositifs médicaux et logiciels de santé ; équilibre sécurité, efficacité et sûreté. | Très importante pour comprendre les responsabilités entre soins, biomédical, DSI, RSSI et fournisseurs. |
| ISO 27799:2025 | Contrôles de sécurité de l'information propres au secteur de la santé, fondés sur ISO/IEC 27002:2022. | Référence dédiée aux organisations de santé et aux dispositifs intégrant du logiciel. Remplace l'édition 2016. |
| ISO/IEC 27001:2022 + A1:2024 | Exigences d'un système de management de la sécurité de l'information (SMSI). | Cadre organisationnel pour gouverner les risques de sécurité. |
| ISO/IEC 27002:2022 | Catalogue de mesures de sécurité : accès, cryptographie, ressources humaines, incidents, etc. | Guide de contrôles à adapter au contexte. Ne constitue pas en soi une certification. |
| IEC 81001-5-1:2021 | Secure software lifecycle en santé. | Complète la gouvernance d'entreprise par la sécurité du produit logiciel. |

Ne pas confondre IEC 80001-1 et IEC 81001-5-1 :
- IEC 80001-1 porte sur la gestion des risques du réseau de santé connecté et les responsabilités organisationnelles ;
- IEC 81001-5-1 porte sur les activités de cybersécurité dans le cycle de vie du logiciel de santé.

## 5. Interopérabilité et représentation des données

| Référence | Nature | Rôle possible |
|---|---|---|
| HL7 v2 | Standard de messagerie de santé | Échanges administratifs et observations entre moniteurs, centrales et SIH selon les interfaces disponibles. |
| HL7 FHIR | Standard de ressources et d'API de santé | Représenter Patient, Device, Observation, Provenance et autres informations structurées. |
| IHE PCD | Profils d'intégration de dispositifs de soins | Décrire des cas d'échange entre dispositifs, systèmes de monitorage et applications cliniques. |
| IEEE 11073 | Famille de standards de communication de dispositifs médicaux au point de soin | Étudier la représentation et les échanges appareil–système. |
| LOINC | Terminologie d'identification d'observations | Coder le type de mesure de manière cohérente, si l'interopérabilité est dans le périmètre. |
| UCUM | Système unifié de codes d'unités | Représenter les unités de mesure sans ambiguïté. |

En France, le CI-SIS de l'ANS définit les règles et standards d'interopérabilité des logiciels de santé. Il s'appuie sur HL7 CDA, HL7 FHIR, DICOM et des profils IHE. Les volets et guides doivent être choisis selon le cas d'usage, pas par simple accumulation de standards.

Pour le POC, FHIR peut servir à représenter ou exporter des observations ; cela ne signifie pas que toutes les courbes temps réel doivent être envoyées en FHIR.

## 6. Réglementation européenne et française

### 6.1 Règlement européen sur les dispositifs médicaux (MDR 2017/745)

Le MDR encadre les dispositifs médicaux mis sur le marché ou mis en service dans l'Union européenne. Il exige notamment :
- finalité prévue définie par le fabricant ;
- respect des exigences générales de sécurité et de performance ;
- système de gestion des risques ;
- documentation technique ;
- évaluation clinique et suivi après commercialisation selon les cas ;
- processus qualité et vigilance ;
- justification des solutions de conception et validation.

La règle 11 de l'annexe VIII classe les logiciels selon leur finalité :
- logiciel fournissant des informations utilisées pour des décisions diagnostiques ou thérapeutiques : en principe classe IIa, avec des règles IIb/III selon la gravité potentielle ;
- logiciel destiné à surveiller des processus physiologiques : en principe classe IIa, mais IIb lorsque la surveillance porte sur des paramètres physiologiques vitaux dont les variations peuvent entraîner un danger immédiat ;
- autres logiciels : classe I, sous réserve de leur qualification et de leurs fonctions.

La guidance MDCG 2019-11, révision 1 de juin 2025, aide à qualifier et classer les logiciels au regard du MDR et de l'IVDR. Elle n'est pas juridiquement contraignante, mais constitue une interprétation commune de référence.

**Application au projet :** un simulateur pédagogique qui génère des données artificielles et qui n'est pas destiné à être utilisé pour surveiller, diagnostiquer ou traiter un patient n'est pas automatiquement un dispositif médical. Cette conclusion dépend de la finalité revendiquée, des fonctionnalités et de l'usage réel. Si la finalité change, une qualification réglementaire spécifique sera nécessaire.

### 6.2 RGPD

Les données de santé sont des catégories particulières de données personnelles au sens de l'article 9. Le traitement réel nécessite une base juridique et une condition applicable de l'article 9, ainsi que les obligations générales de protection des données.

**Application au POC :** utiliser des données synthétiques qui ne reprennent pas des dossiers réels et ne permettent pas d'identifier une personne. Si des données personnelles de santé réelles sont introduites, le périmètre juridique et sécurité doit être réévalué avant toute collecte.

### 6.3 HDS — Hébergement de données de santé

L'article L.1111-8 du Code de la santé publique encadre l'hébergement de données de santé à caractère personnel recueillies dans le cadre d'activités de prévention, diagnostic, soins ou suivi, pour le compte des personnes ou organismes à l'origine du recueil ou du patient.

L'obligation HDS vise le prestataire hébergeur lorsque les conditions du texte sont réunies. Elle ne signifie pas que chaque logiciel de santé, chaque serveur local d'un hôpital ou chaque POC utilisant des données fictives doit automatiquement obtenir une certification HDS.

L'ANS affiche actuellement les référentiels de certification et d'accréditation HDS v2.1 sur sa procédure de certification. Le calendrier réglementaire et la date d'entrée en vigueur de chaque exigence doivent être contrôlés dans l'arrêté applicable et le Journal officiel avant tout contrat ou déploiement.

### 6.4 PGSSI-S

La Politique générale de sécurité des systèmes d'information de santé rassemble des référentiels d'exigences, des guides et des recommandations. Certains documents sont opposables ; d'autres sont des guides pratiques. Les référentiels sont présentés avec des paliers de sécurité adaptés au contexte.

Le bon usage consiste à sélectionner les documents PGSSI-S correspondant au type de traitement, au rôle de l'acteur et au niveau de sécurité visé.

### 6.5 Référentiels HAS et recommandations françaises

Le référentiel HAS de certification des établissements de santé version 2027 inclut notamment :
- critère 2.3-12 : surveillance visuelle et sonore des patients en soins critiques, procédure de gestion des systèmes de surveillance et des seuils d'alarme, report des alarmes de scopes et ventilateurs par des professionnels formés, continuité pendant le transport ;
- critère 3.1-07 : maîtrise des risques de sécurité numérique, entraînement aux attaques, plan de continuité et reprise ;
- critère 3.1-08 : comptes individuels, habilitations, suppression des accès lors des changements de statut, sauvegardes et authentification renforcée à distance.

Ces critères s'adressent aux établissements de santé ; ils servent ici de référentiel métier et organisationnel pour le réalisme du POC.

## 7. Ce qui est réellement pertinent pour notre POC

| Référence | À appliquer comme exigence légale au POC ? | Utilisation recommandée dans le projet |
|---|---|---|
| IEC 60601 et sous-parties | Non, pas au logiciel de simulation seul. | Comprendre les comportements et limites des vrais équipements. |
| IEC 60601-1-8 | Non, pas certification du POC. | Organiser les types, priorités et états d'alarme simulés. |
| ISO 14971 | Pas une obligation de certification pour un POC pédagogique. | Faire une analyse de risques structurée. |
| IEC 62304 | Pas automatiquement applicable si le POC n'est pas un logiciel médical. | S'inspirer de la traçabilité, du versionnement, des tests et de la gestion des changements. |
| IEC 62366-1 | Pas une obligation de certification du POC. | Tester l'ergonomie et les erreurs d'utilisation du dashboard. |
| IEC 80001-1 | Pas une certification du POC isolé. | Analyser les risques aux frontières entre réseau, appareils et SI hospitalier. |
| IEC 81001-5-1 | Pas automatiquement obligatoire pour ce POC. | S'inspirer du cycle de développement sécurisé. |
| ISO 27799 / 27001 / 27002 | Pas de certification à rechercher pour le POC. | Constituer une checklist sécurité et gouvernance. |
| HL7 / FHIR / IHE | Selon besoin d'interopérabilité. | Définir un modèle d'échange ou un export, si justifié. |
| MDR | À qualifier selon la finalité réelle. | Maintenir le simulateur hors de l'usage clinique et sans revendication médicale. |
| RGPD | Si des données personnelles sont traitées. | Privilégier des données synthétiques non personnelles. |
| HDS | Si un hébergeur tiers héberge des données personnelles de santé dans les conditions légales. | Éviter ce sujet en restant local/synthétique pour le POC. |
| HAS / PGSSI-S / ANSM / CNIL | Références de pratique, d'organisation et de sécurité. | Traduire leurs principes en scénarios et critères de test. |

## 8. Sources officielles

- **H66** IEC 60601-1, version consolidée incluant A1:2012 et A2:2020 : https://webstore.iec.ch/en/publication/2605
- **H67** IEC 60601-1-8, version consolidée 2006+A1:2012+A2:2020 : https://webstore.iec.ch/en/publication/2598
- **H68** IEC 60601-1-2:2014+A1:2020 : https://webstore.iec.ch/en/publication/67554
- **H69** IEC 80601-2-49:2018+A1:2024 : https://webstore.iec.ch/en/publication/100456
- **H70** IEC 60601-2-27:2011 : https://webstore.iec.ch/en/publication/2638
- **H71** IEC 80601-2-30:2018 : https://www.iso.org/standard/70653.html
- **H72** ISO 80601-2-61:2026 : https://webstore.iec.ch/en/publication/74527
- **H73** ISO 14971:2019 : https://www.iso.org/fr/standard/72704.html
- **H74** IEC 62304:2006+A1:2015 : https://www.iso.org/fr/standard/38421.html
- **H75** IEC 62366-1:2015+A1:2020 : https://www.iso.org/fr/standard/63179.html
- **H76** IEC 80001-1:2021 : https://webstore.iec.ch/en/publication/34263
- **H77** IEC 81001-5-1:2021 : https://www.iso.org/standard/76097.html
- **H78** ISO 13485:2016 : https://www.iso.org/fr/standard/13485
- **H79** ISO 27799:2025 : https://www.iso.org/fr/standard/84647.html
- **H80** ISO/IEC 27001:2022 : https://www.iso.org/fr/standard/27001
- **H81** ISO/IEC 27002:2022 : https://www.iso.org/fr/standard/75652.html
- **H82** ISO 20417:2026 : https://www.iso.org/standard/20417
- **H83** ISO 15223-1:2021+A1:2025 : https://www.iso.org/fr/standard/77326.html
- **H84** Règlement (UE) 2017/745 (MDR) : https://eur-lex.europa.eu/eli/reg/2017/745/oj/eng
- **H85** MDCG 2019-11 Rev.1, qualification et classification du logiciel, juin 2025 : https://health.ec.europa.eu/system/files/2025-06/mdcg_2019_11_en.pdf
- **H86** MDCG 2019-16 Rev.1, cybersécurité des dispositifs médicaux : https://health.ec.europa.eu/document/download/b23b362f-8a56-434c-922a-5b3ca4d0a7a1_en?filename=md_cybersecurity_en.pdf
- **H87** ANS — PGSSI-S : https://esante.gouv.fr/securite/politique-generale-de-securite-des-systemes-d-information-de-sante
- **H88** ANS — Doctrine et CI-SIS interopérabilité : https://esante.gouv.fr/doctrine/interoperabilite
- **H89** ANS — procédure de certification HDS v2.1 : https://esante.gouv.fr/produits-services/hds/procedure-de-certification-hebergeur-de-donnees-de-sante
- **H90** Code de la santé publique, article L.1111-8 : https://www.legifrance.gouv.fr/codes/article_lc/LEGIARTI000033862549
- **H91** RGPD, règlement (UE) 2016/679, article 9 : https://eur-lex.europa.eu/eli/reg/2016/679/
- **H92** CNIL — Guide de la sécurité des données personnelles, édition 2024 : https://www.cnil.fr/fr/guide-de-la-securite-des-donnees-personnelles-nouvelle-edition-2024
- **H93** HAS — Référentiel de certification des établissements de santé, version 2027 : https://www.has-sante.fr/jcms/p_4139595/fr/referentiel-de-certification-des-etablissement-de-sante-pour-la-qualite-des-soins-version-2027
- **H94** HAS — Flash Sécurité Patient, surveillance des patients en soins critiques, 25 avril 2024 : https://www.has-sante.fr/jcms/p_3511526/fr/flash-securite-patient-surveillance-des-patients-en-service-de-soins-critiques-une-veille-sans-faille-pour-qu-aucun-patient-ne-defaille
- **H95** ANSM — Gestion des alarmes des dispositifs médicaux dans les établissements de santé, septembre 2019 : https://ansm.sante.fr/uploads/2020/10/16/20201016-rapport-gestion-alarmes-dm.pdf
- **H96** ANS — Programme CaRE, axe 4 Sécurité opérationnelle : https://esante.gouv.fr/produits-services/cybersecurite/programme-care/programme-care-axe-4-securite-operationnelle

## 9. Mise à jour nécessaire avant tout usage réglementaire

Avant toute décision qui viserait un dispositif médical réel ou un déploiement clinique :
1. vérifier le texte consolidé applicable ;
2. vérifier les éditions EN harmonisées publiées au Journal officiel pour le MDR ;
3. vérifier les amendements et corrigenda de chaque norme ;
4. vérifier le champ d'application des obligations RGPD et HDS ;
5. vérifier les versions des référentiels ANS et HAS ;
6. faire valider la qualification réglementaire et la stratégie de conformité par les personnes compétentes.

Les textes complets ISO/IEC sont souvent payants. Les résumés publics utilisés ici permettent d'identifier le domaine et le statut, mais ne suffisent pas à démontrer une conformité détaillée.
