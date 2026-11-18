# Monitorage hospitalier — dossier de référence

**Version :** 0.1  
**Date de mise à jour :** 18 novembre 2026  
**Périmètre confirmé :** monitorage hospitalier.  
**Statut :** analyse documentaire, aucun choix d'architecture ni de technologie validé.

## Objectif

Décrire la réalité du monitorage dans les établissements de santé : environnements de soins, équipements, systèmes centralisés, métiers, parcours opérationnels, données, alarmes, intégration informatique et besoins.

Ce dossier est volontairement découpé par thème. Chaque document traite un sujet défini et possède ses propres sources. Il ne faut pas fusionner tous les résultats dans un fichier unique.

## Lire dans cet ordre

### 1. Comprendre les environnements de soins

- [Réanimation et soins critiques](01-contextes/01-reanimation-soins-critiques.md)
- [Bloc opératoire et SSPI](01-contextes/02-bloc-operatoire-sspi.md)
- [Cardiologie et télémétrie hospitalière](01-contextes/03-cardiologie-telemetrie.md)
- [Unités de soins conventionnelles](01-contextes/04-unites-conventionnelles.md)
- [Urgences et transport intrahospitalier](01-contextes/05-urgences-et-transport.md)

- [Néonatologie et pédiatrie](01-contextes/06-neonatologie-et-pediatrie.md) — surveillance cardiorespiratoire néonatale, alarmes et profils pédiatriques.

### 2. Comprendre les équipements et systèmes actuels

- [Moniteurs de chevet et moniteurs de transport](02-systemes/01-moniteurs-de-chevet.md)
- [Centrales de surveillance et systèmes centralisés](02-systemes/02-centrales-de-surveillance.md)
- [Télémétrie hospitalière sans fil](02-systemes/03-telemetrie-hospitaliere.md)
- [Intégration et interopérabilité](02-systemes/04-integration-et-interoperabilite.md)

### 3. Comprendre les métiers et opérations

- [Acteurs et responsabilités](03-metiers/01-acteurs-et-responsabilites.md)
- [Cycle de vie patient, lit et appareil](03-metiers/02-cycle-patient-lit-appareil.md)
- [Alarmes, événements et traitement](03-metiers/03-alarmes-et-traitement.md)

### 4. Transformer le terrain en besoins testables

- [Catalogue des besoins métiers](04-besoins/01-catalogue-besoins-metiers.md)
- [Scénarios et indicateurs à simuler](04-besoins/02-scenarios-et-indicateurs.md)

### 5. Sources

- [Registre des sources hospitalières](05-sources/README.md)

## Ce que le dossier établit déjà

1. En soins critiques, la surveillance continue des paramètres physiologiques est une exigence explicitement mentionnée dans le cadre français des soins critiques. La HAS détaille en outre les conditions organisationnelles de la surveillance et des alarmes [H01, H02].
2. En salle de surveillance postinterventionnelle (SSPI), le Code de la santé publique décrit les fonctions de surveillance instrumentale par poste et la continuité pendant le transfert [H03].
3. Des systèmes commerciaux de surveillance centralisée existent chez plusieurs fabricants : Philips, GE HealthCare, Dräger et Mindray. Leurs fonctions et capacités annoncées ne sont pas identiques [H06–H09].
4. La télémétrie hospitalière désigne notamment le suivi sans fil de patients mobiles, avec des mesures transmises vers une infrastructure centrale. Les pratiques d'organisation et de surveillance humaine varient selon les établissements [H10, H11].
5. En unités conventionnelles, le monitorage continu portable constitue une évolution et/ou une modalité sélective ; il ne faut pas le confondre avec les contrôles intermittents habituels [H12, H13].
6. L'enquête ANSM réalisée en 2017 auprès de 631 services a documenté les modes de report d'alarmes et leurs difficultés ; cette photographie est historique et ne doit pas être présentée comme une mesure de 2026 [H33].
7. Des marchés publics français 2023–2029 détaillent les moniteurs, centrales, logiciels, alarmes, intégration, maintenance et formation recherchés par les établissements [H34–H37].
8. Des retours d'expérience documentent un système BeneVision au CHU de Toulouse et un démonstrateur 5G à quatre lits de mannequins ; ces deux cas sont de nature différente et ne doivent pas être confondus avec une installation clinique standard [H38, H39].

## Règles de preuve

Chaque document distingue :
- **Fait réglementaire ou institutionnel** : texte ou recommandation officielle.
- **Fonction produit documentée** : caractéristique décrite par le fabricant ; cela ne prouve pas le déploiement dans un hôpital particulier.
- **Résultat d'étude** : résultat publié dans la littérature ; préciser population, contexte et limites.
- **Besoin métier déduit** : exigence candidate déduite d'un processus documenté ; elle doit être validée avec les professionnels.
- **Question ouverte** : information qui n'a pas encore été confirmée.

Ne jamais extrapoler une caractéristique produit à l'ensemble des hôpitaux. Ne jamais présenter un seuil ou un comportement simulé comme une règle clinique.

## Hors périmètre provisoire

- Télésurveillance de patients à domicile.
- Remplacement d'une centrale clinique ou d'un moniteur certifié.
- Décision ou diagnostic médical automatisé.
- Connexion à un réseau hospitalier réel.
- Utilisation de données patient réelles.

Ces limites pourront être réexaminées si le sujet académique l'exige explicitement.
