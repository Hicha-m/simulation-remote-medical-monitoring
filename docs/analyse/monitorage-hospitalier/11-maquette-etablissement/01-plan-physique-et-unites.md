# Plan physique et unités de la maquette

**Date :** 18 novembre 2026  
**Site :** HOSP-DEMO-01 — Hôpital de démonstration  
**Statut :** plan fictif stabilisé pour les scénarios du POC, révisable par version.

## 1. Vue générale

Le site comporte deux bâtiments cliniques. Le bâtiment A regroupe les urgences, les soins critiques, la cardiologie et la médecine. Le bâtiment B regroupe le bloc, la SSPI et les secteurs de chirurgie cardio-vasculaire. Le sous-sol du bâtiment A héberge les fonctions techniques de la maquette.

Ce choix n'est pas une recommandation architecturale hospitalière. Il donne une géographie simple pour tester les déplacements entre zones et les pannes localisées.

## 2. Bâtiments et niveaux

| ID | Bâtiment / niveau | Contenu principal |
|---|---|---|
| BAT-A | Bâtiment A — clinique principale | Urgences, réanimation adulte, USC, cardiologie, médecine / traumatologie. |
| BAT-A-S1 | Bâtiment A — sous-sol | Local informatique, cœur réseau, local électrique et UPS. |
| BAT-B | Bâtiment B — secteur interventionnel et chirurgical | Bloc opératoire, SSPI, CVICU et chirurgie cardiaque. |
| EXT-ENERGIE | Zone technique extérieure | Groupe électrogène de secours simulé et arrivée d'énergie. |

### Bâtiment A

| Niveau | ID niveau | Unités et zones |
|---|---|---|
| RDC | A-RDC | Urgences (UNIT-URG), SAUV, imagerie (ZONE-IMG). |
| R+1 | A-R1 | Réanimation adulte (UNIT-REA-ADU), USC (UNIT-USC). |
| R+2 | A-R2 | Cardiologie hospitalisation (UNIT-CARD-HOSP), médecine / traumatologie (UNIT-MED-TRAUMA). |
| Sous-sol | A-S1 | Local IT (ZONE-IT), local électrique / UPS (ZONE-ELEC). |

### Bâtiment B

| Niveau | ID niveau | Unités et zones |
|---|---|---|
| RDC | B-RDC | Bloc opératoire (UNIT-BLOC), SSPI (UNIT-SSPI). |
| R+1 | B-R1 | Réanimation cardio-vasculaire (UNIT-CVICU), chirurgie cardiaque (UNIT-CHIR-CARD). |

## 3. Plan schématique — bâtiment A

    BÂTIMENT A
    ┌───────────────────────────────────────────────────┐
    │ RDC — A-RDC                                       │
    │  [Urgences / SAUV] ─── [Imagerie]                 │
    ├───────────────────────────────────────────────────┤
    │ R+1 — A-R1                                        │
    │  [Réanimation adulte] ─── [USC]                   │
    │  [Poste de soins / centrale REA]                  │
    ├───────────────────────────────────────────────────┤
    │ R+2 — A-R2                                        │
    │  [Cardiologie] ─── [Médecine / traumatologie]     │
    │  [Centrale télémétrie CARD]                       │
    ├───────────────────────────────────────────────────┤
    │ Sous-sol — A-S1                                   │
    │  [Local IT / réseau] ─── [Local électrique / UPS] │
    └───────────────────────────────────────────────────┘

## 4. Plan schématique — bâtiment B

    BÂTIMENT B
    ┌───────────────────────────────────────────────────┐
    │ RDC — B-RDC                                       │
    │  [Bloc opératoire x2] ─── [SSPI x4 postes]        │
    ├───────────────────────────────────────────────────┤
    │ R+1 — B-R1                                        │
    │  [CVICU x4 lits] ─── [Chirurgie cardiaque x4 lits]│
    └───────────────────────────────────────────────────┘

Les plans sont schématiques : ils ne prétendent pas représenter des distances, accès, circulations propres ou contraintes réglementaires réelles. Les chambres et positions sont définies dans le catalogue de la maquette.

## 5. Catalogue des unités

| Unit ID | Nom affiché | Localisation | Nature | Rôle dans le POC |
|---|---|---|---|---|
| UNIT-URG | Urgences | BAT-A / A-RDC | Service d'accueil | Admission et premier monitorage. |
| UNIT-REA-ADU | Réanimation adulte polyvalente | BAT-A / A-R1 | Service de référence | Monitorage multiparamétrique multi-lits. |
| UNIT-USC | Unité de soins continus | BAT-A / A-R1 | Surveillance continue | Destination de transfert. |
| UNIT-CARD-HOSP | Cardiologie hospitalisation | BAT-A / A-R2 | Hospitalisation spécialisée | Patient cardiologique et option télémétrie. |
| UNIT-MED-TRAUMA | Médecine / traumatologie | BAT-A / A-R2 | Hospitalisation | Destination après soins critiques. |
| UNIT-BLOC | Bloc opératoire | BAT-B / B-RDC | Secteur interventionnel | Parcours chirurgical ; salles plutôt que lits. |
| UNIT-SSPI | Salle de surveillance post-interventionnelle | BAT-B / B-RDC | Secteur de réveil | Monitorage court et transfert. |
| UNIT-CVICU | Soins intensifs cardio-vasculaires | BAT-B / B-R1 | Unité spécialisée | Parcours MIMIC cardio-vasculaire. |
| UNIT-CHIR-CARD | Chirurgie cardiaque | BAT-B / B-R1 | Hospitalisation chirurgicale | Destination après CVICU. |

## 6. Réseau, centrales et systèmes informatiques sur le plan

| Objet | ID | Emplacement fictif | Fonction |
|---|---|---|---|
| Poste / centrale REA | CENTRAL-REA-01 | BAT-A / A-R1 / REA-POSTE | Vue multi-lits de réanimation adulte. |
| Poste / centrale USC | CENTRAL-USC-01 | BAT-A / A-R1 / USC-POSTE | Vue des patients USC. |
| Centrale télémétrie | CENTRAL-CARD-01 | BAT-A / A-R2 / CARD-POSTE | Suivi des émetteurs mobiles. |
| Centrale CVICU | CENTRAL-CVICU-01 | BAT-B / B-R1 / CVICU-POSTE | Vue multi-lits cardio-vasculaire. |
| Centrale SSPI | CENTRAL-SSPI-01 | BAT-B / B-RDC / SSPI-POSTE | Vue des postes de réveil simulés. |
| Zone de sortie | ZONE-SORTIE | BAT-A / A-RDC | Zone non clinique de sortie / attente, sans lit de service. |
| Commutateur distribution A | NET-A-DIST-01 | BAT-A / A-S1 | Distribution réseau du bâtiment A. |
| Commutateur distribution B | NET-B-DIST-01 | BAT-B / B-R1 / local technique | Distribution réseau du bâtiment B. |
| Cœur réseau | NET-CORE-01 | BAT-A / A-S1 / ZONE-IT | Interconnexion des réseaux simulés. |
| Serveur logique du POC | SRV-POC-01 | BAT-A / A-S1 / ZONE-IT | Réception, stockage et API du simulateur. |
| UPS réseau / serveurs | UPS-IT-01 | BAT-A / A-S1 / ZONE-ELEC | Secours électrique fictif des composants raccordés. |
| Groupe électrogène simulé | GEN-01 | EXT-ENERGIE | Source de secours pour les zones configurées. |

La présence et la localisation de ces composants sont des hypothèses de la maquette, pas un constat sur un établissement réel.

## 7. Règles de représentation

- Une unité médicale peut avoir plusieurs chambres.
- Une chambre peut contenir un ou plusieurs emplacements de soin.
- Un lit ou poste a un identifiant unique, indépendant du patient.
- Un appareil peut être fixe, transportable ou porté par le patient.
- Une centrale appartient à une zone de surveillance, pas nécessairement à un seul service administratif.
- Une panne réseau ou électrique possède un périmètre explicite : appareil, chambre, étage, bâtiment ou site.
- La carte affiche séparément l'état du patient, du lit, de l'appareil, de la liaison et de la session de surveillance.

## 8. Évolutions par version

Les changements de nombre de lits, de chambres, d'unités ou de coordonnées doivent faire évoluer facilityMapVersion. Les scénarios de rejeu conservent la version de carte utilisée afin de rester reproductibles.
