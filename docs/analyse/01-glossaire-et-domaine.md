# 01 — Glossaire et domaine

**Version :** 0.1 — **Date :** 18 novembre 2026  
**Statut :** définitions de travail ; les définitions réglementaires et cliniques doivent être vérifiées dans leur contexte.

Ce glossaire sert à éviter qu'un même mot désigne plusieurs réalités au cours de la conception. Il ne fixe pas de valeur médicale de référence.

## 1. Domaine médical et organisationnel

| Terme | Définition de travail | Point à préciser pour le projet |
|---|---|---|
| Patient | Personne concernée par un suivi de santé. | Patient hospitalisé, patient à domicile, patient fictif ? |
| Télésanté | Ensemble de pratiques de santé réalisées à distance au moyen de technologies numériques. | Le sujet concerne-t-il une activité de télésurveillance réglementée ou un autre usage ? |
| Télésurveillance médicale | Activité associant une surveillance médicale, l'analyse de données et d'alertes transmises au moyen d'un dispositif médical numérique, selon le cadre français. | Le périmètre exact dépend du contexte et des textes applicables. |
| Monitorage physiologique | Surveillance de paramètres physiologiques d'une personne, souvent avec actualisation fréquente. | Quelles variables, quelle fréquence et quel usage ? |
| Monitorage centralisé | Regroupement des informations de plusieurs moniteurs au sein d'un poste de surveillance. | À distinguer de la télésurveillance de personnes à domicile. |
| Équipe soignante | Professionnels qui participent au suivi et à la prise en charge. | Composition et organisation réelles à documenter. |
| Opérateur de télésurveillance | Équipe ou professionnel responsable de l'organisation et du suivi de l'activité de télésurveillance dans le cadre français. | Ne pas confondre avec l'administrateur technique du serveur. |
| Triage d'alertes | Opération de reconnaissance, de classement et d'orientation des alertes reçues. | Qui trie, selon quelles procédures et avec quelle responsabilité ? |
| Continuité des soins | Organisation permettant que le suivi soit assuré dans le temps et lors des relais entre intervenants. | Horaires, astreintes, relais, absence de réponse et clôture. |
| Parcours patient | Suite des étapes et interactions liées au suivi d'un patient. | Inclusion, suivi, réévaluation, sortie ou fin du suivi. |

La définition légale française de l'activité de télésurveillance médicale est notamment portée par l'article L.162-48 du Code de la sécurité sociale [S09]. Les exemples de tri des alertes et de rôles sont décrits par le ministère [S08].

## 2. Mesures physiologiques

| Terme | Signification | Unité courante | Précaution |
|---|---|---|---|
| Fréquence cardiaque (FC / HR) | Nombre de battements cardiaques par unité de temps. | battements/minute (bpm) | La valeur seule ne décrit pas un rythme ECG. |
| Pression artérielle (PA / BP) | Pression exercée par le sang sur les artères. | mmHg | Une mesure est généralement composée de valeurs systolique et diastolique ; la méthode et le contexte comptent. |
| Pression systolique | Valeur associée à la phase de contraction cardiaque. | mmHg | Ne pas définir de seuil clinique générique dans le code sans protocole validé. |
| Pression diastolique | Valeur associée à la phase de relâchement cardiaque. | mmHg | Idem. |
| Saturation périphérique en oxygène (SpO₂) | Estimation non invasive de la saturation en oxygène de l'hémoglobine. | % | Dépend de la qualité du signal et des conditions de mesure. |
| Fréquence respiratoire (FR / RR) | Nombre de cycles respiratoires par unité de temps. | cycles/minute | La méthode de mesure doit être identifiée. |
| Température corporelle | Mesure de température selon un site et un instrument déterminés. | °C | Le site et le type de capteur doivent être conservés. |
| Électrocardiogramme (ECG) | Enregistrement de l'activité électrique du cœur. | signal échantillonné, souvent mV et Hz | Il peut s'agir d'un signal temporel, pas seulement d'une valeur isolée. |
| Poids | Masse corporelle mesurée. | kg | Mesure contextuelle, généralement moins fréquente. |
| Glycémie | Concentration de glucose dans le sang ou un autre échantillon selon la méthode. | mmol/L ou g/L | Les unités et méthodes doivent être explicites. |

FHIR décrit notamment les constantes, la pression artérielle, la température, les données de pouls oxymétrique et les mesures ECG comme des usages de la ressource Observation [S07].

**Aucune plage normale, valeur d'alerte ou règle de décision clinique n'est fixée dans ce document.** Elles dépendent de la population, de la pathologie, du protocole, de l'appareil et de la responsabilité clinique. Les données simulées ne doivent pas être interprétées comme un conseil médical.

## 3. Objets techniques du système

| Terme | Définition de travail |
|---|---|
| Capteur | Élément qui observe une grandeur physique ou physiologique et produit un signal. |
| Appareil médical | Équipement utilisé pour recueillir ou produire des informations ou réaliser une fonction médicale. Son statut réglementaire dépend notamment de la destination prévue par le fabricant. |
| Moniteur | Équipement qui affiche ou enregistre un ou plusieurs paramètres, parfois en continu. |
| Client simulateur | Programme qui reproduit le comportement d'un appareil ou d'une source de mesure sans être un appareil médical réel. |
| Passerelle (gateway) | Composant qui reçoit des données d'appareils et les relaie vers un autre réseau ou service. |
| Serveur | Programme ou machine qui reçoit des requêtes ou des messages et fournit des services. |
| Ingestion | Entrée des données dans le système, depuis leur réception jusqu'à leur acceptation ou rejet. |
| Validation de données | Contrôle du format, des unités, de l'identité, de l'horodatage et de la cohérence technique. Ce n'est pas une validation médicale. |
| Persistance | Conservation de données au-delà de leur présence temporaire en mémoire. |
| Base relationnelle | Base structurée autour de tables et de relations entre données. |
| Base temporelle | Stockage optimisé pour des séries de mesures horodatées. |
| Tableau de bord | Interface synthétique qui présente des informations utiles à un utilisateur. |
| Historique | Ensemble ordonné de mesures et d'événements passés. |
| Événement | Fait horodaté intéressant pour le système : mesure reçue, appareil déconnecté, alerte créée, alerte acquittée, etc. |

## 4. Transport et temps réel

| Terme | Définition de travail | Questions |
|---|---|---|
| Réseau | Ensemble de moyens permettant à des composants d'échanger des données. | LAN, Wi-Fi, réseau hospitalier, Internet, réseau mobile ? |
| TCP | Protocole de transport fournissant un flux fiable et ordonné entre deux extrémités. | Gestion des connexions et des coupures. |
| HTTP / HTTPS | Protocole de requête-réponse pour les échanges applicatifs ; HTTPS protège le canal avec TLS. | Requêtes périodiques, API ou autre mécanisme ? |
| MQTT | Protocole de messagerie publish/subscribe, souvent utilisé pour des échanges entre objets et services. | Broker, authentification, QoS, reconnexion, messages retenus ? |
| WebSocket | Canal bidirectionnel persistant entre un client et un serveur. | Utile pour quelles interactions du tableau de bord ? |
| Server-Sent Events (SSE) | Mécanisme de diffusion d'événements du serveur vers un client HTTP. | Suffisant pour un tableau de bord principalement descendant ? |
| Temps réel | Expression désignant une mise à jour dans un délai compatible avec un objectif d'usage. | Aucun seuil de délai n'est donné dans le sujet. |
| Latence | Temps écoulé entre deux événements de référence. | Mesurer séparément appareil → serveur, traitement, stockage et affichage. |
| Débit | Quantité de données traitée par unité de temps. | Mesures/seconde, octets/seconde, événements/seconde. |
| Gigue (jitter) | Variabilité du délai de transmission ou de réception. | Peut dégrader la régularité d'un flux. |
| Perte de message | Message envoyé mais jamais reçu ou pris en compte. | Comment la détecter et la mesurer ? |
| Doublon | Message reçu plusieurs fois. | Comment éviter de compter plusieurs fois une mesure ? |
| Message tardif | Message reçu après une mesure plus récente. | Faut-il conserver l'heure de mesure et l'heure de réception ? |

L'expression « le plus rapidement possible » doit devenir un ou plusieurs objectifs mesurables, à définir après compréhension des usages. Les métriques candidates sont la latence médiane et les percentiles élevés, le taux de perte, le taux de doublons, le retard de rattrapage après coupure et la disponibilité de l'interface.

## 5. Alertes et qualité de données

| Terme | Définition de travail |
|---|---|
| Seuil | Limite utilisée par une règle pour identifier une condition. Un seuil technique de qualité de données n'est pas un seuil médical. |
| Alerte | Événement signalant une situation qui nécessite une vérification ou une action selon une organisation définie. |
| Alarme | Signal sonore, visuel ou autre destiné à attirer l'attention. Le terme peut avoir une portée normative ou clinique selon le contexte. |
| Acquittement | Action explicite indiquant qu'un utilisateur a pris connaissance d'une alerte. Cela ne signifie pas qu'elle est résolue. |
| Escalade | Transmission d'une alerte à un autre rôle ou niveau de responsabilité lorsque les conditions définies sont réunies. |
| Clôture | Fin du traitement d'une alerte, avec statut et trace des actions. |
| Artefact | Valeur ou portion de signal qui ne représente pas correctement le phénomène visé, par exemple à cause d'un mouvement ou d'un mauvais contact. |
| Donnée manquante | Mesure attendue mais non reçue dans la fenêtre définie. |
| Donnée périmée | Dernière mesure trop ancienne au regard d'une règle de fraîcheur. |
| Valeur aberrante | Valeur présentant une incohérence technique ou statistique ; ce terme ne signifie pas automatiquement une urgence médicale. |
| Observabilité | Capacité à comprendre l'état interne du système à partir de métriques, journaux et traces. |

## 6. Sécurité et interopérabilité

| Terme | Définition de travail |
|---|---|
| Donnée personnelle | Information qui concerne une personne identifiée ou identifiable. |
| Donnée de santé | Donnée personnelle relative à la santé physique ou mentale d'une personne, selon le RGPD. |
| Donnée synthétique | Donnée artificielle produite pour représenter des situations sans correspondre à un dossier réel. |
| Pseudonymisation | Remplacement des identifiants directs par des identifiants indirects ; la réidentification reste possible avec des informations séparées. |
| Authentification | Vérification de l'identité d'un utilisateur ou d'un composant. |
| Autorisation / habilitation | Détermination de ce qu'une identité authentifiée est autorisée à consulter ou à faire. |
| RBAC | Contrôle d'accès fondé sur des rôles, auxquels sont associés des droits. |
| Moindre privilège | Limitation des droits au strict nécessaire pour réaliser une mission. |
| Chiffrement en transit | Protection des données pendant leur transmission, par exemple au moyen de TLS. |
| Chiffrement au repos | Protection des données stockées, selon les mécanismes de chiffrement retenus. |
| Journal d'audit | Trace des actions importantes, de leur auteur, de leur date et de leur résultat. |
| HDS | Cadre français de certification applicable à certaines activités d'hébergement de données de santé à caractère personnel. Son application dépend de la situation concrète. |
| RGPD | Règlement européen relatif à la protection des données personnelles. |
| Dispositif médical numérique (DMN) | Logiciel ou dispositif relevant de la réglementation médicale et des règles propres à la télésurveillance lorsque les critères applicables sont réunis. |
| HL7 | Organisation et famille de standards d'échange d'informations de santé. |
| FHIR | Standard HL7 moderne pour représenter et échanger des ressources de santé au moyen d'interfaces et de formats structurés. |
| Observation (FHIR) | Ressource représentant une mesure ou une assertion, par exemple une constante physiologique. |
| Provenance (FHIR) | Ressource décrivant l'origine et les processus qui ont contribué à produire ou modifier une ressource. |

## 7. Références principales du glossaire

- [S07] HL7 FHIR R5 — Observation : https://www.hl7.org/fhir/observation.html
- [S09] Code de la sécurité sociale — télésurveillance médicale : https://www.legifrance.gouv.fr/codes/id/LEGISCTA000044565906
- [S17] ANS — champ d'application HDS : https://esante.gouv.fr/faq/quel-est-le-champ-dapplication-de-la-legislation-relative-lhebergement-de-donnees-de-sante-caractere-personnel
- [S21] Règlement RGPD : https://eur-lex.europa.eu/legal-content/FR/TXT/?uri=CELEX:32016R0679
- [S22] Règlement européen relatif aux dispositifs médicaux : https://eur-lex.europa.eu/legal-content/FR/TXT/?uri=CELEX:32017R0745

## 8. Questions terminologiques restantes

1. Le terme « télésurveillance » est-il employé dans son sens réglementaire français ou dans un sens pédagogique plus large ?
2. Le projet surveille-t-il des constantes ponctuelles ou des signaux physiologiques continus ?
3. Les appareils sont-ils des moniteurs hospitaliers, des objets connectés, des dispositifs implantés ou des simulateurs abstraits ?
4. Le tableau de bord est-il un poste central de monitorage, une plateforme de suivi clinique ou les deux ?
5. Le mot « alerte » désigne-t-il une notification technique, une alerte de qualité de données ou une alerte médicale ?
