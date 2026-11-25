# Points critiques, stratégie de test et critères d'acceptation

**Date de mise à jour :** 25 novembre 2026  
**Statut :** critères d'acceptation de la première version du système ; les seuils de performance et règles cliniques restent à valider. La priorisation F-01 à F-22 est consignée dans le cahier de décisions.

## 1. Quels sont les points critiques du système ?

Le système peut sembler fonctionner visuellement tout en étant dangereux ou incohérent. Voir des courbes à l'écran ne suffit pas.

Les points critiques sont les suivants :

1. **Identité et association** : la mesure doit appartenir au bon patient, au bon séjour, à la bonne session et au bon appareil.
2. **Intégrité temporelle** : la date de mesure, l'ordre, les doublons et les retards doivent être gérés correctement.
3. **Alarmes** : une alarme doit être reçue, identifiée, affichée et suivie jusqu'à sa résolution ; l'acquittement ne doit pas la faire disparaître à tort.
4. **Fraîcheur des données** : une valeur ancienne ne doit jamais être présentée comme actuelle.
5. **Transferts** : les associations doivent être mises à jour sans mélanger les données de deux lieux ou deux patients.
6. **Disponibilité** : la perte d'un appareil, du réseau, du serveur ou de la base doit être visible et gérée.
7. **Sécurité et traçabilité** : les sources et utilisateurs doivent être identifiés ; les actions sensibles doivent être journalisées.
8. **Ergonomie** : l'utilisateur doit comprendre quel patient est surveillé, par quel appareil, avec quelles données et à quel moment.
9. **Performance** : la charge multi-patients doit être mesurée ; un écran réactif sur un seul patient ne prouve pas que le système tient la charge.

La HAS cite des défauts de surveillance associés à des moniteurs mal configurés, des alarmes techniques mal interprétées, une organisation insuffisante et des difficultés de report [H02]. L'ANSM insiste sur le déclenchement, la transmission au bon opérateur et la réponse adaptée aux alarmes [H95].

## 2. Priorisation des risques pour la première version

| Priorité | Risque | Conséquence simulée | Principe de maîtrise |
|---|---|---|---|
| P0 — bloquant | Mesure attribuée au mauvais patient. | Mélange de données et tableau de bord trompeur. | Contrôle strict des liens patient / séjour / lit / appareil / session. |
| P0 — bloquant | Alarme perdue ou masquée. | Événement critique non visible dans la centrale. | Cycle d'alarme séparé, visibilité et tests de bout en bout. |
| P0 — bloquant | Donnée périmée affichée comme actuelle. | Fausse impression de surveillance active. | Horodatage visible, indicateur de fraîcheur et état technique. |
| P0 — bloquant | Transfert mal géré. | Les données continuent sur l'ancien lit ou sont reliées au mauvais contexte. | Historique des affectations et sessions explicites. |
| P0 — bloquant | Doublon ou message désordonné. | Valeur incorrecte dans la dernière mesure ou historique incohérent. | Déduplication et ordre temporel. |
| P1 — majeur | Perte réseau ou redémarrage non détecté. | Trou dans les données ou état faussement nominal. | Détection, état dégradé, reprise et journalisation. |
| P1 — majeur | Accès non autorisé. | Consultation ou modification injustifiée. | Authentification, rôles et contrôle côté serveur. |
| P1 — majeur | Action non tracée. | Impossible de reconstituer qui a modifié une affectation ou une configuration. | Journal d'audit append-only pour les événements sensibles. |
| P2 — important | Interface trop dense ou confuse. | Erreur d'interprétation pendant la démonstration. | Vue multi-patients hiérarchisée et vue détaillée. |
| P2 — important | Performance sous charge insuffisante. | Retard ou perte lors de plusieurs flux simultanés. | Campagnes de charge avec mesures de latence et pertes. |

## 3. Catalogue initial de tests d'acceptation

Les critères ci-dessous sont vérifiables sans définir de seuil clinique.

| ID | Test | Résultat attendu / critère d'acceptation |
|---|---|---|
| CRIT-01 | Deux patients ont des mesures simultanées. | Chaque observation apparaît uniquement dans la session et la fiche du patient correspondants. |
| CRIT-02 | Un appareil inconnu ou non associé envoie une mesure. | La mesure est rejetée ou mise en quarantaine ; elle n'apparaît pas sur la fiche d'un patient au hasard. |
| CRIT-03 | Un appareil est réaffecté à un autre patient. | L'ancienne session est clôturée ; les nouvelles mesures sont liées à la nouvelle session ; l'historique ancien reste intact. |
| CRIT-04 | Le serveur reçoit une mesure ancienne après une mesure plus récente. | La chronologie conserve les deux événements ; la dernière valeur connue n'est pas remplacée par une mesure plus ancienne. |
| CRIT-05 | Le même message est envoyé deux fois. | Le message est dédupliqué selon son identifiant ; aucune seconde observation métier n'est créée. |
| CRIT-06 | Une mesure ne possède aucune valeur. | La valeur est marquée absente ou invalide selon le contrat ; elle n'est jamais transformée en zéro. |
| CRIT-07 | Aucune nouvelle mesure n'arrive pendant la durée configurée. | La donnée passe visiblement à l'état périmé ; la dernière valeur reste consultable avec son heure. |
| CRIT-08 | Une alarme est déclenchée. | Elle apparaît dans la vue patient et la vue alarmes avec sa source, son horodatage et sa priorité d'origine. |
| CRIT-09 | Un utilisateur acquitte une alarme toujours active. | L'état devient acquitté mais reste actif jusqu'à l'événement de résolution. |
| CRIT-10 | Un défaut technique est produit (capteur débranché, appareil hors ligne). | Le défaut est distinct d'une alarme physiologique et son origine est visible. |
| CRIT-11 | Un patient est transféré pendant une session active. | Le changement de lieu est horodaté ; aucune mesure future n'est attribuée à l'ancien lit par erreur. |
| CRIT-12 | Le réseau est coupé puis rétabli. | La perte de flux est visible ; la reprise ne crée ni doublons ni faux retour à la normale. |
| CRIT-13 | Le serveur redémarre. | Les données déjà persistées et l'historique des alarmes sont retrouvés après reprise. |
| CRIT-14 | Un client non authentifié tente d'émettre. | La connexion ou les messages sont refusés et l'événement est journalisé. |
| CRIT-15 | Un utilisateur sans rôle adapté tente une action sensible. | L'action est refusée côté serveur et une trace d'audit est créée. |
| CRIT-16 | Une affectation ou une configuration est modifiée. | L'auteur, l'heure, l'objet modifié et les anciennes/nouvelles valeurs sont traçables. |
| CRIT-17 | Plusieurs clients transmettent simultanément. | Les messages sont reçus et traités sans mélange d'identités ; débit, latence et pertes sont mesurés. |
| CRIT-18 | Un scénario complet est rejoué avec la même configuration. | Les événements simulés sont reproductibles et suivent la même chronologie logique. |

## 4. Les tests les plus importants à réussir en premier

### Lot 1 — Intégrité et identité

- CRIT-01 : séparation des patients.
- CRIT-02 : appareil non associé.
- CRIT-03 : réaffectation.
- CRIT-04 : ordre temporel.
- CRIT-05 : déduplication.
- CRIT-06 : absence de donnée.

Ce lot évite que le système affiche des informations fausses ou mélangées.

### Lot 2 — Alarmes et fraîcheur

- CRIT-07 : données périmées.
- CRIT-08 : transmission d'alarme.
- CRIT-09 : acquittement distinct de résolution.
- CRIT-10 : alarmes techniques.

Ce lot vérifie le cœur du monitorage et son rendu dans la centrale.

### Lot 3 — Parcours et continuité

- CRIT-11 : transfert.
- CRIT-12 : perte réseau et reprise.
- CRIT-13 : redémarrage.

Ce lot permet de démontrer un parcours réaliste plutôt qu'une simple visualisation de courbes.

### Lot 4 — Sécurité et charge

- CRIT-14 : client inconnu.
- CRIT-15 : autorisation utilisateur.
- CRIT-16 : audit.
- CRIT-17 : charge multi-clients.
- CRIT-18 : reproductibilité.

## 5. Indicateurs techniques à mesurer plus tard

Les objectifs chiffrés ne sont pas fixés maintenant, mais les mesures devront exister :

- latence entre mesure simulée, réception serveur et affichage ;
- latence de bout en bout d'une alarme ;
- taux de messages perdus, rejetés et dupliqués ;
- retard des messages tardifs ;
- délai de détection d'un appareil silencieux ;
- délai de reprise après reconnexion ;
- nombre d'appareils et de patients simultanés ;
- consommation CPU / mémoire / stockage ;
- durée de récupération après redémarrage.

Les résultats devront préciser la machine, la configuration, le nombre de patients et la durée du test. Les seuils seront décidés après le dimensionnement du scénario global.

## 6. Ce qui doit rester hors de l'acceptation clinique

La première version ne doit pas être évaluée sur sa capacité à diagnostiquer, prédire ou recommander un traitement. Les critères portent sur :

- la bonne réception et association des données synthétiques ;
- leur intégrité, leur fraîcheur et leur persistance ;
- l'affichage fidèle des états et alarmes simulés ;
- la gestion des transferts et défaillances ;
- la sécurité du système informatique ;
- la reproductibilité et la mesurabilité des scénarios.

Les seuils physiologiques et les priorités médicales devront être issus d'un protocole validé par des professionnels si le projet les inclut ultérieurement.

## 7. Critère global de réussite de la première version

La première version sera convaincante lorsqu'il pourra jouer un parcours patient complet avec plusieurs appareils et plusieurs patients, recevoir des données à intervalles configurés, gérer une alarme et un transfert, faire apparaître une coupure technique, reprendre sans corrompre l'historique et démontrer qu'aucune donnée n'est attribuée au mauvais patient.

La réussite ne se mesure donc pas au nombre de courbes affichées, mais à la fiabilité de toute la chaîne.

## Sources

- [H02] HAS — surveillance des patients en soins critiques, 2024.
- [H95] ANSM — gestion des alarmes des dispositifs médicaux, 2019.
- [H106] SFAR — surveillance des patients pendant le transport intrahospitalier.
- [H73–H77] Références ISO/IEC sur gestion des risques, logiciels, réseaux et cybersécurité, pour orienter la démarche sans prétendre à une certification de la première version.
