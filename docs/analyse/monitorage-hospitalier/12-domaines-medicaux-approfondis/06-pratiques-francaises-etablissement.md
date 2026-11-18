# 06 — Pratiques françaises et fonctionnement d'un établissement

**Version :** 1.0 — **Date :** 18 novembre 2026  
**Objectif :** ancrer le modèle dans les pratiques françaises, tout en identifiant ce qui doit être confirmé localement.

## 1. Ce que le cadre français permet d'établir

Les sources françaises disponibles permettent d'affirmer les principes suivants, mais pas de décrire une organisation unique valable dans tous les hôpitaux :

- La surveillance en soins critiques s'appuie sur une organisation de service, du matériel, des procédures, la formation du personnel et une présence organisée autour de la centrale [H128].
- Le réglage des alarmes doit être adapté au patient et vérifié à l'admission et à la prise de poste dans le cadre décrit par la HAS [H128].
- Les alarmes techniques, le report, la concentration d'alarmes et la fatigue liée aux alarmes sont des enjeux de sécurité documentés par l'ANSM [H129].
- L'identification fiable du patient est un enjeu transversal à toutes les étapes du parcours ; l'INS et le RNIV structurent les règles françaises d'identitovigilance [H126, H127].
- Le dossier patient comporte des dimensions administratives et médicales ; le monitorage ne doit pas se substituer à l'ensemble du DPI [H126].
- Les systèmes d'information hospitaliers doivent intégrer des contraintes de disponibilité, de sécurité, de continuité, d'interopérabilité et de traçabilité ; le contexte d'établissement doit être étudié avec la DSI, le biomédical et les équipes de soins.

## 2. Organisation fonctionnelle à documenter avec le service

| Sujet | Question terrain précise | Pourquoi le projet en dépend |
|---|---|---|
| Admission | Qui crée le séjour, confirme l'identité et affecte le patient au lit ? | Initialisation du contexte de surveillance. |
| Mise en monitorage | Qui branche le moniteur, démarre la session et confirme le bon patient ? | Évite les associations erronées. |
| Paramétrage patient | Qui définit les paramètres suivis et limites d'alarme ? | Configuration individualisée. |
| Poste central | Qui surveille la centrale et combien de lits sont sous son périmètre ? | Routage, vues multi-lits et charge humaine. |
| Alarme | Qui reçoit le signal au chevet et à la centrale ? | Destinataires et escalade. |
| Réponse | Comment la prise en compte et la résolution sont-elles tracées ? | Cycle de vie d'une alarme. |
| Relève | Comment les patients, alarmes ouvertes et incidents sont-ils transmis ? | Continuité entre équipes. |
| Transfert | Qui clôt l'ancienne affectation et qui démarre la nouvelle ? | Continuité de monitorage et historique. |
| Maintenance | Comment un appareil est-il retiré, remplacé et remis en service ? | Inventaire et statut dispositif. |
| Incident central/réseau | Quelle procédure locale s'applique en mode dégradé ? | Continuité et gestion des pertes. |
| Formation | Quelle formation existe pour les moniteurs et centrales ? | Compétences et erreurs d'utilisation. |
| Gouvernance | Qui peut modifier les limites, destinataires et profils ? | Habilitations et audit. |

## 3. Questions spécifiques aux pratiques françaises

À confirmer auprès du tuteur ou d'un professionnel :

1. Le service de référence est-il organisé autour d'une centrale unique, de plusieurs centrales ou d'une organisation répartie ?
2. Qui est responsable de la surveillance à la centrale et qui reste responsable au chevet ?
3. Le personnel reçoit-il les alarmes sur des terminaux mobiles, des répétiteurs, les autres moniteurs ou seulement la centrale ?
4. Existe-t-il une règle locale d'escalade si une alarme n'est pas prise en compte ?
5. Quelles étapes de vérification sont effectuées à l'admission, à chaque changement de patient et à chaque relève ?
6. Quel système administratif alimente les mouvements patient (admission, transfert, sortie) ?
7. Les observations du monitorage sont-elles archivées dans la centrale, le dossier patient, un serveur de données ou plusieurs systèmes ?
8. Quels équipements sont généralement intégrés au système central (moniteurs, respirateurs, anesthésie, pompes) ?
9. Comment les appareils sont-ils inventoriés et suivis par le biomédical ?
10. Quelles procédures s'appliquent lors de la perte du réseau, de l'alimentation, de la centrale ou d'un serveur ?
11. Quel niveau de données reste disponible localement au moniteur lorsque la centrale est indisponible ?
12. Comment les limites d'alarme et les profils sont-ils adaptés aux patients et contrôlés ?
13. Quels événements doivent être tracés pour reconstituer un incident ?
14. Quelles particularités diffèrent réellement entre les services choisis ?

## 4. Interopérabilité et systèmes français

Le système hospitalier peut comporter des fonctions distinctes :
- DPI / dossier patient ;
- ADT (admission, déplacement, sortie) ;
- système de monitorage et centrale ;
- systèmes de résultats biologiques et d'imagerie ;
- annuaire et gestion des identités professionnelles ;
- supervision réseau et sécurité ;
- outils de maintenance biomédicale.

Les standards et référentiels à examiner selon le flux réel comprennent HL7 v2, HL7 FHIR, IHE PCD, IEEE 11073, CI-SIS, LOINC et UCUM [H88, H130, H131]. La simple mention d'un standard dans le dossier ne signifie pas que le projet doit tous les implémenter.

## 5. Frontière réglementaire et sécurité

L'expression « vrai projet » signifie que la qualité d'ingénierie, le niveau de documentation et la rigueur des exigences doivent être ceux d'un projet complet. Elle ne signifie pas que le logiciel peut être utilisé sur des patients ou raccordé à une infrastructure hospitalière.

La qualification réglementaire d'un logiciel dépend notamment de sa finalité prévue et de ses fonctions. Le guide MDCG 2019-11 Rev.1 (juin 2025) précise cette analyse ; tout logiciel utilisé dans le secteur de la santé n'est pas automatiquement un dispositif médical, et le traitement de données médicales ne suffit pas à le décider [H135].

Avant toute connexion à un dispositif réel, à un DPI ou à un réseau hospitalier, il faut un accord explicite de l'établissement, une analyse de sécurité et de protection des données, une validation technique et clinique, et une clarification de la qualification réglementaire. Le présent projet ne doit pas revendiquer une conformité médicale ou une aptitude à la surveillance réelle sans ces travaux.

## 6. Références

- [H126] Ministère de la Santé, identité/identitovigilance et dossier patient.
- [H127] ANS, INS/RNIV.
- [H128] HAS, Flash sécurité patient du 25 avril 2024.
- [H129] ANSM, rapport alarmes 2019.
- [H130] HL7 FHIR Observation Profiles.
- [H131] IHE Patient Care Device.
- [H135] Commission européenne, MDCG 2019-11 Rev.1, juin 2025.
