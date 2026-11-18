# Architecture technique 04 — Données et intégration au SIH

**Version :** 0.1 — **Date :** 18 novembre 2026

## 1. Les données ne sont pas toutes de même nature

| Famille | Exemple | Usage |
|---|---|---|
| Identité patient | Identifiant patient, identité administrative | Rattacher les données à la bonne personne. |
| Séjour / ADT | Admission, transfert, sortie, unité, lit | Maintenir le contexte d'affectation. |
| Données physiologiques | FC, PA, SpO₂, FR, température | Suivi des paramètres mesurés. |
| Courbes | ECG, pléthysmogramme, respiration | Visualisation temporelle des signaux. |
| Événements | Alarme, défaut capteur, déconnexion | Supervision et historique des événements. |
| Métadonnées appareil | Modèle, identifiant, configuration, version | Gestion du parc et interprétation des flux. |
| Données d'exploitation | Journal système, maintenance, état serveur | Diagnostic, cybersécurité et continuité. |

## 2. Admission, transfert et sortie (ADT)

Les mouvements patient sont importants dans les systèmes de monitorage. GE documente l'import de données ADT du système hospitalier vers le réseau de monitorage afin de limiter les erreurs de saisie.

Cela peut permettre de rapprocher l'identité administrative du patient de son lit et du moniteur associé.

Il reste nécessaire de vérifier :
- qui est la source de vérité de l'identité ;
- comment sont gérées les homonymies ;
- comment le transfert est répercuté vers les moniteurs ;
- comment les erreurs d'association sont corrigées ;
- comment la session précédente est clôturée ;
- comment le système réagit en cas d'indisponibilité du SIH.

## 3. HL7 et IHE PCD

Plusieurs fournisseurs annoncent des échanges HL7 ou IHE HL7 vers les systèmes hospitaliers.

HL7 v2 est fréquemment utilisé pour des échanges d'observations et d'informations administratives. Les profils IHE PCD décrivent des transactions d'interopérabilité entre dispositifs de soins et systèmes d'information.

Cependant, un système peut employer un protocole propriétaire pour communiquer entre moniteur et centrale, puis utiliser HL7 uniquement pour exporter certaines informations vers le SIH.

**Il ne faut donc pas assimiler HL7 à l'intégralité du protocole temps réel du moniteur.**

## 4. FHIR

FHIR peut servir à représenter des ressources structurées telles que Patient, Device, Observation et Provenance.

Il peut être étudié comme format de représentation ou interface d'interopérabilité du POC. Il n'est pas démontré par les sources consultées que tous les flux des centrales actuelles soient nativement échangés en FHIR.

## 5. Archivage et traçabilité

Les systèmes peuvent archiver les tendances, courbes, événements, rapports et historiques. Il faut déterminer :
- ce qui est conservé sur le moniteur ;
- ce qui est conservé à la centrale ;
- ce qui est envoyé au DPI ;
- ce qui est archivé séparément ;
- la durée de conservation applicable ;
- les droits d'accès à l'historique ;
- le statut de la donnée (brute, calculée, validée ou exportée).

## 6. Sources

- [H40] GE CARESCAPE Gateway, ADT, HL7, NTP et flux XML : https://www.gehealthcare.com/-/media/86efd534d0c94edb831beacde0c0f7eb.pdf
- [H45] Mindray BeneVision CMS, eGateway / IHE HL7 : https://www.mindray.com/content/dam/xpace/en/resources/brochure/BeneVision_CMS.pdf
- [H46] IHE Devices Technical Framework Rev. 11.0 : https://profiles.ihe.net/DEV/index.html
- [H47] HL7 FHIR Observation : https://www.hl7.org/fhir/observation.html
