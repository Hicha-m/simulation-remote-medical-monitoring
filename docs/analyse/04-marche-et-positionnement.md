# 04 — Marché et positionnement

**Version :** 0.1 — **Date :** 18 novembre 2026  
**Statut :** étude de marché qualitative et exploratoire. Aucune estimation de taille de marché n'est réalisée.

## 1. Périmètre de l'étude

Le mot « marché » recouvre plusieurs secteurs qui ne doivent pas être confondus :

1. le monitorage physiologique des patients dans les établissements de santé ;
2. la télésurveillance médicale de patients suivis à distance ;
3. les dispositifs médicaux et capteurs qui produisent les mesures ;
4. les plateformes logicielles de collecte, d'analyse et de coordination ;
5. les infrastructures d'intégration, d'hébergement et de sécurité ;
6. les services de déploiement, de formation, de support et d'accompagnement.

Le sujet de projet se situe potentiellement à l'intersection de plusieurs de ces secteurs. Le périmètre doit être précisé avant toute comparaison directe de prix, de fonctionnalités ou de fournisseurs.

## 2. Signal concret du marché hospitalier français : UniHA

UniHA publie un Système d'Acquisition Dynamique (SAD) consacré à la télésurveillance médicale, référence M_2941, sur la période 2023–2029. Le marché vise la mise à disposition de dispositifs médicaux numériques de télésurveillance, d'accessoires de collecte de données et de prestations complémentaires. Les marchés spécifiques peuvent être organisés par catégorie de pathologie et selon les besoins des établissements [S24].

La liste des candidats admis publiée sur la page UniHA est indiquée comme mise à jour en août 2026. Elle comprend :

- Abbott Medical
- Axomove
- Be Ys Health Solutions
- Biosency
- Biotronik France
- Boston Scientific
- Cardidom
- Careline Solutions
- Comunicare Solutions
- Continuum Plus Santé
- Cureety
- Datamedcare
- eDevice SAS
- Epoca U&I
- Foedora
- Glooko France
- Healabs
- Implicity
- Medtronic France
- MicroPort CRM
- MHComm
- MN Santé
- MyDiabby Healthcare
- Newcard
- NP Medical
- Predict4Health
- Resilience
- Semeia
- Steto
- SRETT

Cette liste est un indicateur concret de l'existence d'un écosystème de fournisseurs et d'un cadre d'achat hospitalier organisé. Elle ne signifie pas que tous les candidats ont été déployés dans tous les hôpitaux, qu'ils ont tous remporté les mêmes marchés ou qu'ils fournissent des fonctionnalités identiques. Elle ne donne pas non plus, à elle seule, le chiffre d'affaires du secteur [S24].

UniHA indique que le marché a été créé par les acheteurs hospitaliers de la filière Santé digitale & numérique d'UniHA de l'AP-HM. Cela constitue un point d'entrée local pertinent pour approfondir l'environnement hospitalier marseillais [S24].

## 3. Segments observables

| Segment | Exemples identifiés | Type de besoin traité | Ce que le POC pourrait comparer |
|---|---|---|---|
| Télésurveillance en oncologie | Resilience, Cureety (candidat UniHA) | Suivi à distance, symptômes, questionnaires et alertes selon les parcours de soins. | Inclusion du patient, questionnaire, suivi, alertes et coordination. |
| Télésurveillance de maladies chroniques | Semeia / MedicWise | Collecte de données, suivi et plans adaptés à des pathologies. | Mesures répétées, historique, personnalisation et suivi longitudinal. |
| Suivi de dispositifs cardiaques implantés | Biotronik, Medtronic, Abbott, Boston Scientific, Implicity | Transmission de données d'appareils et identification d'événements cardiaques ou de problèmes de transmission. | Multi-appareils, alertes, fréquence de réception, état de connectivité. |
| Agrégation multi-constructeurs | Implicity | Consolidation d'informations provenant de plusieurs fabricants de dispositifs implantables. | Hétérogénéité des sources et normalisation. |
| Monitorage hospitalier au lit du patient | Famille de moniteurs physiologiques et stations centrales à explorer | Affichage de paramètres physiologiques et alarmes dans l'établissement. | Flux fréquents, supervision multi-patients, affectation lit-patient et continuité. |

Les descriptions des segments commerciaux sont établies à partir des documentations fournisseurs [S12–S16] et de la liste UniHA [S24]. Les caractéristiques et niveaux de preuve doivent être vérifiés produit par produit.

## 4. Exemples documentés de fonctionnement

### Resilience — retour d'expérience à Marseille

Le retour d'expérience publié décrit un projet de télésurveillance en oncologie à l'Hôpital Européen de Marseille, déployé à partir de décembre 2023. Il décrit le rôle des médecins, infirmiers, coordinateur, direction et équipe informatique ; l'inclusion et l'accompagnement du patient ; le traitement des alertes et la coordination dans la journée [S12].

Limite : il s'agit d'une publication éditée par le fournisseur, qui rapporte un retour d'expérience d'un service partenaire. Ce n'est pas une étude indépendante et le modèle organisationnel ne peut pas être extrapolé à tous les services.

### BIOTRONIK — transmission automatique de données cardiaques

BIOTRONIK décrit un flux quotidien depuis un appareil implanté vers un transmetteur à domicile, puis un serveur consulté par les médecins. Le fournisseur présente également des alertes configurables, notamment lorsqu'une transmission manque plusieurs jours [S14].

Enseignement à examiner : les systèmes réels ne se limitent pas à détecter des valeurs anormales ; ils doivent également connaître la situation de la source et identifier les absences de transmission.

### Implicity — agrégation de plusieurs fabricants

Implicity présente une plateforme qui regroupe les informations de plusieurs fabricants de dispositifs cardiaques implantés et propose des workflows orientés alertes [S15].

Enseignement à examiner : l'interopérabilité entre appareils et fournisseurs constitue une problématique à part entière.

### Semeia — personnalisation selon la pathologie

Semeia présente MedicWise comme une plateforme de télésurveillance pour maladies chroniques, avec collecte automatisée, analyse avancée, restitution, alertes et plans de suivi personnalisés [S16].

Enseignement à examiner : les mesures, leur fréquence, les questions posées au patient et les règles de suivi peuvent dépendre du domaine clinique.

## 5. Qui sont les utilisateurs, décideurs et bénéficiaires possibles ?

La chaîne de valeur peut inclure plusieurs catégories d'acteurs :

- **Bénéficiaire :** patient, personne suivie ou équipe de soins.
- **Utilisateur quotidien :** infirmier, médecin, coordinateur, personnel de surveillance.
- **Prescripteur ou responsable médical :** selon le dispositif et le parcours.
- **Décideur d'établissement :** direction, direction des systèmes d'information, direction médicale, achats.
- **Acteur technique :** informatique hospitalière, biomédical, cybersécurité.
- **Acteur de conformité :** DPO, responsable de traitement, hébergeur, fabricant et exploitant de dispositif médical selon le cas.
- **Fournisseur :** éditeur, fabricant de capteurs, intégrateur ou hébergeur.

La personne qui utilise le dashboard n'est donc pas nécessairement celle qui décide de l'achat, paramètre les règles, gère les équipements ou assume la responsabilité clinique.

## 6. Besoins à vérifier auprès des utilisateurs

Les besoins ci-dessous sont des axes d'enquête, et non des conclusions établies :

| Axe | Question d'étude |
|---|---|
| Temps disponible | Combien de temps les professionnels consacrent-ils au tri et au suivi ? |
| Charge d'alertes | Combien d'alertes sont utiles, répétitives, non pertinentes ou difficiles à traiter ? |
| Priorisation | Quelles informations doivent apparaître en premier et pourquoi ? |
| Continuité | Comment une équipe transmet-elle les alertes non résolues ? |
| Fiabilité des données | Comment les professionnels distinguent-ils une mesure réelle, une absence de mesure et un artefact ? |
| Lisibilité | Quelle information doit être visible sans ouvrir le dossier complet ? |
| Intégration | Quelles données doivent entrer ou sortir du dossier patient informatisé ? |
| Accessibilité | Quels obstacles empêchent certains patients d'utiliser l'appareil ou l'application ? |
| Traçabilité | Quelles actions et consultations doivent être historisées ? |
| Sécurité | Comment sont gérés les accès, les comptes, les appareils et les incidents ? |
| Coût opérationnel | Quelles ressources sont mobilisées pour déployer, former, maintenir et exploiter la solution ? |

## 7. Pistes de différenciation à tester

Ces pistes ne sont pas des affirmations d'originalité. Elles devront être comparées aux produits existants et validées avec de vrais utilisateurs.

### Piste A — Un laboratoire de simulation plutôt qu'un simple dashboard

Construire un environnement qui permet de créer, paramétrer, rejouer et comparer des situations : mesures normales, évolution progressive, absence de données, appareil déconnecté, retard, doublons, artefacts et pics de messages.

Question de différenciation : les plateformes existantes permettent-elles aux équipes, étudiants ou intégrateurs de tester de manière reproductible les comportements du système en présence d'incidents ?

### Piste B — Montrer toute la chaîne d'une alerte

Conserver la trace de l'origine de l'événement : mesure, appareil, réception, validation, règle, création de l'alerte, affichage, acquittement, transfert et clôture.

Question : les utilisateurs et évaluateurs ont-ils besoin de comprendre pourquoi une alerte est apparue et ce qu'il s'est passé ensuite ?

### Piste C — Simuler la charge humaine

Faire varier le nombre de patients, le nombre de sources, les fréquences d'envoi et les règles d'alerte pour étudier la charge de travail, les files d'attente, les priorités et les relais d'équipe.

Question : quelle charge est réaliste pour le service étudié et quelles limites d'organisation sont les plus importantes ?

### Piste D — Simuler les défaillances des appareils et des réseaux

Ne pas considérer l'appareil comme une source parfaite : signal médiocre, mesure manquante, faible batterie, perte de réseau, horloge décalée, reconnexion et duplication.

Question : quelle partie de la fiabilité des solutions existantes est liée à la qualité des capteurs, à la connectivité et aux mécanismes logiciels de reprise ?

### Piste E — Interopérabilité pédagogique

Présenter comment une mesure interne pourrait être représentée en FHIR, validée, convertie ou exportée vers un autre système.

Question : quelle profondeur d'interopérabilité est démontrable dans un projet académique sans reproduire un SIH complet ?

### Piste F — Sécurité observable et démontrable

Rendre visibles les rôles, autorisations, connexions, tentatives refusées, actions sensibles, journaux et scénarios d'incident.

Question : peut-on faire de la sécurité un comportement testable et démontrable, plutôt qu'une simple mention dans le rapport ?

### Piste G — Accessibilité et sobriété d'usage

Simuler les difficultés d'utilisation côté patient et étudier des interfaces claires, sobres et adaptées aux différents niveaux de maîtrise du numérique.

Question : quelles adaptations ont un impact réel sur l'adoption et la continuité du suivi ?

## 8. Ce qu'il ne faut pas conclure trop tôt

- « Personne ne propose de simulateur complet » : non vérifié.
- « Tous les concurrents ont les mêmes besoins » : faux périmètre de comparaison.
- « Le projet peut remplacer un outil hospitalier » : aucune preuve, aucune validation et aucun objectif de remplacement.
- « Une interface plus jolie est une valeur ajoutée suffisante » : non démontré.
- « L'intelligence artificielle est nécessaire » : aucune nécessité établie.
- « Le marché est énorme » : aucune étude quantitative n'est menée ici.
- « Les produits commerciaux ne sont pas ouverts » : licences et architectures à vérifier individuellement.

## 9. Limites de cette première étude

- La taille totale du marché, les parts de marché et les tarifs ne sont pas étudiés.
- Les appels d'offres et cahiers des charges détaillés UniHA nécessitent un accès adhérent.
- Les retours d'expérience publics sont peu nombreux et parfois publiés par des fournisseurs.
- Les solutions de monitorage hospitalier central n'ont pas encore fait l'objet d'un benchmark produit complet.
- Il manque des entretiens directs avec des équipes de soins, des biomédicaux et des équipes SI.

## 10. Prochaine étape de l'étude de marché

1. Départager les trois interprétations du sujet.
2. Sélectionner deux ou trois domaines cliniques de comparaison, sans les confondre.
3. Rechercher des cahiers des charges et retours d'expérience d'établissements.
4. Réaliser des entretiens exploratoires avec des professionnels.
5. Comparer les solutions sur une même grille fonctionnelle et organisationnelle.
6. Rechercher les limites ou difficultés non résolues avec preuves.
7. Valider ou écarter les pistes de différenciation.
