# 01 — Questionnaire précis pour le tuteur

**Version :** 1.0 — **Date de préparation :** 18 novembre 2026  
**Objet :** obtenir les décisions et contraintes qui déterminent le périmètre du projet.  
**Contexte confirmé :** système de monitorage hospitalier reliant des moniteurs de chevet à une ou plusieurs centrales de surveillance.

> Consigne d'utilisation : remplir les zones « Réponse du tuteur » pendant ou juste après la réunion. Une question non traitée reste marquée « À confirmer ». Ne pas remplacer une réponse du tuteur par une supposition de l'équipe.

## 1. Périmètre hospitalier et services

### TUT-01 — Service de référence

**Question à poser :**  
« Quel service doit constituer le premier périmètre clinique complet du système ? Merci de choisir un service précis, et pas simplement “l'hôpital”. »

**Choix :**
- [ ] Réanimation adulte polyvalente
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

**Réponse du tuteur :**  
............................................................................

**Décision / précision :**  
............................................................................

### TUT-02 — Nombre de services à couvrir

**Question à poser :**  
« Le système doit-il gérer un seul service, plusieurs services partageant une centrale, ou plusieurs services ayant chacun leur propre centrale ? Parmi les services ci-dessus, lesquels doivent réellement être fonctionnels dans la version livrée le 8 janvier 2027 ? »

**Choix :**
- [ ] Un seul service, avec une seule centrale
- [ ] Plusieurs services, une centrale par service
- [ ] Plusieurs services, une centrale principale commune
- [ ] Plusieurs services avec centrales locales et supervision transversale
- [ ] Autre architecture : ______________________________

**Services obligatoires au rendu :**  
1. ____________________  2. ____________________  3. ____________________

**Services facultatifs / extension :**  
............................................................................

**Réponse / décision :**  
............................................................................

### TUT-03 — Population surveillée

« Quelle population le système doit-il prendre en charge dans son périmètre initial ? »

- [ ] Adultes uniquement
- [ ] Adultes et pédiatrie
- [ ] Adultes, pédiatrie et néonatologie
- [ ] Autre : ____________________

**Les profils adultes/pédiatriques/néonataux doivent-ils être des profils distincts avec leurs propres paramètres et configurations ?**  
Réponse : ....................................................................

### TUT-04 — Mobilité des patients

« Les patients doivent-ils rester dans un lit fixe ou le système doit-il gérer aussi la télémétrie, les déplacements et le monitorage pendant les transports ? »

- [ ] Patients fixes au lit uniquement
- [ ] Patients mobiles en télémétrie
- [ ] Transports entre services avec moniteur de transport
- [ ] Déplacements vers imagerie / bloc / examens
- [ ] Toutes ces situations
- [ ] Autre : ____________________

**Situations obligatoires :** ...................................................

### TUT-05 — Organisation des centrales

« Pour les services retenus, combien de centrales faut-il représenter et quelles vues un poste central doit-il avoir ? »

- [ ] Une vue limitée à son propre service
- [ ] Vue multi-lits du service
- [ ] Vue de plusieurs services
- [ ] Transfert de surveillance entre centrales
- [ ] Terminal mobile / répétiteur
- [ ] Autre : ____________________

**Précisions / nombre de lits ou patients simultanés :**  
............................................................................

## 2. Fonctionnalités attendues — comportements du système

> Ici, « fonctionnalité » signifie une action ou un comportement que le logiciel doit offrir à ses utilisateurs. Cela ne désigne pas une technologie, un framework ou un langage.

Pour chaque ligne, demander : **obligatoire**, **souhaitée** ou **hors périmètre**, puis préciser les critères de réussite.

| ID | Fonctionnalité concrète à valider | Obligatoire / souhaitée / exclue | Précisions du tuteur |
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

**Fonctionnalités interdites ou à ne surtout pas développer :**  
............................................................................

### TUT-06 — Actions utilisateur par rôle

« Quels rôles doivent exister et quelles actions chaque rôle peut-il effectuer ? »

| Rôle | Visualiser | Acquitter | Modifier profil/limites | Affecter appareil/lit | Administrer comptes |
|---|---|---|---|---|---|
| Infirmier/ère | | | | | |
| Médecin | | | | | |
| Personnel de centrale | | | | | |
| Biomédical | | | | | |
| Administrateur technique | | | | | |
| Autre : | | | | | |

**Réponse / règles d'autorisation :**  
............................................................................

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

### TUT-17 — Langage principal et rôle de Java

« Java est-il une obligation académique ou une technologie suggérée ? Si Java est obligatoire, doit-il être utilisé pour le serveur uniquement, les simulateurs de moniteurs, l'interface ou tous les composants ? »

- [ ] Java obligatoire pour tous les composants
- [ ] Java obligatoire pour le backend uniquement
- [ ] Java obligatoire pour les clients simulateurs uniquement
- [ ] Java fortement recommandé mais alternatives autorisées
- [ ] Langage libre
- [ ] Autre : ____________________

**Version Java imposée :** ____________________

**Frameworks imposés/interdits :** ____________________

**Réponse du tuteur :**  
............................................................................

### TUT-18 — Alternatives autorisées à Java

« Si le langage n'est pas imposé, quelles alternatives sont acceptées et sur quels composants ? »

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

### TUT-20 — Communication entre moniteurs et serveur

« Quel niveau de communication réseau attendez-vous et avez-vous un protocole imposé ? »

- [ ] TCP avec protocole applicatif défini par l'équipe
- [ ] WebSocket
- [ ] MQTT
- [ ] gRPC
- [ ] HTTP/REST pour gestion + protocole temps réel séparé
- [ ] HL7 / IHE / IEEE 11073 à implémenter
- [ ] Standards à étudier mais pas nécessairement à implémenter
- [ ] Libre

**Débit, latence, nombre de moniteurs et clients simultanés attendus :**  
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

### TUT-26 — Livrables du 8 janvier 2027

« Quels éléments exacts seront évalués et dans quel format ? »

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
