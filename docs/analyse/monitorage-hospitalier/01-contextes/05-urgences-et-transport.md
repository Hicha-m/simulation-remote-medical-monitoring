# Environnement 05 — Urgences et transport intrahospitalier

**Version :** 0.1 — **Date :** 18 novembre 2026

## 1. Les urgences ne sont pas une zone homogène

Une structure d'urgence regroupe plusieurs espaces et niveaux de prise en charge : accueil et triage, zones d'attente surveillées, circuits d'évaluation rapide, salles de soins, salle d'accueil des urgences vitales (SAUV) / déchocage et espaces d'observation.

Le référentiel SFMU sur l'architecture des structures de médecine d'urgence décrit ces zones et précise que les organisations doivent être adaptées à l'activité, aux ressources et à l'infrastructure. Il distingue notamment le triage, les zones d'attente et la SAUV [H17].

Les besoins de monitorage ne sont donc pas les mêmes dans une salle d'attente, un box de soins et une salle de déchocage. La présence d'un moniteur multiparamétrique ne doit pas être supposée à chaque étape.

## 2. La salle d'accueil des urgences vitales

La SFMU publie un référentiel spécifique sur la mise en place, la gestion, l'utilisation et l'évaluation d'une SAUV. Cette source doit servir de base pour étudier l'organisation du déchocage, les espaces, les équipements, les équipes et la disponibilité du matériel [H18].

Pour le POC, les besoins candidats sont :
- identifier le patient et le poste de prise en charge ;
- afficher les paramètres nécessaires à l'équipe ;
- recueillir des données de plusieurs équipements ;
- rendre visibles les alarmes au bon endroit ;
- conserver un historique pendant la phase de prise en charge ;
- organiser la transmission lors d'un transfert vers une unité ou l'imagerie.

Les détails de paramètres et de rôles devront être établis à partir du référentiel complet et d'un professionnel des urgences.

## 3. Le transport intrahospitalier est une phase à part entière

La HAS qualifie le transport intrahospitalier des patients de soins critiques de composante à part entière de leur prise en charge. Elle indique que la surveillance continue ne doit pas être interrompue pendant le déplacement et identifie des risques liés au matériel, aux personnels, à la communication, aux réglages et à la surveillance [H19].

Le Code de la santé publique précise en SSPI que la surveillance postinterventionnelle ne s'interrompt pas pendant le transfert [H03].

Le référentiel de certification HAS 2024 inclut également la maîtrise du transport intrahospitalier parmi les critères évalués : professionnels formés, matériel adapté, sécurité et confort du patient [H20].

## 4. Exemple d'équipement : moniteur portable

Dräger présente l'Infinity M540 comme un moniteur qui peut être retiré de sa station d'accueil pour le transport, tout en continuant à surveiller les paramètres et alarmes ; les données sont ensuite accessibles au retour sur une station d'accueil et au système central. Le fabricant annonce également un stockage de tendances et d'événements [H10].

Philips positionne l'IntelliVue X3 comme moniteur utilisable en soins intensifs et en transport [H06].

Ces exemples illustrent le principe d'une surveillance qui suit le patient, plutôt qu'un patient qui doit rester relié à une station fixe.

## 5. Retours d'expérience documentés par la HAS

Le flash de la HAS du 21 mars 2024 présente trois événements indésirables réels déclarés :

1. **Bouteille d'oxygène épuisée pendant un transport vers l'IRM :** le patient était ventilé ; la réserve d'oxygène s'est vidée et le changement d'indication de FiO₂ sur l'écran n'a pas entraîné de perception des alarmes. La HAS relève notamment l'absence de formation à une nouvelle bouteille, l'absence de vérification des réserves, l'absence de procédure et des difficultés de compatibilité / raccordement du matériel.
2. **Erreur de montage d'un circuit de ventilation :** le matériel et la procédure n'étaient pas suffisamment préparés et connus ; la vérification du montage et la disponibilité d'un circuit prêt à l'emploi étaient défaillantes.
3. **Raccordement à un ventilateur à l'arrêt au retour du patient :** un changement d'équipe, une répartition des tâches non anticipée et une vérification absente ont contribué à l'événement. La surveillance cardiaque a également été débranchée au cours du transfert lit-brancard.

La HAS rappelle que la surveillance continue ne doit pas être interrompue et que le transport doit être organisé avec personnel formé, procédure, matériel, liste de vérification et possibilité d'appel d'urgence [H19].

Ces événements sont particulièrement pertinents pour un laboratoire de simulation : ils montrent des défaillances de coordination et d'équipement qu'un test de réseau seul ne couvrirait pas.

## 6. Besoins métiers candidats pour un transport

| ID | Besoin | Justification |
|---|---|---|
| TR-01 | Maintenir le suivi pendant le déplacement. | Continuité attendue pour les patients de soins critiques. |
| TR-02 | Disposer d'un équipement adapté au transport. | Le matériel et les conditions diffèrent du chevet fixe. |
| TR-03 | Afficher l'état de la batterie et de la connexion. | Le transport dépend d'un appareil autonome et de liaisons radio éventuelles. |
| TR-04 | Conserver les mesures durant les zones sans réseau. | Éviter les trous de données et permettre une reprise contrôlée. |
| TR-05 | Retrouver l'historique au point d'arrivée. | La surveillance et les tendances doivent rester accessibles. |
| TR-06 | Relier la destination et le nouveau lit au patient. | Éviter les erreurs d'affectation. |
| TR-07 | Transmettre les informations à l'équipe d'accueil. | La prise en charge est un passage de responsabilité. |
| TR-08 | Vérifier le matériel avant le départ. | Les procédures de transport et la disponibilité du matériel sont importantes. |

Les besoins TR-03 à TR-06 constituent des exigences candidates déduites des systèmes portables et de la nécessité de continuité. Ils ne sont pas présentés comme des fonctions obligatoires de tous les moniteurs.

## 7. Scénario opérationnel à étudier

1. Un transport est décidé et préparé.
2. L'équipe vérifie le patient, la destination et le matériel.
3. Le monitorage est basculé vers un équipement transportable ou une configuration adaptée.
4. Les mesures continuent d'être observées.
5. Une perte de réseau, une alarme ou une panne éventuelle survient.
6. À l'arrivée, le patient est installé et les équipements sont reconnectés.
7. Les données du transport sont conservées et rendues accessibles.
8. Une transmission est réalisée à l'équipe d'accueil.

Cette séquence est un scénario d'analyse informatique et organisationnelle, pas un protocole de transport clinique.

## 8. Sources

- **[H03]** Code de la santé publique, surveillance postinterventionnelle : https://www.legifrance.gouv.fr/codes/section_lc/LEGITEXT000006072665/LEGISCTA000006198881/2026-07-22
- **[H06]** Philips, gamme IntelliVue : https://www.philips.fr/healthcare/brand/intellivue-patient-monitors
- **[H10]** Dräger, Infinity M540 : https://www.draeger.com/fr_fr/Products/Infinity-M540-monitor
- **[H17]** SFMU, Architecture des structures de médecine d'urgence (2024) : https://www.sfmu.org/fr/vie-professionnelle/outils-professionnels/referentiels-sfmu/architecture-des-structures-de-medecine-d-urgence-2024-/ref_id/52
- **[H18]** SFMU, Référentiel SAUV : https://www.sfmu.org/fr/vie-professionnelle/outils-professionnels/referentiels-sfmu/recommandations-concernant-la-mise-en-place-la-gestion-l-utilisation-et-l-evaluation-d-une-salle-d-accueil-des-urgences-vitales-sauv-/ref_id/16
- **[H19]** HAS, Flash Sécurité Patient — Transport intrahospitalier des patients de soins critiques : https://www.has-sante.fr/upload/docs/application/pdf/2024-03/flash_secrutie_patient_-transport_intrahospitalier_des_patients_de_soins_critiques_..._le_transport_lui_aussi_est_critique.pdf
- **[H20]** HAS, Manuel de certification des établissements de santé, version 2024, critère 2.3-22 : https://www.has-sante.fr/upload/docs/application/pdf/2023-09/manuel_2024.pdf
