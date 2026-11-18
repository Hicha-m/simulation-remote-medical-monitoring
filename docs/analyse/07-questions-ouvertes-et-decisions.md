# 07 — Questions ouvertes et journal des décisions

**Version :** 0.1 — **Date :** 18 novembre 2026  
**Statut :** backlog de recherche ; aucune décision fonctionnelle ou technique validée.

## 1. Questions bloquantes sur le périmètre

Ces questions conditionnent une grande partie de l'analyse :

| ID | Question | Pourquoi elle est structurante | Interlocuteur ou source à solliciter |
|---|---|---|---|
| Q-001 | Le système représente-t-il des patients hospitalisés, des patients à domicile ou les deux ? | Change les acteurs, appareils, réseaux et parcours. | Encadrant du projet. |
| Q-002 | Le mot « télésurveillance » est-il employé au sens réglementaire français ? | Change le domaine métier et les contraintes applicables. | Encadrant, professionnel de santé, documentation institutionnelle. |
| Q-003 | Quels appareils les clients doivent-ils simuler ? | Détermine le comportement, les messages et les données. | Encadrant, biomédical, documentation fabricant. |
| Q-004 | Les mesures sont-elles ponctuelles, périodiques ou des signaux continus ? | Change les protocoles, volumes et stockage. | Encadrant et équipe métier. |
| Q-005 | Quelles constantes sont indispensables et lesquelles sont optionnelles ? | Détermine le modèle de données. | Encadrant et professionnel compétent. |
| Q-006 | Quelle organisation humaine doit être représentée ? | Détermine les rôles, habilitations et workflows. | Service hospitalier ou retour d'expérience documenté. |

## 2. Questions sur les mesures et appareils

- Q-007 : Les appareils ont-ils chacun un identifiant stable ?
- Q-008 : Un patient peut-il avoir plusieurs appareils ?
- Q-009 : Un appareil peut-il être réaffecté à un autre patient ?
- Q-010 : Une mesure comporte-t-elle une heure de mesure et une heure de réception ?
- Q-011 : Les messages incluent-ils qualité du signal, batterie et connectivité ?
- Q-012 : Faut-il simuler des signaux ECG ou uniquement des valeurs numériques ?
- Q-013 : Quels événements techniques peuvent rendre une mesure non exploitable ?
- Q-014 : Quelle fréquence d'émission est réaliste pour chaque famille de données ?
- Q-015 : Les paramètres doivent-ils être configurables par patient, appareil ou protocole ?

## 3. Questions sur les alertes et l'organisation

- Q-016 : Qui peut créer ou modifier les règles d'alerte ?
- Q-017 : Les alertes sont-elles techniques, métier, médicales ou plusieurs catégories distinctes ?
- Q-018 : Qui reçoit chaque catégorie d'alerte ?
- Q-019 : Quelle est la différence entre réception, visualisation, acquittement, traitement et clôture ?
- Q-020 : Existe-t-il une priorisation ou une escalade documentée ?
- Q-021 : Comment les alertes non résolues passent-elles d'une équipe à une autre ?
- Q-022 : Quelles vues sont utiles à une infirmière, à un médecin, à un coordinateur et à un administrateur ?
- Q-023 : Comment représenter les situations sans transmission ?
- Q-024 : Comment distinguer mesure aberrante, défaut de capteur et situation nécessitant une évaluation clinique ?

Aucun seuil médical ne sera fixé tant qu'une source clinique et un périmètre de responsabilité ne seront pas identifiés.

## 4. Questions réseau et performances

- Q-025 : Quel délai entre la mesure et l'affichage est attendu ?
- Q-026 : Le sujet demande-t-il du temps réel strict ou une actualisation quasi immédiate ?
- Q-027 : Quel est le volume de messages attendu et le pic à simuler ?
- Q-028 : Le client conserve-t-il localement des mesures en cas de coupure ?
- Q-029 : Le serveur doit-il gérer les doublons, messages retardés et désordonnés ?
- Q-030 : Une reconnexion doit-elle déclencher un rattrapage ?
- Q-031 : Quel comportement doit avoir le dashboard quand le serveur ou la base devient indisponible ?
- Q-032 : Quelles métriques de performance doivent figurer dans la démonstration ?

Métriques candidates : latence médiane, p95, p99, taux de perte, taux de doublons, débit soutenu, débit en pic, temps de reprise et fraîcheur affichée. Les objectifs chiffrés restent à définir.

## 5. Questions sur les données, le stockage et l'interopérabilité

- Q-033 : Quelles données doivent être historisées ?
- Q-034 : Quelle durée de conservation est pertinente pour le POC ?
- Q-035 : L'historique doit-il être consulté par patient, appareil, paramètre ou période ?
- Q-036 : Une base relationnelle suffit-elle ou existe-t-il un besoin spécifique de séries temporelles ?
- Q-037 : Le format FHIR est-il demandé, souhaitable ou hors périmètre ?
- Q-038 : Faut-il simuler des interfaces avec un dossier patient ou un système hospitalier ?
- Q-039 : Quels exports sont nécessaires ?
- Q-040 : Quelle traçabilité des transformations et de l'origine des mesures est attendue ?

## 6. Questions de sécurité

- Q-041 : Le POC sera-t-il strictement alimenté par des données synthétiques ?
- Q-042 : Quels types d'utilisateurs et quels périmètres de données faut-il distinguer ?
- Q-043 : Comment authentifier les clients simulateurs ?
- Q-044 : Quel niveau de journalisation est nécessaire pour démontrer les contrôles ?
- Q-045 : Comment gérer la révocation d'un compte ou d'un appareil ?
- Q-046 : Quelles pannes ou attaques doivent être simulées ?
- Q-047 : L'application est-elle exclusivement locale ou accessible sur Internet ?
- Q-048 : Le projet prévoit-il une hébergement tiers ou l'utilisation d'un service externe ?

## 7. Questions de réalisation et d'évaluation

- Q-049 : Quelles sont les contraintes de calendrier et de répartition du travail ?
- Q-050 : Java est-il une obligation pour tous les composants ou seulement une technologie centrale ?
- Q-051 : Une application desktop, web ou hybride est-elle attendue ?
- Q-052 : Les interfaces patient et personnel hospitalier sont-elles toutes les deux nécessaires ?
- Q-053 : Quels livrables sont évalués : code, démonstration, tests, dossier, présentation ?
- Q-054 : La priorité est-elle le réalisme opérationnel, la performance réseau, la sécurité, l'interface ou l'architecture ?
- Q-055 : Qu'est-ce qui permettra de dire objectivement que le POC est concluant ?
- Q-056 : Qui pourra relire les scénarios métier et valider qu'ils sont plausibles ?

## 8. Premières personnes à interroger

Sans supposer qu'elles sont toutes accessibles, les catégories suivantes peuvent aider à vérifier le terrain :

1. **Encadrant du projet :** interprétation attendue du sujet, critères d'évaluation, contraintes académiques.
2. **Infirmier ou infirmière :** informations utiles, charge de travail, gestion des alertes et transmissions.
3. **Médecin ou responsable de parcours :** rôle médical, niveau d'information nécessaire et limites de la simulation.
4. **Ingénieur biomédical :** appareils, flux, alarmes, affectation et maintenance.
5. **Équipe informatique hospitalière :** réseau, intégration, sécurité, identités et contraintes d'exploitation.
6. **DPO ou référent sécurité :** protection des données, habilitations, journalisation et hébergement.

Les questions doivent porter sur les processus de travail, pas sur des dossiers ou des informations médicales identifiantes.

## 9. Journal des décisions

| ID | Sujet | État | Décision | Justification / preuve | Date |
|---|---|---|---|---|---|
| DEC-001 | Contexte d'utilisation | Ouvert | Aucune | Les interprétations hospitalier / domicile / hybride sont à départager. | 18/11/2026 |
| DEC-002 | Paramètres médicaux | Ouvert | Aucune | Les mesures attendues ne sont pas détaillées. | 18/11/2026 |
| DEC-003 | Protocoles réseau | Ouvert | Aucune | Le sujet ne prescrit aucun protocole. | 18/11/2026 |
| DEC-004 | Base de données | Ouvert | Aucune | Volumes, requêtes et rétention non définis. | 18/11/2026 |
| DEC-005 | Interface graphique | Ouvert | Aucune | Type d'interface et utilisateurs à confirmer. | 18/11/2026 |
| DEC-006 | Sécurité | À cadrer | Aucune | Principes et niveau de démonstration à préciser. | 18/11/2026 |
| DEC-007 | Échelle du système | Ouvert | Aucune | Petit, moyen et large restent à comparer. | 18/11/2026 |
| DEC-008 | Valeur ajoutée | À rechercher | Aucune | Les pistes doivent être confrontées aux usages et à l'existant. | 18/11/2026 |

### Règle de gestion

Une décision n'est validée que si elle comporte :
- un choix explicite ;
- les alternatives examinées ;
- les raisons du choix ;
- les contraintes et conséquences ;
- une source ou un résultat de test lorsque cela est possible ;
- la date et les personnes ayant validé.

Une hypothèse de travail ne doit pas être convertie automatiquement en décision.
