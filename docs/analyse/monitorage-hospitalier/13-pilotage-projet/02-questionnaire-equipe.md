# 02 — Questionnaire d'organisation de l'équipe de trois

**Version :** 1.1 — **Date :** 25 novembre 2026  
**Équipe :** Hicham, Omar et Nawfel.  
**Échéance commune :** 8 janvier 2027.

Ce document est à remplir par Hicham, Omar et Nawfel. Il sert à rendre visibles les disponibilités, compétences et responsabilités. Les rôles ne sont pas préattribués : l'équipe les choisit elle-même. Il y a quatre chantiers fonctionnels pour trois personnes ; un membre peut donc être responsable de plusieurs chantiers, avec une relecture croisée.

## 1. Disponibilité réelle

Les trois membres identifiés sont Hicham, Omar et Nawfel. Les réponses de disponibilité restent à compléter par chacun.

### 1.1 Fiche individuelle

À compléter par chaque membre.

| Information | Hicham | Omar | Nawfel |
|---|---|---|---|
| Nom / identifiant | Hicham | Omar | Nawfel |
| Heures disponibles par semaine | | | |
| Disponibilités en semaine | | | |
| Disponibilités le week-end | | | |
| Indisponibilités / examens / vacances | | | |
| Disponibilité du 21 décembre au 4 janvier | | | |
| Présence possible le 7-8 janvier | | | |
| Préférence : backend / UI / réseau Java / données / tests / documentation | | | |

**Question à poser à chacun :** « Combien d'heures réalistes peux-tu consacrer au projet chaque semaine, en tenant compte des cours, examens, fêtes et autres engagements ? »

## 2. Compétences et appétences

Évaluer chaque domaine de 1 (débutant) à 5 (autonome/expérimenté).

| Domaine | Hicham | Omar | Nawfel |
|---|---:|---:|---:|
| Java / JVM | | | |
| Programmation réseau en Java | | | |
| Autres langages | | | |
| Backend / API | | | |
| Interface desktop | | | |
| Interface web | | | |
| SQL / modélisation BDD | | | |
| Séries temporelles / signaux | | | |
| Données médicales / recherche documentaire | | | |
| Cybersécurité | | | |
| Tests automatisés | | | |
| Docker / déploiement / CI | | | |
| Git / revue de code | | | |
| Documentation / présentation | | | |

**Question :** « Quel domaine souhaites-tu prendre en responsabilité et quel domaine veux-tu éviter ou apprendre ? »

Réponses : ....................................................................

## 3. Répartition des responsabilités

Les quatre chantiers proposés ci-dessous sont des domaines de responsabilité, pas des silos. Avec trois membres, un responsable peut prendre plusieurs chantiers ; les revues et tâches transversales doivent être partagées.

| Chantier | Responsable principal | Binôme / relecteur | Périmètre et livrables |
|---|---|---|---|
| Domaine médical, données et simulation des moniteurs | | | Profils médicaux, datasets, rejeu, données synthétiques, qualité |
| Serveur, réseau et communication temps réel | | | Réception, protocoles, sessions, fiabilité, événements |
| Modèle de données, persistance et sécurité | | | Entités, BDD, historiques, comptes, droits, audit |
| Interface centrale et parcours utilisateur | | | Multi-lits, patient, courbes, alarmes, états, administration |

**Questions :**
1. Chaque domaine possède-t-il un responsable clairement identifié ?
2. Qui peut remplacer le responsable si celui-ci est indisponible ?
3. Quelles tâches doivent être réalisées à deux pour partager le savoir ?
4. Qui est responsable de l'intégration globale et de la livraison ?
5. Qui prépare les scénarios de démonstration et les données d'exemple ?

**Règle proposée :** chaque chantier a un responsable, un relecteur et au moins une documentation permettant à un autre membre de reprendre le travail.

## 4. Interfaces communes avant développement

À définir ensemble avant de coder les modules parallèlement.

- [ ] Identifiants communs : patient, séjour, lit, appareil, session, observation, waveform, alarme.
- [ ] Modèle d'événement et format d'un message.
- [ ] Convention d'horodatage et de fuseau.
- [ ] Unités et codes des paramètres.
- [ ] États de qualité des mesures.
- [ ] Cycle de vie des alarmes.
- [ ] Contrat des API serveur ↔ interface.
- [ ] Gestion des erreurs et réponses.
- [ ] Authentification et rôles.
- [ ] Politique de versionnement des contrats.

**Question :** « Quelles interfaces doit-on verrouiller ensemble avant que les développements se séparent ? »

Réponse / décisions : ..........................................................

## 5. GitHub et intégration

Décider explicitement :

| Sujet | Choix de l'équipe |
|---|---|
| Branche principale | |
| Stratégie de branches | |
| Convention de nommage | |
| Pull Request obligatoire ? | |
| Nombre de relecteurs | |
| Tests obligatoires avant merge | |
| Format des commits | |
| Gestion des conflits | |
| Protection de main | |
| Issues / Projects / milestones | |
| Gestion des versions et releases | |

**Questions :**
- Qui peut fusionner dans la branche principale ?
- Une fonctionnalité est-elle considérée terminée avant intégration et tests ?
- Que fait-on lorsqu'une PR bloque l'intégration ?
- Comment synchronise-t-on les contrats et les migrations de base de données ?

## 6. Réunions et communication

| Rituel | Fréquence proposée | Décision |
|---|---|---|
| Synchronisation courte (blocages, tâches, prochain jalon) | 2 à 3 fois/semaine | |
| Réunion de conception/arbitrage | 1 fois/semaine | |
| Démonstration intégrée | 1 fois/semaine | |
| Revue planning / risques | 1 fois/semaine | |
| Préparation tuteur | aux jalons convenus | |

**Canal principal :** ____________________  
**Lieu de suivi des tâches :** ____________________  
**Délai attendu pour signaler un blocage :** ____________________

## 7. Règles de décision

Pour chaque choix architectural important :
1. un membre formule le problème ;
2. l'équipe liste les options ;
3. les critères et métriques sont décidés avant l'essai ;
4. un prototype ou benchmark court est réalisé si nécessaire ;
5. le résultat est présenté ;
6. la décision, ses compromis et les alternatives rejetées sont enregistrés.

**Question :** « Si deux membres ne sont pas d'accord, comment décidons-nous ? »

- [ ] Consensus obligatoire
- [ ] Vote à la majorité
- [ ] Responsable du domaine propose, équipe valide
- [ ] Référent intégration tranche après comparaison
- [ ] Autre : ____________________

**Réponse et règle de déblocage :** ............................................

## 8. Définition commune de « terminé »

Une tâche n'est considérée terminée que lorsque les éléments retenus sont satisfaits :

- [ ] Code intégré à la branche cible.
- [ ] Tests unitaires ou cas de vérification associés exécutés.
- [ ] Test d'intégration si un autre composant est concerné.
- [ ] Gestion des erreurs et cas limites.
- [ ] Documentation mise à jour.
- [ ] Démonstration reproductible.
- [ ] Relecture effectuée.
- [ ] Aucun secret, fichier patient réel ou donnée sensible dans le dépôt.

**Éléments supplémentaires :** .................................................

## 9. Gestion des retards et des risques

**Questions :**
- À partir de quel retard demande-t-on de l'aide ?
- Quelle tâche peut être réduite sans remettre en cause le résultat ?
- Qui prend en charge une tâche critique bloquée ?
- Quelle fonctionnalité doit être gelée en premier si le planning dérive ?
- Quelle disponibilité minimale faut-il garantir la dernière semaine ?

**Plan de secours choisi :** ...................................................

## 10. Synthèse d'équipe à valider

| Décision | Valeur retenue |
|---|---|
| Objectif commun au 8 janvier | |
| Périmètre minimal garanti | |
| Responsable intégration | |
| Responsables des quatre chantiers | |
| Disponibilité hebdomadaire totale | |
| Réunions prévues | |
| Outil de suivi | |
| Règles Git | |
| Processus d'arbitrage | |
| Plan en cas de retard | |
