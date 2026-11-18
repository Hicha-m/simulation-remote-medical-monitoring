# 02 — Acteurs, parcours et scénarios

**Version :** 0.1 — **Date :** 18 novembre 2026  
**Statut :** cartographie de travail ; rôles et parcours à confirmer avec des professionnels concernés.

## 1. Acteurs possibles

Les acteurs suivants sont présents dans des systèmes de télésurveillance ou de monitorage documentés. Tous ne sont pas nécessairement utiles au périmètre final.

| Acteur | Responsabilité ou interaction possible | À valider |
|---|---|---|
| Patient | Porte les mesures, répond à des questionnaires, utilise un appareil ou une application dans un scénario à domicile. | Le patient est-il un utilisateur direct du POC ? |
| Aidant | Peut aider le patient à utiliser l'application ou à transmettre les informations. | Le scénario prévoit-il cette assistance ? |
| Appareil / moniteur | Produit des mesures ou des signaux et possède une identité technique. | Type de dispositif, identifiant, état, fréquence, protocole. |
| Simulateur client | Reproduit le comportement d'un appareil sans capteur réel. | Doit-il simuler un appareil, un patient, un flux ou plusieurs appareils ? |
| Passerelle | Relie un appareil à un réseau ou à un serveur. | Présente ou non selon l'architecture retenue. |
| Serveur de réception | Reçoit les messages et contrôle leur format et leur origine. | Rôle exact et responsabilité technique. |
| Moteur de règles | Évalue les événements selon des règles paramétrées. | Règles techniques, règles de workflow ou règles cliniques ? |
| Infirmier / infirmière | Peut recevoir, vérifier, classer ou traiter des alertes selon l'organisation réelle. | Rôle, compétences, habilitations, horaires. |
| Médecin | Peut intervenir pour l'analyse médicale et les décisions relevant de sa responsabilité. | Type d'intervention et parcours de recours. |
| Coordinateur de parcours / IDEC | Peut coordonner le suivi, les retours patient et les relais entre acteurs. | Selon le service et le domaine étudié. |
| Opérateur de télésurveillance | Organise l'activité et la continuité du suivi médical au sens du cadre français. | Équipe, fonctionnement, astreinte et responsabilité. |
| Administrateur technique | Gère la plateforme et sa disponibilité. | À distinguer des fonctions cliniques. |
| Administrateur des habilitations | Gère les comptes, rôles et permissions. | Séparation des tâches à vérifier. |
| Ingénieur biomédical | Peut être impliqué dans le suivi des équipements médicaux et leurs interfaces. | Présent surtout dans un scénario hospitalier. |
| Équipe SI / cybersécurité | Gère l'intégration, les réseaux, les identités, les incidents et la sécurité. | Organisation de l'établissement. |
| DPO / référent données personnelles | Accompagne l'organisme sur la protection des données personnelles. | À consulter si un traitement réel est envisagé. |

### Source de terrain identifiée

Dans le retour d'expérience publié par Resilience concernant l'Hôpital Européen de Marseille, le déploiement mobilise notamment la direction, une responsable e-santé, une cheffe de pôle, une équipe informatique, des médecins, des infirmiers et un infirmier de coordination. Une infirmière assure l'inclusion et le traitement des alertes ; l'IDEC exploite les questionnaires pour la prévalidation des cures [S12].

Cette description est propre à un service d'oncologie et à un retour d'expérience édité par un fournisseur. Elle ne doit pas être généralisée à tous les hôpitaux.

## 2. Parcours fonctionnel générique à documenter

Le parcours suivant est un squelette de discussion. Il ne décrit pas une procédure médicale universelle.

1. **Création du suivi** — un dossier de patient ou un patient fictif est créé.
2. **Association** — un ou plusieurs appareils ou sources de données sont associés au suivi.
3. **Configuration** — paramètres attendus, fréquence, unités, règles de qualité et règles de notification sont définis.
4. **Production** — un appareil ou simulateur produit une mesure ou un signal.
5. **Transmission** — le message traverse le réseau et arrive au serveur.
6. **Contrôles techniques** — identité de la source, format, horodatage, intégrité, unité et doublons sont vérifiés.
7. **Enregistrement** — la mesure et ses métadonnées sont conservées.
8. **Traitement** — des règles techniques ou métier peuvent identifier un événement.
9. **Présentation** — la mesure ou l'événement est rendu visible à l'utilisateur concerné.
10. **Triage** — l'événement est vérifié et orienté selon une organisation définie.
11. **Action et suivi** — l'acteur habilité réalise les actions relevant de son rôle.
12. **Clôture ou relais** — le traitement est terminé, transmis ou reste en attente avec une trace.
13. **Fin du suivi** — l'association patient-appareil est arrêtée, le suivi clôturé et les règles de conservation appliquées.

Les étapes 8 à 12 sont particulièrement importantes : une notification affichée ne prouve pas qu'une alerte a été prise en charge.

## 3. Scénarios nominaux

Ces scénarios servent à comprendre le fonctionnement dans des conditions habituelles.

| ID | Scénario | Questions à résoudre |
|---|---|---|
| NOM-01 | Un appareil émet une mesure valide. | Comment l'appareil, le patient, l'heure et l'unité sont-ils identifiés ? |
| NOM-02 | Plusieurs appareils transmettent pour le même patient. | Comment les sources sont-elles distinguées ? |
| NOM-03 | Plusieurs patients transmettent simultanément. | Comment les informations sont-elles réparties et présentées ? |
| NOM-04 | Un utilisateur consulte la liste des patients. | Quels critères de tri et quelles informations minimales ? |
| NOM-05 | Un utilisateur ouvre l'historique d'un patient. | Quelle période, quelle granularité, quels filtres ? |
| NOM-06 | Un utilisateur se connecte à son poste. | Quel rôle et quelles données peut-il consulter ? |
| NOM-07 | Un suivi commence ou se termine. | Comment éviter qu'un appareil reste associé au mauvais patient ? |

## 4. Scénarios d'anomalie de données et de réseau

| ID | Scénario | Problème à observer | Mesures possibles |
|---|---|---|---|
| DATA-01 | Aucun message reçu pendant la période attendue. | Absence de transmission. | Délai depuis la dernière donnée, détection et notification. |
| DATA-02 | Appareil hors ligne. | Rupture de connectivité ou arrêt de l'appareil. | Détection, statut et reprise. |
| DATA-03 | Message reçu en retard. | L'heure de réception diffère de l'heure de mesure. | Latence, ordre d'affichage et historique. |
| DATA-04 | Message reçu plusieurs fois. | Doublon. | Détection et idempotence du traitement. |
| DATA-05 | Messages reçus dans le désordre. | Ordonnancement différent de l'ordre de mesure. | Conservation des deux horodatages. |
| DATA-06 | Mesure sans identité de patient ou d'appareil. | Association impossible. | Rejet, mise en quarantaine ou procédure de rapprochement. |
| DATA-07 | Unité ou format inattendu. | Interprétation incorrecte possible. | Validation et journalisation du rejet. |
| DATA-08 | Signal dégradé ou artefact. | Valeur non représentative ou mesure de faible qualité. | Statut de qualité et distinction d'une alerte médicale. |
| DATA-09 | Horloge du client incorrecte. | Horodatage incohérent. | Comparaison heure appareil / réception. |
| DATA-10 | Coupure réseau puis reconnexion. | Accumulation et renvoi de messages. | Rattrapage, doublons et ordre. |

## 5. Scénarios d'alertes et de coordination

| ID | Scénario | Questions métier |
|---|---|---|
| ALT-01 | Mesure hors d'une zone configurée. | Qui définit la zone ? Qui reçoit l'événement ? |
| ALT-02 | Absence de données attendues. | Quelle durée déclenche une alerte de non-transmission ? |
| ALT-03 | Plusieurs alertes concernent un même patient. | Faut-il les regrouper ou les traiter séparément ? |
| ALT-04 | Plusieurs patients génèrent des alertes au même moment. | Comment les prioriser sans prétendre automatiser une décision clinique ? |
| ALT-05 | Un utilisateur acquitte une alerte. | Que signifie l'acquittement et quelles traces conserver ? |
| ALT-06 | Une alerte n'est pas traitée dans un délai donné. | Existe-t-il une escalade ? Vers quel rôle ? |
| ALT-07 | Une alerte est déclarée non pertinente. | Quel motif et quelle trace ? |
| ALT-08 | Une équipe change de poste. | Comment transmettre les alertes ouvertes et les suivis en cours ? |
| ALT-09 | Un patient ne répond pas ou n'utilise plus l'application. | Quel processus de contact existe réellement ? |
| ALT-10 | Un suivi est transféré à une autre équipe ou unité. | Quels droits, associations et historiques doivent changer ? |

Le ministère français distingue notamment les alertes de mesures hors zone cible des alertes relatives à la non-transmission et décrit des modes de tri manuels ou automatiques [S08]. Cela montre que l'absence de message peut être un événement métier à part entière, distinct d'une mesure physiologique.

## 6. Scénarios d'exploitation et de sécurité

| ID | Scénario | Sujet à tester |
|---|---|---|
| OPS-01 | Serveur d'ingestion indisponible. | Perte, mise en attente ou rattrapage des mesures. |
| OPS-02 | Base de données indisponible. | Comportement à la réception et reprise après incident. |
| OPS-03 | Tableau de bord déconnecté. | Reconnexion et rattrapage de l'état courant. |
| OPS-04 | Redémarrage d'un composant. | Persistance et cohérence des états. |
| OPS-05 | Pic de messages simultanés. | Latence, saturation et files d'attente. |
| SEC-01 | Un utilisateur tente d'accéder à un patient non autorisé. | Contrôle des droits côté serveur. |
| SEC-02 | Un compte est compromis. | Impact, révocation et traçabilité. |
| SEC-03 | Un appareil non enregistré transmet. | Authentification de la source et rejet. |
| SEC-04 | Une mesure est modifiée ou rejouée. | Intégrité, authenticité, détection des rejeux. |
| SEC-05 | Un administrateur consulte des dossiers. | Séparation des droits et journalisation. |
| SEC-06 | Tentatives de connexion répétées. | Limitation, alerte et protection de compte. |
| SEC-07 | Une sauvegarde doit être restaurée. | Intégrité, délai de reprise et vérification. |

## 7. Scénarios propres au monitorage hospitalier

À retenir seulement si l'interprétation A ou C est confirmée :

- association d'un moniteur à un lit et à un patient ;
- transfert du patient d'un lit ou d'une unité vers une autre ;
- débranchement ou remplacement d'un capteur ;
- changement d'équipe ou relève ;
- surveillance par un poste central avec plusieurs écrans ;
- perte temporaire du réseau d'une unité ;
- retour d'un patient ou d'un appareil après transfert.

Ces cas doivent être décrits avec des professionnels du service concerné.

## 8. Scénarios propres à la télésurveillance à domicile

À retenir seulement si l'interprétation B ou C est confirmée :

- inclusion et consentement du patient ;
- remise, configuration ou association d'un appareil ;
- mesure automatique ou saisie manuelle ;
- accompagnement d'un patient peu à l'aise avec le numérique ;
- partage de l'accès avec un aidant ;
- appareil non chargé, non utilisé ou non connecté ;
- absence de mesure et relance du patient ;
- interruption du suivi ou retrait du patient.

Le retour d'expérience de l'Hôpital Européen Marseille décrit notamment l'information du patient, le recueil du consentement, l'accompagnement à l'installation de l'application et les difficultés possibles liées à l'illectronisme ou à la réticence au partage d'informations [S12].

## 9. Priorité de modélisation

Pour chaque scénario retenu, créer ultérieurement une fiche comprenant :

- acteur initiateur ;
- préconditions ;
- événement déclencheur ;
- séquence de messages et de traitements ;
- état avant et après ;
- erreurs et interruptions possibles ;
- notifications visibles ;
- responsabilités humaines ;
- données persistées ;
- traces d'audit ;
- critères permettant de vérifier le résultat.

Aucun seuil clinique ou protocole de prise en charge ne doit être inventé pour remplir ces fiches.
