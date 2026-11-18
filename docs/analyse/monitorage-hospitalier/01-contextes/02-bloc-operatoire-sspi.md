# Environnement 02 — Bloc opératoire et SSPI

**Version :** 0.1 — **Date :** 18 novembre 2026

## 1. Deux phases à distinguer

Le bloc opératoire et la salle de surveillance postinterventionnelle (SSPI) sont liés au parcours chirurgical, mais ils ne correspondent pas exactement au même environnement de monitorage.

- **Bloc opératoire :** le patient est pris en charge pendant une intervention sous anesthésie ou sédation ; le monitorage est associé au poste d'anesthésie et aux équipements utilisés pendant l'acte.
- **SSPI :** après l'intervention, la surveillance se poursuit dans une salle dédiée jusqu'à la récupération des fonctions nécessaires à la sortie ou au transfert.

## 2. Faits réglementaires sur la SSPI

Le Code de la santé publique précise notamment que :

- la surveillance postinterventionnelle commence dès la fin de l'intervention et de l'anesthésie ;
- elle ne s'interrompt pas pendant le transfert du patient ;
- elle se poursuit jusqu'au rétablissement et au maintien de l'autonomie respiratoire, de l'équilibre circulatoire et de la récupération neurologique ;
- chaque poste de SSPI dispose de moyens permettant le contrôle continu du rythme cardiaque avec affichage ECG et alarmes, le contrôle de la saturation en oxygène, la mesure périodique de la pression artérielle et le retour à l'équilibre thermique ;
- la salle comprend également un dispositif d'appel du personnel et du matériel d'assistance ventilatoire avec alarmes [H03].

Ces prescriptions donnent une description fonctionnelle concrète du monitorage en SSPI.

## 3. Équipements et paramètres

| Famille | Exemples de données / fonctions | Source |
|---|---|---|
| Moniteur patient | ECG, fréquence cardiaque, SpO₂, pression artérielle, température selon configuration. | [H03, H06] |
| Poste d'anesthésie | Paramètres hémodynamiques, ventilation, gaz et mesures liées à l'anesthésie selon le système. | [H06, H08] |
| Capnographie | Mesure du CO₂ expiré, utilisée notamment pour surveiller la ventilation. | [H06] |
| Dispositif d'assistance ventilatoire | État et alarmes de ventilation, surpression, débranchement. | [H03] |
| Centrale de surveillance | Vue distante ou centralisée des moniteurs, historiques et alarmes selon l'équipement. | [H07, H08] |
| Système d'appel | Demande de renfort humain lors d'une complication. | [H03] |

Les paramètres réellement utilisés dépendent du patient, du contexte anesthésique et de la prescription. Le document ne définit aucun seuil clinique.

## 4. Produits illustrant les systèmes disponibles

- **Philips IntelliVue MX750 et MX850 :** Philips les positionne pour les soins intensifs et l'anesthésie ; le X3 est présenté pour les soins intensifs et le transport [H06].
- **Dräger Infinity CentralStation :** la centrale annonce l'intégration de données provenant de moniteurs, de ventilateurs et d'appareils d'anesthésie Dräger [H08].
- **GE CARESCAPE Central Station :** la documentation liste l'affichage des données de moniteurs et des paramètres issus de ventilateurs et systèmes connectés [H07].

Ces exemples montrent les familles de produits proposées. Ils ne prouvent pas qu'un bloc ou une SSPI donné utilise ces références.

## 5. Besoins métiers candidats

| ID | Besoin | Pourquoi |
|---|---|---|
| OR-01 | Identifier le patient et le poste de surveillance. | Éviter la confusion entre salles, postes et dossiers. |
| OR-02 | Afficher ensemble les constantes pertinentes. | Le personnel consulte plusieurs paramètres pendant l'intervention et la récupération. |
| OR-03 | Distinguer les sources : moniteur, respirateur, anesthésie. | Chaque équipement peut générer ses propres mesures et alarmes. |
| OR-04 | Conserver l'historique des mesures et événements. | Reconstituer le déroulement et les incidents. |
| OR-05 | Maintenir la surveillance lors du transfert vers la SSPI. | La réglementation précise la continuité pendant le transfert. |
| OR-06 | Déclencher un appel ou une alerte vers le personnel. | Un dispositif d'alerte est prévu en SSPI. |
| OR-07 | Préparer la relève entre équipes. | Transmission de l'anesthésie, de l'intervention, des points de vigilance et des paramètres suivis. |
| OR-08 | Gérer les limites et alarmes adaptées. | Les alarmes doivent avoir un sens dans le contexte patient et intervention. |

## 6. Scénarios à documenter

- préparation d'un poste avant l'arrivée du patient ;
- installation et connexion des capteurs ;
- suivi d'un changement de paramètre ;
- alarme du moniteur patient ;
- alarme provenant d'un ventilateur ou poste d'anesthésie ;
- changement de poste ou de salle ;
- fin d'intervention ;
- transfert sous surveillance vers la SSPI ;
- indisponibilité d'un moniteur pendant le transfert ;
- remise des informations à l'équipe de SSPI ;
- sortie de SSPI après décision médicale.

## 7. Sources

- **[H03]** Code de la santé publique, articles D.6124-97 à D.6124-103, surveillance postinterventionnelle : https://www.legifrance.gouv.fr/codes/section_lc/LEGITEXT000006072665/LEGISCTA000006198881/2026-07-22
- **[H06]** Philips, gamme de moniteurs IntelliVue : https://www.philips.fr/healthcare/brand/intellivue-patient-monitors
- **[H07]** GE HealthCare, CARESCAPE Central Station : https://www.gehealthcare.com/fr-fr/products/patient-monitoring/patient-monitors/carescape-central-station
- **[H08]** Dräger, Infinity CentralStation Wide : https://www.draeger.com/fr_fr/Products/Infinity-CentralStation

## 8. Limites

Ce document ne couvre pas la conception détaillée d'un système d'information anesthésique, le dossier d'anesthésie, les équipements de ventilation spécialisés, ni les prescriptions cliniques. Ces thèmes peuvent faire l'objet de documents séparés si le périmètre du POC les inclut.
