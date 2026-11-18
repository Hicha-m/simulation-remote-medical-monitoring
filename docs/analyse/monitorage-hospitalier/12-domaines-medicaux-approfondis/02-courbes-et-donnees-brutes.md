# 02 — Courbes physiologiques et données brutes

**Version :** 1.0 — **Date :** 18 novembre 2026  
**Objectif :** déterminer quelles formes d'onde doivent être prises en charge, où obtenir des enregistrements documentés et comment préserver leur fidélité.

## 1. Trois niveaux de données

1. **Signal brut / waveform :** suite de valeurs échantillonnées à une cadence connue (ECG, PPG, pression artérielle, respiration, capnogramme).
2. **Numérique monitoré :** valeur calculée ou publiée par le moniteur (HR, SpO₂, pression systolique/diastolique/moyenne, FR, EtCO₂).
3. **Tendance / résumé :** agrégation dans le temps pour historique et tableau de bord.

Une valeur de FC calculée par le moniteur ne doit pas être présentée comme un échantillon ECG. Une valeur NIBP n'est pas un signal continu. Une moyenne minute issue d'un système d'information ne doit pas être présentée comme un échantillon natif du dispositif.

## 2. Courbes à documenter

| Courbe | Origine typique | Intérêt pour le monitorage | Difficultés techniques |
|---|---|---|---|
| ECG | Électrodes cardiaques | Activité électrique, dérivation et détection de battements/événements par le dispositif | Débit élevé, bruit, perte de contact, dérivations multiples et synchronisation. |
| PPG / pleth | Oxymètre optique | Pulsations périphériques, qualité du signal et origine de la SpO₂/pouls | Mouvement, perfusion, position du capteur, lumière ambiante, échelle spécifique. |
| Pression artérielle invasive | Cathéter + transducteur | Courbe battement par battement et valeurs dérivées | Calibration/zéro, artefacts de ligne, amortissement, canaux distincts. |
| Respiration par impédance | Électrodes thoraciques | Cycles respiratoires et FR estimée | Mouvements, artefacts cardiaques, apnée/déconnexion et méthode de calcul. |
| Capnogramme | Capnographe | CO₂ au cours du cycle respiratoire | Retard de prélèvement, déconnexion, fuite, forme et échelle propres au dispositif. |
| Débit/pression/volume ventilatoire | Respirateur | Relation entre ventilation et cycle respiratoire | Dispositif distinct, fréquence et synchronisation propres. |

La prise en charge de toutes ces courbes n'est pas nécessairement exigée au même moment. Le service prioritaire et les besoins de démonstration doivent fixer le sous-ensemble.

## 3. Fréquences observées dans des ressources documentées

Les chiffres ci-dessous sont spécifiques aux jeux de données concernés. Ils ne constituent pas des recommandations de configuration des appareils du projet.

| Source | Contexte et signaux | Résolution publiée | Intérêt | Limite |
|---|---|---|---|---|
| MIMIC-IV Waveform Database v0.1.0 [H122] | Soins intensifs ; ECG, PPG, respiration, pression invasive/non invasive et numériques | Dépend des enregistrements ; en-têtes WFDB à lire par segment | Relier waveform et données cliniques MIMIC-IV ; fichier waveform et CSV numériques distincts | Version initiale documentée de 200 enregistrements ; examiner la couverture exacte de chaque record. |
| MIMIC-III Waveform Database [H132] | Soins intensifs ; jusqu'à huit signaux simultanés | Signaux généralement à 125 Hz ; ECG capturés/stockés avec limitations de décimation et de synchronisation documentées | Comprendre les limites de données récupérées depuis des moniteurs réels | Les auteurs documentent une gigue temporelle et des décalages inter-canaux ; certains usages d'analyse fine ne sont pas fiables. |
| VitalDB [H123] | Bloc opératoire ; biosignaux et informations cliniques | Signaux à 500 Hz ; numériques toutes les 1 à 7 s dans la description publiée | Très riche pour comparer des signaux multiparamétriques et leurs valeurs numériques | Population peropératoire coréenne ; ne représente pas à elle seule une réanimation française. |
| Barcelona SICU Signals v1.0.0 [H124] | Réanimation chirurgicale en Espagne ; signaux multiparamétriques enregistrés avec VitalRecorder et moniteurs Philips | ECG jusqu'à 500 Hz ; PPG et pression invasive à 125 Hz ; capnographie, respiration et courbes ventilatoires à 62,5 Hz ; tendances numériques à 1 Hz | Source européenne récente, réanimation réelle, diversité de signaux | Horodatages absolus, identifiants lits/appareils et données patient ont été retirés ; temps relatif à chaque enregistrement. |
| PhysioNet/CinC Challenge 2015 [H125] | Alarmes d'arythmie ICU et signaux associés | Dépend des enregistrements de la base challenge | Étudier faux positifs, qualité des signaux et alarmes | Dataset de challenge, pas un workflow hospitalier français ni une vérité clinique universelle. |

### Lecture de la documentation waveform

Pour chaque fichier choisi, consigner :
- fréquence d'échantillonnage exacte par signal ;
- unité, gain et calibration fournis dans l'en-tête ;
- date/heure ou origine du temps relatif ;
- canaux présents et absents ;
- trous, segments interrompus et changements de fréquence ;
- compression, conversion ou rééchantillonnage effectué ;
- conditions d'accès et licence ;
- limitations publiées par les auteurs.

Ne jamais supposer que tous les canaux sont présents simultanément.

## 4. Formats et représentation

- **WFDB** : format et outils utilisés dans plusieurs ressources PhysioNet ; préserver les en-têtes et les informations de calibration.
- **VITAL** : format documenté par VitalRecorder/VitalDB ; importer via les outils adaptés plutôt qu'interpréter les fichiers binaires à la main.
- **CSV** : utile pour les valeurs numériques et les exports, mais insuffisant seul pour garantir une waveform volumineuse avec fréquence, précision et temps exacts.
- **Format interne du projet** : peut stocker des métadonnées de segment et les échantillons dans des blocs binaires ; le choix doit être benchmarké.

Un segment de waveform doit au minimum posséder :
`waveformSegmentId`, `patientId`, `encounterId`, `monitoringSessionId`, `deviceId`, `channelId`, `signalCode`, `unit`, `sampleRateHz`, `sampleCount`, `startTime`, `timeBasis`, `calibration`, `qualityStatus`, `sourceDataset`, `sourceRecord`, `checksum`.

Le temps doit être sans ambiguïté. Si la source utilise un temps relatif, le stocker comme relatif et ne pas fabriquer une date hospitalière.

## 5. Stratégie de rejeu proposée à expérimenter

Le lecteur de données ne doit pas être couplé directement au rendu graphique.

1. Un adaptateur lit la source et son en-tête.
2. Il expose un flux canonique d'échantillons/valeurs avec métadonnées.
3. Une horloge de simulation pilote la vitesse (1x, accélérée, pause, reprise).
4. Un émetteur publie les paquets vers le système de monitorage.
5. Le système reçoit les données comme il recevrait celles d'un appareil.
6. Les données de référence peuvent être comparées au rejeu pour vérifier absence de corruption, perte ou duplication.

Les cadences de calcul, émission, transport, réception, persistance et affichage sont mesurées séparément.

## 6. Contrôles techniques indispensables

- conservation du nombre d'échantillons ;
- checksum du fichier/segment source ;
- continuité et monotonie temporelle ;
- identification explicite des trous ;
- exactitude de l'unité et du facteur de conversion ;
- absence de mélange de canaux ;
- absence de mélange entre patient, séjour et session ;
- détection de paquets manquants, répétés ou désordonnés ;
- rendu graphique sans confondre échantillons perdus et valeurs nulles ;
- mesure de la latence d'affichage et du coût mémoire.

## 7. Ressources documentaires prioritaires

1. **Barcelona SICU Signals [H124]** : source européenne récente, très pertinente pour les signaux de soins critiques.
2. **MIMIC-IV Waveform [H122]** : associer signaux et contexte clinique MIMIC-IV.
3. **VitalDB [H123]** : référence riche en peropératoire si le bloc/SSPI fait partie du projet.
4. **PhysioNet Challenge 2015 [H125]** : travailler les alarmes d'arythmie et les faux positifs.
5. **MIMIC-III Waveform [H132]** : étudier les limites de synchronisation et de compression historique.

Les ressources sont ouvertes ou accessibles sous conditions différentes. Avant toute copie ou redistribution, vérifier la page d'accès, la licence, l'attribution et les obligations propres à chaque ressource.

## 8. Références

- [H122] MIMIC-IV Waveform Database, PhysioNet, v0.1.0.
- [H123] VitalDB Open Dataset, documentation officielle.
- [H124] Continuous high-density physiological signals from a surgical intensive care unit at Hospital Clínic de Barcelona, PhysioNet, v1.0.0, publiée le 19 octobre 2026.
- [H125] PhysioNet/CinC Challenge 2015 — Reducing False Arrhythmia Alarms in the ICU.
- [H132] MIMIC-III Waveform Database, PhysioNet.
