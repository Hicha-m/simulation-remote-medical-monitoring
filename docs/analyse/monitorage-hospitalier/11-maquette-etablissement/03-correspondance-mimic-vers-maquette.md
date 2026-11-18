# Correspondance des parcours MIMIC-IV vers la maquette

**Date :** 18 novembre 2026  
**Dataset :** MIMIC-IV Clinical Database Demo 2.2  
**Fichier :** hosp/transfers.csv.gz  
**Principe :** les mouvements et horaires source sont réels dans la base dé-identifiée ; les bâtiments, chambres, lits et appareils cibles sont fictifs.

## 1. Ce que contient réellement la table transfers

La documentation MIMIC indique que la table transfers décrit les localisations physiques du patient pendant son séjour. Elle contient notamment :

- subject_id : identifiant patient anonymisé ;
- hadm_id : identifiant du séjour hospitalier ;
- transfer_id : identifiant unique de localisation physique ;
- eventtype : événement (ed, admit, transfer, discharge) ;
- careunit : nom de l'unité ou du service ;
- intime et outtime : entrée et sortie de cette localisation [H111].

La table ne contient pas de numéro de chambre ou de lit. Le transfer_id permet de conserver la trace du segment de localisation source, pas de déduire un lit de notre maquette.

## 2. Référentiel de correspondance des unités

| careunit MIMIC | Unit ID maquette | Zone physique fictive | Profil de service |
|---|---|---|---|
| Emergency Department | UNIT-URG | BAT-A / A-RDC | Urgences |
| Trauma SICU (TSICU) | UNIT-REA-ADU | BAT-A / A-R1 | Réanimation adulte polyvalente — adaptation fonctionnelle |
| Med/Surg/Trauma | UNIT-MED-TRAUMA | BAT-A / A-R2 | Médecine / traumatologie |
| Medicine/Cardiology | UNIT-CARD-HOSP | BAT-A / A-R2 | Cardiologie hospitalisation |
| Cardiac Vascular Intensive Care Unit (CVICU) | UNIT-CVICU | BAT-B / B-R1 | Soins intensifs cardio-vasculaires |
| Cardiac Surgery | UNIT-CHIR-CARD | BAT-B / B-R1 | Chirurgie cardiaque |
| Coronary Care Unit (CCU) | UNIT-CARD-HOSP ou mapping dédié à créer | BAT-A / A-R2 | Unité coronaire ; ne pas confondre automatiquement avec CVICU |
| Medical Intensive Care Unit (MICU) | UNIT-REA-ADU uniquement en mode profil générique | BAT-A / A-R1 | Réanimation médicale ; spécialité source conservée |
| Surgical Intensive Care Unit (SICU) | UNIT-REA-ADU uniquement en mode profil générique | BAT-A / A-R1 | Réanimation chirurgicale ; spécialité source conservée |
| PACU | UNIT-SSPI | BAT-B / B-RDC | SSPI |
| Discharge Lounge | ZONE-SORTIE à créer dans le modèle de lieux | Zone de sortie | Attente de sortie, pas un lit d'hospitalisation de service |

Un mapping générique vers la réanimation adulte ne signifie pas que MICU, SICU et TSICU sont des services cliniquement équivalents. Le nom source et le profil source doivent rester visibles et conservés. Pour les parcours de référence, seuls les mappings explicites des cas étudiés seront utilisés.

## 3. Parcours réel A — Urgences → Trauma SICU → Med/Surg/Trauma → sortie

**Patient source :** subject_id = 10019568  
**Séjour source :** hadm_id = 28710730

Lignes observées dans le fichier transfers.csv.gz [H120] :

| transfer_id | Type source | Unité source | intime | outtime |
|---:|---|---|---|---|
| 36381328 | ed | Emergency Department | 2120-01-30 19:44:00 | 2120-01-30 22:51:00 |
| 30876334 | admit | Trauma SICU (TSICU) | 2120-01-30 22:51:00 | 2120-01-31 18:25:12 |
| 30037221 | transfer | Med/Surg/Trauma | 2120-01-31 18:25:12 | 2120-02-02 15:40:32 |
| 34768989 | discharge | — | 2120-02-02 15:40:32 | — |

Les dates sont décalées dans le cadre de la dé-identification MIMIC ; leur chronologie relative au sein d'un même patient est conservée. Il ne faut pas les traiter comme des dates de calendrier réelles [H121].

### Affectation physique synthétique déterministe

| Segment source | Unit ID cible | Chambre / lit fictif | Justification |
|---|---|---|---|
| Emergency Department | UNIT-URG | URG-BOX-02 / URG-BED-02 | Deuxième box de la maquette, libre dans le scénario. |
| Trauma SICU | UNIT-REA-ADU | REA-CH-03 / REA-BED-03 | Lit de réanimation adulte disponible. |
| Med/Surg/Trauma | UNIT-MED-TRAUMA | MED-TR-CH-04 / MED-TR-BED-04 | Lit d'hospitalisation conventionnelle. |
| Discharge | Fin de séjour | Aucun lit | Événement de sortie, pas une nouvelle localisation de soin. |

Ces chambres et lits sont attribués par notre scénario. Ils ne viennent pas de MIMIC.

## 4. Parcours réel B — Medicine/Cardiology → CVICU → Cardiac Surgery → sortie

**Patient source :** subject_id = 10004422  
**Séjour source :** hadm_id = 21255400

Ce parcours est vérifié dans transfers.csv.gz [H120] :

| transfer_id | Type source | Unité source | intime | outtime |
|---:|---|---|---|---|
| 31415822 | admit | Medicine/Cardiology | 2111-01-15 14:55:58 | 2111-01-17 09:44:50 |
| 32155744 | transfer | Cardiac Vascular Intensive Care Unit (CVICU) | 2111-01-17 09:44:50 | 2111-01-23 18:18:46 |
| 35494464 | transfer | Cardiac Surgery | 2111-01-23 18:18:46 | 2111-01-25 15:34:47 |
| 32873549 | discharge | — | 2111-01-25 15:34:47 | — |

### Affectation physique synthétique déterministe

| Segment source | Unit ID cible | Chambre / lit fictif |
|---|---|---|
| Medicine/Cardiology | UNIT-CARD-HOSP | CARD-CH-02 / CARD-BED-02 |
| CVICU | UNIT-CVICU | CVICU-CH-02 / CVICU-BED-02 |
| Cardiac Surgery | UNIT-CHIR-CARD | CHIR-CARD-CH-03 / CHIR-CARD-BED-03 |
| Discharge | Fin de séjour | Aucun lit |

Les segments réels MIMIC sont conservés. La chambre et le lit sont des affectations fictives.

## 5. Règle d'attribution des lits pour tout autre patient

Pour rendre les scénarios reproductibles :

1. Trier les segments d'un séjour par intime, puis transfer_id.
2. Résoudre careunit au moyen d'une table de mapping versionnée.
3. Charger la liste triée des lits de l'unité cible.
4. Calculer un point de départ déterministe à partir de subject_id, hadm_id et transfer_id.
5. Choisir le premier lit libre sur l'intervalle [intime, outtime), en parcourant la liste circulairement.
6. Si aucun lit n'est disponible, produire un état capacity_conflict ; ne pas créer un lit artificiel.
7. Enregistrer l'affectation synthétique dans une table distincte avec allocationPolicyVersion.
8. Conserver les champs source sans modification.

Pour les deux parcours montrés ci-dessus, les lits sont figés explicitement dans les tableaux afin que la démonstration soit stable.

## 6. Règles d'intégrité temporelle

- Les intervalles de présence sont traités comme [intime, outtime) : la fin d'un segment ne recouvre pas le début du suivant lorsque les deux timestamps sont identiques.
- Une ligne discharge est un marqueur de fin, elle ne réserve pas de lit.
- Une ligne sans careunit ne doit pas être mappée arbitrairement.
- Plusieurs lignes dans une même unité peuvent représenter deux emplacements physiques successifs ; ne pas les fusionner uniquement parce que careunit est identique.
- Si deux allocations se chevauchent sur un même lit, le scénario doit être refusé ou corrigé explicitement.
- Les dates source ne sont pas remplacées par les dates de rejeu accélérées : conserver sourceIntime, sourceOuttime et simulationTime.

## 7. Provenance des champs

| Champ de la simulation | Source |
|---|---|
| sourceSubjectId, sourceHadmId, sourceTransferId | MIMIC-IV Demo. |
| sourceCareunit, sourceEventtype, sourceIntime, sourceOuttime | MIMIC-IV Demo. |
| targetUnitId | Table de correspondance du POC. |
| targetRoomId, targetBedId | Maquette et politique d'allocation. |
| virtualDeviceId | Catalogue d'appareils simulés. |
| monitoringSessionId | Généré par le POC lors de l'association simulée. |

## 8. Sources

- [H110] MIMIC-IV Clinical Database Demo 2.2 : https://physionet.org/content/mimic-iv-demo/2.2/
- [H111] Documentation de la table transfers : https://mimic.mit.edu/docs/iv/modules/hosp/transfers.html
- [H120] Fichier source hosp/transfers.csv.gz de MIMIC-IV Demo 2.2 : https://physionet.org/content/mimic-iv-demo/2.2/hosp/transfers.csv.gz
- [H121] Documentation MIMIC sur le décalage des dates et les types d'horodatage : https://github.com/MIT-LCP/mimic-iv-website/blob/master/content/basics/times.md
