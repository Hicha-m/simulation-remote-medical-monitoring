# Marché 01 — Écosystème, achats publics et systèmes de monitorage hospitalier en France

**Version :** 0.1  
**Date de consultation :** 18 novembre 2026  
**Objet :** distinguer les systèmes documentés par les fabricants, les pratiques réellement observées et les marchés publics qui montrent les solutions recherchées ou achetées par les établissements.

## 1. Conclusion provisoire

Le marché hospitalier français ne repose pas sur un équipement unique. Les sources consultées montrent un écosystème composé de :

- moniteurs multiparamétriques de chevet ;
- moniteurs transportables ;
- émetteurs de télémétrie pour patients mobiles ;
- centrales de surveillance ;
- postes et écrans déportés ;
- systèmes de gestion et de report des alarmes ;
- logiciels de recueil et d'intégration des données de dispositifs médicaux ;
- interfaces vers le dossier patient informatisé et le système d'information hospitalier ;
- prestations d'installation, de paramétrage, de formation, de maintenance et de cybersécurité.

Les fabricants identifiés dans les références institutionnelles et les marchés comprennent notamment Philips, GE HealthCare, Dräger, Mindray, Nihon Kohden et Spacelabs Healthcare. Les fonctions et périmètres varient selon les produits et les lots de marché [H33–H37].

**Limite importante :** un marché public ou un catalogue de centrale d'achat prouve qu'une solution est référencée, mise en concurrence, attribuée ou proposée aux hôpitaux. Il ne prouve pas, à lui seul, qu'un modèle précis est déjà installé dans chaque établissement adhérent. Pour établir l'installation effective dans un hôpital donné, il faut un retour d'expérience de cet hôpital, un document de déploiement, un inventaire public ou un témoignage vérifiable.

## 2. Ce que l'on sait des pratiques hospitalières françaises

### 2.1 Rapport ANSM sur la gestion des alarmes

L'ANSM a publié en septembre 2019 un rapport sur les alarmes des dispositifs médicaux dans les établissements de santé. Il combine l'analyse de signalements de matériovigilance, une enquête auprès de services hospitaliers, la littérature, les normes et des informations collectées auprès de fabricants [H33].

L'enquête a été réalisée à l'été 2017. Elle a recueilli **631 réponses de services issues de 318 établissements**, réparties entre cinq régions pilotes et entre établissements publics et privés. Le questionnaire visait plusieurs types de services : soins critiques, bloc ou urgences, et unité médicale moins critique [H33].

Résultats de l'enquête à ne pas confondre avec une mesure actuelle 2026 :

| Constat rapporté | Résultat de l'enquête | Interprétation correcte |
|---|---:|---|
| Services disposant d'un système de report d'alarmes de monitorage en temps réel | 56 % des services répondants | Le report d'alarme était déjà une pratique importante dans l'échantillon 2017, mais pas universelle. |
| Report sur centrale de surveillance parmi les services équipés d'un report | 92,44 % | Le report centralisé était le mode dominant dans l'enquête. |
| Report inter-chevet parmi les services équipés d'un report | 40,34 % | Certaines installations diffusaient également les alarmes vers d'autres moniteurs. |
| Report sur mobile dédié (par exemple bip) parmi les services équipés | 3,64 % | Le report par terminal mobile dédié était peu représenté. |
| Report sur smartphone non dédié parmi les services équipés | 0,84 % | Les smartphones non dédiés n'étaient pas le moyen courant dans cet échantillon. |
| Concentration d'alarmes issues de plusieurs dispositifs et marques | 16,32 % des services répondants | La centralisation multi-équipements était nettement moins répandue que le simple report de moniteur. |

La majorité du parc de report d'alarmes recensé par l'ANSM provenait de cinq fabricants : **Philips, GE, Dräger, Mindray et Nihon Kohden**. Le rapport observe aussi que 56,10 % des services désignaient les moniteurs cardiorespiratoires et centrales comme les dispositifs dont la gestion des alarmes les préoccupait le plus [H33].

### 2.2 Les problèmes rencontrés ne sont pas uniquement techniques

Le rapport ANSM décrit des incidents critiques associés :
- à l'acquittement d'une alarme sans intervention ;
- à l'absence de compréhension de l'escalade des alertes sur mobile ;
- à des alarmes non reportées à la centrale ;
- à une alarme de perte de signal non transmise parce que la configuration ne reportait que certaines priorités ;
- à une centrale configurée pour ne montrer qu'une partie des lits ou à des fenêtres d'alarme qui masquaient d'autres événements ;
- à des câbles ou capteurs dégradés ;
- à des batteries ayant entraîné l'arrêt de moniteurs de transport [H33].

Le rapport précise également que seulement 35,29 % des services répondants disposant d'un report d'alarme déclaraient avoir prévu un fonctionnement dégradé en cas de panne de ce report [H33].

**Conséquence pour le projet :** tester seulement l'envoi d'une valeur physiologique ne suffit pas. Il faut étudier le report, la priorité, la destination, la prise de connaissance, l'acquittement, la visibilité de plusieurs patients et le fonctionnement en cas de panne.

## 3. Marchés publics et centrales d'achat : preuves récentes

### 3.1 UniHA — Monitoring multiparamétrique M_1908 (2023–2027)

La centrale d'achat UniHA présente un marché actif du 23 février 2023 au 22 février 2027, coordonné par la filière ingénierie biomédicale du CHU de Rennes. Il porte explicitement sur l'acquisition de moniteurs multiparamétriques et sur les services associés de maintenance et de formation [H34].

Le périmètre couvre :
- patients adultes et pédiatriques, avec protocoles dédiés en néonatalogie ;
- soins intermédiaires, notamment SSPI ;
- blocs opératoires ;
- réanimation et soins critiques ;
- environnement IRM [H34].

Le marché distingue plusieurs lots et familles de produits. La page publique cite notamment :
- moniteurs de soins intermédiaires ;
- moniteurs de soins critiques ;
- moniteurs avec ports universels multi-paramètres ;
- solution de monitorage de paramètres vitaux à distance ;
- moniteur amagnétique ;
- moniteurs transcutanés d'oxygénation et de ventilation ;
- solutions de mesure du débit cardiaque ;
- neuromonitoring peropératoire ;
- solution globale et multisource de gestion des alarmes de dispositifs médicaux ;
- moniteurs respiratoires [H34].

Les titulaires publiés comprennent Mindray Medical France, Nihon Kohden France, Philips France, Schiller France, Radiometer, Edwards Lifesciences, Getinge France, Masimo Europe, Edan et d'autres fournisseurs [H34]. La page n'associe pas nécessairement chaque nom à chaque lot dans sa vue publique ; aucun rattachement lot-fournisseur n'est donc inventé ici.

L'élément intéressant pour notre analyse est que le marché ne traite pas seulement le moniteur : il inclut les services, la formation, les options de location et de garantie, et la possibilité de répondre à l'échelle d'un service, d'un établissement ou d'un GHT. UniHA mentionne également la fatigue liée aux alarmes et les tentatives des industriels pour la réduire [H34].

### 3.2 UniHA — Gestion optimisée d'un parc de monitorage M_2976 (avis de marché 2024)

Un avis de marché publié le 20 décembre 2024 par UniHA concerne des prestations relatives à une gestion optimisée du parc de monitoring patient. Il distingue explicitement les catégories de systèmes de surveillance des patients, les moniteurs, les postes centraux de surveillance et la réparation/maintenance des équipements médicaux [H35].

L'avis porte sur un marché de 48 mois et prévoit une exécution pour les adhérents sur l'ensemble du territoire français, y compris les DROM-COM. Il s'agit d'une procédure de dialogue compétitif [H35].

Point particulièrement révélateur : le critère de capacité technique demande des ressources et références relatives à l'étude préliminaire, l'installation et la mise en service, le paramétrage, la formation, la maintenance et l'assistance sur la durée de vie du matériel. Le critère de références professionnelles impose aux candidats de justifier de solutions de monitorage déjà déployées ou en cours de déploiement, avec au moins 50 lits de réanimation et 50 salles d'opération équipés pour passer cette phase de sélection [H35].

Ce document apporte une information métier très concrète : les acheteurs ne recherchent pas uniquement des appareils. Ils attendent des capacités de déploiement à grande échelle, d'intégration, d'assistance, de formation et de maintenance.

**Limite :** cet avis prouve l'existence d'une procédure et de ses exigences ; à lui seul, il ne prouve pas le résultat final de l'attribution, le nom du fournisseur retenu ni l'installation effective dans un établissement.

### 3.3 RESAH — Gestion de parc en ventilation et monitorage 2025-R023 (2025–2029)

Le RESAH présente une offre disponible du 16 octobre 2025 au 15 octobre 2029 pour la gestion de parc en ventilation, monitorage et logiciels associés. La page distingue deux lots :
- lot 001 : gestion de parc en ventilation, titulaire Dräger France ;
- lot 002 : solutions de recueil de données, titulaire Philips [H36].

Pour le lot Philips, la page du RESAH décrit un ensemble cohérent de composants :
1. IntelliVue PIC iX : station centralisée avec visualisation multi-patients et continuité du suivi ;
2. IntelliVue PM6100 : moniteur multiparamétrique compact de 10 pouces ;
3. IntelliVue PM6300 : moniteur de 15 pouces, avec options supplémentaires ;
4. IntelliVue X3 : moniteur combinant usage au chevet et transport ;
5. IntelliVue MX750 : moniteur semi-modulaire de grand format destiné notamment aux soins critiques ;
6. IntelliVue MX40 : moniteur portable sans fil ;
7. Event Notification : solution de report d'alarmes vers les soignants sur dispositif mobile ;
8. IntelliVue Guardian Software : outil de scoring et de surveillance de patients en hospitalisation conventionnelle ;
9. EarlyVue VS30 : appareil de surveillance ponctuelle des constantes ;
10. Expression MR400 : solution de monitorage dans l'environnement IRM ;
11. Philips MDI / Capsule : plateforme d'intégration de flux issus de dispositifs biomédicaux vers les systèmes d'information ;
12. Philips ICCA : logiciel clinique de réanimation et d'anesthésie ;
13. services d'installation, maintenance, cybersécurité et évolution des équipements [H36].

C'est l'une des sources les plus utiles pour visualiser le système comme un **écosystème** plutôt que comme un moniteur isolé : chevet, transport, centralisation, notification, surveillance intermittente, intégration et logiciel clinique.

**Limite :** le RESAH décrit une offre de centrale d'achat accessible aux adhérents. Cela ne démontre pas que tous les composants sont commandés ensemble ou installés dans tous les établissements.

### 3.4 UGAP — Avis d'attribution 24U009 (publication 2025)

L'avis d'attribution publié le 15 septembre 2025 concerne l'acquisition de matériel de monitorage lourd et de ventilation lourde, avec prestations associées. Les résultats publics identifient plusieurs lots de monitorage attribués [H37] :

| Lot | Objet publié | Titulaire | Valeur mentionnée dans l'avis |
|---|---|---|---:|
| 3 | Monitorage de néonatalogie | Spacelabs Healthcare | 3,5 M€ HT estimés |
| 4 | Environnement de monitorage en réanimation et péri-opératoire | Mindray Medical France | 8 M€ HT estimés |
| 5 | Environnement de monitorage pour équiper un établissement hospitalier | Philips France | 65,5 M€ HT estimés |
| 7 | Environnement de ventilation d'anesthésie et de monitorage | GE Medical Systems | 24,5 M€ HT estimés |
| 8 | Environnement de ventilation et de monitorage communiquant | Dräger France | 35,5 M€ HT estimés |

Les signatures indiquées datent de juillet 2025 [H37].

**Attention sur les montants :** l'avis précise que les valeurs de la partie attribution sont des montants estimés en euros hors taxes par lot sur la durée totale du marché, reconductions comprises. Ce ne sont pas des factures, des achats constatés ou des sommes effectivement consommées par les hôpitaux. L'avis donne aussi des plafonds contractuels pour certains lots ; ceux-ci ne doivent pas être confondus avec les valeurs estimées des offres [H37].

L'avis est une preuve d'attribution de lots dans un marché public et de la présence d'acteurs industriels précis sur ces périmètres. Il n'identifie pas les établissements utilisateurs finaux et ne permet pas d'affirmer quelle solution est installée dans tel hôpital.

## 4. Quels systèmes actuels faut-il donc connaître ?

À partir des documents de fabricants et des marchés étudiés, les principales familles à comparer sont :

| Famille | Exemples documentés | Rôle dans l'écosystème |
|---|---|---|
| Moniteurs de chevet | Philips IntelliVue, GE CARESCAPE, Dräger Infinity, Mindray BeneVision, Spacelabs | Acquisition, affichage, alarmes et enregistrement des paramètres. |
| Moniteurs de transport | Philips X3, Dräger M540, familles GE et Mindray | Continuité de surveillance pendant les déplacements. |
| Télémétrie hospitalière | Mindray TM80, Philips MX40, systèmes équivalents | Suivi sans fil de patients mobiles. |
| Centrales de surveillance | Philips PIC iX, GE CARESCAPE Central Station, Dräger Infinity CentralStation, Mindray BeneVision CMS | Affichage multi-patients, centralisation, alarmes et tendances. |
| Report d'alarmes | Centrales, inter-chevet, bips ou terminaux dédiés, notifications mobiles selon produit | Diffusion vers les personnes et emplacements configurés. |
| Concentration d'alarmes multi-dispositifs | Exemples de solutions intégrées / Digistat, offres d'intégration | Regroupement d'alarmes provenant de plusieurs appareils ou marques. |
| Intégration des dispositifs médicaux | Philips MDI / Capsule, GE Gateway, eGateway et interfaces d'autres fabricants | Transfert des observations et événements vers les systèmes cliniques. |
| DPI / logiciel clinique spécialisé | Philips ICCA et solutions d'autres éditeurs | Documentation et revue des données du séjour. |
| Outils de surveillance ponctuelle / scoring | EarlyVue VS30, Guardian Software et produits équivalents | Recueil intermittent ou détection précoce selon la destination du produit. |

Les exemples ci-dessus ne sont pas une liste exhaustive, ni une recommandation de fournisseur. Les capacités exactes doivent être vérifiées dans les notices, versions et options du produit étudié [H04–H10, H23–H24, H34–H37].

## 5. Ce que les sources permettent réellement d'affirmer

### Faits bien établis

- Des centrales multi-patients et des moniteurs de chevet sont des catégories d'équipement clairement identifiées dans les marchés publics français [H35, H37].
- Les établissements peuvent acheter des moniteurs multiparamétriques avec maintenance et formation, sur plusieurs segments de soins [H34].
- Des offres actuelles associent moniteurs, centrales, notification d'alarmes et intégration de données [H36].
- Des procédures d'achat demandent des références de déploiement à grande échelle et des prestations de mise en service, paramétrage, formation, maintenance et assistance [H35].
- Une enquête nationale ANSM a documenté en 2017 la diffusion du report d'alarmes, avec un usage majoritaire des centrales et inter-chevet [H33].

### Ce qui n'est pas encore démontré

- Le pourcentage actuel (2026) des hôpitaux utilisant chacune de ces marques.
- Le nombre de lits réellement équipés par fournisseur.
- La part exacte de l'écosystème français par constructeur.
- Les systèmes effectivement utilisés dans les différents services de l'AP-HM.
- Les protocoles réseau et interfaces réellement activés dans chaque hôpital.
- Les volumes de données, délais de bout en bout et taux de disponibilité réels.
- L'organisation concrète de la surveillance des alarmes dans chaque service.

Ces informations nécessitent des études de déploiement, des documents d'établissement ou des échanges avec les équipes hospitalières.

## 6. Besoins métiers qui émergent de l'étude du marché

1. **Vision globale du patient :** regrouper mesures, courbes, appareils, alarmes et historique autour d'une même identité.
2. **Vue multi-patients :** surveiller plusieurs lits ou patients et ouvrir rapidement un détail.
3. **Continuité :** maintenir le suivi entre chevet, transport, imagerie et nouveau service.
4. **Identité et mouvements :** gérer admission, transfert, sortie, changement de lit et remplacement de moniteur.
5. **Gestion des alarmes :** report, priorités, acquittement, escalade, réponse humaine et fonctionnement dégradé.
6. **Interopérabilité :** agréger les données de plusieurs familles d'équipements et fabricants.
7. **Qualité de données :** distinguer mesure réelle, signal dégradé, capteur débranché et perte de connexion.
8. **Cycle de vie du matériel :** installation, configuration, maintenance, requalification, nettoyage et réaffectation.
9. **Formation et support :** accompagner les utilisateurs et maintenir leurs connaissances.
10. **Intégration DPI :** faire parvenir les données utiles au dossier patient sans supposer que chaque courbe brute y est stockée.
11. **Cybersécurité :** sécuriser dispositifs, réseau, centrales, terminaux et interfaces.
12. **Mesure de la performance :** connaître la latence, la fraîcheur des données, les pertes, les reprises et les événements non transmis.

## 7. Conséquences pour notre analyse et le POC

Le benchmark suggère qu'il faudra éviter un modèle simpliste composé uniquement de « client qui envoie des constantes → serveur → écran ».

Un système hospitalier actuel peut comporter plusieurs niveaux et responsabilités :
- un ou plusieurs dispositifs sources ;
- un réseau / une infrastructure de communication ;
- une centrale de monitorage ;
- éventuellement des systèmes de report et de concentration des alarmes ;
- un système d'intégration biomédicale ;
- un dossier patient ou logiciel clinique ;
- des utilisateurs et une organisation de réponse.

Pour conserver la faisabilité, le POC n'aura pas nécessairement à implémenter tous ces éléments. Mais l'analyse doit identifier ceux qui sont indispensables au scénario de service finalement sélectionné.

## 8. Sources

- **[H33] ANSM**, *Gestion des alarmes des dispositifs médicaux dans les établissements de santé*, septembre 2019. Enquête auprès de 631 services / 318 établissements, réalisée à l'été 2017 : https://ansm.sante.fr/uploads/2020/10/16/20201016-rapport-gestion-alarmes-dm.pdf
- **[H34] UniHA**, *Monitoring multiparamétrique*, marché M_1908, actif du 23/02/2023 au 22/02/2027 : https://www.uniha.org/marche/monitoring-multiparametrique-m-1908
- **[H35] BOAMP**, avis de marché n° 24-143962, UniHA, *Prestations relatives à une gestion optimisée du parc de monitoring patient*, publié le 20/12/2024, marché M_2976 : https://www.boamp.fr/telechargements/FILES/PDF/2024/12/24-143962.pdf
- **[H36] RESAH**, offre 2025-R023, *Gestion de parc en ventilation et monitorage*, disponible du 16/10/2025 au 15/10/2029 : https://espace-acheteur.resah.fr/gestion-de-parc-en-ventilation-et-monitorage
- **[H37] UGAP / BOAMP**, avis d'attribution n° 25-102326 du 15/09/2025, procédure 24U009 : https://www.francemarches.com/files/BOAMP/25-102326.html

## 9. Prochaines recherches

1. Obtenir les CCTP et BPU des marchés M_1908 et M_2976 si accessibles, afin de lire les exigences techniques et les critères détaillés.
2. Identifier des cas de déploiement public par établissement, et non uniquement des catalogues de fournisseurs.
3. Rechercher les systèmes effectivement utilisés dans des établissements français comparables à l'AP-HM.
4. Interroger un ingénieur biomédical sur la composition réelle du parc : moniteurs, centrales, télémétrie, interfaces et maintenance.
5. Interroger une équipe de soins sur les parcours quotidiens, les vues utilisées et le traitement des alarmes.
6. Mettre à jour les chiffres d'adoption et les systèmes de report d'alarmes si une enquête nationale plus récente est disponible.
