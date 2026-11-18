# Couverture 02 — Questions et arbitrages avant la conception

**Version :** 0.1 — **Date :** 18 novembre 2026  
**Statut :** questions ouvertes ; elles ne constituent pas des décisions.

## 1. Périmètre hospitalier

- Quel service sert de référence principale : réanimation, cardiologie, SSPI, urgences ou unité conventionnelle ?
- Le POC doit-il représenter une seule unité ou une petite organisation multi-services ?
- Les patients sont-ils tous fixes au lit, ou certains sont-ils mobiles en télémétrie ?
- Les transferts vers imagerie et autres unités font-ils partie du scénario ?
- Faut-il inclure néonatologie ou pédiatrie, ou les garder comme extension ?

## 2. Équipements simulés

- Moniteur multiparamétrique complet ou plusieurs familles spécialisées ?
- Faut-il représenter un respirateur, une pompe et leurs alarmes séparément ?
- Le POC simule-t-il les courbes ECG et SpO₂ ou seulement les valeurs numériques ?
- Quels états techniques reproduire : câble, batterie, capteur, réseau, maintenance ?
- Comment un appareil est-il identifié et associé au patient ?
- Quels comportements d'appareils doivent être spécifiques aux fabricants ou rester génériques ?

## 3. Clients simulateurs

- Un processus par appareil, par patient ou par source physiologique ?
- Combien de clients sont attendus dans chaque scénario ?
- Les fréquences sont-elles fixes, variables ou paramétrées par mesure ?
- Les simulations doivent-elles être déterministes et rejouables ?
- Quel est le comportement en cas de perte réseau : tampon local, perte ou retransmission ?
- Les clients doivent-ils disposer d'une horloge simulée accélérable ?

## 4. Serveur et traitement

- Comment authentifier et autoriser les sources ?
- Le serveur reçoit-il des messages unitaires, des lots ou des flux continus ?
- Faut-il un traitement synchrone ou une file d'événements ?
- Comment valider format, unité, horodatage, identité et qualité ?
- Comment gérer un message inconnu, dupliqué ou tardif ?
- Le serveur peut-il fonctionner si la base de données est temporairement indisponible ?
- Quelles informations d'observabilité exposer ?

## 5. Stockage

- Les valeurs numériques et les courbes sont-elles conservées de la même manière ?
- Quelle durée d'historique est nécessaire au scénario ?
- Quelles requêtes devront être rapides ?
- Quel volume par appareil et par minute ?
- Faut-il conserver les messages bruts reçus ?
- Comment historiser les affectations patient, lit et appareil ?
- Comment stocker les alarmes, acquittements et changements d'état ?
- Quelle stratégie de sauvegarde et de restauration démontrer ?

## 6. Interface

- Tableau de bord desktop ou web ?
- Combien de patients à visualiser simultanément ?
- Vue multi-lits, vue patient, vue appareil et vue alarmes séparées ?
- Quels rôles et quelles autorisations ?
- Les vues doivent-elles afficher les courbes en temps réel ?
- Comment représenter une donnée périmée ou un appareil hors ligne ?
- Quelles actions sont permises depuis la centrale ?
- Faut-il simuler plusieurs écrans, répétiteurs ou terminaux mobiles ?

## 7. Temps réel et dimensionnement

- Que signifie « le plus rapidement possible » pour l'encadrant ?
- Quel délai de référence entre mesure simulée, réception et affichage ?
- Quel débit soutenu et quel pic ?
- Combien de patients, appareils, utilisateurs et flux simultanés ?
- Quelles statistiques de latence : médiane, p95, p99 ?
- Comment vérifier la perte, duplication et reprise après coupure ?
- Quelles performances doivent être mesurées sur une configuration matérielle connue ?

## 8. Sécurité

- Les données seront-elles exclusivement synthétiques ?
- L'environnement restera-t-il local et isolé ?
- Faut-il authentifier séparément chaque client simulateur ?
- Quels rôles utilisateurs sont nécessaires ?
- Quelles actions sont journalisées ?
- Quelles fonctions de sécurité sont obligatoires pour l'évaluation académique ?
- Quelles menaces sont simulées sans exécuter de malware ni toucher un réseau réel ?
- Comment tester la révocation d'un appareil ou compte ?
- Quelle procédure de sauvegarde et de reprise faut-il démontrer ?

## 9. Contraintes de réalisation

- Quelle version de Java est attendue ?
- Tous les composants doivent-ils être en Java ?
- L'interface doit-elle être desktop ou web ?
- Frameworks et librairies autorisés ?
- Base de données imposée ou libre ?
- Durée disponible, taille de l'équipe et modalités d'évaluation ?
- Démonstration attendue : combien de scénarios et à quel niveau de réalisme ?

## 10. Arbitrages à enregistrer

Chaque arbitrage futur devra inclure :
1. question ou besoin ;
2. alternatives étudiées ;
3. preuves et contraintes ;
4. choix validé ;
5. conséquences ;
6. date et auteur de la validation.

Aucune question de cette liste ne doit être considérée comme décidée tant qu'une réponse explicite n'a pas été enregistrée.
