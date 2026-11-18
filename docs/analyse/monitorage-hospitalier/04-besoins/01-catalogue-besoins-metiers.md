# Besoins 01 — Catalogue des besoins métiers du monitorage hospitalier

**Version :** 0.1 — **Date :** 18 novembre 2026  
**Statut :** catalogue de besoins candidats, non validés et non priorisés.

Ce catalogue transforme les processus documentés en besoins analysables. Il ne constitue pas encore un cahier des charges. Aucun seuil clinique, délai de réponse ou volumétrie n'est présumé.

## 1. Identités, lits et affectations

| ID | Besoin métier | Contexte | Source / justification |
|---|---|---|---|
| ID-01 | Identifier sans ambiguïté le patient suivi. | Tous | Les systèmes de centrale gèrent l'admission et les mouvements [H04]. |
| ID-02 | Associer un patient à un séjour et à une unité. | Tous | Cycle patient et gestion des admissions / transferts [H04, H22]. |
| ID-03 | Associer un appareil ou transmetteur à un patient. | Tous | Admission et configuration des moniteurs [H22]. |
| ID-04 | Associer le patient à un lit ou emplacement. | Unités avec poste fixe | Gestion des lits et contexte de surveillance [H02, H04]. |
| ID-05 | Traiter les transferts et changements d'appareil. | Tous | Les centrales gèrent admission, sortie et déplacement [H04]. |
| ID-06 | Empêcher qu'un ancien lien patient-appareil reste actif. | Tous | Besoin déduit du cycle d'association ; à valider localement. |
| ID-07 | Conserver l'historique des affectations. | Tous | Traçabilité du parcours ; besoin candidat. |

## 2. Acquisition et qualité des données

| ID | Besoin métier | Contexte | Source / justification |
|---|---|---|---|
| DATA-01 | Recevoir les paramètres et courbes produits par un moniteur. | Soins critiques, bloc, unités équipées | Fonctions de moniteurs et centrales [H04–H10]. |
| DATA-02 | Identifier la source exacte d'une mesure. | Tous | Équipements et interfaces hétérogènes [H24, H25]. |
| DATA-03 | Conserver les unités et le type de mesure. | Tous | Nécessaire à l'interprétation fiable des données. |
| DATA-04 | Conserver heure de mesure et heure de réception. | Tous | Nécessaire pour suivre la fraîcheur et la latence. |
| DATA-05 | Distinguer absence de données et valeur mesurée. | Tous | La perte réseau ou technique ne signifie pas une mesure normale. |
| DATA-06 | Identifier les données invalides ou incomplètes. | Tous | Tâches de dépannage et de gestion des mesures [H22]. |
| DATA-07 | Détecter les doublons et messages tardifs. | Tous | Besoin de fiabilité technique à tester. |
| DATA-08 | Conserver des tendances et événements. | Soins critiques, télémétrie | Fonctions documentées des centrales [H04, H05, H08]. |
| DATA-09 | Signaler les défauts du capteur ou de l'appareil. | Tous | Cas de dépannage de moniteurs [H22]. |
| DATA-10 | Gérer la perte et le retour de connexion. | Télémétrie, transport | Couverture sans fil et continuité [H09, H10]. |

## 3. Consultation et supervision multi-patients

| ID | Besoin métier | Contexte | Source / justification |
|---|---|---|---|
| VIEW-01 | Afficher plusieurs patients simultanément. | Centrale de soins critiques / télémétrie | Centrales multi-patients [H04, H05, H08]. |
| VIEW-02 | Ouvrir une vue détaillée d'un patient. | Tous | Vues détaillées et courbes des centrales [H04]. |
| VIEW-03 | Voir des courbes et valeurs numériques. | Soins critiques / télémétrie | Produits centralisés [H04, H05]. |
| VIEW-04 | Voir la fraîcheur de la dernière donnée. | Tous | Besoin de distinguer données actuelles et données périmées. |
| VIEW-05 | Consulter les tendances et événements historiques. | Soins critiques / télémétrie | Historiques et tendances annoncés par les centrales [H04, H05, H08]. |
| VIEW-06 | Filtrer par service, secteur ou patient. | Établissement | Besoin dérivé des centrales et vues distribuées [H05]. |
| VIEW-07 | Adapter l'affichage à la fonction de l'utilisateur. | Multi-rôles | Postes et permissions configurables selon fabricant [H05]. |
| VIEW-08 | Identifier rapidement le patient concerné par une alarme. | Tous | Report et signalement des alarmes [H02, H04]. |

## 4. Alarmes et événements

| ID | Besoin métier | Contexte | Source / justification |
|---|---|---|---|
| ALM-01 | Distinguer les alarmes physiologiques et techniques. | Tous | HAS et normes d'alarme [H02, H28]. |
| ALM-02 | Diffuser l'alarme vers des destinations configurées. | Soins critiques | Centrale, inter-chevet, répétiteurs, portables [H02]. |
| ALM-03 | Signaler l'alarme à l'équipe responsable. | Tous | Organisation des rôles à documenter [H02, H11]. |
| ALM-04 | Tracer la prise de connaissance. | Tous | Besoin de traitement en boucle fermée [H11, H14]. |
| ALM-05 | Distinguer acquittement et résolution. | Tous | Besoin fonctionnel à valider. |
| ALM-06 | Transmettre ou escalader un événement non pris en charge. | Tous | Organisations de surveillance centralisée [H14]. |
| ALM-07 | Consulter l'historique d'une alarme. | Tous | Historique d'événements dans les centrales [H04, H08]. |
| ALM-08 | Analyser la fréquence et la durée des alarmes. | Soins critiques / télémétrie | Études sur volume et durée des alarmes [H15, H26]. |
| ALM-09 | Identifier les alarmes répétitives ou non actionnables. | Soins critiques / télémétrie | Gestion de l'alarme et fatigue [H14, H15, H26]. |
| ALM-10 | Documenter les limites d'alarme et leurs changements. | Tous | HAS demande des réglages adaptés et leur vérification [H02]. |
| ALM-11 | Prévoir un fonctionnement dégradé si le report d'alarme ne fonctionne plus. | Soins critiques / télémétrie | L'ANSM rapporte que 35,29 % des services interrogés avaient prévu un fonctionnement dégradé [H33]. |
| ALM-12 | Regrouper des alarmes provenant de plusieurs équipements ou fabricants. | Soins critiques / unités équipées | 16,32 % des services répondants disposaient d'une concentration d'alarmes multi-dispositifs [H33]. |
| ALM-13 | Vérifier que la vue centrale présente tous les lits / patients attendus. | Centrale multi-patients | Le rapport ANSM décrit un incident où l'écran de centrale n'affichait qu'une partie des lits [H33]. |

## 5. Organisation du travail

| ID | Besoin métier | Contexte | Source / justification |
|---|---|---|---|
| OPS-01 | Définir les rôles qui observent et traitent les alarmes. | Soins critiques / télémétrie | Les organisations de monitor watchers varient [H11, H14]. |
| OPS-02 | Organiser une relève sans perdre les événements ouverts. | Soins critiques / télémétrie | HAS demande des contrôles à chaque prise de poste [H02]. |
| OPS-03 | Vérifier le système lors de l'admission. | Soins critiques | HAS [H02]. |
| OPS-04 | Prévoir la présence pendant les pauses et périodes de nuit. | Soins critiques | HAS [H02]. |
| OPS-05 | Documenter les transmissions entre équipes. | Bloc/SSPI/transport | Transmission et continuité [H03, H19]. |
| OPS-06 | Former les professionnels à l'utilisation des alarmes. | Soins critiques | HAS [H02]. |
| OPS-07 | Gérer les transports avec une surveillance adaptée. | Transport | HAS [H19, H20]. |

## 6. Gestion technique et biomédicale

| ID | Besoin métier | Contexte | Source / justification |
|---|---|---|---|
| DEV-01 | Identifier les équipements et leurs caractéristiques. | Tous | Gestion d'équipement et profils IHE PCD [H25]. |
| DEV-02 | Connaître l'état de connexion et disponibilité d'un appareil. | Tous | Besoin de supervision technique. |
| DEV-03 | Gérer les indisponibilités et interventions de maintenance. | Tous | Processus biomédical à documenter auprès d'un établissement. |
| DEV-04 | Connaître la localisation ou le secteur d'un équipement. | Télémétrie / parc | Fonctions de localisation annoncées [H09] et profils de gestion d'équipement [H25]. |
| DEV-05 | Conserver l'historique des affectations et maintenances. | Tous | Besoin de gestion du parc à valider. |

## 7. Intégration informatique

| ID | Besoin métier | Contexte | Source / justification |
|---|---|---|---|
| INT-01 | Importer les identités et mouvements patients. | Tous | ADT/EMR annoncés par fournisseurs [H05, H24]. |
| INT-02 | Exporter des observations vers le DPI. | Tous | Fonction présentée par Philips [H23]. |
| INT-03 | Échanger des informations selon des formats structurés. | Tous | HL7 et IHE PCD [H24, H25]. |
| INT-04 | Gérer les erreurs d'interface et les reprises. | Tous | Besoin d'exploitation déduit. |
| INT-05 | Assurer la traçabilité de la provenance des mesures. | Tous | Besoin d'intégrité et d'interopérabilité. |

## 8. Comment utiliser ce catalogue

Chaque besoin devra devenir une fiche détaillée avec :
- acteur concerné ;
- contexte et processus ;
- déclencheur ;
- résultat attendu ;
- données utilisées ;
- erreurs et exceptions ;
- source ou entretien ayant confirmé le besoin ;
- importance métier ;
- possibilité de simulation ;
- critère de test.

**Aucun besoin n'est priorisé à ce stade.** La priorité dépendra du contexte de monitorage retenu et des objectifs du projet.
