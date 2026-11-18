# Scénarios de rejeu reproductibles sur la maquette

**Version maquette :** 1.0  
**Date :** 18 novembre 2026  
**Statut :** scénarios de démonstration ; emplacements et appareils sont synthétiques sauf indication de provenance contraire.

## 1. Scénario MAP-01 — Urgences → réanimation → médecine / traumatologie

### Source

MIMIC-IV Demo 2.2, subject_id=10019568, hadm_id=28710730.

### Affectations

| Ordre | Unité source MIMIC | Lit maquette | Durée source |
|---:|---|---|---:|
| 1 | Emergency Department | URG-BED-02 | 3 h 07 |
| 2 | Trauma SICU (TSICU) | REA-BED-03 | 19 h 34 min 12 s |
| 3 | Med/Surg/Trauma | MED-TR-BED-04 | 45 h 15 min 20 s |
| 4 | Discharge | Aucun | Événement de sortie |

### Ce que montre la carte

1. Le patient apparaît dans le bâtiment A, RDC, box urgence 2.
2. À 22:51, l'affectation précédente se ferme et le patient passe en bâtiment A, R+1, réanimation, chambre 03.
3. À 18:25:12 le lendemain, il passe en bâtiment A, R+2, médecine / traumatologie, chambre 04.
4. À l'heure de sortie, la position redevient libre et le séjour est clôturé.

Les horaires et unités sont réels dans la base dé-identifiée ; les numéros de lits et les changements de carte sont simulés.

### Événements techniques facultatifs

- Associer un moniteur MON-REA-03 à REA-BED-03 à l'entrée en réanimation.
- Simuler une alarme non clinique explicitement marquée synthetic.
- Lors du transfert, clôturer l'association avec l'ancien moniteur.
- Associer un nouveau profil ou aucun appareil selon le service destination.
- Vérifier que les observations antérieures restent rattachées à la session REA.

## 2. Scénario MAP-02 — Cardiologie → CVICU → chirurgie cardiaque

### Source

MIMIC-IV Demo 2.2, subject_id=10004422, hadm_id=21255400.

### Affectations

| Ordre | Unité source MIMIC | Lit maquette | Durée source |
|---:|---|---|---:|
| 1 | Medicine/Cardiology | CARD-BED-02 | 1 jour 18 h 48 min 52 s |
| 2 | Cardiac Vascular ICU | CVICU-BED-02 | 6 jours 8 h 33 min 56 s |
| 3 | Cardiac Surgery | CHIR-CARD-BED-03 | 1 jour 21 h 16 min 1 s |
| 4 | Discharge | Aucun | Événement de sortie |

Les durées sont calculées à partir des heures d'entrée et de sortie du fichier source. Les dates sont décalées pour l'anonymisation.

### Ce que montre la carte

1. Patient placé dans le bâtiment A, R+2, cardiologie, chambre 02.
2. Transfert vers le bâtiment B, R+1, CVICU, chambre 02.
3. Transfert vers le secteur de chirurgie cardiaque, chambre 03.
4. Sortie et libération du lit.

Il s'agit du mapping d'unité vers maquette. Le dataset ne prouve pas le numéro de lit, le moniteur, les mesures précises disponibles ni le fait qu'un appareil ait accompagné le patient.

## 3. Scénario MAP-03 — Transfert pendant une session de monitorage

Scénario synthétique qui réutilise la chronologie de MAP-01.

1. Le patient a une session active en réanimation.
2. Un transfert vers UNIT-MED-TRAUMA est déclenché.
3. La session du moniteur de réanimation est clôturée à l'heure de fin source.
4. Le lit REA redevient disponible.
5. L'affectation physique de médecine est ouverte.
6. Le serveur rejette toute nouvelle mesure tardive qui tenterait d'être associée à la mauvaise session.
7. La chronologie patient reste consultable avec les deux périodes et les deux emplacements.

## 4. Scénario MAP-04 — Panne électrique localisée pendant MAP-01

Scénario synthétique superposé au séjour réel.

1. Le patient est dans REA-BED-03.
2. Déclencher une panne de source normale dans REA-CH-03.
3. Le moniteur passe sur batterie selon sa configuration fictive.
4. Le réseau et la centrale restent disponibles ou non selon les dépendances paramétrées.
5. Afficher l'état propre à cette chambre sans déclarer tout le bâtiment indisponible.
6. Si le réseau de l'étage ou la centrale sont également touchés, signaler une perte de surveillance centralisée.
7. Au rétablissement, vérifier les sessions et les données périmées.

La coupure de courant n'est pas issue du dataset patient. Elle est ajoutée pour tester le fonctionnement dégradé.

## 5. Contrat d'un scénario de rejeu

Chaque scénario doit être accompagné d'un manifeste :

| Champ | Exemple |
|---|---|
| scenarioId | MAP-01 |
| scenarioVersion | 1.0 |
| facilityMapVersion | 1.0 |
| dataset | MIMIC-IV Demo 2.2 |
| sourcePatientId | 10019568 |
| sourceEncounterId | 28710730 |
| allocationPolicyVersion | 1.0 |
| timeScale | 1x, 10x ou 60x |
| syntheticEvents | Liste d'alarme / panne ajoutée |
| expectedOutcome | État attendu des lits, appareils et sessions |

Un même manifeste doit produire la même séquence de mouvements et les mêmes affectations physiques.

## 6. Critères d'acceptation MAP

| ID | Test | Acceptation |
|---|---|---|
| MAP-01 | Afficher le parcours sur la carte. | Le patient passe par les unités et lits indiqués, dans le bon ordre temporel. |
| MAP-02 | Conserver la provenance MIMIC. | Chaque mouvement conserve ses identifiants et horaires source. |
| MAP-03 | Séparer source et cible. | Le numéro de lit fictif n'est jamais présenté comme fourni par MIMIC. |
| MAP-04 | Détecter une collision de lit. | Deux patients ne peuvent pas occuper le même lit sur des intervalles qui se chevauchent. |
| MAP-05 | Gérer un transfert. | L'ancien emplacement est clôturé ; le nouveau est ouvert. |
| MAP-06 | Gérer la sortie. | Aucun lit n'est affecté à l'événement de discharge. |
| MAP-07 | Rejouer la séquence. | Le même manifeste donne les mêmes mouvements, lits et états. |
| MAP-08 | Modifier la version de carte. | Le parcours source reste inchangé ; seule la correspondance géographique change. |
| MAP-09 | Mapping absent. | L'unité source est signalée non mappée et n'est pas affectée arbitrairement. |
| MAP-10 | Capacité atteinte. | Le scénario déclenche capacity_conflict au lieu de créer un lit caché. |

## 7. Limites

- Le POC n'émule pas le réseau ou les appareils d'origine de MIMIC.
- Il ne reconstruit pas les coordonnées de chambres réelles.
- Les horaires MIMIC dé-identifiés ne doivent pas être interprétés comme les dates réelles d'un événement clinique.
- La présence d'un séjour en unité ne prouve pas qu'un paramètre précis était envoyé en continu à une centrale.
- Les lits, appareils et alarmes simulés sont explicitement marqués comme tels.
