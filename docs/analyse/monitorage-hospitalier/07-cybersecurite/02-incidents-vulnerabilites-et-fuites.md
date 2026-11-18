# Cybersécurité 02 — Vulnérabilités, attaques et fuites documentées

**Version :** 0.1 — **Date :** 18 novembre 2026  
**Méthode :** sources officielles, autorités de cybersécurité, établissements, organismes de santé et fabricants. Les faits sont distingués selon leur degré de confirmation.

## 1. État général en France

Le rapport public 2025 de l'Observatoire des signalements d'incidents de sécurité des systèmes d'information en santé et médico-social indique :
- 764 incidents déclarés au CERT Santé en 2025 ;
- 606 structures ayant déclaré au moins un incident ;
- 53 % des incidents d'origine malveillante selon le rapport ;
- 2 incidents majeurs recensés en 2025, contre 3 en 2024 ;
- les compromissions de comptes, fuites de données et tentatives d'escroquerie sont en progression, tandis que les rançongiciels reculent de 30 % sur un an [H51].

Ces chiffres portent sur les signalements des secteurs santé et médico-social, pas uniquement les hôpitaux ni les équipements de monitorage. Ils dépendent aussi des déclarations et de la détection.

Le rapport décrit des vecteurs récurrents : compromission de comptes de messagerie, identifiants VPN ou comptes Active Directory, exploitation de vulnérabilités, phishing, force brute et infostealer [H51].

## 2. Incidents visant directement des dispositifs de monitorage

### 2.1 Contec CMS8000 / Epsimed MN-120 — 2025

**Type :** vulnérabilité dans le firmware d'un moniteur patient.  
**Sources :** CISA et FDA.

La CISA a analysé trois versions de firmware CMS8000 et découvert une fonctionnalité cachée permettant au moniteur de tenter une connexion vers une adresse IP intégrée dans le logiciel et de télécharger des fichiers distants sans vérification habituelle d'intégrité et de version. La CISA a également identifié une fonctionnalité d'exposition de données personnelles [H52].

Les risques évalués incluaient :
- possibilité de prise de contrôle à distance dans certaines conditions ;
- modification de la configuration ;
- exposition de données patient ;
- interruption ou fonctionnement incorrect du moniteur.

La FDA a indiqué ne pas avoir connaissance d'incidents cyber, blessures ou décès attribués à ces vulnérabilités au moment de son avis. Le 2 juillet 2025, elle a annoncé une mise à jour du fabricant retirant la connectivité réseau des appareils concernés ; le moniteur ne peut alors être utilisé que localement [H53].

**À ne pas conclure :** il n'est pas établi publiquement que cette fonctionnalité ait été exploitée dans un hôpital pour manipuler des données réelles. Il s'agit d'une vulnérabilité grave documentée, et non d'une attaque confirmée contre un patient ou un établissement.

### 2.2 Philips IntelliVue / PIC iX — vulnérabilités publiées en 2020 et 2021

**Type :** vulnérabilités applicatives, certificat, contrôle d'accès et disponibilité.

En septembre 2020, NHS England a listé huit vulnérabilités touchant certaines versions IntelliVue, PIC iX et PerformanceBridge Focal Point. Les risques documentés comprennent l'exposition de ressources, une validation insuffisante des entrées, des problèmes de gestion de certificats, l'accès à des informations patient et le redémarrage de services de surveillance [H55].

En novembre 2021, NHS England a documenté trois vulnérabilités affectant certaines versions PIC iX et Efficia CM. Les problèmes comprenaient une validation incorrecte des entrées, une clé cryptographique codée en dur et un algorithme cryptographique jugé faible ou risqué. Les conséquences potentielles incluaient l'accès non autorisé à des données patient et une interruption temporaire de l'affichage physiologique à la centrale [H54].

Les avis indiquaient des calendriers de correction annoncés par Philips. Ces avis historiques concernent des versions précises ; ils ne permettent pas de conclure que les versions actuelles sont vulnérables.

### 2.3 Évaluation indépendante du BSI — système Philips IntelliVue / PIC iX

Le BSI allemand a publié un rapport de cybersécurité sur des dispositifs médicaux connectés. Dans son projet ManiMed, il a testé notamment deux moniteurs Philips IntelliVue MX850 et une station PIC iX [H56].

L'évaluation a identifié des vulnérabilités dans l'application PIC iX, le service d'enrôlement de certificats et la vérification de révocation des certificats sur le moniteur. Le rapport évalue que la combinaison de certains défauts pouvait permettre un déni de service durable dans les conditions étudiées, voire une modification potentielle de données en transit par un attaquant disposant des accès et certificats requis [H56].

Le rapport précise :
- qu'aucune exploitation ou incident d'usage clinique associé n'avait été rapporté à cette date ;
- que le fabricant n'avait pas identifié de dommage patient ;
- que les vulnérabilités nécessitaient un accès physique à certains équipements ou un accès au réseau médical ;
- que des correctifs étaient préparés [H56].

**Limite :** ce rapport est une évaluation de 2020, sur un périmètre précis (une station et deux moniteurs) ; ce n'est pas un audit des versions actuelles ni de l'ensemble des produits Philips.

## 3. Attaques visant le SI hospitalier français

Les cas ci-dessous visent les systèmes d'information des établissements. Les sources publiques consultées ne démontrent pas que les moniteurs physiologiques aient été directement compromis dans ces incidents.

### 3.1 AP-HP — vol de données concernant environ 1,4 million de personnes, 2021

**Type :** vol et exfiltration de fichiers depuis un service de partage sécurisé.

L'AP-HP a indiqué qu'une attaque menée durant l'été 2021 et confirmée le 12 septembre avait permis de voler des fichiers concernant environ 1,4 million de personnes ayant réalisé des tests de dépistage COVID-19 mi-2020, principalement en Île-de-France. Les fichiers comprenaient identité, numéro de sécurité sociale, coordonnées et résultats de tests [H57].

Le service compromis était un outil de partage de fichiers sécurisé, utilisé ponctuellement pour transmettre des données de laboratoires à l'Assurance Maladie et aux ARS. Les premières investigations suggéraient un lien avec une vulnérabilité récente de l'outil de partage de fichiers acquis par l'AP-HP et hébergé sur ses propres infrastructures [H57].

Le système national SI-DEP lui-même n'était pas concerné. Les accès au service ont été coupés et l'incident signalé à la CNIL [H57].

**Leçon :** un service de partage ou d'intégration situé en périphérie du SIH peut exposer des données même si le système clinique principal n'est pas directement compromis.

### 3.2 CHU de Rouen — attaque par chiffrement, novembre 2019

**Type :** attaque de type rançongiciel / chiffrement et compromission du SI.

Le CHU a indiqué que l'attaque du 15 novembre avait chiffré certains fichiers sur des postes et serveurs et rendu la plupart des applications métiers indisponibles. Les admissions, prescriptions et comptes rendus ont dû fonctionner en mode dégradé, par téléphone et transmissions papier. L'ANSSI a accompagné la remédiation ; l'établissement indiquait ne pas avoir constaté de fuite de données médicales ou personnelles à cette date [H58].

Un rapport ultérieur de la Cour des comptes précise que l'attaque avait été rendue possible par la compromission de la messagerie d'un interne, puis par une élévation de privilèges ayant permis la prise de contrôle de l'annuaire [H59].

**Leçon :** un compte utilisateur compromis peut devenir le point de départ d'une attaque contre les services centraux de l'hôpital.

### 3.3 CHSF Corbeil-Essonnes — exfiltration et publication de données, août-septembre 2022

**Type :** attaque informatique avec exfiltration puis publication de données.

Le Centre Hospitalier Sud Francilien indique que l'attaque du 20/21 août 2022 a été suivie d'une divulgation le 23 septembre de données exfiltrées sur le darknet. Le communiqué du 7 octobre précise qu'environ 700 000 courriers d'information ont été envoyés aux usagers et personnels potentiellement concernés [H60].

Cybermalveillance.gouv.fr confirme l'exfiltration de fichiers et le signalement à la CNIL [H61].

Les documents publics consultés ne permettent pas de reconstituer avec certitude le vecteur initial d'intrusion. Il ne faut donc pas attribuer l'incident à un protocole ou logiciel particulier sans source supplémentaire.

**Leçon :** la fuite de données peut se produire avant ou en parallèle du chiffrement des systèmes. La sauvegarde seule ne protège pas contre l'exfiltration.

### 3.4 CH de Versailles — attaque du 3 décembre 2022

**Type :** indisponibilité du SI et perturbation des activités.

Le centre hospitalier a confirmé une attaque sur l'ensemble de son système d'information. Les données personnelles figurant dans le SI sont devenues indisponibles, notamment dossiers patients, état civil et rendez-vous. L'établissement signale un ralentissement de la prise en charge et une désorganisation jusqu'à la mise en place des procédures dégradées. Au moment de son courrier d'information, il indiquait que l'enquête ne permettait pas de mettre en évidence une diffusion illégale des données [H62].

**Leçon :** une attaque peut affecter la disponibilité des données sans que leur publication soit démontrée.

### 3.5 Groupement hospitalier — compromission VPN, novembre 2023

**Type :** accès par vulnérabilité VPN non corrigée, propagation dans l'annuaire et exfiltration.

Le CERT Santé décrit une intrusion probablement permise par une vulnérabilité non corrigée sur un accès VPN. L'attaquant a compromis un contrôleur de domaine et s'est propagé vers les contrôleurs de domaine de deux établissements du groupement. L'établissement a coupé les connexions Internet entrantes et sortantes, ce qui a interrompu la messagerie, la prise de rendez-vous en ligne et la géolocalisation du SAMU [H49].

**Leçon :** la compromission d'une passerelle ou d'un compte peut affecter plusieurs établissements et les services de coordination.

### 3.6 CHD Stell, Rueil-Malmaison — compte administrateur réactivé et ransomware, mars 2025

**Type :** compromission d'un compte ancien, accès VPN et rançongiciel.

Le CERT Santé indique qu'un ancien compte administrateur, réactivé pour un audit, possédait encore un accès VPN et un mot de passe faible. L'attaquant a pu accéder au SI puis chiffrer plusieurs serveurs Windows. L'établissement a coupé les flux VPN, isolé les serveurs affectés, reconstruit l'Active Directory et restauré progressivement les services [H50].

**Leçon :** les comptes temporaires, prestataires et anciens comptes d'administration doivent avoir une durée de vie et une révocation contrôlées.

## 4. Incident chez un fabricant : Mindray, août 2026

Mindray a publié le 19 août 2026 une communication client indiquant qu'un groupe de rançongiciel avait accédé sans autorisation à certains serveurs d'une organisation Mindray à l'étranger, utilisés pour soutenir des processus industriels avec les fournisseurs [H63].

Mindray indique que :
- son équipe sécurité a activé les procédures de réponse ;
- une société indépendante a participé à l'investigation ;
- les serveurs concernés ne contenaient pas d'informations clients ni de données personnelles d'employés ;
- l'entreprise n'a pas trouvé d'indice de compromission de données clients ou personnelles ;
- elle ne s'attendait pas à un impact sur la production ou les opérations [H63].

C'est une attaque réelle contre une organisation fournisseur, mais les éléments publics ne montrent pas que des moniteurs hospitaliers ou données de patients aient été compromis.

## 5. Synthèse : vulnérabilité, attaque, fuite

| Cas | Cible principale | Fuite confirmée ? | Impact clinique ou opérationnel publiquement décrit ? |
|---|---|---|---|
| Contec CMS8000 | Firmware du moniteur | Capacité d'exfiltration identifiée ; exploitation réelle non établie publiquement | Risque potentiel ; FDA ne connaissait pas d'incident ou dommage au moment de l'avis. |
| Philips IntelliVue / PIC iX | Moniteur et centrale | Risque d'exposition documenté | Risque d'interruption et d'accès non autorisé ; pas d'exploitation clinique rapportée dans l'évaluation BSI. |
| AP-HP 2021 | Service de partage de fichiers | Oui, environ 1,4 million de personnes concernées | Données de tests COVID ; SI-DEP non concerné. |
| CHU Rouen 2019 | SI hospitalier / annuaire | Aucune fuite constatée selon le CHU à l'époque | Applications métier indisponibles et fonctionnement dégradé. |
| CHSF 2022 | SI hospitalier | Oui, données publiées sur le darknet | Violation de données ; informations détaillées sur le vecteur initial non établies ici. |
| CH Versailles 2022 | SI hospitalier | Publication illégale non mise en évidence dans le courrier à cette date | Données indisponibles et ralentissement de la prise en charge. |
| Groupement hospitalier 2023 | VPN et annuaire | Exfiltration signalée | Services externes et de coordination interrompus. |
| CHD Stell 2025 | Compte administrateur / VPN / serveurs | Non précisé dans le résumé public consulté | Serveurs Windows chiffrés, reconstruction de l'annuaire et restauration. |
| Mindray 2026 | Serveurs de processus industriels fournisseurs | Mindray déclare aucune donnée client/personnelle compromise | Aucun impact opérationnel client attendu selon le fabricant. |

## 6. Sources

- [H49] CERT Santé — groupement hospitalier, compromission VPN et propagation : https://cyberveille.esante.gouv.fr/retours-d-experience/un-groupement-hospitalier-victime-dune-compromission-de-son-si-suite-une-fuite
- [H50] CERT Santé — CHD Stell, ransomware 2025 : https://cyberveille.esante.gouv.fr/retours-d-experience/compromission-du-si-et-ransomware-au-chd-stell-2025-10-14
- [H51] ANS / CERT Santé — Observatoire des incidents 2025 : https://cyberveille.esante.gouv.fr/sites/default/files/media/document/2026-05/ANS_CERTSante_Rapport_Public_Observatoire_Signalements_ISSIS_2025_VF_0.pdf
- [H52] CISA — Contec CMS8000 Contains a Backdoor : https://www.cisa.gov/sites/default/files/2025-02/fact-sheet-contec-cms8000-contains-a-backdoor-508c_0.pdf
- [H53] FDA — Contec CMS8000 and Epsimed MN-120 Safety Communication : https://www.fda.gov/medical-devices/safety-communications/cybersecurity-vulnerabilities-certain-patient-monitors-contec-and-epsimed-fda-safety-communication
- [H54] NHS England — Philips PIC iX and Efficia vulnerabilities, 2021 : https://digital.nhs.uk/cyber-alerts/2021/cc-3980
- [H55] NHS England — Philips patient monitor vulnerabilities, 2020 : https://digital.nhs.uk/cyber-alerts/2020/cc-3619
- [H56] BSI — Cyber Security Review of Network-Connected Medical Devices, ManiMed : https://www.bsi.bund.de/SharedDocs/Downloads/DE/BSI/DigitaleGesellschaft/ManiMed_Abschlussbericht_EN.pdf
- [H57] AP-HP — vol de données sur le service de partage de fichiers : https://www.aphp.fr/espace-medias/liste-ressources-presse/lap-hp-porte-plainte-suite-une-attaque-informatique-sur-son
- [H58] CHU Rouen — attaque informatique du 15 novembre 2019 : https://www.chu-rouen.fr/le-point-sur-lattaque-informatique-du-15-novembre-2019/
- [H59] Cour des comptes — CHU de Rouen, rapport 2025 : https://www.ccomptes.fr/sites/default/files/2025-04/NDR2025-11.pdf
- [H60] CHSF — communication du 7 octobre 2022 : https://www.corbeil-essonnes.fr/wp-content/uploads/CHSF-COURRIER-RGPD-061022COMCHSF22.pdf
- [H61] Cybermalveillance.gouv.fr — violation de données du CHSF : https://www.cybermalveillance.gouv.fr/tous-nos-contenus/actualites/violation-donnees-chsf-formulaire-lettre-plainte-electronique
- [H62] Centre Hospitalier de Versailles — attaque du 3 décembre 2022 : https://www.ch-versailles.fr/Ressources/FCK/Courrier%20d%E2%80%99information%20personnes%20-%20CyberAttaque%20-%20CHV.pdf
- [H63] Mindray — communication client sur l'incident du 19 août 2026 : https://www.mindray.com/content/dam/xpace/en_us/products-solutions/solutions/hospital-wide/Cyber-Security-Incident-customer-letter.pdf
