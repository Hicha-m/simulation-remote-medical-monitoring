# DEV — Développement du système de monitorage hospitalier

**Périmètre :** étapes 1 à 6.  
**Objectif :** livrer une application fonctionnelle en environnement local avant sa conteneurisation.  
**Échéance générale du projet :** 8 janvier 2027.

## Mode de lecture

Suivre les étapes dans l'ordre des dépendances. Chaque étape possède un objectif, un travail à faire, des vérifications et des livrables. Les décisions médicales doivent venir de sources documentées ou être validées par un professionnel compétent. Une donnée synthétique ne devient jamais un seuil clinique ou un protocole médical.

La programmation réseau doit être réalisée en Java : c'est la contrainte technique confirmée par le tuteur. Cela ne rend pas Java obligatoire pour toute l'application. L'équipe choisira explicitement quels composants portent le code réseau Java (serveur, clients simulateurs, passerelle ou combinaison), puis définira les contrats permettant aux autres composants, éventuellement développés dans d'autres langages, de communiquer avec eux. Les autres choix technologiques sont libres.

## 1. Contexte et objectif

Le système représente un environnement hospitalier où des moniteurs de chevet surveillent des patients et transmettent des observations, des signaux et des alarmes à une ou plusieurs centrales de surveillance.

L'application doit permettre de comprendre :
- quel patient est surveillé ;
- dans quel séjour, service, chambre et lit ;
- par quel moniteur et quelle session ;
- quelles mesures numériques et courbes sont reçues ;
- à quelle heure les données ont été mesurées et reçues ;
- quelle est leur qualité technique et leur fraîcheur ;
- quelles alarmes sont actives, signalées, acquittées ou résolues ;
- quels événements de transfert, déconnexion ou reprise ont eu lieu.

Le périmètre des services, paramètres, utilisateurs et fonctionnalités est défini par l'équipe, qui dispose de liberté de choix. La réanimation adulte polyvalente est retenue comme premier périmètre fonctionnel. La cible du système est multi-services, avec centrales locales et supervision transversale ; les autres services seront intégrés progressivement.

## 2. Architecture logique à réaliser

La séparation des responsabilités doit rester explicite, même si plusieurs composants sont déployés dans un seul processus au départ.

| Couche logique | Responsabilité |
|---|---|
| Simulateurs / adaptateurs de moniteurs | Produire ou rejouer les signaux et valeurs, simuler les états des appareils, envoyer les événements. |
| Ingestion et communication | Authentifier la source, recevoir les messages, vérifier format, séquence, horodatage et provenance. |
| Métier / domaine | Gérer les patients, séjours, affectations, sessions, alarmes, qualité et règles de workflow. |
| Persistance | Conserver patients fictifs, affectations, observations, waveforms, alarmes, audits et configurations. |
| Présentation — centrales locales et supervision transversale | Afficher les patients, lits, appareils, valeurs, courbes, tendances, états techniques et alarmes du périmètre autorisé ; agréger les informations de plusieurs services pour la supervision transversale. |
| Administration | Gérer utilisateurs, rôles, profils, appareils, services et paramètres autorisés. |

Le découpage physique en processus, services ou modules sera choisi après le cadrage. Ne pas créer de microservices uniquement pour reproduire un schéma : il faut justifier chaque séparation par un besoin mesurable ou une frontière métier.

## 3. Scénario de bout en bout de référence

Le parcours principal à faire fonctionner doit couvrir :

1. création ou chargement d'un patient fictif et d'un séjour ;
2. affectation du patient à un service, une chambre et un lit ;
3. association d'un moniteur virtuel au patient et à une session ;
4. émission d'une ou plusieurs observations et, si retenu, de segments de courbe ;
5. réception, validation, horodatage et persistance des données ;
6. affichage dans la centrale locale du service et, si le périmètre multi-centrales est intégré à l'itération, remontée contrôlée vers la supervision transversale ;
7. émission d'une alarme ou d'un défaut technique de simulation ;
8. réception de l'alarme, affichage, prise de connaissance et résolution ;
9. transfert ou clôture de la session ;
10. consultation de l'historique après redémarrage.

Le scénario doit être déterministe et rejouable : même source, même version, même paramètres, même chronologie logique.

## 4. Règles métier et données à préserver

Les entités métier au minimum à considérer sont :
- Patient et identité de démonstration ;
- Séjour ;
- Mouvement / localisation ;
- Service, chambre et lit ;
- Moniteur, canal et capteur ;
- Affectation appareil-patient ;
- Session de monitorage ;
- Observation numérique ;
- Segment de waveform ;
- Indicateur de qualité ;
- Alarme et événements de son cycle de vie ;
- Utilisateur, rôle et affectation d'équipe ;
- Configuration et journal d'audit.

Règles non négociables proposées :
- aucune donnée ne doit être rattachée à un patient uniquement par un paramètre fourni par un client non authentifié ;
- toute observation doit avoir une source et une session ou être mise en quarantaine ;
- observation time, received time et stored time restent distincts ;
- une donnée absente n'est jamais convertie en zéro ;
- une mesure plus ancienne ne remplace pas silencieusement une mesure plus récente ;
- les doublons sont identifiables ;
- une donnée périmée reste consultable mais doit être marquée comme telle ;
- l'acquittement d'une alarme ne vaut pas résolution ;
- les changements d'affectation, de configuration et les actions sensibles sont historisés ;
- les données de recherche et événements synthétiques conservent une provenance distincte.

## 5. Déroulement du développement

### Étape 1 — Analyse fonctionnelle et règles métier

**Objectif :** transformer les ressources médicales en exigences testables et comprendre qui fait quoi.

**Travail à faire :**
1. figer les services concernés et les populations ;
2. lister les acteurs : personnel au chevet, poste central, médecin, biomédical, administrateur ;
3. décrire les parcours admission, association moniteur, surveillance, alarme, relève, transfert et sortie ;
4. rédiger les cas d'utilisation avec acteur, déclencheur, déroulement nominal, préconditions, erreurs et résultat attendu ;
5. construire la matrice des droits par rôle ;
6. identifier les cas d'erreur : patient inconnu, appareil inconnu, mauvaise association, signal absent, retard, doublon, alarme non acquittée, centrale indisponible, utilisateur non habilité ;
7. transformer les besoins prioritaires en critères d'acceptation.

**Vérifications :**
- chaque fonctionnalité obligatoire a un acteur et un scénario ;
- chaque scénario a au moins un cas d'erreur ;
- les règles médicales et les règles logicielles sont séparées ;
- les seuils et profils cliniques possèdent une source ou sont explicitement fictifs/non cliniques.

**Livrables :**
- cahier des exigences fonctionnelles ;
- catalogue des acteurs et cas d'utilisation ;
- matrice de droits ;
- règles métier versionnées ;
- matrice de traçabilité exigences → tests.

**Jalon :** décision documentée du périmètre par l'équipe ; présentation au tuteur pour retour si utile.

### Étape 2 — Prototype d'interface et parcours

**Objectif :** valider les écrans, les interactions et la hiérarchie des informations avant de stabiliser l'interface applicative.

**Écrans candidats :**
1. connexion et sélection du contexte de démonstration ;
2. vue centrale multi-patients / multi-lits ;
3. vue détaillée d'un patient ;
4. vue courbes et tendances ;
5. tableau de bord des alarmes ;
6. détail et historique d'une alarme ;
7. affectation patient / lit / moniteur ;
8. transfert et clôture de session ;
9. administration des utilisateurs, appareils et profils ;
10. état système et incidents de communication.

Tous les écrans ne sont pas nécessairement obligatoires : ils dépendent des fonctionnalités validées.

**États à maquettiser :**
- fonctionnement nominal ;
- valeur absente ou périmée ;
- signal de qualité dégradée ;
- moniteur hors ligne ;
- perte de centrale ou de réseau ;
- alarme active non acquittée ;
- alarme acquittée mais encore active ;
- aucune donnée disponible ;
- accès refusé.

**Points de vigilance :**
- ne pas coder uniquement la couleur pour représenter un état ;
- identifier le patient, le lit et le moniteur sans ambiguïté ;
- distinguer valeur physiologique, qualité technique et état de communication ;
- afficher clairement l'heure de la dernière mesure ;
- ne pas masquer une alarme active par un acquittement ;
- ne pas présenter une donnée périmée comme actuelle.

**Vérifications :**
- parcours cliquables entre les vues ;
- cas d'erreur accessibles ;
- cohérence entre chaque fonctionnalité et son élément d'interface ;
- revue par les trois membres et validation du tuteur.

**Livrables :**
- maquettes ou prototype interactif ;
- carte de navigation ;
- inventaire des composants ;
- décisions d'ergonomie et états dégradés.

**Jalon :** validation du parcours utilisateur avant le gel de l'interface.

### Étape 3 — Couche données et modèle de domaine

**Objectif :** construire un modèle persistant qui garantit l'intégrité des patients, appareils, sessions, observations et alarmes.

**Travail à faire :**
1. créer le modèle conceptuel et le schéma de persistance ;
2. définir les clés, contraintes, relations et index ;
3. séparer valeurs numériques, échantillons de waveform, alarmes, état technique et audit ;
4. définir les unités, codes de paramètre et provenance ;
5. conserver les horodatages source, réception et stockage ;
6. définir les migrations versionnées ;
7. fournir des données synthétiques et un adaptateur de rejeu des datasets autorisés ;
8. écrire les requêtes de consultation : dernière valeur, historique, données par patient, session, appareil et période ;
9. définir la durée et la stratégie de conservation des signaux bruts en fonction du volume mesuré.

**Vérifications :**
- intégrité référentielle ;
- absence de rattachement patient/appareil ambigu ;
- unicité des identifiants de message ;
- données manquantes distinctes de zéro ;
- migration depuis une base vide et depuis une version précédente ;
- sauvegarde et restauration de test ;
- tests de volumétrie sur un échantillon représentatif.

**Livrables :**
- schéma et migrations ;
- dictionnaire de données ;
- scripts de peuplement ;
- jeux de données et manifeste de provenance ;
- requêtes de vérification ;
- rapport de test d'intégrité.

### Étape 4 — Couche métier, ingestion et simulateurs

**Objectif :** recevoir et traiter les données de moniteurs avec un comportement fiable et explicable.

**Travail à faire :**
1. définir le contrat de message appareil → système ;
2. développer le ou les clients simulateurs de moniteur ;
3. développer un adaptateur de rejeu pour les formats de données sélectionnés ;
4. contrôler les identités appareil, patient, séjour et session ;
5. gérer les numéros de séquence, horodatages, déduplication et messages tardifs ;
6. gérer les valeurs numériques et les paquets waveform selon des chemins adaptés ;
7. gérer les états de qualité, capteur absent, signal dégradé et appareil silencieux ;
8. implémenter les événements d'alarme et le cycle métier ;
9. exposer les API ou flux nécessaires à la centrale ;
10. externaliser toute configuration et les secrets.

**Scénarios techniques à vérifier :**
- appareil inconnu ;
- session clôturée ;
- message trop ancien ;
- message dupliqué ;
- perte de paquets ;
- ordre de réception différent de l'ordre source ;
- perte puis reprise réseau ;
- surcharge temporaire ;
- panne de base ;
- redémarrage du serveur.

**Vérifications :**
- tests unitaires des règles ;
- tests de contrat des messages ;
- tests d'ingestion avec plusieurs clients simultanés ;
- aucune observation ambiguë affichée sur un patient ;
- chaque rejet/quarantaine est explicable ;
- la source d'une alarme reste identifiable.

**Livrables :**
- code des services métier ;
- simulateurs et adaptateurs de données ;
- contrat versionné des messages ;
- spécification API ;
- tests unitaires et d'intégration.

### Étape 5 — Couche présentation : centrale de surveillance

**Objectif :** raccorder l'interface aux services métier et permettre de suivre plusieurs patients de façon claire.

**Travail à faire :**
1. implémenter les écrans validés ;
2. afficher les dernières valeurs et leur fraîcheur ;
3. afficher les courbes avec leur échelle, unité et horodatage ;
4. distinguer les alarmes physiologiques, techniques et de communication ;
5. présenter les alarmes actives, acquittées, escaladées et résolues ;
6. afficher le patient, son lit, son moniteur et sa session ;
7. gérer les états de chargement, erreur et reconnexion ;
8. appliquer les droits d'accès côté serveur, sans se reposer sur l'affichage conditionnel de l'interface ;
9. rendre visible l'état dégradé de chaque composant.

**Vérifications :**
- aucune connexion directe entre le navigateur et la base de données ;
- contrôle d'autorisation côté serveur ;
- mise à jour de l'écran sans mélange entre patients ;
- rendu de données anciennes avec leur heure et leur état ;
- affichage des alarmes sans disparition lors d'un acquittement ;
- comportement compréhensible lorsque le flux est interrompu.

**Livrables :**
- code de la centrale ;
- documentation des vues ;
- captures ou vidéo des parcours ;
- tests d'interface et d'autorisation.

### Étape 6 — Intégration et recette

**Objectif :** prouver que la solution complète fonctionne sur des scénarios reproductibles.

**Travail à faire :**
- exécuter les parcours nominaux sur une base initialisée ;
- tester au moins deux patients et deux moniteurs simultanés ;
- faire un transfert pendant une surveillance active ;
- injecter des alarmes et défauts de capteurs ;
- couper puis rétablir le réseau ;
- redémarrer les composants ;
- tester les droits et l'audit ;
- vérifier l'historique des observations et alarmes ;
- rédiger la procédure d'installation locale.

**Matrice de recette :**

| ID | Scénario | Résultat attendu | Résultat obtenu | Statut |
|---|---|---|---|---|
| DEV-01 | Deux moniteurs transmettent simultanément | Données liées aux bons patients | À renseigner | |
| DEV-02 | Appareil inconnu | Message refusé ou mis en quarantaine | À renseigner | |
| DEV-03 | Mesure tardive | Historique conservé, dernière valeur non régressée | À renseigner | |
| DEV-04 | Capteur déconnecté | État technique distinct d'une alarme physiologique | À renseigner | |
| DEV-05 | Alarme acquittée encore active | Alarme toujours visible comme active | À renseigner | |
| DEV-06 | Transfert patient | Nouvelle affectation historisée, pas de mélange | À renseigner | |
| DEV-07 | Perte réseau | Flux marqué indisponible, reprise contrôlée | À renseigner | |
| DEV-08 | Redémarrage serveur | Données persistées retrouvées | À renseigner | |
| DEV-09 | Accès non autorisé | Action refusée côté serveur et journalisée | À renseigner | |
| DEV-10 | Rejeu identique | Chronologie logique reproductible | À renseigner | |

**Livrables :**
- application locale intégrée ;
- cahier de recette rempli ;
- procédure d'installation ;
- documentation d'architecture ;
- version de référence à conteneuriser.

## 6. Ce qui doit être préparé dès DEV pour Docker et Metrics

Même si ces phases viennent après, l'application doit être conçue pour les rendre possibles.

- configuration par variables d'environnement ;
- absence d'adresses IP et de secrets codés en dur ;
- processus démarrables et arrêtables séparément lorsque cela est justifié ;
- stockage persistant séparé du système de fichiers éphémère ;
- endpoint ou mécanisme de santé par composant ;
- journaux structurés vers la sortie standard ;
- horodatages normalisés et synchronisés ;
- compteurs de messages, pertes, doublons et alarmes ;
- scripts de peuplement et de rejeu reproductibles ;
- tests automatisés exécutables sans saisie manuelle.

L'instrumentation de base se développe pendant DEV. Les campagnes de mesure approfondies restent dans la phase Metrics.

## 7. Ce qui vient après

Après validation locale, la même application est conteneurisée dans [Docker.md](Docker.md). Les résultats d'intégration deviennent une base de comparaison. Le code métier ne doit pas être réécrit pour changer de mode de déploiement.

## 8. Livrables et critères de sortie de DEV

| Livrable | Critère de sortie |
|---|---|
| Exigences et scénarios | Validés et traçables |
| Maquettes | Parcours et états dégradés revus |
| Modèle de données | Migrations et intégrité vérifiées |
| Serveur et simulateurs | Mesures reçues et traitées de bout en bout |
| Centrale | Vues multi-patients et alarmes opérationnelles |
| Tests | Tous les tests P0 passent |
| Installation locale | Reproductible sur un environnement propre |
| Configuration | Externalisée et documentée |

**DEV est terminé lorsque l'application locale est intégrée et démontrable.** Une capture d'écran seule ou un serveur qui démarre sans scénario complet ne suffit pas.
