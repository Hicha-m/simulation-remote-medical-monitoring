# Métier 01 — Acteurs et responsabilités dans le monitorage hospitalier

**Version :** 0.1 — **Date :** 18 novembre 2026  
**Statut :** cartographie générique ; les responsabilités exactes varient selon service et établissement.

## 1. Pourquoi séparer les rôles

Un système de monitorage ne se limite pas à l'utilisateur qui regarde un écran. Plusieurs professionnels interviennent autour du patient, du matériel, des alarmes, de la configuration, de la maintenance et des systèmes informatiques.

La HAS souligne que l'organisation de la surveillance en soins critiques doit couvrir l'architecture, le matériel, les procédures, la formation et la présence des personnels près de la centrale [H02].

## 2. Acteurs cliniques

| Acteur | Activités possibles | Interaction avec le système |
|---|---|---|
| Infirmier / infirmière au chevet (IDE) | Installer les capteurs, vérifier le patient et les mesures, répondre aux alarmes, assurer les soins, transmettre les informations. | Consultation du moniteur, gestion des alarmes selon habilitations, actions documentées. |
| Médecin | Définir ou prescrire les paramètres et la surveillance requise selon le contexte, interpréter les informations et décider de la prise en charge. | Consultation des mesures, tendances, courbes et événements. |
| Aide-soignant / personnel paramédical selon unité | Participer à certaines tâches de surveillance et de soins dans le cadre des responsabilités autorisées. | Peut signaler un événement ou aider à la surveillance, sans se voir attribuer automatiquement le rôle de décision clinique. |
| Infirmier de coordination / cadre | Organiser le suivi et le travail des équipes, les transmissions et parfois la gestion d'un service. | Visibilité sur les patients, les événements en attente et la continuité. |
| Personnel de salle de surveillance / monitor watcher | Dans certaines organisations, observer une banque de moniteurs et signaler les événements aux équipes responsables. | Poste central et communication avec les équipes au chevet. |
| Médecin anesthésiste | Surveiller le patient au bloc et organiser le suivi anesthésique périopératoire. | Moniteur et poste d'anesthésie, alarmes et données associées. |
| Équipe de transport | Maintenir la prise en charge et la surveillance pendant un déplacement. | Moniteur portable, respirateur, équipements de transport et transmission à l'arrivée. |

La fonction de surveillance centrale par un « monitor watcher » n'est pas uniforme. La littérature décrit des établissements où l'observation est effectuée par les infirmiers au chevet et d'autres où un personnel dédié observe les moniteurs et alerte l'équipe responsable [H11, H14].

## 3. Acteurs techniques et organisationnels

| Acteur | Responsabilités possibles | Interaction avec le système |
|---|---|---|
| Ingénieur biomédical | Gestion du parc de dispositifs, suivi technique, maintenance, contrôles et relations fournisseurs. | Inventaire des appareils, état, maintenance et incidents techniques. |
| Technicien biomédical | Installation, vérification, réparation et préparation des équipements. | Statut des dispositifs, numéros de série, disponibilité et maintenance. |
| DSI / équipe informatique | Réseau, serveurs, comptes techniques, intégration et disponibilité des services. | Gestion réseau, interfaces, supervision et mises à jour. |
| Équipe cybersécurité | Réduction du risque cyber, suivi des incidents, contrôle des accès et vulnérabilités. | Journaux, alertes de sécurité, segmentation et gestion des comptes. |
| Administrateur applicatif | Configuration fonctionnelle et technique des outils. | Comptes, profils, paramètres et référentiels. |
| Direction / cadre de santé | Organisation des moyens, procédures et formation. | Indicateurs d'activité, ressources et continuité opérationnelle. |
| Fournisseur / mainteneur | Fournit, maintient et fait évoluer le matériel et les logiciels selon le contrat. | Mise à jour, support, diagnostic et cycle de vie produit. |

## 4. Exemple de séparation des responsabilités autour d'une alarme

| Étape | Acteur possible | Ce qui doit être clair |
|---|---|---|
| L'appareil détecte une condition | Moniteur ou dispositif | Quelle condition, quelle priorité et quelle source ? |
| L'événement est visible à la centrale | Système | Où l'alarme est-elle diffusée ? |
| L'alarme est observée | Personnel désigné | Qui est chargé de regarder la centrale ? |
| Le professionnel au chevet est alerté | Observateur / système de notification | Comment confirmer que le message a été reçu ? |
| La situation est évaluée | Professionnel compétent | Qui prend la décision clinique ? |
| L'action est tracée | Équipe concernée | Où et comment documenter ? |
| L'événement est clôturé | Rôle autorisé selon procédure | Quel statut signifie que le suivi est terminé ? |

Ce tableau est une grille d'analyse et ne constitue pas un protocole de soins.

## 5. Besoins d'habilitation à explorer

- IDE : patients et appareils de son unité, affichage et actions permises par la procédure.
- Médecin : accès aux données nécessaires à sa mission et à l'historique clinique autorisé.
- Personnel de surveillance centrale : vue des patients relevant de son périmètre et possibilité de transmettre les événements.
- Biomédical : informations techniques sur le dispositif, sans accès automatique au détail clinique non nécessaire.
- DSI : supervision et administration technique sans accès clinique généralisé.
- Administrateur : gestion des comptes et configurations avec journalisation des opérations sensibles.

Les rôles exacts et leurs droits doivent être définis avec l'établissement ; ce modèle n'est pas une matrice d'habilitation officielle.

## 6. Sources

- **[H02]** HAS, Flash Sécurité Patient — surveillance des patients en soins critiques : https://www.has-sante.fr/jcms/p_3511526/fr/flash-securite-patient-surveillance-des-patients-en-service-de-soins-critiques-une-veille-sans-faille-pour-qu-aucun-patient-ne-defaille
- **[H11]** Monitor-watcher use, nurses' knowledge of electrocardiographic monitoring, and arrhythmia detection, 2021 : https://pmc.ncbi.nlm.nih.gov/articles/PMC8246648/
- **[H14]** Strengthening Telemetry Safety Through Standardized Physiological Parameter Monitor Technician Education, 2026 : https://pmc.ncbi.nlm.nih.gov/articles/PMC13680767/
- **[H22]** Simulation-Based Usability Testing of Physiologic Monitors, 2021 : https://nursing.jmir.org/2021/1/e20584
