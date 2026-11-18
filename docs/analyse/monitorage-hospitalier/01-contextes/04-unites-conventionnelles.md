# Environnement 04 — Unités de soins conventionnelles

**Version :** 0.1 — **Date :** 18 novembre 2026  
**Périmètre :** médecine, chirurgie et unités d'hospitalisation hors soins critiques.

## 1. Pratique de base : surveillance intermittente

Dans les services conventionnels, la surveillance des constantes ne repose pas nécessairement sur un moniteur multiparamétrique continu à chaque lit.

Une revue narrative publiée dans le *British Journal of Anaesthesia* décrit les observations habituelles en service général comme intermittentes, souvent à chaque relève ou avec des intervalles pouvant atteindre 4 à 6 heures selon les pratiques et les populations étudiées. Elle décrit aussi l'apparition de dispositifs portables, sans fil et continus pour les patients sélectionnés [H12].

Cette fréquence ne constitue pas une règle française universelle : elle dépend du service, du patient et des protocoles. Le point à retenir est la différence entre :
- contrôles ponctuels réalisés par le personnel avec des appareils mobiles ;
- surveillance continue par un moniteur de chevet ;
- surveillance continue avec capteur portable et transmission sans fil vers une centrale ou une application clinique.

## 2. Dispositifs rencontrés dans ce type d'environnement

| Dispositif | Usage général | Données possibles |
|---|---|---|
| Moniteur de constantes mobile | Réaliser des observations au lit, puis passer au patient suivant. | PA non invasive, SpO₂, fréquence cardiaque, température selon équipement. |
| Moniteur multiparamétrique de chevet | Surveiller en continu certains patients. | ECG, SpO₂, respiration, pression, température, selon configuration. |
| Capteur portable / wearable | Suivre des constantes sans fil chez certains patients. | Combinaison variable de FC, SpO₂, FR, température, activité, etc. |
| Centrale ou console de visualisation | Afficher les données et événements transmis par les équipements connectés. | Mesures, alarmes, états et historique selon système. |
| Dossier patient informatisé | Conserver et présenter les observations utiles au parcours de soins. | Valeurs ponctuelles, résultats et observations ; modalité d'intégration à vérifier. |

## 3. Le monitorage continu en unité conventionnelle : évolution sélective

Une revue systématique de 2024 consacrée aux essais randomisés sur les constantes en continu dans les unités non critiques conclut que les données disponibles ne démontrent pas clairement une amélioration des résultats cliniques par rapport aux soins usuels, malgré l'intérêt potentiel de la détection plus précoce. Les auteurs demandent des essais plus larges et standardisés [H13].

Une revue des expériences infirmières en 2025 identifie des avantages perçus (sentiment de sécurité, détection plus rapide), mais également des inconvénients : surcharge d'informations, stress induit par les variations, sur-surveillance, gêne du patient, défauts techniques, besoin de formation et nécessité de réduire les alarmes inutiles [H16].

Il faut donc éviter de présenter le déploiement de capteurs continus à tous les lits comme la pratique standard déjà acquise. C'est une piste et une évolution technologique dont les bénéfices dépendent de la population et de l'organisation.

## 4. Besoins métiers candidats

| ID | Besoin | Explication |
|---|---|---|
| WARD-01 | Faire des observations ponctuelles rapidement. | Le personnel circule entre plusieurs patients. |
| WARD-02 | Enregistrer les mesures avec leur date et leur contexte. | Une valeur isolée doit être rattachée au patient et à l'observation. |
| WARD-03 | Identifier les patients nécessitant une surveillance renforcée. | Le niveau de monitorage dépend de l'état et de la prescription. |
| WARD-04 | Passer d'une mesure ponctuelle à un suivi continu. | Le patient peut changer de niveau de surveillance selon le parcours. |
| WARD-05 | Éviter les interruptions dans l'observation des patients équipés. | Connexion, batterie, retrait du capteur et perte de réseau doivent être visibles. |
| WARD-06 | Gérer les alertes sans créer une surcharge ingérable. | Un volume important de notifications peut gêner le travail. |
| WARD-07 | Préserver l'interaction soignant-patient. | La technologie ne doit pas réduire le soin à l'écran et aux notifications. |
| WARD-08 | Former le personnel à l'usage et à l'interprétation du dispositif. | La formation et l'intégration du workflow sont des conditions d'usage. |
| WARD-09 | Consulter les tendances au fil du séjour. | L'évolution peut être plus informative qu'une mesure isolée. |
| WARD-10 | Documenter les actions et réévaluations. | Une alerte ou une valeur anormale doit s'inscrire dans le parcours de prise en charge. |

## 5. Scénarios utiles pour la simulation

- mesure ponctuelle lors d'une tournée ;
- saisie manuelle ou acquisition automatique ;
- patient sélectionné pour monitorage continu ;
- capteur qui se décolle ou est retiré ;
- batterie faible ;
- données manquantes ;
- mesure reçue alors que le patient a changé de chambre ;
- notification reçue sur un poste mobile ;
- accumulation de notifications ;
- soignant qui consulte la tendance avant de revoir le patient ;
- transfert vers un service de soins critiques.

## 6. Limites et questions

Les études disponibles sont hétérogènes et souvent centrées sur les patients postopératoires ou à risque. La généralisation à toutes les unités, spécialités et populations est limitée.

Questions à approfondir :
- quelles constantes sont relevées de manière intermittente dans le service visé ?
- quels patients sont équipés d'un monitorage continu et selon quelle indication ?
- quelles sont les fréquences de collecte réelles ?
- comment les mesures rejoignent-elles le dossier patient ?
- qui reçoit les alertes d'un wearable ?
- quel est le plan de réponse lorsque le réseau ou le dispositif tombe en panne ?

## 7. Sources

- **[H12]** Continuous vital sign monitoring of patients recovering from surgery on general wards: a narrative review, *British Journal of Anaesthesia*, 2024 : https://pubmed.ncbi.nlm.nih.gov/39779421/
- **[H13]** Outcomes in patients receiving continuous monitoring of vital signs on general wards: systematic review and meta-analysis of randomised controlled trials, 2024 : https://pmc.ncbi.nlm.nih.gov/articles/PMC11468343/
- **[H16]** Nurses' experiences with inhospital continuous monitoring of vital signs in general wards: a systematic review, 2025 : https://pmc.ncbi.nlm.nih.gov/articles/PMC12373230/
