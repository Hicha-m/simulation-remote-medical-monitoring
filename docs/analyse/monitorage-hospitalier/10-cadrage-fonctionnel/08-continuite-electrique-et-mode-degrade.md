# Continuité électrique, panne et fonctionnement dégradé

**Date :** 18 novembre 2026  
**Statut :** modèle fonctionnel pour un POC de simulation. Ce document ne décrit pas une installation électrique réelle et ne remplace aucune procédure hospitalière.

## 1. Une coupure électrique est un scénario majeur

La panne peut toucher un seul circuit, une chambre, un étage, un bâtiment ou tout le site. Elle peut également affecter différemment les équipements médicaux, le réseau et la centrale de surveillance.

Il faut distinguer au moins quatre choses :

1. L'alimentation électrique du moniteur au chevet.
2. L'alimentation électrique des autres appareils connectés au patient.
3. L'alimentation de la centrale, de ses écrans, des commutateurs réseau et des points d'accès Wi-Fi.
4. L'alimentation des serveurs, passerelles et services informatiques partagés.

Un moniteur qui reste alimenté sur sa batterie ne garantit pas que la centrale puisse encore recevoir ses données. Inversement, le serveur central peut rester allumé alors qu'un moniteur de chevet n'a plus d'alimentation.

## 2. Comment la continuité est organisée en pratique ?

Les établissements définissent une architecture électrique adaptée aux activités et aux équipements critiques. Les documents ministériels français décrivent notamment :

- des sources électriques normales et des sources autonomes de remplacement ;
- des groupes électrogènes et des circuits de secours ;
- des onduleurs (UPS/ASI) pour maintenir certains systèmes sans interruption ou permettre un arrêt maîtrisé ;
- des capacités d'autonomie documentées pour les onduleurs et les groupes ;
- des essais, de la maintenance et des procédures de fonctionnement dégradé.

La circulaire ministérielle DHOS/E4/2006/393 cite notamment les activités opératoires, la SSPI, les urgences, l'anesthésie, la réanimation, les soins intensifs et la néonatologie parmi les activités qui doivent bénéficier d'une continuité électrique. Elle décrit plusieurs architectures de sources de secours, la maintenance et les essais des groupes [H116]. Cette circulaire est ancienne : elle sert ici à documenter les principes et ne doit pas être présentée comme une vérification de toutes les règles techniques applicables en 2026.

La circulaire demande également d'identifier, pour les sites sensibles, la chaîne de secours, les équipements, les localisations et les autonomies temporelles des onduleurs et groupes électrogènes [H116].

### Rôle des différentes protections

| Élément | Rôle | Ce qu'il ne garantit pas à lui seul |
|---|---|---|
| Batterie interne d'un moniteur | Permet à l'appareil de fonctionner lorsque son alimentation secteur disparaît, selon son modèle et l'état de sa batterie. | Ne maintient pas la centrale ou le réseau en fonctionnement. |
| Circuit électrique secouru | Alimente les équipements raccordés aux circuits prioritaires lorsque la source normale est indisponible. | Ne signifie pas que toutes les prises de toutes les chambres sont secourues. |
| Onduleur (UPS/ASI) | Maintient temporairement l'alimentation de ses charges et peut lisser le transfert vers une autre source. | Son autonomie est limitée et dépend de la charge et de l'état des batteries. |
| Groupe électrogène | Fournit de l'énergie aux circuits secourus pendant une panne prolongée, si le système démarre et fonctionne correctement. | Ne protège pas contre tous les défauts de distribution ou les pannes de son propre équipement. |
| Alimentation de secours du réseau | Maintient les commutateurs, points d'accès et équipements réseau qui en dépendent. | Si un élément intermédiaire n'est pas secouru, la communication peut quand même être interrompue. |

Les manuels de centrales de surveillance précisent eux aussi que la centrale doit être raccordée à l'alimentation de secours de l'établissement ou protégée par un onduleur ; le manuel Mindray avertit qu'une coupure brutale peut provoquer une défaillance du système [H117].

## 3. La continuité du monitorage dépend d'une chaîne entière

Pour qu'une donnée arrive à la centrale, plusieurs éléments doivent rester opérationnels :

- appareil de mesure ;
- capteur ;
- alimentation de l'appareil ;
- connexion filaire ou radio ;
- récepteur, point d'accès ou commutateur ;
- réseau de transport ;
- serveur ou centrale de surveillance ;
- écran et poste de travail.

Une seule panne dans cette chaîne peut rendre la surveillance centralisée indisponible.

Le guide ministériel du volet numérique du Plan blanc rappelle qu'une panne du réseau de l'établissement peut compromettre le monitorage centralisé et demande une organisation dégradée permettant notamment de poursuivre la supervision des alarmes et de fonctionner en mode déconnecté de la base de données patient [H114]. La HAS ne remplace pas le fabricant ou les services techniques : les contre-mesures et les responsabilités doivent être définies avec eux.

## 4. Scénario A — Coupure du réseau électrique normal, secours opérationnel

1. La source électrique normale devient indisponible.
2. Les équipements concernés basculent sur leurs moyens de secours.
3. Les moniteurs alimentés par batterie continuent à fonctionner dans la limite de leur autonomie.
4. Les circuits secourus alimentent les équipements concernés.
5. Les onduleurs maintiennent les équipements informatiques et réseau raccordés à leurs sorties.
6. Le groupe électrogène prend en charge les circuits qui lui sont affectés, selon l'installation.
7. La centrale continue à recevoir les données si l'ensemble du chemin de communication est secouru.
8. Les événements de bascule et les états de batterie sont journalisés.

**Ce que le POC doit montrer :** l'alimentation normale est perdue, mais les appareils, le réseau et la centrale restent disponibles grâce aux dispositifs de secours simulés.

Ne pas inventer un délai de bascule ou une autonomie universelle. Les durées doivent être configurées comme propriétés de la maquette et seront différentes selon les équipements et l'installation réelle.

## 5. Scénario B — Centrale ou réseau indisponible, moniteurs de chevet encore alimentés

C'est un scénario particulièrement important.

1. Les moniteurs de chevet continuent à acquérir et afficher les données localement.
2. La liaison avec la centrale est perdue parce qu'un commutateur, un point d'accès, une passerelle ou la centrale elle-même n'est plus disponible.
3. La centrale marque les données comme périmées et l'état de communication comme dégradé.
4. Les données ne sont plus présentées comme une surveillance centralisée active.
5. Le personnel suit la procédure locale : surveillance au chevet, report manuel ou autre dispositif de secours prévu par l'établissement.
6. Les alarmes locales restent gérées selon les caractéristiques et les réglages du dispositif ; le comportement exact doit être vérifié dans la documentation du fabricant.
7. Le défaut est journalisé avec son périmètre et sa durée.
8. Au retour du réseau, les associations patient / lit / appareil sont revérifiées et les trous de données restent visibles.

L'ANSM a documenté le risque d'une perturbation des alarmes réparties lors d'une intervention sur le réseau hospitalier [H95]. Certains systèmes réactivent un signal local lorsque la communication avec la centrale est interrompue ; ce comportement doit être vérifié pour le matériel réellement simulé et ne peut pas être généralisé à tous les modèles.

## 6. Scénario C — Échec d'un moyen de secours ou panne prolongée

1. La source normale est indisponible.
2. La chaîne de secours ne remplit pas sa fonction : défaut de démarrage du groupe, batterie UPS insuffisante, circuit secouru défaillant ou manque d'autonomie.
3. La zone touchée est identifiée : chambre, secteur, étage ou bâtiment.
4. Les professionnels et les responsables techniques suivent les procédures de l'établissement.
5. Les appareils passent sur leur batterie interne lorsque cette fonction existe et que leur batterie est disponible.
6. La surveillance centralisée est considérée comme dégradée si la centrale, le réseau ou ses dépendances ne sont plus alimentés.
7. Les mesures, observations et actions nécessaires sont consignées dans le support de fonctionnement dégradé défini par l'établissement.
8. La cellule de crise et les services techniques déterminent les mesures de continuité, les priorités de charge et les éventuels transferts.
9. Le retour à la normale est réalisé de façon contrôlée ; les appareils et leurs associations sont vérifiés avant de considérer la supervision comme rétablie.

La décision clinique de déplacer un patient ou de modifier ses soins n'appartient jamais au simulateur.

## 7. Scénario D — Panne électrique localisée

Une panne peut ne toucher qu'une chambre ou une partie d'un étage.

Exemple de simulation :

- la chambre REA-03 perd son circuit normal ;
- le moniteur passe sur batterie ;
- les autres chambres de réanimation restent alimentées ;
- le switch de l'étage reste actif si son alimentation est secourue ;
- le poste central continue à fonctionner ;
- la carte de l'étage montre une chambre en alimentation dégradée, mais les autres lits ne sont pas marqués en panne.

Il faut éviter de transformer une panne locale en indisponibilité totale de l'établissement.

## 8. États à représenter dans le modèle

| Objet | États simulés |
|---|---|
| Source normale | available, failed |
| Groupe électrogène | stopped, starting, supplying, failed, maintenance |
| Onduleur | normal, battery, low_battery, exhausted, failed |
| Circuit secouru | available, unavailable |
| Moniteur | mains_power, internal_battery, low_battery, off |
| Réseau de service | connected, degraded, unavailable |
| Centrale | online, degraded, offline |
| Session patient | active, locally_monitored, central_monitoring_lost, ended |

Ces états sont des états de simulation. Ils ne reproduisent pas les automates propriétaires de tous les fabricants.

## 9. Événements à journaliser

Chaque incident doit être exploitable dans une chronologie :

- power_source_lost ;
- ups_on_battery ;
- generator_start_requested ;
- generator_supply_active ;
- generator_start_failed ;
- ups_low_battery ;
- backup_circuit_lost ;
- device_on_internal_battery ;
- monitoring_network_lost ;
- central_station_offline ;
- manual_degraded_mode_started ;
- electrical_supply_restored ;
- network_restored ;
- monitoring_session_verified.

Les événements portent un horodatage, un périmètre géographique, une source, un état avant/après et un identifiant de corrélation. Une panne d'alimentation ne doit pas être confondue avec une simple déconnexion réseau.

## 10. Tests d'acceptation à ajouter

| ID | Injection de panne | Résultat attendu |
|---|---|---|
| PWR-01 | Perte de la source électrique normale. | Les objets raccordés à un secours configuré passent dans l'état correspondant ; la panne est visible et horodatée. |
| PWR-02 | Bascule vers le groupe électrogène. | L'état de la source et les équipements alimentés sont mis à jour ; les services non concernés ne sont pas marqués en panne. |
| PWR-03 | Le groupe électrogène ne démarre pas. | Une défaillance du secours est visible ; le POC ne prétend pas que la continuité est garantie. |
| PWR-04 | Onduleur en batterie puis autonomie épuisée. | Le compte à rebours simulé atteint l'état indisponible ; les éléments dépendants tombent selon leur alimentation. |
| PWR-05 | Coupure localisée d'une chambre. | Seuls les lits et appareils de la zone sont affectés, sauf dépendance réseau commune. |
| PWR-06 | Le réseau de l'étage tombe alors que les moniteurs sont alimentés. | Les moniteurs restent localement actifs si leur profil le permet ; la centrale indique perte de remontée et données périmées. |
| PWR-07 | La centrale perd son alimentation. | La centrale passe hors ligne ; les moniteurs ne sont pas présentés comme éteints si leur alimentation reste disponible. |
| PWR-08 | Retour de l'alimentation et du réseau. | La reconnexion est contrôlée ; les anciennes mesures ne sont pas affichées comme actuelles ; aucune association patient / appareil n'est perdue. |
| PWR-09 | Le journal d'événements est consulté après restauration. | La chronologie permet de reconstruire le début, le périmètre, les bascules et la fin de l'incident. |
| PWR-10 | L'incident est rejoué avec la même configuration. | Le scénario est reproductible et les états finaux sont identiques. |

## 11. Ce que le POC doit réellement simuler

Il ne faut pas calculer l'électrotechnique d'un hôpital. Le POC doit simuler les dépendances et les transitions :

- une source normale tombe ;
- un UPS prend une charge donnée ;
- un groupe démarre ou échoue ;
- une zone est secourue ou non ;
- un appareil possède ou non une batterie ;
- le réseau et la centrale restent disponibles ou non ;
- les professionnels passent en mode dégradé et rétablissent la supervision.

Les durées d'autonomie et de démarrage seront des paramètres explicites de la maquette, jamais des affirmations sur un hôpital réel. Un établissement réel doit fournir les plans, les schémas électriques, les capacités et les procédures locales.

## 12. Références

- [H114] Ministère de la Santé — Guide d'aide à la préparation au volet numérique du Plan blanc, 2023, notamment la gestion des centrales de surveillance et le mode dégradé en soins critiques.
- [H116] Circulaire DHOS/E4/2006/393 — conditions techniques d'alimentation électrique des établissements de santé ; document ancien, cité pour ses principes et à confronter aux textes et normes applicables au moment d'une conception réelle.
- [H117] Mindray — BeneVision Central Monitoring System, Operator's Manual, exigences d'alimentation de la centrale et de protection UPS.
- [H95] ANSM — Gestion des alarmes des dispositifs médicaux, 2019.
