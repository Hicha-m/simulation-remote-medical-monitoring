# Méthodologie de réalisation — DEV → Docker → Metrics

**Projet :** système de monitorage hospitalier  
**Échéance :** 8 janvier 2027  
**Équipe :** Hicham, Omar et Nawfel (3 personnes)  
**Contrainte technique confirmée :** programmation réseau en Java ; autres technologies libres.  
**Statut :** méthode de travail adaptée à une équipe de trois.

## Principe

Le projet sera réalisé selon trois grandes phases successives, inspirées des consignes du dépôt [OmarBenje/Intern — docs/consignes](https://github.com/OmarBenje/Intern/tree/master/docs/consignes).

1. **DEV** — concevoir et développer l'application complète, la faire fonctionner localement et valider les parcours métier.
2. **Docker** — reconstruire et exécuter la même application dans une infrastructure conteneurisée et reproductible.
3. **Metrics** — mesurer le fonctionnement, la charge, la latence, l'intégrité des flux, la disponibilité et les limites du système.

La méthode de référence comporte également une phase de déploiement sur machines virtuelles entre DEV et Docker. Elle n'est pas retenue comme phase obligatoire dans notre plan actuel : le choix pourra être réexaminé si le tuteur ou les objectifs de comparaison l'exigent.

## Documents

- [DEV — Analyse, conception, développement et intégration](DEV.md) — étapes 1 à 6.
- [Docker — Conteneurisation et infrastructure](Docker.md) — étapes 7 à 10.
- [Metrics — Instrumentation, campagnes et analyse](Metrics.md) — étapes 11 à 14.
- [CI/CD — Intégration et livraison continues](CI-CD.md) — processus transversal aux trois phases.

## Logique de passage entre phases

| Passage | Conditions de sortie |
|---|---|
| Cadrage → DEV | Services, utilisateurs, fonctionnalités, parcours et exigences prioritaires validés. |
| DEV → Docker | Application locale intégrée, parcours nominaux validés, tests P0 passants, configuration externalisée, procédure locale documentée. |
| Docker → Metrics | Environnement Compose reproductible, données persistantes, santé des services vérifiée, même scénario exécutable après redémarrage. |
| Metrics → Livraison | Campagnes reproductibles, résultats bruts conservés, limites explicitées, incidents critiques corrigés ou documentés. |

## CI/CD : transversal et progressif

La CI/CD n'est pas reportée à la fin :
- dès DEV : vérifications automatiques à chaque Pull Request, tests, analyse statique et contrôle des dépendances ;
- pendant Docker : construction des images, tests d'intégration via Compose, vérification de la configuration et publication versionnée ;
- pendant Metrics : campagnes courtes de non-régression automatisées et campagnes de charge contrôlées, déclenchées séparément ;
- à la livraison : version candidate identifiée, procédures vérifiées et artefacts reproductibles.

## Règles de méthode

Chaque étape doit présenter :
1. un objectif précis ;
2. des prérequis ;
3. le travail demandé ;
4. les vérifications à effectuer ;
5. les livrables ;
6. les critères permettant de passer à l'étape suivante.

Les exemples de métriques ou de configurations ne sont pas des résultats. Les valeurs cibles seront fixées par l'équipe à partir des besoins argumentés et des essais mesurés ; le tuteur peut être sollicité pour avis.

## Documents de référence du projet

- [Analyse et contexte hospitalier](../analyse/monitorage-hospitalier/README.md)
- [Domaines médicaux approfondis](../analyse/monitorage-hospitalier/12-domaines-medicaux-approfondis/README.md)
- [Cadrage et questionnaires](../analyse/monitorage-hospitalier/13-pilotage-projet/README.md)
- [Planning Gantt générique](../analyse/monitorage-hospitalier/13-pilotage-projet/03-gantt-generique.md)
- [Stratégies et arbitrages critiques](../analyse/monitorage-hospitalier/13-pilotage-projet/04-strategies-et-arbitrages-critiques.md)

## Référence méthodologique

La structure s'inspire des documents DEV, Docker et Metrics de [OmarBenje/Intern](https://github.com/OmarBenje/Intern/tree/master/docs/consignes). Le contenu, les exigences médicales, les tests et les critères de sortie sont adaptés à notre projet ; les contraintes propres au projet de notes de cours ne sont pas reprises.
