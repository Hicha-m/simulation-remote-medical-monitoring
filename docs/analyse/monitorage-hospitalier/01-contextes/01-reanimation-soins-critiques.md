# Environnement 01 — Réanimation et soins critiques

**Version :** 0.1 — **Date :** 18 novembre 2026  
**Type de source privilégié :** réglementation française, HAS, documentations équipements.

## 1. Pourquoi cet environnement est central

La réanimation et les soins intensifs sont le contexte hospitalier où la surveillance multiparamétrique continue est la plus directement établie dans le cadre français. Le décret relatif aux conditions techniques de fonctionnement des soins critiques prévoit des équipements permettant la surveillance paramétrique continue en réanimation et en soins intensifs [H01].

La HAS rappelle que la surveillance doit être organisée 24h/24 et met en évidence des événements indésirables liés à un défaut de surveillance [H02].

## 2. Organisation réelle à prendre en compte

La HAS décrit plusieurs éléments concrets :

- un poste de soins adapté à la surveillance des patients ;
- une surveillance visuelle et sonore des patients et des appareils des chambres ;
- un report des alarmes du moniteur multiparamétrique de chevet et des appareils critiques ;
- une centrale d'alarme au poste de soins ;
- selon la configuration, un report vers les moniteurs d'autres chambres, des répétiteurs dans les circulations et des dispositifs portatifs affectés à des professionnels ;
- une procédure de gestion du système et des alarmes ;
- une vérification de la configuration lors de l'admission et à chaque prise de poste ;
- une présence organisée près de la centrale d'alarme, en particulier lors des périodes vulnérables (nuit, pauses) ;
- une formation initiale et continue du personnel [H02].

Ce sont des pratiques recommandées par la HAS à partir de l'analyse de déclarations d'événements indésirables. Elles constituent une référence française importante, mais chaque unité doit organiser son dispositif selon ses locaux, ses équipements et son activité.

## 3. Équipements et flux observables

Un environnement de soins critiques peut associer :

| Composant | Fonction | Information / événement |
|---|---|---|
| Moniteur de chevet multiparamétrique | Mesure et affiche les paramètres du patient. | Valeurs, courbes, limites et alarmes. |
| Capteurs et accessoires | Acquièrent les signaux physiologiques. | ECG, SpO₂, pression, respiration, température, etc. selon configuration. |
| Respirateur | Assure une assistance ventilatoire et fournit des paramètres respiratoires. | Mesures et alarmes propres au ventilateur. |
| Pompe à perfusion et autres dispositifs critiques | Administrent un traitement ou soutiennent une fonction. | État, événements et alarmes selon possibilité d'intégration. |
| Réseau de monitorage | Transporte les données des équipements vers les systèmes de surveillance. | Messages, état de connexion, pertes et retards. |
| Centrale de surveillance | Permet de visualiser plusieurs patients et de relayer les alarmes. | Vues multi-patients, événements et historique. |
| Répétiteur / notification distante | Rend une alarme visible ou audible dans une autre zone. | Notification et localisation de l'équipement/patient. |
| Poste clinique | Permet aux professionnels d'accéder aux informations et d'organiser le suivi. | Consultation, réglages autorisés, actions et transmissions. |

La centrale Dräger Infinity CentralStation, par exemple, annonce l'intégration de données de monitorage, d'alarmes et d'historiques en temps réel ; elle annonce une surveillance de 32 ou 64 patients selon configuration et une intégration des données d'appareils de ventilation et d'anesthésie Dräger [H08]. Cela illustre une offre produit, pas une preuve de déploiement dans un service donné.

## 4. Besoins métiers propres aux soins critiques

| ID | Besoin candidat | Justification terrain | À valider |
|---|---|---|---|
| ICU-01 | Voir simultanément plusieurs patients. | Poste de soins et centrale de surveillance multi-patients. | Nombre de chambres et disposition de l'écran. |
| ICU-02 | Relier un patient à son moniteur et à son lit. | Vérification à l'admission et gestion du système. | Processus local d'admission et transfert. |
| ICU-03 | Visualiser les paramètres, courbes et alarmes. | Surveillance multiparamétrique continue. | Paramètres réellement affichés selon spécialité. |
| ICU-04 | Diffuser l'alarme au bon endroit. | Centrale, inter-chevet, répétiteurs ou dispositifs portatifs. | Cartographie des zones et responsabilités. |
| ICU-05 | Vérifier les limites d'alarme par patient. | La HAS préconise des limites adaptées et une vérification à chaque relève. | Qui configure et qui valide ? |
| ICU-06 | Détecter un moniteur ou un équipement non connecté. | La surveillance dépend de l'installation et de la bonne configuration. | Quels états techniques sont remontés ? |
| ICU-07 | Maintenir une supervision lors des pauses et de nuit. | La HAS demande une organisation de présence près de la centrale. | Organisation réelle du service. |
| ICU-08 | Former les professionnels à la conduite à tenir. | La HAS insiste sur la formation initiale et continue. | Parcours de formation et évaluation. |
| ICU-09 | Consulter l'historique des événements. | Les centrales de fabricants exposent des historiques et tracés. | Quelle durée, quelle granularité, quels exports ? |
| ICU-10 | Distinguer alarme patient et défaut technique. | Les procédures doivent traiter l'alarme et le fonctionnement du système. | Taxonomie locale et priorités. |

## 5. Scénario opérationnel à étudier

**Admission d'un patient en soins critiques**

1. Le patient est admis et affecté à une chambre ou un lit.
2. Le personnel associe ou vérifie les dispositifs de surveillance.
3. Les capteurs appropriés sont connectés.
4. Les paramètres nécessaires et limites d'alarme sont configurés conformément à la prescription et aux procédures locales.
5. L'affichage au chevet et le report à la centrale sont vérifiés.
6. Le fonctionnement des alarmes et de leur diffusion est vérifié.
7. Lors de la relève, le système et les alarmes sont à nouveau contrôlés selon la procédure du service.

Cette séquence est une décomposition analytique des points mis en avant par la HAS ; elle n'est pas présentée comme une procédure universelle officielle.

## 6. Défaillances à simuler (sans règle médicale)

- moniteur non associé au bon patient ;
- capteur débranché ;
- centrale non joignable ;
- alarme locale audible mais non reportée ;
- mauvais paramétrage ou profil non adapté ;
- répétiteur indisponible ;
- notification mobile non reçue ;
- absence de professionnel à proximité du poste de surveillance ;
- patient déplacé sans mise à jour de l'affectation ;
- changement d'équipe sans vérification ;
- bruit ou multiplication des alarmes qui gêne la perception.

## 7. Sources

- **[H01]** Légifrance, décret n° 2022-694 du 26 avril 2022 relatif aux conditions techniques de fonctionnement de l'activité de soins critiques : https://www.legifrance.gouv.fr/eli/decret/2022/4/26/SSAH2206984D/jo/texte
- **[H02]** HAS, Flash Sécurité Patient « Surveillance des patients en service de soins critiques », 29 avril 2024 : https://www.has-sante.fr/jcms/p_3511526/fr/flash-securite-patient-surveillance-des-patients-en-service-de-soins-critiques-une-veille-sans-faille-pour-qu-aucun-patient-ne-defaille
- **[H08]** Dräger, Infinity CentralStation Wide : https://www.draeger.com/fr_fr/Products/Infinity-CentralStation

## 8. Questions à vérifier auprès d'un professionnel

- La centrale est-elle dans le poste infirmier ou dans une salle de surveillance dédiée ?
- Qui est explicitement chargé de surveiller les alarmes ?
- Les alarmes des respirateurs et pompes sont-elles remontées dans la même interface ?
- Comment les patients sont-ils déplacés et réaffectés ?
- Comment les équipes règlent-elles les alarmes et évitent-elles qu'elles soient trop nombreuses ?
- Quelles alarmes sont locales, centralisées ou transmises à distance ?
