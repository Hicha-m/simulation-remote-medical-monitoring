# 01 — Cahier de décisions et questions de cadrage

**Version :** 1.1 — **Date de mise à jour :** 25 novembre 2026  
**Objet :** guider les choix de conception de l'équipe et consigner les validations utiles.  
**Contexte confirmé :** système de monitorage hospitalier reliant des moniteurs de chevet à une ou plusieurs centrales de surveillance.

## Informations déjà confirmées

- Le tuteur laisse à l'équipe la liberté de définir le périmètre fonctionnel, l'architecture, les technologies, l'interface, le stockage et le déploiement. Aucune autre limite de conception n'a été communiquée à ce stade.
- **La partie programmation réseau doit être réalisée en Java.** Cette contrainte ne signifie pas que toute l'application doit être écrite en Java.
- Les choix restant dans ce document sont donc d'abord des décisions à prendre par Hicham, Omar et Nawfel. Ils peuvent ensuite être présentés au tuteur pour validation ou avis, sans lui demander de choisir à la place de l'équipe.

> Consigne d'utilisation : Hicham souhaite répondre lui-même aux questions de conception. Les champs « Réponse / décision de l'équipe » sont donc laissés vierges. Les questions cliniques ou réglementaires qui dépassent les connaissances de l'équipe devront être documentées et, si nécessaire, soumises à un professionnel compétent.

## Statut de ce cahier : baseline initiale évolutive

Ce cahier sert à établir une **première base de référence du projet** à partir des réponses initiales de Hicham, Omar et Nawfel. Cette baseline n'est pas un cahier des charges figé et ne bloque pas les évolutions.

- Une réponse peut commencer comme hypothèse, être retenue provisoirement, puis être confirmée par un test ou une source.
- Une décision peut être révisée si un essai, une contrainte découverte, un retour du tuteur ou une meilleure compréhension du besoin le justifie.
- Une évolution ne doit pas effacer silencieusement le choix précédent : noter l'ancienne valeur, la nouvelle, la raison, les preuves et les impacts sur le code, les données, le réseau, les tests et le planning.
- Les décisions structurantes et leurs changements sont consignés dans le [journal d'arbitrages](04-strategies-et-arbitrages-critiques.md).
- Le cahier reflète l'état courant ; le journal conserve l'historique.

Pour chaque réponse, utiliser si possible l'un de ces statuts : **Ouvert**, **Hypothèse**, **Décidé provisoirement**, **Vérifié**, **À réexaminer**, **Abandonné**. Une réponse « décidée » n'est pas forcément irréversible.

## 1. Périmètre hospitalier et services

### TUT-01 — Service de référence

**Question à trancher par l'équipe :**  
« Quel service doit constituer le premier périmètre clinique complet du système ? Merci de choisir un service précis, et pas simplement “l'hôpital”. »

**Choix :**
- [x] Réanimation adulte polyvalente
- [ ] Réanimation spécialisée (préciser : cardiaque, neuro, autre)
- [ ] Unité de surveillance continue (USC)
- [ ] Cardiologie avec télémétrie hospitalière
- [ ] Urgences / SAUV
- [ ] Bloc opératoire
- [ ] SSPI / salle de réveil
- [ ] Unité conventionnelle d'hospitalisation
- [ ] Pédiatrie
- [ ] Néonatologie
- [ ] Autre : ______________________________

**Réponse / décision de l'équipe :**

La réanimation adulte polyvalente est retenue comme service de référence initial. Elle permet de travailler sur un monitorage multiparamétrique continu, la gestion des alarmes et la surveillance simultanée de plusieurs patients.

Le développement initial portera sur des moniteurs multiparamétriques simulés, plusieurs patients et plusieurs lits. Le système devra recevoir les mesures, les associer correctement aux patients et aux équipements, les stocker, les afficher sur une station centrale et gérer les alarmes.

Ce choix définit le premier périmètre clinique, pas une limite à long terme. Une fois le socle fonctionnel, l'architecture devra permettre l'intégration progressive d'autres équipements, tels que des ventilateurs et des pompes à perfusion, et l'adaptation à d'autres services hospitaliers.

**Décision / précision :** service initial confirmé ; extensions matérielles et cliniques prévues comme évolutions, non exigées dans le premier périmètre.

### TUT-02 — Nombre de services à couvrir

**Question à trancher par l'équipe :**  
« Le système doit-il gérer un seul service, plusieurs services partageant une centrale, ou plusieurs services ayant chacun leur propre centrale ? Parmi les services ci-dessus, lesquels doivent réellement être fonctionnels dans la version livrée le 8 janvier 2027 ? »

**Choix :**
- [ ] Un seul service, avec une seule centrale
- [ ] Plusieurs services, une centrale par service
- [ ] Plusieurs services, une centrale principale commune
- [x] Plusieurs services avec centrales locales et supervision transversale
- [ ] Autre architecture : ______________________________

**Services obligatoires au premier périmètre fonctionnel :**  
1. Réanimation adulte polyvalente.

**Services facultatifs / extension :**  
USC, cardiologie avec télémétrie, urgences / SAUV et SSPI.

**Réponse / décision :**

Le système est conçu pour prendre en charge plusieurs services hospitaliers. Chaque service peut disposer de sa propre centrale locale, tandis qu'une infrastructure commune assure la supervision transversale. Le développement commencera par la réanimation adulte polyvalente ; les autres services seront intégrés progressivement.

La cible multi-services ne signifie pas que tous les services doivent être complètement développés dès la première version. La topologie technique exacte et le niveau d'indépendance des centrales restent à définir dans le System Design.

### TUT-03 — Population surveillée

« Quelle population le système doit-il prendre en charge dans son périmètre initial ? »

- [x] Adultes uniquement
- [ ] Adultes et pédiatrie
- [ ] Adultes, pédiatrie et néonatologie
- [ ] Autre : ____________________

**Les profils adultes/pédiatriques/néonataux doivent-ils être des profils distincts avec leurs propres paramètres et configurations ?**  
Réponse : Oui. Les profils adultes, pédiatriques et néonataux devront être distincts et configurables selon leurs paramètres, valeurs de référence et règles d'alarme. Le premier développement concernera uniquement les adultes ; l'architecture devra permettre l'ajout ultérieur des profils pédiatriques et néonataux sans remettre en cause le fonctionnement général.

Les valeurs de référence et seuils ne seront pas inventés : ils devront provenir de sources documentées ou d'une validation compétente. Pour le démonstrateur, tout profil synthétique sera explicitement identifié comme non clinique.

### TUT-04 — Mobilité des patients

« Les patients doivent-ils rester dans un lit fixe ou le système doit-il gérer aussi la télémétrie, les déplacements et le monitorage pendant les transports ? »

- [x] Patients fixes au lit uniquement
- [ ] Patients mobiles en télémétrie
- [ ] Transports entre services avec moniteur de transport
- [ ] Déplacements vers imagerie / bloc / examens
- [ ] Toutes ces situations
- [ ] Autre : ____________________

**Situations obligatoires :**

Surveillance continue de patients installés dans des lits identifiés, avec association explicite entre patient, séjour, service, lit, moniteur et session de surveillance. Le système doit aussi gérer les changements de lit, les déconnexions et reconnexions des équipements, tout en conservant l'historique des affectations et des mesures.

La télémétrie et le monitorage pendant les transports sont hors du premier périmètre.

### TUT-05 — Organisation des centrales

« Pour les services retenus, combien de centrales faut-il représenter et quelles vues un poste central doit-il avoir ? »

- [ ] Une vue limitée à son propre service
- [x] Vue multi-lits du service
- [x] Vue de plusieurs services
- [x] Transfert de surveillance entre centrales
- [ ] Terminal mobile / répétiteur
- [ ] Autre : ____________________

**Précisions / nombre de lits ou patients simultanés :**

Les centrales locales doivent afficher les différents lits et patients de leur service. Une supervision transversale doit pouvoir consulter plusieurs services. Le système doit conserver la continuité du suivi lors du transfert de surveillance d'un patient entre deux services / centrales.

Le nombre de lits et de patients simultanés reste à dimensionner.

**Réponse / décision :**

L'organisation cible comporte des centrales locales par service et une supervision transversale. Les centrales ne doivent pas être de simples écrans simulés indépendants : plusieurs composants doivent réellement communiquer à travers le réseau, distribuer les données aux centrales concernées et remonter les informations vers la supervision globale.

Cette exigence décrit le comportement logique attendu ; elle ne présume pas encore du choix monolithe, SOA ou microservices, ni du nombre de serveurs physiques. L'architecture et les frontières réseau restent à étudier.

**Scénario de validation réseau associé :**

1. Plusieurs moniteurs simulés envoient simultanément les mesures de leurs patients.
2. Les centrales locales reçoivent et affichent les données correspondant à leurs services.
3. La supervision transversale reçoit les informations des deux services simulés.
4. Une connexion réseau entre composants est interrompue ; l'incident et l'état dégradé deviennent visibles.
5. La connexion est rétablie ; les transmissions reprennent, l'interruption reste traçable dans l'historique et aucune mesure ne se retrouve attribuée au mauvais patient.

Ce scénario doit devenir un test d'intégration reproductible. Il reste à définir si le deuxième service est entièrement développé ou représenté par une centrale secondaire minimale dans la première version ; le périmètre clinique complet initial reste la réanimation adulte.

## 2. Fonctionnalités attendues — comportements du système

> Ici, « fonctionnalité » signifie une action ou un comportement que le logiciel doit offrir à ses utilisateurs. Cela ne désigne pas une technologie, un framework ou un langage.

Pour chaque ligne, demander : **obligatoire**, **souhaitée** ou **hors périmètre**, puis préciser les critères de réussite.

| ID | Fonctionnalité concrète à valider | Obligatoire / souhaitée / exclue | Précisions / justification de l'équipe |
|---|---|---|---|
| F-01 | Créer et clôturer un séjour patient | | |
| F-02 | Affecter un patient à un service, une chambre et un lit | | |
| F-03 | Associer/dissocier un moniteur à un patient et à une session de surveillance | | |
| F-04 | Gérer l'inventaire et l'état de connexion des moniteurs | | |
| F-05 | Recevoir automatiquement les mesures des moniteurs | | |
| F-06 | Afficher les valeurs numériques en temps réel | | |
| F-07 | Afficher les courbes ECG, PPG, pression, respiration ou CO₂ | | |
| F-08 | Afficher les tendances et l'historique d'un patient | | |
| F-09 | Détecter et afficher les alarmes physiologiques | | |
| F-10 | Détecter et afficher les alarmes techniques des appareils | | |
| F-11 | Reporter une alarme vers une centrale et/ou un terminal | | |
| F-12 | Acquitter une alarme sans la clôturer automatiquement | | |
| F-13 | Gérer le silence temporaire, la pause et la réactivation d'une alarme | | |
| F-14 | Escalader une alarme non prise en compte | | |
| F-15 | Gérer les affectations des soignants et la relève | | |
| F-16 | Transférer un patient et sa surveillance entre services | | |
| F-17 | Gérer les états dégradés : capteur, moniteur, réseau, centrale, serveur | | |
| F-18 | Conserver l'historique et les traces d'audit | | |
| F-19 | Gérer les comptes, rôles et droits utilisateurs | | |
| F-20 | Rejouer un scénario médical ou une trace de données | | |
| F-21 | Exporter un historique ou un rapport | | |
| F-22 | Administrer les profils de paramètres, alarmes et appareils | | |

**Les trois fonctionnalités considérées comme les plus importantes :**  
1. ____________________  2. ____________________  3. ____________________

**Fonctionnalités exclues du périmètre actuel :**

- Connexion à de véritables dispositifs médicaux hospitaliers : seuls des équipements simulés seront utilisés.
- Utilisation de données personnelles réelles de patients : privilégier des données synthétiques ou des données de recherche dé-identifiées, dans le respect de leurs conditions d'accès et de réutilisation.
- Prescription de traitements ou génération d'ordres médicaux réels.
- Prise de décision médicale autonome ou diagnostic.
- Intégration à un véritable SIH ou à un dossier patient informatisé.
- Envoi de véritables alertes à des soignants ou à des services d'urgence.

L'IA prédictive n'est pas exclue comme perspective expérimentale future, mais elle ne doit pas être une dépendance de l'architecture ni une condition de fonctionnement du système de monitorage.

### TUT-06 — Actions utilisateur par rôle

« Quels rôles doivent exister et quelles actions chaque rôle peut-il effectuer ? »

| Rôle | Visualiser | Acquitter | Modifier profil/limites | Affecter appareil/lit | Administrer comptes |
|---|---|---|---|---|---|
| Infirmier/ère | ✓ | ✓ | — | ✓ | — |
| Médecin | ✓ | ✓ | ✓ | ✓ | — |
| Personnel de centrale | ✓ | ✓ | Selon droits | ✓ | — |
| Biomédical | Limité | — | — | ✓ | — |
| Administrateur technique | ✓ | ✓ | ✓ | ✓ | ✓ |
| Autre : | | | | | |

**Réponse / règles d'autorisation :**

Première proposition de rôles :
- **Infirmier / infirmière :** surveillance quotidienne des patients et gestion des alarmes.
- **Médecin :** consultation des données et historiques ; modification des profils et limites selon les habilitations qui seront définies.
- **Personnel de centrale :** surveillance simultanée des lits et coordination des alarmes du service.
- **Biomédical :** inventaire, état, diagnostic et maintenance des équipements ; accès limité aux informations patient.
- **Administrateur technique :** gestion des comptes, droits et configuration technique.

**À préciser avant implémentation :** séparer les permissions techniques et médicales. En particulier, les droits d'administration technique ne doivent pas donner automatiquement accès à la modification des seuils cliniques ou à l'acquittement des alarmes. Les droits d'affectation d'un moniteur, d'un patient et d'un lit devront également être définis précisément. Les actions sensibles devront être journalisées. La matrice ci-dessus est une première proposition, à affiner.

## 3. Réalisme médical, paramètres et données

### TUT-07 — Paramètres physiologiques obligatoires

« Quels paramètres doivent obligatoirement être présents pour chaque moniteur de chevet ? »

- [ ] ECG / fréquence cardiaque
- [ ] SpO₂ / pléthysmogramme / pouls
- [ ] PANI : systolique, diastolique, moyenne
- [ ] PAI : courbe et valeurs
- [ ] Fréquence respiratoire / courbe respiratoire
- [ ] Température
- [ ] EtCO₂ / capnogramme
- [ ] Autre : ____________________

**Paramètres obligatoires par service :**  
............................................................................

### TUT-08 — Courbes et signaux bruts

« Faut-il afficher uniquement des nombres, des courbes en direct, ou aussi permettre de rejouer et d'analyser les signaux physiologiques bruts ? Quelles courbes doivent être incluses dans la version livrée ? »

- [ ] Valeurs numériques uniquement
- [ ] ECG
- [ ] PPG / pléthysmogramme
- [ ] Pression artérielle invasive
- [ ] Respiration
- [ ] Capnographie
- [ ] Courbes ventilateur
- [ ] Rejeu de données enregistrées
- [ ] Export des signaux bruts

**Résolution/fréquence exigée ou source à utiliser :**  
............................................................................

### TUT-09 — Origine des données médicales

« Quelle méthode d'alimentation des moniteurs est attendue ? »

- [ ] Génération entièrement synthétique
- [ ] Rejeu de données publiques réelles dé-identifiées
- [ ] Données publiques + scénarios synthétiques d'artefacts et de pannes
- [ ] Données fournies par le tuteur / établissement
- [ ] Autre : ____________________

**Bases acceptées (MIMIC, VitalDB, PhysioNet, Barcelona SICU, autre) :**  
............................................................................

**Contraintes d'accès, citation, licence et redistribution :**  
............................................................................

### TUT-10 — Qualité de la mesure

« Devons-nous simuler des mesures imparfaites et leur qualité : électrode décollée, mouvement, PPG faible, brassard échoué, valeur périmée, perte de signal ? Quelles situations doivent être démontrées ? »

Réponse : ....................................................................

### TUT-11 — Seuils et profils d'alarme

« Les limites d'alarme doivent-elles provenir d'un profil documenté, être configurables par patient ou être fournies par un professionnel ? Qui validera les profils et les exemples ? »

- [ ] Seuils fournis par le tuteur
- [ ] Profils issus de documentation publique identifiée
- [ ] Paramétrage fictif explicitement non clinique
- [ ] Validation par un professionnel de santé
- [ ] Autre : ____________________

**Réponse / source de référence :**  
............................................................................

## 4. Workflow des alarmes et pratiques métier

### TUT-12 — Circuit de réception d'une alarme

« Pour le service retenu, qui doit recevoir chaque type d'alarme : moniteur local, centrale, infirmier affecté, terminal mobile, médecin ou autre destinataire ? »

**Réponse par catégorie (physiologique, technique, réseau) :**  
............................................................................

### TUT-13 — Acquittement et escalade

« Quel comportement exact attendez-vous lorsqu'une alarme n'est pas acquittée ? Faut-il un délai d'escalade configurable, un deuxième destinataire, une relance, ou seulement une alarme visible persistante ? »

**Règle attendue :**  
............................................................................

**Délai ou méthode de validation :**  
............................................................................

### TUT-14 — Relève et transfert

« Faut-il gérer la transmission des alarmes encore ouvertes lors d'une relève, ainsi que le transfert d'un patient entre deux centrales sans perdre son historique ? »

- [ ] Oui, relève des alarmes ouvertes
- [ ] Oui, transfert inter-service
- [ ] Oui, passage moniteur fixe ↔ moniteur transport
- [ ] Non
- [ ] Autre : ____________________

**Précisions :** ....................................................................

## 5. Informations patient et données personnelles

### TUT-15 — Contexte patient nécessaire

« Quelles informations patient sont nécessaires à la supervision : identité de démonstration, âge/profil, séjour, unité, lit, contexte d'admission, antécédents ou traitements ? Quelles informations sont explicitement hors sujet ? »

**Champs obligatoires :** ........................................................

**Champs exclus :** .............................................................

### TUT-16 — Données réelles / INS / DPI

« Le système doit-il simplement utiliser des identités fictives, simuler les échanges administratifs, ou prévoir une interopérabilité avec un DPI ? L'INS est-elle à étudier comme référence conceptuelle ou à implémenter ? »

- [ ] Identités fictives seulement
- [ ] Simulation d'un flux ADT
- [ ] Modèle compatible conceptuellement INS / RNIV
- [ ] Interface de test avec système externe autorisé
- [ ] Autre : ____________________

**Réponse / limites :** ..........................................................

## 6. Contraintes techniques — technologies séparées des fonctionnalités

### TUT-17 — Périmètre de la programmation réseau Java

**Contrainte confirmée : la programmation réseau doit être réalisée en Java.** L'équipe doit maintenant préciser dans son architecture quels composants portent cette responsabilité et où se trouvent les frontières entre réseau, métier et interface.

**Questions à trancher :**
- Quel composant Java ouvre et gère les connexions réseau ?
- Le client simulateur, le serveur, ou les deux doivent-ils contenir le code réseau évalué ?
- Comment les composants non Java communiqueront-ils avec ce composant Java ?
- Quelle version de Java et quelle bibliothèque réseau utiliser ?

**Périmètre Java retenu :**  
............................................................................

**Version et bibliothèques envisagées :**  
............................................................................

**Réponse / décision de l'équipe :**  
............................................................................

### TUT-18 — Technologies libres pour les autres composants

En dehors de la programmation réseau qui doit être réalisée en Java, les technologies sont libres. Quelles technologies l'équipe souhaite-t-elle évaluer pour le backend métier, les simulateurs, l'interface, les traitements de signaux et les outils ?

- [ ] Kotlin/JVM — proche de l'écosystème Java, backend ou clients JVM
- [ ] C# / .NET — serveur et applications desktop/web
- [ ] Python — simulation, acquisition/rejeu, API ou traitements
- [ ] TypeScript / Node.js — serveur événementiel et interface web
- [ ] C++ — acquisition/traitement de signaux à forte contrainte
- [ ] JavaScript/TypeScript côté interface seulement
- [ ] Mélange de langages autorisé
- [ ] Aucune alternative, Java uniquement

**Restrictions et justification :**  
............................................................................

### TUT-19 — Type d'interface

« Quelle forme d'application faut-il livrer ? »

- [ ] Desktop JavaFX
- [ ] Desktop Swing
- [ ] Application web (navigateur)
- [ ] Backend Java + interface React/TypeScript
- [ ] Backend Java + autre framework : ____________________
- [ ] Application hybride
- [ ] Libre

**Systèmes d'exploitation et navigateurs cibles :**  
............................................................................

### TUT-20 — Conception des communications réseau (implémentation Java)

La programmation réseau doit être réalisée en Java, mais le protocole applicatif reste à choisir par l'équipe. Il faut distinguer le langage d'implémentation (Java) du protocole de communication (TCP, WebSocket, MQTT, etc.).

- [ ] TCP avec protocole applicatif défini par l'équipe
- [ ] WebSocket
- [ ] MQTT
- [ ] gRPC
- [ ] HTTP/REST pour gestion + protocole temps réel séparé
- [ ] HL7 / IHE / IEEE 11073 à implémenter
- [ ] Standards à étudier mais pas nécessairement à implémenter
- [ ] Libre

**Charge que l'équipe décide de viser (moniteurs, paramètres, messages/s, latence, clients simultanés) et justification :**  
............................................................................

### TUT-21 — Base de données et stockage

« Quel stockage est imposé ou accepté pour les patients, mesures numériques, alarmes, journaux et courbes brutes ? »

- [ ] PostgreSQL / autre SQL
- [ ] SQLite
- [ ] MongoDB / document
- [ ] InfluxDB / base temporelle
- [ ] PostgreSQL + extension temporelle
- [ ] Fichiers de signaux + base de métadonnées
- [ ] Architecture hybride
- [ ] Libre

**Volume ou durée d'historique attendus :**  
............................................................................

### TUT-22 — Déploiement et infrastructure

« Où l'application doit-elle fonctionner et comment doit-elle être installée ? »

- [ ] Un ordinateur unique
- [ ] Plusieurs ordinateurs sur un LAN
- [ ] Machines virtuelles / Docker
- [ ] Serveur central + clients répartis
- [ ] Démonstration sur réseau isolé
- [ ] Autre : ____________________

**Contraintes matérielles et réseau :**  
............................................................................

### TUT-23 — Sécurité obligatoire

« Quelles protections doivent être réellement implémentées et démontrées ? »

- [ ] Authentification des utilisateurs
- [ ] Rôles et habilitations
- [ ] Authentification des moniteurs
- [ ] TLS/chiffrement en transit
- [ ] Gestion des secrets
- [ ] Journal d'audit
- [ ] Sauvegarde et restauration
- [ ] Révocation d'un appareil/compte
- [ ] Tests d'accès non autorisé
- [ ] Autre : ____________________

**Exigences et critères :**  
............................................................................

## 7. Charge, qualité, livrables et évaluation

### TUT-24 — Charge de référence

« Quelle charge devons-nous démontrer : combien de lits, patients, moniteurs, paramètres par moniteur, utilisateurs et alarmes simultanées ? »

**Patients :** ______  **Moniteurs :** ______  **Utilisateurs :** ______

**Cadence / débit :** ____________________  
**Durée de test :** ____________________

### TUT-25 — Performances attendues

« Quels délais et taux d'erreur acceptez-vous pour l'affichage d'une mesure et d'une alarme ? Souhaitez-vous une mesure de latence médiane, p95, p99, débit, pertes et reprise après coupure ? »

Réponse : ....................................................................

### TUT-26 — Livrables du 8 janvier 2027 et soutenance

« Quels éléments exacts seront évalués et dans quel format ? Une soutenance est-elle prévue à une date distincte de la livraison ? Quelles sont sa durée, ses règles de participation et les modalités du rapport ? »

**Préparation interne en attendant les consignes :** l'équipe prévoit un rapport technique structuré, un support oral et une démonstration reproductible. Ce sont des hypothèses de préparation, pas des modalités confirmées.

- [ ] Application exécutable
- [ ] Dépôt source complet
- [ ] Documentation utilisateur
- [ ] Documentation technique / architecture
- [ ] Modèle de données / SQL
- [ ] Diagrammes UML
- [ ] Plan de test et résultats
- [ ] Rapport final
- [ ] Présentation orale
- [ ] Démonstration en direct
- [ ] Vidéo de démonstration
- [ ] Autre : ____________________

**Heure limite / format de remise / lieu :**  
............................................................................

### TUT-27 — Barème et priorités

« Comment les points sont-ils répartis entre fonctionnalités, réalisme médical, réseau, sécurité, base de données, interface, qualité du code, tests et documentation ? »

| Critère | Coefficient / importance | Commentaire |
|---|---|---|
| Fonctionnalités métier | | |
| Réalisme médical | | |
| Communication réseau / temps réel | | |
| Interface utilisateur | | |
| Base de données / historique | | |
| Cybersécurité | | |
| Tests et robustesse | | |
| Architecture / qualité du code | | |
| Documentation / présentation | | |

### TUT-28 — Validation intermédiaire et ressources

« À quelles dates pouvez-vous examiner nos livrables intermédiaires ? Pouvez-vous nous orienter vers un professionnel de santé, un biomédical, une équipe de réanimation ou des documents de fonctionnement du service ? »

**Dates de validation :**  
1. ____________________  2. ____________________  3. ____________________

**Personnes / ressources proposées :**  
............................................................................

## 8. Synthèse à remplir après la réunion

| Décision | Réponse retenue | Validée par | Date |
|---|---|---|---|
| Service de référence | | | |
| Services supplémentaires | | | |
| Population | | | |
| Fonctionnalités obligatoires | | | |
| Paramètres et courbes | | | |
| Sources de données | | | |
| Workflow d'alarmes | | | |
| Langage / rôle de Java | | | |
| Interface | | | |
| Réseau / protocoles | | | |
| Stockage | | | |
| Sécurité | | | |
| Charge cible | | | |
| Livrables / barème | | | |
