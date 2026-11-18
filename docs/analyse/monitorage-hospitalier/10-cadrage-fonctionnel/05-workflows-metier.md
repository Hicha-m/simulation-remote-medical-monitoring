# Workflows métier dérivés de données hospitalières réelles

**Date :** 18 novembre 2026  
**Statut :** workflows reconstruits à partir de données hospitalières dé-identifiées et de recommandations françaises. Ils ne sont pas des protocoles médicaux français.

## 1. Méthode : séparer le réel, l'officiel et le simulé

Le POC doit conserver la provenance de chaque événement :

| Provenance | Signification | Exemple |
|---|---|---|
| research_dataset | Donnée extraite d'un jeu de données hospitalier de recherche. | Admission, mouvement de service, mesure chartée. |
| official_guidance | Étape ou mesure issue d'un texte ou guide institutionnel. | Organisation dégradée, continuité de surveillance. |
| synthetic_scenario | Événement ajouté pour tester le logiciel. | Panne électrique, coupure réseau, perte de centrale, panne de groupe. |
| user_action | Action effectuée par un utilisateur dans la simulation. | Association d'un appareil, acquittement d'une alarme. |

Ne jamais présenter une association de lit générée pour notre maquette comme une donnée hospitalière réelle. Ne jamais présenter un événement synthétique de panne comme un événement trouvé dans MIMIC ou HiRID.

## 2. Données réelles consultables

### MIMIC-IV Demo 2.2

MIMIC-IV Demo est un sous-ensemble de démonstration de 100 patients anonymisés issus du Beth Israel Deaconess Medical Center. Les identifiants ont été remplacés et les dates décalées de façon cohérente pour protéger les personnes [H110].

| Table | Champs / contenu | Ce que nous pouvons reconstituer |
|---|---|---|
| admissions | Identifiants de séjour, heures d'admission et de sortie, origine et destination. | Ouverture et fermeture d'un séjour hospitalier. |
| transfers | Patient, séjour, type d'événement, unité, heures d'entrée et sortie. | Présence dans une unité et transferts successifs. |
| icustays | Séjour de soins intensifs, unité et période. | Ouverture et fermeture du profil de soins intensifs. |
| chartevents | Item, valeur, unité, heure de mesure documentée et heure d'enregistrement. | Chronologie des observations chartées. |
| inputevents / outputevents | Apports, sorties et événements documentés. | Éventuels événements de suivi et traitements, si le périmètre les inclut. |

La base distingue les données hospitalières générales des données issues du système clinique de soins intensifs. La présence d'une mesure dans chartevents ne signifie pas que nous possédons le paquet réseau brut émis par le moniteur [H112].

### Parcours réel MIMIC-IV Demo : urgences → Trauma SICU → Med/Surg/Trauma → sortie

Le séjour de démonstration identifié par subject_id 10019568 et hadm_id 28710730 contient les événements de mouvement suivants [H110, H111] :

| Événement enregistré | Début (date décalée) | Fin (date décalée) | Durée calculée |
|---|---|---|---:|
| Emergency Department | 2120-01-30 19:44:00 | 2120-01-30 22:51:00 | 3 h 07 |
| Trauma SICU | 2120-01-30 22:51:00 | 2120-01-31 18:25:12 | 19 h 34 min 12 s |
| Med/Surg/Trauma | 2120-01-31 18:25:12 | 2120-02-02 15:40:32 | 45 h 15 min 20 s |
| Discharge | 2120-02-02 15:40:32 | — | Fin du séjour |

C'est une chronologie enregistrée dans la base de démonstration. Les dates sont déplacées pour l'anonymisation et ne sont pas des dates calendaires réelles de prise en charge.

Ce parcours prouve concrètement qu'un épisode hospitalier peut être constitué de plusieurs segments de localisation. Pour le POC, il fournit une base pour générer les événements d'admission, de transfert et de sortie.

**Ce que cette trace ne fournit pas :** un plan d'étage, un numéro de chambre, un numéro de lit, l'identifiant exact d'un moniteur ou la totalité des actions des soignants. Les emplacements physiques et les associations appareil-lit seront créés dans notre hôpital fictif et marqués synthetic_scenario.

### Deuxième parcours réel : chirurgie cardiaque → CVICU → chirurgie cardiaque → sortie

Un autre séjour de démonstration, subject_id 10005817 et hadm_id 20626031, montre les séquences [H110] :

| Événement enregistré | Début (date décalée) | Fin (date décalée) |
|---|---|---|
| Cardiac Surgery | 2132-12-12 01:44:24 | 2132-12-15 09:29:01 |
| Cardiac Vascular Intensive Care Unit | 2132-12-15 09:29:01 | 2132-12-17 18:06:07 |
| Cardiac Surgery | 2132-12-17 18:06:07 | 2132-12-20 15:04:14 |
| Discharge | 2132-12-20 15:04:14 | — |

Ce second exemple montre un transfert vers une unité de soins intensifs cardiovasculaires puis un retour dans le service de chirurgie. Les dates sont également décalées.

Dans les données de monitorage chartées, les champs charttime et storetime sont distincts : l'heure associée à l'observation ne doit pas être confondue avec l'heure de son enregistrement [H110, H112]. Le mapping entre itemid et signification médicale doit passer par le dictionnaire officiel de la base ; si le code n'est pas mappé, le POC doit le laisser explicitement inconnu plutôt que deviner.

## 3. Fréquences réellement observées dans les bases

Il n'existe pas de fréquence universelle à reprendre pour chaque appareil :

- eICU vitalPeriodic : les interfaces transmettent généralement des moyennes à la minute ; les valeurs sont stockées en médianes sur cinq minutes. Ces valeurs ne sont pas nécessairement validées par un soignant au moment de leur archivage [H113].
- HiRID : la plupart des paramètres de monitorage au chevet sont enregistrés toutes les deux minutes [H115].
- MIMIC-IV : cadence et présence dépendent de la mesure, du système source et de la façon dont l'information est chartée [H112].

**Décision proposée :** chaque profil d'appareil aura une cadence configurable. La simulation distinguera la fréquence d'acquisition, de calcul, d'émission, de réception et d'affichage. Un jeu de données charté ne doit pas être présenté comme un flux brut de capteur.

## 4. Workflow A — Admission, mouvement et affectation physique

### Partie issue des données réelles

1. Créer ou retrouver le patient anonymisé.
2. Ouvrir le séjour correspondant à l'admission.
3. Créer le premier segment de localisation à l'heure indiquée par le dataset.
4. Lorsqu'une nouvelle ligne transfers commence, clôturer le segment précédent et ouvrir le suivant.
5. Conserver le type d'événement, le nom de l'unité et les heures source.
6. Terminer le séjour à l'événement de sortie.

### Partie simulée pour la carte

1. Mapper l'unité MIMIC vers un service de notre hôpital fictif.
2. Affecter un bâtiment, étage, chambre et lit synthétiques.
3. Afficher le lit et le patient sur la carte.
4. En cas de transfert, choisir un lit destination compatible et libre.
5. Enregistrer l'affectation physique dans une table séparée du mouvement source.

Le modèle doit conserver la source originale de l'événement et l'affectation de démonstration dans des champs séparés.

## 5. Workflow B — Activation du monitorage et rejeu des observations

### Partie issue des données réelles

1. Détecter l'entrée dans une unité de soins intensifs à partir de la table de mouvements et/ou icustays.
2. Charger les observations chartées disponibles pendant la période.
3. Mapper les itemid à des codes de paramètres à partir du dictionnaire MIMIC.
4. Conserver la valeur, l'unité, charttime, storetime et l'item source.
5. Trier les événements à partir de l'heure de mesure documentée, sans effacer l'heure d'enregistrement.
6. Rejouer la chronologie en temps réel ou accélérée.

### Partie simulée

1. Associer une source virtuelle de rejeu à une session de surveillance.
2. Assigner un deviceId fictif et un profil de moniteur générique.
3. Émettre les observations vers le serveur.
4. Montrer sur la carte et le dashboard quelle source virtuelle est associée au lit.
5. À la sortie de l'unité, clôturer la session et conserver l'historique.

**Important :** les appareils de la maquette sont des sources virtuelles. La présence de mesures dans un dossier de recherche ne prouve pas que le modèle de moniteur ou le protocole d'origine est connu.

## 6. Workflow C — Transfert entre services

### Partie issue des données réelles

La chronologie source indique quand un patient quitte une unité et entre dans la suivante, par exemple Emergency Department → Trauma SICU → Med/Surg/Trauma [H111].

### Partie simulée du système de monitorage

1. Préparer la destination sur la carte.
2. Identifier si le patient conserve son dispositif, utilise un moniteur de transport ou attend la nouvelle installation.
3. Clôturer l'ancienne affectation physique.
4. Déplacer le patient vers le lit synthétique de destination.
5. Clôturer l'association de l'appareil précédent si un changement est simulé.
6. Associer le nouvel appareil ou la source de transport.
7. Ouvrir une nouvelle session de surveillance, avec des bornes temporelles explicites.
8. Vérifier que les mesures antérieures restent rattachées à l'ancienne session.
9. Afficher au dashboard une chronologie patient continue, mais segmentée par service et appareil.

Les traces MIMIC indiquent les mouvements entre unités ; la continuité d'appareil ou le modèle exact de moniteur n'est pas déduit de ces traces.

## 7. Workflow D — Alarmes

### Ce qui vient des données réelles

Les jeux MIMIC-IV, HiRID et eICU peuvent contenir des observations, des événements et des informations cliniques, mais ils ne fournissent pas un cycle complet et universel d'alarme centralisée : déclenchement sonore, report à la centrale, prise de connaissance, acquittement et résolution.

### Ce qui vient des recommandations françaises

La HAS et l'ANSM décrivent les risques associés au mauvais réglage, à la mauvaise transmission, à l'interprétation ou au traitement des alarmes [H02, H95].

### Ce qui sera simulé

1. Un appareil virtuel ou un scénario synthétique déclenche un événement.
2. Le serveur le lie à la bonne session, au patient et à la localisation.
3. La centrale affiche l'origine et l'état de l'événement.
4. Un utilisateur prend connaissance et acquitte.
5. L'événement reste actif tant qu'il n'est pas résolu par une nouvelle condition simulée.
6. Le cycle complet est journalisé.

Les seuils et priorités cliniques ne sont pas établis à partir des bases de données.

## 8. Workflow E — Coupure électrique / mode dégradé

### Sources

Le guide ministériel du volet numérique du Plan blanc demande de prévoir un mode dégradé pour maintenir l'organisation de surveillance en soins critiques lorsque le réseau ou les systèmes sont indisponibles [H114]. La circulaire électrique DHOS de 2006 décrit les principes de continuité électrique, les sources de secours, les onduleurs et les groupes pour les activités critiques ; son actualité réglementaire doit être vérifiée avant tout usage prescriptif [H116]. Le manuel de centrale Mindray précise des conditions d'alimentation de secours de la centrale et avertit d'un risque en cas de perte brutale d'alimentation [H117].

### Ce qui sera simulé

1. Déclarer une panne de secteur sur un périmètre de la carte.
2. Déterminer quels objets ont une batterie interne ou sont raccordés à un circuit secouru selon la configuration fictive.
3. Faire passer les moniteurs sur batterie quand leur profil le prévoit.
4. Faire basculer les UPS ou la source génératrice simulée.
5. Vérifier séparément l'alimentation de la centrale, des switches, des points d'accès et du serveur.
6. Si la centrale n'est plus joignable, passer la surveillance à l'état dégradé et marquer les mesures comme périmées.
7. Afficher l'activation de la procédure locale de fonctionnement dégradé.
8. Au retour des systèmes, vérifier les associations et rendre visibles les périodes sans données.

Ce scénario est décrit intégralement dans [08 — Continuité électrique et mode dégradé](08-continuite-electrique-et-mode-degrade.md). Les temps de bascule et autonomies sont des paramètres fictifs de test, non des valeurs universelles.

## 9. Rejouer des séjours réels avec des événements synthétiques

La meilleure approche pour le POC est de combiner :

- les admissions et transferts réels anonymisés de MIMIC-IV Demo ;
- des observations temporelles réelles de MIMIC-IV, HiRID ou eICU ;
- des lits, chambres et appareils virtuels, clairement identifiés comme simulés ;
- des alarmes synthétiques fondées sur les recommandations HAS/ANSM ;
- des défaillances électriques et réseau synthétiques fondées sur le guide du Plan blanc et les principes d'alimentation secourue ;
- des actions utilisateur issues de la manipulation de la simulation.

Chaque événement doit conserver un champ de provenance afin que la démonstration soit auditée et reproductible.

## Sources

- [H02] HAS — Surveillance des patients en soins critiques, 2024.
- [H95] ANSM — Gestion des alarmes des dispositifs médicaux, 2019.
- [H110] MIMIC-IV Clinical Database Demo 2.2.
- [H111] Documentation MIMIC-IV — table transfers.
- [H112] Documentation MIMIC-IV — schema overview.
- [H113] eICU — vitalPeriodic.
- [H114] Ministère de la Santé — guide du volet numérique du Plan blanc, 2023.
- [H115] HiRID — Data details.
- [H116] Circulaire DHOS/E4/2006/393 — alimentation électrique des établissements de santé.
- [H117] Mindray — BeneVision Central Monitoring System, Operator's Manual.
