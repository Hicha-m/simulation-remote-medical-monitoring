# Parcours hospitaliers complets et personas

**Date :** 18 novembre 2026  
**Statut :** scénarios composites fictifs construits à partir de processus et de données documentés ; ils ne constituent pas des protocoles médicaux.

## 1. Peut-on obtenir des logs réels ?

Oui, sous certaines formes, mais il faut distinguer les traces disponibles :

| Type de trace | Exemple | Ce que cela permet de comprendre | Limite |
|---|---|---|---|
| Dossier patient informatisé | Admission, diagnostic, traitements, actes, sorties. | Parcours administratif et médical. | Données personnelles sensibles ; accès opérationnel non public. |
| Journal de mouvements | Entrée, sortie, changement d'unité ou de lit. | Séquence des lieux et durées de séjour. | N'explique pas nécessairement les mesures ou les alarmes. |
| Données de monitorage / dossier de soins intensifs | Constantes, courbes dérivées, observations, réglages de dispositifs. | Évolution temporelle de l'état surveillé et des équipements. | Peuvent être agrégées, nettoyées ou issues d'un système particulier. |
| Journal d'alarmes d'un moniteur ou d'une centrale | Déclenchement, priorité, état, acquittement, historique. | Cycle de vie d'une alarme. | Souvent propriétaire, non publié ou absent des bases de recherche généralistes. |
| Retour d'expérience HAS / ANSM | Cas anonymisé d'événement indésirable et analyse des causes. | Défaillances de surveillance, de transfert ou d'organisation. | Récit structuré, pas un flux technique exhaustif. |

Le ministère rappelle que le dossier patient est créé dès l'admission et rassemble des volets administratif et médical [H109]. La HAS publie des retours d'expérience sur des événements réels en soins critiques, notamment des cas où la déconnexion d'un système, le report d'alarme ou l'organisation humaine ont contribué à un défaut de surveillance [H02].

## 2. Bases de données de recherche à étudier

Ces jeux de données proviennent de véritables environnements hospitaliers, mais ne sont pas des journaux opérationnels français et ne doivent pas être traités comme des protocoles de soins.

| Base | Couverture | Apport au POC | Accès et précautions |
|---|---|---|---|
| MIMIC-IV [H100] | Dossier hospitalier et système d'information des soins intensifs du Beth Israel Deaconess Medical Center. Contient admissions, transferts, mesures, traitements et événements documentés. | Modéliser patient, hospitalisation, séjour d'unité et chronologie. | Accès réservé aux utilisateurs qualifiés, formation de recherche et accord d'utilisation. |
| MIMIC-IV-ED [H101] | Séjours aux urgences, triage, constantes ponctuelles, traitements et orientation. | Modéliser arrivée, triage, première mesure, attente et orientation. | Données anonymisées de recherche ; unités et pratiques américaines. |
| HiRID [H102] | Admissions en soins intensifs du Bern University Hospital ; données de monitorage, dispositifs, observations, laboratoires et traitements. Beaucoup de paramètres de chevet sont enregistrés toutes les deux minutes. | Comprendre la densité temporelle des observations et les sources multiples. | Dates et données démographiques transformées pour l'anonymisation. |
| eICU [H103] | Base multicentrique de plus de 200 000 admissions en soins intensifs. | Étudier la variabilité entre unités et les interfaces. | Les données dépendent des interfaces disponibles dans chaque unité ; une mesure absente de la base n'a pas nécessairement été absente du soin. Accès soumis à conditions. |
| AmsterdamUMCdb [H104] | Unités de soins intensifs et de haute dépendance d'Amsterdam UMC, adultes, 2003–2016 pour la version publiée 1.5.0. | Comparaison européenne et données longitudinales de soins intensifs. | Accès de recherche soumis à approbation ; données anciennes et issues d'un établissement particulier. |

### Ce que ces bases ne donnent pas automatiquement

- Le flux réseau exact émis par un moniteur donné.
- Le protocole propriétaire de la centrale.
- Tous les événements sonores ou visuels d'une alarme.
- La manière dont une infirmière a physiquement réagi à chaque alarme.
- Une représentation complète et uniforme des transferts pour tous les patients.
- Les pratiques exactes d'un établissement français.

**Recommandation :** s'en servir pour comprendre les structures, les unités, les horodatages, les fréquences et la variété des observations. Pour le POC, créer des scénarios synthétiques propres, rejouables et documentés.

## 3. Pourquoi utiliser plusieurs personas ?

Un seul parcours ne représente pas un hôpital. Les patients n'arrivent pas tous de la même manière, ne reçoivent pas les mêmes appareils et ne terminent pas leur séjour dans le même service.

Les personas ci-dessous sont des personnages fictifs. Les valeurs physiologiques et les seuils ne sont volontairement pas définis dans ce document.

### Persona P01 — Admission aux urgences puis soins critiques

**Profil fictif :** adulte admis aux urgences pour une dégradation respiratoire, puis orienté vers une réanimation adulte.

| Étape | Lieu et événement | Appareils / données simulés | Ce que le système doit gérer |
|---|---|---|---|
| 1 | Arrivée aux urgences et création du dossier de passage. | Première série de constantes, identifiant de passage. | Créer le contexte d'hospitalisation sans supposer que le patient est déjà affecté à un lit de réanimation. |
| 2 | Triage et installation dans une zone de surveillance. | Moniteur multiparamétrique ou appareils ponctuels selon la zone. | Associer les données au bon patient et au bon passage. |
| 3 | Décision d'orientation vers les soins critiques. | Événement de transfert et nouvelle localisation. | Préparer le changement d'unité et garder l'historique. |
| 4 | Admission en réanimation et installation au lit. | Moniteur de chevet ; éventuellement respirateur et pompes représentés comme sources séparées. | Associer lit, moniteur, patient et séjour d'unité ; vérifier la fraîcheur des données. |
| 5 | Épisode de surveillance avec événement physiologique ou technique simulé. | Observations, état de capteur, alarme. | Détecter, transmettre, afficher, acquitter et clôturer l'événement sans confondre ces étapes. |
| 6 | Stabilisation et transfert vers USC ou unité conventionnelle. | Moniteur de transport, puis équipement du service d'accueil. | Ne pas mélanger les mesures avant et après transfert ; tracer la continuité et le changement d'appareil. |
| 7 | Fin de l'hospitalisation. | Fin de session et désassociation des équipements. | Fermer le suivi, conserver l'historique et rendre l'appareil disponible selon son état. |

**Scénarios critiques :** transfert pendant une surveillance active, perte de connexion, mesure tardive provenant de l'ancien appareil, alarme non acquittée, appareil affecté au mauvais lit.

### Persona P02 — Parcours chirurgical et réveil en SSPI

**Profil fictif :** adulte programmé pour une intervention chirurgicale, puis surveillé en SSPI avant retour en hospitalisation.

| Étape | Lieu et événement | Appareils / données simulés | Ce que le système doit gérer |
|---|---|---|---|
| 1 | Admission et préparation préopératoire. | Identité, séjour et lieu de prise en charge. | Créer et retrouver le bon séjour. |
| 2 | Entrée au bloc opératoire. | Moniteur d'anesthésie ou moniteur multiparamétrique. | Associer le patient à la salle et à l'appareil. |
| 3 | Fin de l'intervention et transfert vers SSPI. | Moniteur de transport et mesures de surveillance. | Garder une surveillance identifiée pendant le mouvement. |
| 4 | Installation sur un poste de SSPI. | ECG, SpO₂, PNI, température selon le profil simulé. | Associer un nouveau poste et conserver l'historique précédent. |
| 5 | Événement ou alarme pendant le réveil. | Observation ou alarme simulée. | Afficher l'événement et tracer l'acquittement et la résolution. |
| 6 | Décision de sortie de SSPI et transfert en unité d'hospitalisation. | Événement de sortie et fin de session. | Clore le profil SSPI et désassocier les appareils. |
| 7 | Sortie de l'établissement. | Clôture du séjour. | Conserver la chronologie et éviter une session de monitorage orpheline. |

La réglementation française précise la continuité de la surveillance postinterventionnelle pendant le transfert [H03, H108].

**Scénarios critiques :** transfert sans rupture de suivi, changement de poste, clôture de la session, traçabilité des heures d'entrée et de sortie.

### Persona P03 — Patient de cardiologie sous télémétrie

**Profil fictif :** adulte admis en cardiologie après une évaluation aux urgences ; il peut se déplacer dans l'unité.

| Étape | Lieu et événement | Appareils / données simulés | Ce que le système doit gérer |
|---|---|---|---|
| 1 | Passage aux urgences. | ECG initial et constantes. | Créer le lien entre le passage aux urgences et l'hospitalisation. |
| 2 | Admission en cardiologie. | Transmetteur de télémétrie portable. | Associer un appareil mobile à la bonne personne et à la bonne session. |
| 3 | Déplacement du patient dans l'unité. | ECG / fréquence cardiaque, état radio et batterie. | Conserver le contexte patient malgré la mobilité. |
| 4 | Perte de signal ou sortie de zone simulée. | Événement technique de télémétrie. | Déclencher un état technique visible et ne pas présenter les anciennes valeurs comme actuelles. |
| 5 | Événement ECG simulé. | Événement d'alarme provenant de l'émetteur. | Afficher la source, le patient, l'heure, la priorité d'origine et l'état de traitement. |
| 6 | Fin de surveillance et sortie. | Désassociation de l'émetteur. | Terminer la session et rendre l'appareil réutilisable selon son état. |

**Scénarios critiques :** mobilité, perte de couverture, batterie faible, mauvais appairage et confusion entre acquittement et résolution.

### Persona P04 — Patient qui se dégrade en unité conventionnelle

**Profil fictif :** adulte hospitalisé en médecine conventionnelle, initialement suivi par des mesures ponctuelles, puis transféré vers une unité de surveillance renforcée.

| Étape | Lieu et événement | Appareils / données simulés | Ce que le système doit gérer |
|---|---|---|---|
| 1 | Admission en unité conventionnelle. | Identité, lit et mesures ponctuelles. | Ne pas créer artificiellement un flux continu si le patient n'a pas de moniteur connecté. |
| 2 | Mesures périodiques. | Constantes horodatées, sans flux permanent. | Distinguer mesure ponctuelle, donnée absente et équipement hors ligne. |
| 3 | Dégradation simulée et décision d'escalade par les professionnels. | Nouveaux relevés et événement d'orientation. | Enregistrer le changement de niveau de surveillance sans prendre de décision médicale automatique. |
| 4 | Transfert vers USC ou réanimation. | Moniteur de transport puis moniteur de chevet. | Gérer la nouvelle association et la continuité de l'historique. |
| 5 | Retour éventuel en unité conventionnelle ou sortie. | Clôture ou changement de session. | Conserver la chronologie et clôturer proprement les équipements. |

**Scénarios critiques :** mesures espacées, donnée périmée, escalade, transfert et absence de faux sentiment de surveillance continue.

## 4. Événements à représenter dans tous les parcours

Le simulateur doit pouvoir produire une chronologie d'événements indépendante des personas :

- patient enregistré ;
- admission ou ouverture d'un séjour ;
- affectation à une unité, une chambre et un lit ;
- appareil associé ou désassocié ;
- session de surveillance démarrée ou terminée ;
- observation physiologique reçue ;
- état technique modifié ;
- alarme déclenchée, acquittée et résolue ;
- patient déplacé ou transféré ;
- séjour clôturé.

Chaque événement doit conserver son horodatage, son origine et son contexte patient / séjour / unité / lit / appareil lorsque ces informations sont disponibles.

## 5. Sources

- [H02] HAS — Flash Sécurité Patient, surveillance en soins critiques, 2024.
- [H03] Code de la santé publique — articles D6124-97 à D6124-103.
- [H100] MIMIC-IV ; [H101] MIMIC-IV-ED ; [H102] HiRID ; [H103] eICU ; [H104] AmsterdamUMCdb.
- [H108] SFAR — dossier anesthésique et surveillance post-interventionnelle.
- [H109] Ministère de la Santé — dossier patient, admission et parcours.


## 6. Parcours de référence tirés d'une base réelle

Les quatre personas de ce document restent des scénarios composites. Pour éviter de confondre un scénario pédagogique avec un parcours observé, les deux séquences suivantes sont issues de MIMIC-IV Demo 2.2. Les identifiants sont ceux du jeu de données anonymisé et les dates ont été décalées pour la confidentialité [H110].

### Trace réelle A — Urgences, soins intensifs, unité médico-chirurgicale, sortie

Séjour subject_id 10019568, hadm_id 28710730 :

| Segment réel enregistré | Début | Fin |
|---|---|---|
| Emergency Department | 2120-01-30 19:44 | 2120-01-30 22:51 |
| Trauma SICU | 2120-01-30 22:51 | 2120-01-31 18:25:12 |
| Med/Surg/Trauma | 2120-01-31 18:25:12 | 2120-02-02 15:40:32 |
| Discharge | 2120-02-02 15:40:32 | — |

Ce parcours permet de tester une succession réelle de segments de localisation. La chambre, le lit et les appareils exacts ne sont pas connus dans cette trace ; ils devront être générés dans notre maquette.

### Trace réelle B — Chirurgie cardiaque, CVICU, chirurgie cardiaque, sortie

Séjour subject_id 10005817, hadm_id 20626031 :

| Segment réel enregistré | Début | Fin |
|---|---|---|
| Cardiac Surgery | 2132-12-12 01:44:24 | 2132-12-15 09:29:01 |
| Cardiac Vascular Intensive Care Unit | 2132-12-15 09:29:01 | 2132-12-17 18:06:07 |
| Cardiac Surgery | 2132-12-17 18:06:07 | 2132-12-20 15:04:14 |
| Discharge | 2132-12-20 15:04:14 | — |

Les horaires proviennent des enregistrements MIMIC-IV Demo ; ce ne sont pas des dates de soins réelles à utiliser comme calendrier. Ces traces décrivent les mouvements enregistrés, pas la totalité des actions de soignants ou des alarmes.

Source de référence : [H110] MIMIC-IV Demo et [H111] documentation de la table transfers.
