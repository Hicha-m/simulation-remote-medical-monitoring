# Workflows métier — définition et scénarios

**Date :** 18 novembre 2026  
**Statut :** workflows génériques à valider avec le contexte de service choisi.

## 1. Qu'est-ce qu'un workflow ?

Un workflow métier est une suite d'étapes qui décrit **qui fait quoi, à quel moment, à la suite de quel événement et avec quel résultat attendu**.

Ce n'est pas :
- une classe Java ;
- une route HTTP ;
- un protocole réseau ;
- une maquette d'écran.

C'est la description du fonctionnement réel à représenter. Elle sert ensuite à concevoir l'interface, le serveur, la base de données et les tests.

Exemple simple : quand un patient arrive dans une unité, quelqu'un doit vérifier son identité, l'affecter à un lit, associer le moniteur, vérifier les mesures et s'assurer que la centrale reçoit les données.

## 2. Workflow A — Admission et association patient / appareil

**Déclencheur :** admission ou arrivée d'un patient dans un service.

| Ordre | Acteur | Action | Résultat attendu |
|---:|---|---|---|
| 1 | Système administratif simulé | Crée ou retrouve le patient et le séjour. | Identifiants patient et séjour disponibles. |
| 2 | Personnel du service | Affecte le patient à une unité et un lit. | Localisation de référence définie. |
| 3 | Personnel du service | Sélectionne l'appareil destiné au patient. | Appareil connu, disponible et compatible avec le profil simulé. |
| 4 | Personnel du service | Associe l'appareil à la session de surveillance. | Lien patient / séjour / lit / appareil / session créé. |
| 5 | Appareil simulé | Envoie son état et ses premières observations. | La centrale reçoit les données avec le bon contexte. |
| 6 | Personnel du service | Vérifie le bon patient, la bonne localisation et l'affichage. | Session utilisable et contrôle tracé. |

**Exceptions à simuler :** appareil déjà affecté, patient inconnu, identifiant ambigu, lit occupé, message envoyé avant association et session précédente non clôturée.

## 3. Workflow B — Réception et affichage d'une mesure

**Déclencheur :** un appareil produit une nouvelle mesure.

| Ordre | Acteur / composant | Action | Résultat attendu |
|---:|---|---|---|
| 1 | Appareil simulé | Produit une mesure horodatée. | Message avec identifiant, paramètre, valeur, unité et qualité. |
| 2 | Serveur d'ingestion | Authentifie la source et valide le contrat. | Message accepté ou rejeté avec motif. |
| 3 | Serveur de contexte | Vérifie l'association patient / séjour / appareil. | Pas de mélange entre patients. |
| 4 | Traitement | Gère doublons, retards et ordre des mesures. | Historique cohérent. |
| 5 | Persistance | Enregistre la mesure et sa provenance. | Mesure consultable après redémarrage contrôlé. |
| 6 | Distribution | Publie la nouvelle donnée à l'interface. | Vue patient et vue multi-patients actualisées. |
| 7 | Interface | Affiche valeur, unité, heure et fraîcheur. | L'utilisateur distingue donnée récente et donnée ancienne. |

## 4. Workflow C — Déclenchement et traitement d'une alarme

**Déclencheur :** un appareil ou une règle de simulation produit une alarme.

| Ordre | Acteur / composant | Action | Résultat attendu |
|---:|---|---|---|
| 1 | Appareil ou moteur de simulation | Déclenche l'alarme. | Événement unique avec origine et heure. |
| 2 | Serveur | Valide et transmet l'événement. | Le bon contexte patient et appareil est conservé. |
| 3 | Centrale | Affiche l'alarme selon la priorité simulée. | L'alarme est visible et non confondue avec une simple mesure. |
| 4 | Personnel habilité | Prend connaissance de l'alarme. | Identité de l'acteur et heure enregistrées. |
| 5 | Personnel habilité | Acquitte l'alarme. | L'état devient « acquittée », mais l'alarme peut rester active. |
| 6 | Personnel / appareil simulé | La condition disparaît ou le défaut est corrigé. | Événement de résolution. |
| 7 | Centrale | Archive le cycle de vie. | Déclenchement, affichage, acquittement et résolution consultables. |

Le rapport ANSM recommande que l'alarme appropriée soit déclenchée au bon moment, reçue par le bon opérateur et suivie d'une réponse appropriée dans un délai adapté [H95]. Il signale également le risque de fatigue lié aux fausses alarmes ou alarmes non pertinentes [H95].

Pour le POC, il faut simuler les étapes et les états sans décider de seuils médicaux ni prétendre définir la conduite clinique.

## 5. Workflow D — Transfert d'un patient

**Déclencheur :** décision de déplacer le patient vers une autre chambre, un autre service ou une zone d'examen.

| Ordre | Acteur | Action | Résultat attendu |
|---:|---|---|---|
| 1 | Personnel / système administratif | Déclare le transfert. | Événement de mouvement avec origine et destination. |
| 2 | Personnel | Vérifie le moyen de surveillance utilisé pendant le mouvement. | Appareil de transport ou continuité explicitement définie. |
| 3 | Système | Met à jour le lieu du patient et la session correspondante. | Localisation courante sans effacer l'historique. |
| 4 | Appareil | Continue ou reprend la transmission selon le scénario. | Mesures rattachées à la session correcte. |
| 5 | Personnel du service d'accueil | Reçoit le patient et vérifie le contexte. | Nouvelle affectation confirmée. |
| 6 | Système | Clôture l'ancienne affectation et conserve la nouvelle. | Aucune donnée postérieure au transfert n'est attribuée à l'ancien lit. |

Le parcours SSPI et les transports de patients de soins critiques donnent des exemples documentés où la continuité du monitorage pendant le déplacement est importante [H03, H106].

## 6. Workflow E — Déconnexion et reprise d'un appareil

**Déclencheur :** perte du réseau, arrêt d'un appareil ou déconnexion d'un capteur.

1. L'appareil signale son changement d'état si la liaison fonctionne encore.
2. Si le serveur ne reçoit plus de message, il détecte l'absence de nouvelles données selon le délai défini par le profil.
3. La centrale marque les données comme périmées et l'appareil comme potentiellement déconnecté.
4. Elle conserve la dernière mesure avec son horodatage ; elle ne l'affiche pas comme valeur actuelle.
5. L'appareil se reconnecte.
6. Le système distingue nouvelles données, données retardées et doublons éventuels.
7. La reprise est journalisée.

La durée au-delà de laquelle un appareil est considéré comme silencieux reste un paramètre à fixer par profil ; ne pas la coder arbitrairement comme règle universelle.

## 7. Workflow F — Sortie et remise à disposition d'un appareil

**Déclencheur :** transfert définitif ou sortie du patient.

1. Le séjour ou la session de surveillance est terminé.
2. La relation patient / appareil est clôturée avec une date et un auteur.
3. Les flux futurs de cet appareil ne sont plus associés à l'ancien patient.
4. L'historique des observations et alarmes est conservé.
5. L'appareil passe dans un état distinct : disponible, nettoyage, maintenance ou hors service.
6. Une nouvelle affectation nécessite une nouvelle session.

## 8. Workflow G — Changement d'équipe et configuration

**Déclencheur :** relève, changement d'affectation ou modification de configuration simulée.

- La liste des patients et appareils actifs est revue.
- Les alarmes actives non résolues restent visibles.
- Les changements de paramètres de simulation sont attribués à un acteur.
- L'ancienne et la nouvelle configuration sont historisées.
- La centrale ne doit pas effacer une alarme active simplement parce que l'utilisateur change.

La HAS souligne l'importance de la vérification de la surveillance et de la formation en soins critiques [H02].

## 9. Comment transformer un workflow en logiciel

Pour chaque workflow, on pourra ensuite produire :

1. un diagramme de séquence (acteurs et messages) ;
2. un diagramme d'états (patient, appareil, session ou alarme) ;
3. les données nécessaires ;
4. les règles de validation ;
5. les cas d'erreur ;
6. les tests d'acceptation.

Il est prématuré de choisir les classes Java ou les endpoints avant d'avoir stabilisé ces workflows.
