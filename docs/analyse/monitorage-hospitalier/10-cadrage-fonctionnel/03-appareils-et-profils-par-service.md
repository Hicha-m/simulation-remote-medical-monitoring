# Appareils à simuler et profils par service

**Date :** 18 novembre 2026  
**Statut :** proposition de périmètre fonctionnel ; aucune marque ni interface réelle n'est imposée.

## 1. Est-ce que le système change selon le service ?

**Oui, le système opérationnel change selon le service ; non, cela n'oblige pas à construire un logiciel complètement différent pour chaque service.**

Il faut distinguer trois niveaux :

1. **Le socle commun du système hospitalier** : identité du patient, séjour, unité, lit, appareil, réception, horodatage, stockage, supervision et journalisation.
2. **Les profils locaux du service** : types d'appareils autorisés, paramètres suivis, fréquence des données, modes de mobilité, organisation des alarmes et rôles utilisateurs.
3. **Les équipements et intégrations présents sur le terrain** : marques, modèles, centrales, réseaux, passerelles et protocoles supportés.

Un fabricant documente par exemple une centrale capable de gérer admission, sortie et déplacement de patients, moniteurs de chevet et émetteurs de télémétrie, avec affichage de paramètres et d'historiques [H04]. Cela montre qu'un socle peut servir plusieurs usages, mais ne signifie pas que tous les appareils de tous les fabricants sont automatiquement compatibles.

## 2. Profils d'équipements par service

| Service | Appareils typiques | Données / événements possibles | Profil logiciel à prévoir |
|---|---|---|---|
| Réanimation | Moniteur multiparamétrique, respirateur, pompes, moniteur de transport, centrale. | ECG/FC, SpO₂, respiration, PNI/pression invasive, température, CO₂, paramètres de ventilation, alarmes et états techniques. | Profil multiparamétrique dense, plusieurs sources par patient, alarmes et état de connexion détaillés. |
| USC | Moniteur multiparamétrique selon l'unité et le patient, éventuellement équipements de soutien. | Constantes, tendances, alarmes et changements d'état. | Profil configurable ; ne pas supposer une liste d'appareils universelle. |
| Cardiologie / télémétrie | Émetteur ECG portable, centrale, parfois moniteur de chevet. | ECG, fréquence, événements de rythme, batterie, qualité du signal, perte de couverture. | Profil mobile : appareil porté, localisation approximative par zone, état radio et session de télémétrie. |
| Bloc / SSPI | Moniteur d'anesthésie, moniteur patient, ventilation et capnographie selon situation, moniteur de transport. | ECG, SpO₂, PNI, température, CO₂, paramètres ventilatoires et alarmes. | Profil périopératoire, transfert entre postes et clôture de la surveillance post-interventionnelle. |
| Urgences / SAUV | Moniteur multiparamétrique, ECG, oxymètre, PNI, moniteur de transport. | Évaluation initiale, constantes, événements, affectation à une zone et orientation. | Profil dynamique, admissions rapides, zones temporaires et transferts fréquents. |
| Conventionnel | Appareil de mesure ponctuelle, oxymètre ou moniteur portable selon les besoins. | Mesures ponctuelles, horodatage, source et tendance ; éventuellement alertes d'un appareil connecté. | Profil de mesures intermittentes, sans fabriquer artificiellement un flux continu. |
| Néonatologie | Moniteur cardiorespiratoire spécialisé, capteurs adaptés, incubateur. | Fréquence cardiaque, respiration, SpO₂, apnées et température selon l'équipement. | Profil séparé avec données, limites et terminologie néonatales validées par des spécialistes. |

## 3. Familles d'appareils à distinguer

### A. Moniteur multiparamétrique de chevet

C'est le meilleur appareil pivot pour le POC.

Il peut exposer plusieurs observations issues de capteurs différents : ECG / fréquence cardiaque, SpO₂, respiration, pression artérielle non invasive, température, pression invasive et CO₂ selon la configuration.

À simuler au départ :
- un identifiant d'appareil ;
- une association à un patient et à une session ;
- plusieurs canaux de mesure ;
- des horodatages propres à chaque mesure ;
- une qualité de signal ;
- des alarmes physiologiques et techniques ;
- un état de connexion.

Les paramètres disponibles ne sont pas identiques sur tous les modèles. Les familles de données ci-dessus sont illustrées par les documentations fabricants, notamment GE CARESCAPE [H04].

### B. Émetteur de télémétrie portable

À traiter comme un appareil distinct du moniteur de chevet.

Il peut suivre un patient mobile, transmettre des données ECG et fournir des informations de batterie ou de liaison. La configuration de paramètres dépend du modèle ; le Mindray BeneVision TM80 est un exemple de produit de télémétrie hospitalière [H09].

À simuler :
- association à un patient ;
- connexion / perte de signal ;
- batterie ;
- données ECG et fréquence ;
- alarme issue de l'émetteur ;
- fin de session et restitution de l'appareil.

### C. Moniteur de transport

Il accompagne le patient entre deux zones ou services. Il peut reprendre un sous-ensemble des mesures et fonctionner sur batterie.

À simuler :
- changement de lieu ;
- appareil temporaire ;
- passage entre un moniteur fixe et un moniteur de transport ;
- maintien de l'identité du patient ;
- horodatages et continuité des observations.

La SFAR décrit des modalités de surveillance pendant les transports intrahospitaliers des patients d'anesthésie et de soins critiques [H106].

### D. Respirateur

Il ne faut pas le confondre avec un simple canal du moniteur multiparamétrique. Il s'agit d'une source autonome de données et d'alarmes.

Pour une extension, on pourrait simuler :
- fréquence respiratoire mesurée ;
- paramètres de ventilation et réglages ;
- état de fonctionnement ;
- alarme de déconnexion ou de pression, sans reproduire de conduite médicale.

### E. Pompe à perfusion

Autre appareil indépendant, avec des événements et alarmes qui lui sont propres.

Pour une extension :
- état marche / pause ;
- débit configuré ;
- volume restant ;
- alarme de ligne ou de réservoir ;
- état technique et batterie selon le modèle.

Ces deux familles sont à ajouter après le socle moniteur, car elles augmentent la diversité des contrats et des règles.

## 4. Proposition de périmètre d'appareils pour le premier POC

| Priorité | Appareil ou sous-système | Pourquoi | Décision proposée |
|---|---|---|---|
| P0 | Moniteur multiparamétrique de chevet simulé | Permet de couvrir le besoin central : plusieurs patients, plusieurs paramètres, flux périodiques et alarmes. | À simuler. |
| P0 | Centrale de surveillance logicielle | Regroupe les données, affiche les patients et gère le cycle de vie des alarmes. | À développer comme interface du POC. |
| P0 | Moniteur de transport simplifié | Permet de démontrer les changements de lieu et d'appareil. | À représenter par un profil distinct ou un mode transport. |
| P1 | Émetteur de télémétrie | Introduit patient mobile, sans-fil, batterie et couverture. | Extension recommandée après les parcours de base. |
| P1 | Respirateur simulé | Introduit des données et alarmes d'un équipement indépendant. | Extension après validation des contrats. |
| P2 | Pompe à perfusion | Ajoute une autre famille d'événements et d'alarmes. | Hors premier périmètre sauf demande explicite. |
| P2 | Poste d'anesthésie et équipements spécialisés | Très contextualisés. | Hors premier périmètre. |

## 5. Architecture fonctionnelle commune avec profils

Le modèle logique proposé :

- un patient possède un ou plusieurs séjours ;
- un séjour contient des séjours d'unité et des transferts ;
- un séjour d'unité est associé à un lieu et éventuellement à un lit ;
- une session de surveillance relie un patient, un appareil et une période ;
- un appareil publie des observations et des événements techniques ;
- les paramètres et modes actifs proviennent d'un profil d'équipement ;
- les règles d'affichage et d'alarme proviennent d'un profil de service et du contexte simulé.

Le patient, le lit et l'appareil sont donc trois entités différentes. Le changement de lit ne doit pas changer l'identité du patient ; le remplacement d'un moniteur ne doit pas créer un nouveau patient.

## 6. Points à ne pas figer

- Le fabricant simulé.
- Le protocole réseau.
- La fréquence de chaque paramètre.
- Les limites physiologiques et niveaux cliniques d'alarme.
- Le nombre d'appareils d'un service.
- L'intégration réelle de pompes et respirateurs.

Le POC doit simuler des comportements génériques inspirés de systèmes existants, pas prétendre émuler leur protocole propriétaire.

## Sources

- [H02] HAS — surveillance des patients en soins critiques.
- [H04] GE HealthCare — CARESCAPE Central Station.
- [H09] Mindray — BeneVision TM80.
- [H106] SFAR — surveillance pendant le transport intrahospitalier.
