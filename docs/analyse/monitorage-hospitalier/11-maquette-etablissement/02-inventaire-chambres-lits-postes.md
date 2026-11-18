# Inventaire des chambres, lits et postes

**Version maquette :** facilityMapVersion = 1.0  
**Date :** 18 novembre 2026  
**Statut :** inventaire fictif et explicite pour les tests du POC.

## 1. Urgences — UNIT-URG

Localisation : bâtiment A, RDC.

| Salle / zone | ID | Positions | Type |
|---|---|---|---|
| Box urgence 1 | URG-BOX-01 | URG-BED-01 | Lit / poste de soins |
| Box urgence 2 | URG-BOX-02 | URG-BED-02 | Lit / poste de soins |
| Box urgence 3 | URG-BOX-03 | URG-BED-03 | Lit / poste de soins |
| Box urgence 4 | URG-BOX-04 | URG-BED-04 | Lit / poste de soins |
| SAUV 1 | URG-SAUV-01 | SAUV-BED-01 | Poste de prise en charge |
| SAUV 2 | URG-SAUV-02 | SAUV-BED-02 | Poste de prise en charge |
| Triage 1 | URG-TRIAGE-01 | — | Poste de triage, pas un lit |
| Triage 2 | URG-TRIAGE-02 | — | Poste de triage, pas un lit |

## 2. Réanimation adulte — UNIT-REA-ADU

Localisation : bâtiment A, R+1. Six chambres individuelles fictives.

| Chambre | Bed ID | Profil d'appareil proposé |
|---|---|---|
| REA-CH-01 | REA-BED-01 | Moniteur multiparamétrique de chevet |
| REA-CH-02 | REA-BED-02 | Moniteur multiparamétrique de chevet |
| REA-CH-03 | REA-BED-03 | Moniteur multiparamétrique de chevet |
| REA-CH-04 | REA-BED-04 | Moniteur multiparamétrique de chevet |
| REA-CH-05 | REA-BED-05 | Moniteur multiparamétrique de chevet |
| REA-CH-06 | REA-BED-06 | Moniteur multiparamétrique de chevet |

Poste de soins : REA-POSTE-01. Centrale : CENTRAL-REA-01.

## 3. USC — UNIT-USC

Localisation : bâtiment A, R+1. Quatre positions fictives.

| Chambre | Bed ID |
|---|---|
| USC-CH-01 | USC-BED-01 |
| USC-CH-02 | USC-BED-02 |
| USC-CH-03 | USC-BED-03 |
| USC-CH-04 | USC-BED-04 |

Les appareils sont affectés selon un profil de patient ; la maquette ne suppose pas que toutes les positions ont systématiquement le même équipement.

Poste de soins : USC-POSTE-01. Centrale : CENTRAL-USC-01.

## 4. Cardiologie hospitalisation — UNIT-CARD-HOSP

Localisation : bâtiment A, R+2.

| Chambre | Bed ID | Profil proposé |
|---|---|---|
| CARD-CH-01 | CARD-BED-01 | Monitorage / télémétrie selon scénario |
| CARD-CH-02 | CARD-BED-02 | Monitorage / télémétrie selon scénario |
| CARD-CH-03 | CARD-BED-03 | Monitorage / télémétrie selon scénario |
| CARD-CH-04 | CARD-BED-04 | Monitorage / télémétrie selon scénario |

Poste de soins : CARD-POSTE-01. Centrale : CENTRAL-CARD-01.

Un séjour MIMIC en Medicine/Cardiology sera rattaché à cette unité cible uniquement pour les besoins du parcours de démonstration. Le nom MIMIC d'origine reste conservé.

## 5. Médecine / traumatologie — UNIT-MED-TRAUMA

Localisation : bâtiment A, R+2.

| Chambre | Bed ID |
|---|---|
| MED-TR-CH-01 | MED-TR-BED-01 |
| MED-TR-CH-02 | MED-TR-BED-02 |
| MED-TR-CH-03 | MED-TR-BED-03 |
| MED-TR-CH-04 | MED-TR-BED-04 |
| MED-TR-CH-05 | MED-TR-BED-05 |
| MED-TR-CH-06 | MED-TR-BED-06 |

Le profil par défaut est une hospitalisation sans monitorage continu permanent. Un équipement ne sera associé que si le scénario le prévoit.

## 6. Bloc et SSPI — UNIT-BLOC, UNIT-SSPI

Localisation : bâtiment B, RDC.

| Zone | ID | Position | Type |
|---|---|---|---|
| Salle opératoire 1 | OR-01 | OR-TABLE-01 | Table d'intervention, pas un lit d'hospitalisation |
| Salle opératoire 2 | OR-02 | OR-TABLE-02 | Table d'intervention, pas un lit d'hospitalisation |
| SSPI poste 1 | SSPI-POST-01 | SSPI-BED-01 | Poste de surveillance post-interventionnelle |
| SSPI poste 2 | SSPI-POST-02 | SSPI-BED-02 | Poste de surveillance post-interventionnelle |
| SSPI poste 3 | SSPI-POST-03 | SSPI-BED-03 | Poste de surveillance post-interventionnelle |
| SSPI poste 4 | SSPI-POST-04 | SSPI-BED-04 | Poste de surveillance post-interventionnelle |

## 7. CVICU — UNIT-CVICU

Localisation : bâtiment B, R+1. Quatre positions fictives.

| Chambre | Bed ID |
|---|---|
| CVICU-CH-01 | CVICU-BED-01 |
| CVICU-CH-02 | CVICU-BED-02 |
| CVICU-CH-03 | CVICU-BED-03 |
| CVICU-CH-04 | CVICU-BED-04 |

Poste de soins : CVICU-POSTE-01. Centrale : CENTRAL-CVICU-01.

Cette unité spécialisée est une extension de parcours ; elle n'est pas fusionnée avec la réanimation adulte polyvalente.

## 8. Chirurgie cardiaque — UNIT-CHIR-CARD

Localisation : bâtiment B, R+1.

| Chambre | Bed ID |
|---|---|
| CHIR-CARD-CH-01 | CHIR-CARD-BED-01 |
| CHIR-CARD-CH-02 | CHIR-CARD-BED-02 |
| CHIR-CARD-CH-03 | CHIR-CARD-BED-03 |
| CHIR-CARD-CH-04 | CHIR-CARD-BED-04 |

## 9. Règles d'allocation des lits

1. Un lit ne peut accueillir qu'un patient à la fois sur un intervalle actif.
2. Le mouvement patient est historisé avec startAt et endAt.
3. Une affectation ne supprime jamais la précédente ; elle la clôture.
4. Un appareil ne constitue pas une propriété du lit ; il dispose de sa propre table d'association.
5. Une position de bloc (table opératoire) n'est pas un lit d'hospitalisation.
6. Une chambre peut être temporairement indisponible sans que le service entier le soit.
7. Toute surcharge de capacité donne une erreur explicite ou une file d'attente ; aucun lit n'est créé silencieusement.

## 10. Capacités fictives de la maquette

| Unité | Positions |
|---|---:|
| Urgences / SAUV | 6 |
| Réanimation adulte | 6 |
| USC | 4 |
| Cardiologie hospitalisation | 4 |
| Médecine / traumatologie | 6 |
| SSPI | 4 |
| CVICU | 4 |
| Chirurgie cardiaque | 4 |
| **Total positions de prise en charge** | **38** |
| Bloc opératoire | 2 tables (non comptées comme lits) |

Ces capacités sont choisies pour le POC ; elles ne représentent ni des moyennes ni des minimums réglementaires.
