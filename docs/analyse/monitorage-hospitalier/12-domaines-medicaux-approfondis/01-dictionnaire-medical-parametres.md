# 01 — Dictionnaire médical des paramètres de monitorage

**Version :** 1.0 — **Date :** 18 novembre 2026  
**Statut :** dictionnaire initial ; profils et seuils à valider cliniquement.

## 1. Principe : décrire la mesure avant de choisir son affichage

Pour toute observation, le système doit savoir précisément :
- ce qui a été mesuré ou calculé ;
- par quel appareil, capteur et canal ;
- si la donnée est un nombre, une courbe, un événement dérivé ou un état technique ;
- quelle est son unité ;
- quelle est son heure de mesure et son heure de réception ;
- quelle qualité le dispositif ou le traitement lui attribue ;
- quel patient, séjour, lieu et session de monitorage sont concernés.

Ne pas réduire tous ces objets à une colonne `value` et un nom de paramètre.

## 2. Paramètres multiparamétriques à étudier

| Paramètre | Ce que représente la donnée numérique | Signal ou origine possible | Unité usuelle d'affichage | Particularités à conserver |
|---|---|---|---|---|
| Fréquence cardiaque (FC / HR) | Nombre de battements estimé par unité de temps | ECG, parfois estimation dérivée d'un signal pulsatile | batt/min (bpm) | Indiquer la source de calcul ; ne pas la confondre avec le pouls SpO₂. |
| ECG | Tracé électrique cardiaque et dérivations | Électrodes ECG | mV pour le signal calibré ; fréquence en Hz pour l'échantillonnage | Dérivation, gain, vitesse/échelle d'affichage si disponible, qualité du contact. Les résultats dérivés (QRS, intervalles RR, QT/QTc, analyse ST, étiquettes de rythme/arythmie) doivent être séparés du signal et identifiés comme calculs/événements du dispositif. |
| Fréquence du pouls (PULSE) | Fréquence des pulsations périphériques détectées | Pléthysmographie, parfois autre signal pulsatile | batt/min | Valeur distincte de HR ; un écart peut être informatif ou lié à la qualité du signal. |
| Saturation périphérique en oxygène (SpO₂) | Estimation de la saturation en oxygène | Oxymètre et photopléthysmogramme (PPG) | % | Ajouter qualité du signal, indice de perfusion si fourni, site/capteur si connu. |
| Pléthysmogramme (PLETH) | Forme d'onde pulsatile optique | Capteur d'oxymétrie | amplitude calibrée par l'appareil ou unité relative | L'amplitude n'est pas une saturation ; préserver l'échelle et la provenance du fabricant/source. |
| Pression artérielle non invasive (PANI / NIBP) | Mesure par brassard : systolique, diastolique et moyenne | Brassard oscillométrique | mmHg | Mesure ponctuelle/intermittente ; heure de début et de fin, bras/site, résultat/échec, statut du cycle. |
| Pression artérielle invasive (PAI / IBP) | Pression continue issue d'un transducteur | Courbe de pression artérielle invasive | mmHg | Conserver le canal (ART, radial, fémoral, etc. si disponible), zéro/calibration et qualité de la ligne. |
| Pression veineuse centrale (PVC / CVP) | Pression veineuse centrale | Transducteur invasif | mmHg | Canal distinct de la pression artérielle ; dépend de la configuration et de la méthode. |
| Pression artérielle pulmonaire (PAP) | Pression pulmonaire invasive | Cathéter adapté | mmHg | Ne pas l'assimiler à la pression artérielle systémique. Paramètre spécialisé, à confirmer selon le service. |
| Fréquence respiratoire (FR / RR) | Nombre de cycles respiratoires estimé | Impédance thoracique, capnographie, débit/pression ventilatoire ou autre méthode | cycles/min | Méthode de calcul et source obligatoires ; les sources peuvent fournir des résultats différents. |
| Courbe respiratoire | Signal associé aux cycles respiratoires | Impédance, débit, pression ou autre canal | unité dépendant du signal | Identifier explicitement la modalité : ne pas fusionner plusieurs courbes sous un nom générique. |
| CO₂ télé-expiratoire (EtCO₂) | Concentration/pression de CO₂ en fin d'expiration | Capnographe | mmHg ou kPa | Préciser l'unité, la méthode et la présence d'une courbe capnogramme. |
| Capnogramme | Évolution du CO₂ pendant le cycle respiratoire | Capnographe | mmHg ou kPa selon l'axe | Distinguer la courbe et la valeur numérique EtCO₂. |
| Température | Température mesurée à un site donné | Sonde de température | °C | Site de mesure (ex. centrale, cutané, autre) et type de sonde si connus. |

**Attention :** les unités ci-dessus décrivent des unités usuelles et non une obligation d'affichage universelle. Le contrat logiciel devra normaliser les codes et unités sans perdre la valeur/unité source. UCUM peut servir à représenter les unités ; LOINC peut identifier les observations ; les profils HL7 FHIR Observation apportent des modèles pour plusieurs signes vitaux [H88, H130].

### Mesures et événements ECG dérivés à traiter séparément\n\nSelon les capacités du moniteur et le profil clinique, certains appareils fournissent des valeurs ou événements calculés à partir de l'ECG : intervalle RR, durée QRS, QT/QTc, analyse du segment ST, battements ectopiques ou étiquettes d'arythmie. Ces sorties ne sont pas équivalentes au tracé ECG brut. Conserver le nom de l'algorithme ou du fabricant lorsqu'il est connu, sa version, les dérivations utilisées, l'heure source et le fait qu'il s'agit d'une interprétation automatique du moniteur. Ne pas implémenter de diagnostic de rythme ou de seuil d'alarme clinique sans demande explicite et validation appropriée.\n\n## 3. Paramètres issus d'autres dispositifs

Ils ne doivent pas être artificiellement présentés comme des mesures du moniteur multiparamétrique si leur source est un respirateur ou un autre appareil.

| Famille | Données possibles | Source | Décision nécessaire |
|---|---|---|---|
| Ventilateur | pression des voies aériennes, PEEP, volume courant, volume minute, fréquence réglée/mesurée, FiO₂, débit, courbes pression/volume/débit | Respirateur | Inclure ou non le respirateur et ses alarmes comme appareil indépendant. |
| Pompe à perfusion | débit programmé, volume perfusé, volume restant, état de perfusion, occlusion, porte ouverte, batterie | Pompe | Distinguer les paramètres de traitement des observations physiologiques. |
| Appareil d'anesthésie | gaz, agents, concentrations, pressions et courbes spécifiques | Station d'anesthésie | Pertinent surtout si bloc/SSPI dans le périmètre. |
| ECG diagnostique | tracé 12 dérivations et compte rendu associé | Électrocardiographe | Ne pas confondre un examen ponctuel 12 dérivations avec le monitorage continu de rythme. |

## 4. Métadonnées obligatoires pour une observation

| Champ logique | Description | Exemple fictif |
|---|---|---|
| observationId | Identifiant stable de l'observation | `obs-000042` |
| patientId | Référence interne du patient | `pat-demo-004` |
| encounterId | Séjour concerné | `enc-demo-2026-014` |
| monitoringSessionId | Session de surveillance en cours | `ms-rea-004-02` |
| deviceId / channelId | Appareil et canal source | `mon-rea-04 / ECG-II` |
| code | Code interne versionné et, si disponible, code standard | `HR` + LOINC éventuel |
| display | Libellé lisible | Fréquence cardiaque |
| value / unit | Valeur et unité source/normalisée | `78 / /min` |
| observedAt | Heure attribuée à la mesure par la source | horodatage ISO 8601 |
| receivedAt | Heure de réception par le serveur | horodatage ISO 8601 |
| storedAt | Heure de persistance | horodatage ISO 8601 |
| sourceSequence | Numéro de séquence ou compteur du flux | `18425` |
| qualityStatus | Qualité technique de la mesure | `GOOD`, `SUSPECT`, `INVALID` |
| measurementMethod | Méthode/senseur si connue | `ECG`, `PPG`, `NIBP` |
| sourceReference | Jeu de données, fichier, segment et échantillon d'origine | référence de rejeu |
| profileVersion | Version du profil de dispositif | `adult-icu-monitor-v1` |

Les noms ci-dessus forment un modèle conceptuel. Ils ne constituent pas un schéma SQL définitif.

## 5. Données numériques et courbes : ne pas confondre

- **Courbe brute :** série ordonnée d'échantillons, avec fréquence et temps d'échantillonnage.
- **Valeur dérivée :** résultat calculé par un appareil ou un algorithme à partir d'un signal (par exemple HR à partir de l'ECG).
- **Valeur intermittente :** résultat de mesure ponctuelle (par exemple NIBP).
- **Tendance :** valeur agrégée ou rééchantillonnée pour une visualisation historique.
- **Événement :** changement détecté (alarme, artefact, déconnexion, changement d'état).

Il faut conserver la relation entre une valeur dérivée et son signal source lorsqu'elle est disponible, sans prétendre recalculer les mesures comme le ferait l'appareil d'origine.

## 6. Profil de paramètres par service

Le profil de service doit sélectionner un sous-ensemble du dictionnaire plutôt que changer la définition des paramètres.

- Réanimation adulte : ECG/FC, SpO₂/PPG, respiration, PANI et/ou PAI, température ; CO₂ et données ventilatoires selon le patient.
- USC : combinaison adaptée au type de surveillance réellement prescrit et à l'organisation locale.
- Cardiologie/télémétrie : rythme/ECG et FC prioritaires ; autres mesures selon le contexte.
- Bloc/SSPI : ECG, SpO₂, NIBP/IBP, respiration, EtCO₂ et température selon le type d'anesthésie et le poste.
- Urgences/SAUV : profils variables selon l'état du patient et la phase de prise en charge.
- Pédiatrie/néonatologie : profils distincts ; ne pas reprendre les profils ni seuils adultes.

Cette liste est une carte de recherche, pas un protocole de prescription.

## 7. Références

- [H122] MIMIC-IV Waveform Database — ECG, PPG, respiration, pressions et données numériques issues de moniteurs de chevet.
- [H123] VitalDB — signaux et données numériques peropératoires.
- [H124] Barcelona SICU Signals — signaux ICU multiparamétriques et fréquences natives documentées.
- [H130] HL7 FHIR R4 — profils Observation, dont BP, HR, SpO₂, température, fréquence respiratoire.
