# Comparaison des services et choix du service de référence

**Date de mise à jour :** 25 novembre 2026  
**Décision :** réanimation adulte polyvalente retenue comme premier périmètre clinique. Le système cible est multi-services, mais le développement initial se concentre sur ce service.

## 1. Pourquoi le service change le système

Le système ne peut pas être conçu comme si tous les services hospitaliers utilisaient le même matériel et les mêmes pratiques. Le contexte détermine notamment :

- les profils de patients et les paramètres pertinents ;
- les équipements réellement présents ;
- la fréquence et la nature des mesures ;
- la mobilité des patients ;
- les personnes responsables de regarder les écrans et de répondre aux alarmes ;
- le nombre de transferts et les changements d'affectation ;
- le type de centrale, les moyens de report et les interfaces disponibles.

La HAS insiste en soins critiques sur l'organisation de la surveillance, la configuration des moniteurs, la gestion des alarmes, les locaux et la formation [H02]. Le Code de la santé publique décrit, pour la surveillance continue, une observation clinique et biologique répétée et méthodique [H105]. Ces textes ne signifient pas que tous les services ont une architecture informatique identique.

## 2. Comparaison fonctionnelle

| Service | But de la surveillance | Équipements courants ou possibles | Organisation et événements caractéristiques | Complexité du cadrage initial |
|---|---|---|---|---|
| Réanimation adulte | Surveillance continue de patients présentant une ou plusieurs défaillances d'organes et recevant des traitements intensifs. | Moniteur multiparamétrique, respirateur, pompes, pression invasive, capnographie selon le cas, centrale. | Plusieurs sources simultanées ; alarmes physiologiques et techniques ; changements fréquents de configuration ; transferts sous surveillance. | Élevée : c'est le contexte le plus riche, mais aussi celui qui multiplie les interfaces et cas limites. |
| Unité de soins continus (USC) | Observer des patients dont la gravité ou le traitement exige une observation répétée et méthodique, avec possibilité de transfert vers des soins plus intensifs. | Moniteur de chevet selon les besoins, appareils de mesure, parfois équipements de soutien. | Surveillance renforcée ; escalade vers réanimation si aggravation ; organisation propre à l'établissement. | Moyenne à élevée : bon compromis si le niveau de surveillance et les appareils locaux sont confirmés. |
| Cardiologie avec télémétrie | Suivre notamment l'activité électrique cardiaque de patients qui peuvent se déplacer dans l'unité. | Émetteur ECG porté par le patient, récepteur et centrale de télémétrie ; parfois SpO₂ ou PNI complémentaires. | Association du transmetteur au patient ; mobilité et couverture radio ; événement de rythme ; sortie de télémétrie. | Moyenne : excellent pour le sans-fil et les alarmes ECG, moins représentatif des équipements de réanimation. |
| Bloc opératoire et SSPI | Surveiller le patient pendant l'anesthésie puis la récupération post-interventionnelle. | Moniteur d'anesthésie, ECG, SpO₂, PNI, température, capnographie et ventilation selon le contexte. | Séquences courtes, changement de poste, transfert sous surveillance et transmission écrite à la sortie de SSPI. | Moyenne : très bon parcours de bout en bout, mais centré sur la période périopératoire. |
| Urgences / SAUV | Évaluer rapidement des patients d'origines et de gravités très variables. | Moniteur multiparamétrique, ECG, oxymètre, PNI, moniteur de transport, équipements de réanimation selon la zone. | Arrivée non programmée, triage, identité parfois provisoire, affectation rapide, changements de zone et orientation. | Élevée : forte diversité des flux et des états, moins facile à réduire à un profil d'équipement unique. |
| Hospitalisation conventionnelle | Suivi quotidien de patients dont la surveillance est souvent intermittente, avec intensification selon l'état. | Appareils de mesure ponctuelle ; monitorage continu ou portable pour certains patients et organisations. | Relevés périodiques, détection d'une dégradation, appel d'équipe et transfert vers USC/réanimation. | Faible à moyenne pour un système de monitorage continu généraliste ; excellent comme étape d'un parcours. |
| Néonatologie / réanimation néonatale | Surveillance adaptée aux nouveau-nés et prématurés. | Moniteur cardiorespiratoire néonatal, capteurs spécifiques, incubateur et équipements spécialisés. | Paramètres, limites et pratiques propres à la population néonatale. | Très élevée : à séparer du profil adulte et à ne pas mélanger au premier périmètre adulte. |

## 3. Différences particulièrement importantes

### Réanimation et USC

L'USC n'est pas simplement une « petite réanimation ». Le Code de la santé publique la décrit comme une organisation d'observation répétée et méthodique [H105]. Les recommandations communes SRLF/SFAR/SFMU de 2018 traitent séparément de la typologie des patients, de la structure de l'unité et de son organisation médicale et paramédicale [H107].

Conséquence pour le simulateur : il faut définir des profils d'unité et ne pas supposer que les mêmes appareils, fréquences ou alarmes existent partout.

### Cardiologie et télémétrie

La télémétrie hospitalière met l'accent sur un appareil portable associé à un patient mobile et sur la réception des signaux dans une station centrale. Certains produits offrent l'admission, la sortie et le déplacement du patient, le suivi d'émetteurs et des historiques de courbes et d'alarmes [H04, H09].

Conséquence : les tests d'association, de couverture radio, de batterie et de perte de connexion deviennent centraux.

### SSPI

Le Code de la santé publique précise que la surveillance commence dès la fin de l'intervention, ne s'interrompt pas pendant le transfert et se poursuit jusqu'au rétablissement des fonctions requises [H03, H108]. C'est un excellent environnement pour tester la continuité d'une session de monitorage entre deux lieux.

### Hospitalisation conventionnelle

Il ne faut pas supposer que chaque lit d'un service conventionnel dispose d'un moniteur multiparamétrique connecté en permanence. La surveillance peut être ponctuelle ou continue selon le patient et l'organisation. Le système devra donc distinguer « pas de mesure attendue à cet instant » de « appareil connecté mais sans données » et de « appareil hors ligne ».

## 4. Matrice de choix pour le projet

Évaluation qualitative relative au sujet académique, pas classement médical :

| Critère | Réanimation | USC | Cardiologie / télémétrie | SSPI | Urgences |
|---|---:|---:|---:|---:|---:|
| Flux multiparamétriques continus | Très fort | Variable selon unité | Fort, surtout ECG | Fort pendant le réveil | Variable selon zone |
| Diversité des appareils | Très forte | Moyenne à forte | Faible à moyenne | Forte | Forte |
| Complexité des alarmes | Très forte | Moyenne à forte | Forte sur ECG | Forte et contextuelle | Variable |
| Mobilité / transferts | Forte | Moyenne | Forte | Très forte sur un parcours court | Très forte |
| Données de recherche disponibles | Très bonnes | Plus limitées | Bonnes pour ECG / télémétrie | Plus spécialisées | Bonnes via MIMIC-IV-ED |
| Facilité de cadrage initial | Faible | Moyenne | Moyenne | Moyenne | Faible |

## 5. Premier périmètre fonctionnel retenu

### Réanimation adulte polyvalente

La réanimation adulte polyvalente est retenue comme premier service à rendre fonctionnel. La première version doit couvrir :

- une centrale affichant plusieurs lits ;
- des moniteurs multiparamétriques de chevet ;
- des mesures physiologiques structurées ;
- des alarmes physiologiques et techniques ;
- des états de connexion des appareils ;
- des associations patient / séjour / lit / appareil ;
- des transferts vers et depuis les urgences ou une unité moins intensive.

La réanimation est retenue parce que la surveillance multiparamétrique continue, les risques de défaut de surveillance et les alarmes en font un contexte riche pour concevoir et tester le système. Ces pratiques restent à traduire en exigences logicielles sourcées et non en règles cliniques inventées. Des bases de recherche dédiées à la réanimation existent également, notamment MIMIC-IV, HiRID, eICU et AmsterdamUMCdb [H100–H104].

### Services d'extension

L'USC, la cardiologie avec télémétrie, les urgences / SAUV et la SSPI sont conservés comme extensions possibles. Ils ne remplacent pas le service initial : leur intégration viendra après la validation du socle de monitorage et des échanges entre centrales.

## 6. Ce que nous ne devons pas décider maintenant

- Le nombre exact de lits simulés et la charge cible.
- Le nombre d'appareils par lit.
- Les seuils d'alarme et les conduites médicales.
- Les fréquences de production des mesures.
- La marque ou le protocole d'un fabricant.
- La topologie réseau, les frontières entre centrales et supervision, ou les bibliothèques Java.

Ces choix interviennent après validation du contexte et des scénarios.

## Sources

- [H02] HAS — Surveillance des patients en soins critiques, 2024.
- [H03] Code de la santé publique — surveillance postinterventionnelle.
- [H04] GE HealthCare — CARESCAPE Central Station.
- [H09] Mindray — BeneVision TM80.
- [H100] MIMIC-IV ; [H102] HiRID ; [H103] eICU ; [H104] AmsterdamUMCdb.
- [H105] Code de la santé publique, art. D6124-117.
- [H107] SRLF / SFAR / SFMU — recommandations USC, 2018.
- [H108] SFAR — dossier anesthésique et surveillance post-interventionnelle.
