# Recommandations 02 — Pratiques de conception, d'organisation et de sécurité

**Version :** 0.1 — **Date :** 18 novembre 2026  
**Objectif :** traduire les normes et recommandations institutionnelles en sujets concrets à analyser et en comportements à simuler.

## 1. Recommandations métier pour le monitorage

### 1.1 Surveillance et alarmes

Le référentiel HAS version 2027 précise pour les soins critiques :
- surveillance visuelle et sonore de tous les patients ;
- procédure de gestion des systèmes de surveillance ;
- définition et adaptation des seuils d'alarme ;
- report des alarmes des moniteurs et ventilateurs ;
- professionnels formés ;
- continuité de la surveillance durant le transport [H93].

La HAS 2024 explique également comment des alarmes mal perçues, mal configurées, mal reportées ou noyées dans le bruit peuvent contribuer à des événements graves [H94].

**Pour le projet :**
- différencier alarme physiologique, technique et réseau ;
- séparer détection, signal local, report, réception, prise de connaissance, intervention et clôture ;
- rendre visible la destination de l'alarme ;
- gérer les événements non acquittés ;
- conserver les changements de configuration ;
- afficher la fraîcheur des mesures ;
- simuler la perte du chemin de report ;
- inclure une relève avec alertes ouvertes.

La norme IEC 60601-1-8 porte sur les systèmes d'alarme des appareils électromédicaux. Elle ne définit pas à elle seule le workflow humain ni l'organisation de surveillance d'un service.

### 1.2 Admission, transfert et sortie

Les systèmes centralisés du marché documentent des fonctions d'admission, sortie et déplacement. La HAS rappelle la continuité de surveillance pendant les transports.

**Pour le projet :**
- enregistrer une session de monitorage ;
- associer patient, séjour, unité, lit et appareil ;
- historiser l'affectation ;
- éviter qu'un ancien patient reste associé à son appareil ;
- gérer le changement d'un moniteur ;
- conserver la chronologie d'un transport ;
- faire apparaître les données indisponibles pendant un déplacement.

### 1.3 Continuité opérationnelle

Le référentiel HAS 2027 mentionne des plans de continuité et de reprise pour les activités critiques, l'entraînement aux attaques et les modes dégradés [H93]. Le programme CaRE de l'ANS comprend un axe de continuité et reprise d'activité ainsi qu'un axe sur les accès distants [H96].

**Pour le projet :**
- définir le comportement de chaque composant en cas de panne ;
- identifier les fonctions qui restent disponibles localement ;
- distinguer panne de moniteur, panne réseau, panne centrale et panne de base ;
- simuler la reprise et le rattrapage des données ;
- vérifier qu'une interface en retard ne présente pas de données anciennes comme actuelles ;
- documenter une procédure métier dégradée fictive.

## 2. Recommandations de sécurité

### 2.1 Gouvernance et inventaire

- identifier chaque appareil, serveur, poste, passerelle et application ;
- conserver modèle, version, propriétaire, usage et date de maintenance ;
- documenter les connexions et les flux ;
- identifier les dépendances et les accès distants ;
- retirer les comptes, services et appareils inutilisés.

Les recommandations PGSSI-S de l'ANS doivent être choisies selon le type de service et les paliers de sécurité visés [H87].

### 2.2 Identités et droits

Le référentiel HAS 2027 demande des identifiants personnels, sans comptes partagés, des règles d'habilitation, une mise à jour des accès lors des changements de statut et une authentification renforcée à deux facteurs pour les accès distants [H93].

**Pour le projet :**
- comptes individuels fictifs ;
- rôles distincts ;
- moindre privilège ;
- révocation de compte ;
- authentification des clients simulateurs ;
- journalisation des actions sensibles ;
- test d'accès à un patient hors périmètre.

### 2.3 Réseau

- segmenter les zones logiques ;
- n'autoriser que les flux nécessaires ;
- séparer les chemins d'administration et les chemins de monitorage ;
- documenter la destination et la nature de chaque flux ;
- surveiller les communications anormales ;
- éviter les accès Internet directs depuis les simulateurs et services du laboratoire.

IEC 80001-1 est la référence d'étude pour la gestion des risques de réseaux qui intègrent des dispositifs médicaux. Le POC doit s'en inspirer sans déclarer une conformité normative.

### 2.4 Logiciel et mises à jour

- définir des versions reproductibles ;
- inventorier les dépendances ;
- maintenir les composants et systèmes ;
- vérifier l'intégrité des artefacts de déploiement ;
- centraliser la gestion des secrets ;
- séparer les environnements de développement, test et démonstration ;
- prévoir une procédure de correction et de retour arrière.

IEC 62304 et IEC 81001-5-1 fournissent des références de cycle de vie logiciel et de sécurité pour les logiciels médicaux/de santé, selon le statut et le périmètre du produit.

### 2.5 Données et confidentialité

- utiliser des identifiants fictifs ;
- ne pas importer de dossiers réels ;
- minimiser les données ;
- ne pas stocker de secrets dans les logs ;
- protéger les sauvegardes ;
- limiter les exports ;
- contrôler l'accès et l'utilisation des données ;
- définir une politique de conservation et de suppression adaptée.

La CNIL rappelle que la sécurité doit être adaptée à la sensibilité du traitement et fournit un guide opérationnel pour l'authentification, les habilitations, les postes, les réseaux, les serveurs, la journalisation, les sauvegardes et les incidents [H92].

### 2.6 Réponse à incident

Prévoir des scénarios non destructifs :
- compte compromis simulé ;
- appareil inconnu ;
- message altéré ;
- service indisponible ;
- base inaccessible ;
- sauvegarde restaurée ;
- accès distant refusé ;
- tentative d'export non autorisé.

Le référentiel HAS 2027 attend que les établissements s'entraînent aux incidents, sachent reconnaître les attaques et disposent de plans de continuité et reprise [H93].

## 3. Recommandations d'ergonomie et de facteurs humains

Les exigences humaines ne sont pas secondaires : une centrale peut recevoir les bonnes valeurs et rester dangereuse si l'information est mal présentée ou si les alarmes ne sont pas comprises.

À étudier :
- identité et localisation du patient constamment visibles ;
- différence nette entre donnée récente, ancienne et absente ;
- hiérarchie visuelle cohérente ;
- code couleur non utilisé comme seul moyen de distinction ;
- distinction entre alarme, défaut technique et message d'information ;
- affichage de la source et de l'heure ;
- accès rapide à la vue détaillée du patient ;
- gestion explicite de l'acquittement ;
- retour visuel après action ;
- prévention des clics accidentels ;
- contrôle des changements d'alarme ;
- tests utilisateurs avec des scénarios de relève, de transport et d'alertes simultanées.

IEC 62366-1 fournit un processus d'ingénierie de l'aptitude à l'utilisation des dispositifs médicaux. Pour notre POC, on peut en reprendre l'esprit pour identifier les erreurs d'usage et tester les interfaces, sans revendiquer de conformité.

## 4. Recommandations de performance et de fiabilité

Ne pas écrire simplement « temps réel ». Définir les événements de référence et mesurer séparément :
- émission du message ;
- réception par le serveur ;
- validation ;
- persistance ;
- diffusion vers l'interface ;
- rendu visible ;
- réception d'une alerte ;
- prise de connaissance.

Indicateurs :
- latence médiane, p95 et p99 ;
- débit soutenu et débit de pointe ;
- pertes, doublons et rejets ;
- retard de rattrapage ;
- temps de détection d'une déconnexion ;
- durée d'indisponibilité ;
- temps de restauration ;
- fraîcheur des données affichées ;
- nombre d'alarmes ouvertes / non acquittées.

Les objectifs numériques doivent venir du contexte métier choisi et d'une configuration de test explicitement décrite.

## 5. Recommandations sur les preuves

Pour chaque exigence future, conserver :
- source ou entretien ;
- besoin métier associé ;
- risque traité ;
- composant responsable ;
- test prévu ;
- résultat du test ;
- décision et justification.

Une fonction n'est pas « validée » parce qu'elle fonctionne une fois en démonstration. Il faut un scénario répétable et un critère de succès explicite.

## 6. Références

- HAS, référentiel de certification version 2027 [H93].
- HAS, Flash Sécurité Patient surveillance en soins critiques 2024 [H94].
- ANSM, rapport de gestion des alarmes 2019 [H95].
- ANS, PGSSI-S [H87].
- ANS, programme CaRE [H96].
- CNIL, guide de sécurité des données personnelles 2024 [H92].
- IEC 60601-1-8, IEC 80001-1, IEC 62366-1, IEC 62304, IEC 81001-5-1 [H67, H76, H74, H75, H77].
