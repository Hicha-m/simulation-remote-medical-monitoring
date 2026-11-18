# 04 — Gestion concrète des alarmes par les soignants

**Version :** 1.0 — **Date :** 18 novembre 2026  
**Objectif :** représenter le circuit humain complet d'une alarme, et pas uniquement un seuil qui change la couleur d'une valeur.

## 1. Ce que montrent les sources françaises

La HAS décrit une organisation collective : positionnement et diffusion des alarmes, procédure de réglage adaptée au patient, vérification au moment de l'admission et de la prise de poste, formation, présence à proximité de la centrale et limitation de la pollution sonore [H128].

Les retours d'expérience HAS décrivent notamment des alarmes techniques de déconnexion restées sans réponse, dans un contexte de nombreuses alarmes non vitales ou fausses, d'un report limité, d'une difficulté de configuration inter-chevet et d'un manque de formation [H128].

L'ANSM rappelle qu'une bonne gestion d'alarme suppose que l'alarme appropriée se déclenche au bon moment, soit reçue par l'opérateur approprié et provoque une réponse appropriée dans un délai adapté [H129]. Le rapport aborde également le report et la concentration des alarmes et le risque de fatigue liée aux alarmes.

Ces sources ne définissent pas une organisation identique dans tous les services. Les rôles, temporisations, niveaux et circuits exacts doivent être confirmés auprès du service de référence.

## 2. Catégories à distinguer

| Catégorie | Origine | Exemples génériques | Réponse attendue dans le logiciel |
|---|---|---|---|
| Physiologique | Valeur ou événement associé au patient | limite de FC/SpO₂/pression, événement ECG configuré | Alarme liée au patient et au paramètre, avec configuration et provenance. |
| Technique du dispositif | Moniteur, sonde ou capteur | lead-off, capteur absent, défaut batterie, mesure impossible | Défaut appareil/canal, distinct d'une alarme physiologique. |
| Communication / système | Réseau, passerelle, centrale, serveur | appareil silencieux, perte de liaison, centrale injoignable | Indiquer quelle partie du parcours de transmission est affectée. |
| Organisationnelle | Absence d'affectation ou de destinataire | aucun soignant affecté, relève non prise en compte | Signaler une lacune de routage ; ne pas inventer un destinataire. |

Une priorité doit être portée par l'événement et interprétée selon le profil/paramétrage de la source ou du service. Ne pas créer de seuil ou de priorité médicale universelle sans validation.

## 3. Cycle métier à représenter

Le système doit distinguer plusieurs étapes, qui peuvent ne pas toutes être présentes dans tous les produits ou établissements.

1. **Détection / émission locale** : le dispositif crée l'alarme.
2. **Transmission** : elle est envoyée vers la centrale ou le système de report.
3. **Réception** : le serveur ou la centrale enregistre l'événement.
4. **Notification** : le destinataire configuré est averti (console, répétiteur, terminal).
5. **Prise de connaissance (acquittement)** : un professionnel indique qu'il a vu l'alarme.
6. **Évaluation / intervention** : action humaine réalisée hors du logiciel ou tracée si le périmètre le prévoit.
7. **Résolution / fin de condition** : la condition qui a déclenché l'alarme se termine ou l'appareil la clôt.
8. **Escalade** : un autre destinataire est notifié en cas de règle non satisfaite.
9. **Clôture documentaire** : l'historique est conservé, même si l'alarme est terminée.

Le système ne doit jamais assimiler automatiquement « acquitté », « silence sonore », « condition résolue » et « intervention effectuée ».

## 4. États d'alarme proposés

| État | Sens |
|---|---|
| ACTIVE_UNACKNOWLEDGED | Condition active, pas encore acquittée. |
| ACTIVE_ACKNOWLEDGED | Condition active, prise de connaissance enregistrée. |
| NOTIFIED | Notification émise vers un ou plusieurs destinataires. |
| ESCALATED | Règle d'escalade déclenchée ; conserver le destinataire et l'heure. |
| CLEARED | Condition de déclenchement terminée selon la source ou la règle configurée. |
| SILENCED / PAUSED | Signal sonore temporairement interrompu ou suspendu, à distinguer de l'état physiologique. |
| CANCELLED | Événement invalidé/annulé selon une règle explicite et auditée. |
| COMMUNICATION_FAILED | Report vers une destination échoué ; état de transport séparé de l'état clinique. |

Un modèle d'événements historisé est préférable à l'écrasement d'un champ `status` : il permet de reconstruire qui a fait quoi, à quelle heure et sur quel terminal.

## 5. Rôles humains à modéliser

| Acteur | Responsabilités possibles à valider |
|---|---|
| Infirmier/ère du secteur | Surveillance des patients affectés, prise de connaissance, évaluation et réponse selon les procédures du service. |
| Infirmier/ère au poste central | Supervision d'un groupe de lits, réception des reports, répartition et transmission des alertes selon l'organisation. |
| Médecin | Évaluation médicale et décisions relevant de sa compétence ; le logiciel ne doit pas simuler automatiquement une décision médicale. |
| Aide-soignant / autre professionnel | Peut percevoir/transmettre une situation selon sa fonction et l'organisation locale ; ne pas lui attribuer par défaut le rôle de destinataire principal. |
| Cadre de santé / responsable d'unité | Organisation des effectifs, procédures, formation et gestion de la relève. |
| Biomédical | Maintenance, vérification, inventaire, configuration technique et incidents matériel selon l'organisation. |
| DSI / administrateur | Infrastructure, comptes, réseau, disponibilité, sauvegarde et journaux techniques. |

Le rôle « destinataire d'une alarme » doit être paramétrable et lié à une équipe/plage de service. Il ne faut pas coder en dur un schéma de responsabilités supposé universel.

## 6. Scénario de prise de poste et de relève

1. Le professionnel s'authentifie avec son compte individuel.
2. Le système affiche les lits/patients de son secteur autorisé.
3. Les appareils et sessions actuellement actifs sont visibles.
4. Les alarmes actives non résolues sont présentées avec leur état d'acquittement.
5. Les alarmes temporisées/silencées et les problèmes de communication sont explicitement signalés.
6. La relève enregistre une transmission des événements encore ouverts si cette fonction est dans le périmètre.
7. Les changements de destinataire ou d'affectation sont historisés.

La validation de la surveillance et des réglages au moment de l'admission ou de la prise de poste est explicitement signalée par la HAS pour les services concernés [H128]. Les modalités précises sont à obtenir du tuteur/professionnel.

## 7. Stratégies d'architecture d'alarme à comparer

| Option | Description | Points forts | Limites/risques |
|---|---|---|---|
| A — Alarme créée et routée par le moniteur | Le moniteur produit l'événement et le transmet avec sa priorité et ses métadonnées. | Proche du fonctionnement d'un vrai système multi-fabricants, conserve la provenance. | Simuler l'hétérogénéité des appareils et leur configuration est plus exigeant. |
| B — Calcul centralisé | Les mesures sont transmises et le serveur applique les règles de seuil/profil. | Paramétrage central, tests reproductibles, simplicité de démonstration. | Le serveur devient responsable du calcul ; risque de confondre une règle logicielle expérimentale avec une fonction du moniteur. |
| C — Hybride | Le moniteur simule ses alarmes natives et le serveur génère uniquement les alarmes système/communication ou des règles explicitement séparées. | Sépare mieux la source clinique simulée et la supervision informatique. | Contrat d'événement plus riche et gestion des doublons nécessaires. |

Ne pas décider sans prototype comparatif. Tout seuil clinique doit venir d'un profil validé, d'une documentation de source ou d'une valeur explicitement marquée comme synthétique/non clinique.

## 8. Indicateurs mesurables

- nombre d'alarmes par patient-heure et par catégorie ;
- nombre de notifications réussies/échouées ;
- latence source → centrale → terminal (médiane, p95, p99) ;
- délai de prise de connaissance simulée ;
- délai de résolution simulée ;
- nombre et taux d'escalades ;
- alarmes non acquittées à la relève ;
- temps passé en silence/pause ;
- doublons, pertes, réordonnancements ;
- proportion d'alarmes classées comme non actionnables seulement lorsqu'une annotation de référence existe.

Ne pas optimiser uniquement la réduction du nombre d'alarmes : une baisse peut masquer une perte d'alarmes pertinentes. La détection des alarmes importantes et les faux négatifs doivent être mesurés conjointement.

## 9. Scénarios de validation

- ALM-01 : alarme physiologique active non acquittée.
- ALM-02 : acquittement sans résolution.
- ALM-03 : alarme technique capteur déconnecté.
- ALM-04 : perte du report vers la centrale.
- ALM-05 : plusieurs alarmes simultanées sur plusieurs lits.
- ALM-06 : destinataire indisponible et escalade.
- ALM-07 : relève avec alarme active.
- ALM-08 : alarme mise en pause puis réactivée.
- ALM-09 : panne réseau pendant une alarme.
- ALM-10 : notification livrée en double ou hors ordre.
- ALM-11 : modification d'une limite ou d'un routage, avec audit.
- ALM-12 : événement clos, mais conservé dans l'historique.

## 10. Références

- [H128] HAS, Flash sécurité patient — surveillance des patients en soins critiques, 25 avril 2024.
- [H129] ANSM, Gestion des alarmes des dispositifs médicaux dans les établissements de santé, septembre 2019.
- [H131] IHE Patient Care Device — DEC et Alarm Communication Management.
