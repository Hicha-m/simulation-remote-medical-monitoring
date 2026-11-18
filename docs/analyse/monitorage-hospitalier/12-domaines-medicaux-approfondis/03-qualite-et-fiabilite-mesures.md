# 03 — Qualité et fiabilité des mesures

**Version :** 1.0 — **Date :** 18 novembre 2026  
**Objectif :** empêcher qu'une mesure absente, ancienne ou techniquement douteuse soit présentée comme une mesure fiable et actuelle.

## 1. Deux axes à ne jamais confondre

Le système doit distinguer :

- **Qualité technique de la mesure :** le capteur, le signal et la chaîne d'acquisition sont-ils exploitables ?
- **Interprétation physiologique :** la valeur est-elle en dehors des limites configurées pour ce patient/profil ?

Une FC inhabituelle n'est pas automatiquement un artefact. Une SpO₂ dans une plage attendue n'est pas automatiquement fiable si le signal PPG est de mauvaise qualité.

Le statut clinique (dans les limites configurées / alarme / état à examiner) ne doit jamais remplacer le statut technique de qualité.

## 2. États de qualité proposés

| Code | Signification | Comportement interface |
|---|---|---|
| GOOD | Donnée déclarée exploitable selon les informations disponibles | Afficher normalement avec provenance et heure. |
| SUSPECT | Doute qualité ou artefact possible | Marquer visiblement ; ne pas la traiter comme fiable sans réserve. |
| INVALID | Source ou validation indique que la mesure ne doit pas être utilisée | Ne pas la remplacer par zéro ; conserver l'événement et expliquer le rejet. |
| SENSOR_OFF | Capteur déconnecté ou non détecté | Afficher l'état technique, pas une valeur physiologique nominale. |
| UNAVAILABLE | Aucune valeur disponible ou mesure non prise | Indiquer « indisponible » ; distinguer d'une valeur nulle. |
| STALE | Dernière valeur trop ancienne selon la règle de fraîcheur configurée | Afficher dernière valeur + heure, avec état périmé. |
| UNKNOWN | La source ne fournit pas assez d'informations pour conclure | Ne pas inventer un état qualité. |

La règle de passage à STALE dépend du profil d'appareil et de la cadence attendue. Elle doit être configurée et mesurée, et non définie comme une durée universelle.

## 3. Artefacts et situations à simuler

| Paramètre/capteur | Artefacts/défauts possibles | Effet logiciel à représenter |
|---|---|---|
| ECG | Électrode décollée, mauvais contact, mouvement, bruit secteur, dérive de ligne de base, saturation, câble débranché | Tracé bruité ou interrompu, qualité dégradée, état électrode/câble si connu. |
| PPG / SpO₂ | Mouvement, capteur déplacé, lumière ambiante, perfusion faible, pression ou position du capteur, signal pulsatile faible | Qualité PPG basse, SpO₂ absente/suspecte, pouls non exploitable selon la source. |
| NIBP | Brassard mal posé, fuite, mouvement, échec de cycle, mesure interrompue | Événement de mesure échouée avec raison si connue ; aucune valeur fabriquée. |
| IBP | Ligne obstruée, bulle, amortissement/résonance, zéro incorrect, transducteur déconnecté | Courbe déformée ou coupée, défaut technique distinct d'une variation physiologique. |
| Respiration par impédance | Mouvements, électrode déconnectée, interférence cardiaque | FR indisponible/suspecte et courbe annotée si possible. |
| Capnographie | Ligne de prélèvement débranchée/obstruée, fuite, eau, absence de prélèvement | Perte/altération du capnogramme et statut technique de l'appareil. |
| Température | Sonde déconnectée, emplacement différent, temps de stabilisation | Valeur indisponible ou douteuse avec site et état sonde. |

Ces cas sont des familles d'artefacts à documenter à partir des sources techniques et des jeux de données ; ils ne constituent pas une procédure de dépannage au lit du patient.

## 4. Champs qualité à conserver

- `qualityStatus` : code d'état défini ci-dessus.
- `qualityReason[]` : motif connu (motion, lead_off, low_perfusion, sensor_disconnected, signal_gap, source_flag, etc.).
- `qualitySource` : qualité déclarée par le dispositif, issue du dataset, calculée par le projet ou inconnue.
- `qualityAlgorithmVersion` : version si une estimation est calculée.
- `signalQualityIndex` : valeur numérique optionnelle ; unité/plage/définition obligatoires.
- `validFrom` / `validTo` : période de validité si la source la fournit.
- `observedAt`, `receivedAt`, `storedAt` : trois instants distincts.
- `sampleRateHz`, `sampleCount`, `missingSamples` : pour les signaux.
- `sourceSequence` et `messageId` : ordre et déduplication.

Un indice SQI calculé par le projet doit être explicitement identifié comme un indicateur expérimental, avec sa formule, son domaine de validité et sa version. Il ne doit pas se substituer silencieusement à la qualité déclarée par le moniteur.

## 5. Fraîcheur des données

La fraîcheur se calcule par rapport au dernier événement reçu et à la cadence attendue du profil, mais elle ne doit pas effacer les événements historiques.

Règles de conception :
1. conserver l'heure source et l'heure de réception ;
2. détecter les ruptures de séquence et les retards ;
3. signaler les données devenues périmées ;
4. garder la dernière valeur et son timestamp visibles, mais marquées ;
5. ne pas remplacer la dernière valeur par zéro ou une valeur précédente plus récente en apparence ;
6. ne jamais réordonner l'historique en effaçant l'ordre de réception ;
7. distinguer perte réseau, absence de mesure, capteur déconnecté et arrêt volontaire de la session.

## 6. Politique de traitement : stratégies à comparer

| Stratégie | Principe | Avantage | Risque | Mesures de comparaison |
|---|---|---|---|---|
| S1 — Tout conserver et marquer | Stocker les échantillons bruts et leurs flags ; filtrage uniquement à l'affichage | Traçabilité maximale | Volume de stockage et visualisation chargée | Volume/heure, coût CPU, temps de requête, capacité de rejeu. |
| S2 — Brut + qualité calculée | Conserver le brut et ajouter un indicateur de qualité dérivé versionné | Aide à l'analyse et à l'affichage | Faux classement GOOD/SUSPECT | Sensibilité/spécificité sur segments annotés, taux de fausses exclusions, coût de calcul. |
| S3 — Prétraiter et ne garder qu'une version corrigée | Filtrer ou rééchantillonner avant stockage principal | Moins de volume et rendu simplifié | Perte d'information et correction erronée | Erreur de reconstruction, fidélité morphologique, échantillons perdus, volume. |

**Orientation de départ : S1 ou S2.** Garder les données de référence est essentiel pour pouvoir expliquer et reproduire les résultats. Le filtrage ou le rééchantillonnage doit rester une vue dérivée, non destructive, tant que la validation n'est pas faite.

## 7. Plan de tests qualité

- QUA-01 : électrode ECG déconnectée.
- QUA-02 : ECG bruité par mouvement.
- QUA-03 : PPG de faible qualité et SpO₂ manquante.
- QUA-04 : cycle NIBP échoué.
- QUA-05 : courbe IBP interrompue ou artefactée.
- QUA-06 : paquet réseau retardé après une valeur plus récente.
- QUA-07 : paquet dupliqué.
- QUA-08 : trou de waveform avec compteur d'échantillons.
- QUA-09 : source sans flag qualité : état UNKNOWN.
- QUA-10 : dernière mesure périmée sans disparition de l'historique.
- QUA-11 : comparaison du signal original et du signal affiché.
- QUA-12 : redémarrage de la session sans fausse remise à GOOD.

## 8. Indicateurs objectifs

- pourcentage d'échantillons manquants ;
- nombre et durée des segments interrompus ;
- erreur de reconstruction après transport et stockage ;
- délai entre observation et affichage (médiane, p95, p99) ;
- délai de détection d'une mesure périmée ;
- taux de messages dupliqués ou désordonnés ;
- sensibilité/spécificité de détection d'artefacts seulement si un jeu annoté fiable existe ;
- taux de segments classés à tort GOOD ;
- consommation CPU, mémoire et stockage.

Les seuils d'acceptation doivent être fixés après un benchmark sur une configuration matérielle et un jeu de test explicitement décrits.

## 9. Références

- [H124] Barcelona SICU Signals — signaux multiparamétriques haute résolution.
- [H125] PhysioNet Challenge 2015 — détection de fausses alarmes d'arythmie et qualité des signaux.
- [H133] Revue sur les indices de qualité PPG et les artefacts de mouvement.
- [H134] Revue sur les artefacts de mouvement ECG.
