# Cybersécurité 03 — Prévention, détection, réponse et continuité

**Version :** 0.1 — **Date :** 18 novembre 2026

## 1. Le cadre français : PGSSI-S et CERT Santé

La PGSSI-S est un corpus de référentiels, guides et exigences de sécurité pour les systèmes d'information de santé. Elle est élaborée par l'Agence du Numérique en Santé avec les acteurs institutionnels, les établissements, les professionnels et les industriels. Elle propose des paliers de sécurité adaptés au contexte [H48].

Le CERT Santé publie un observatoire annuel et des retours d'expérience. Le rapport 2025 détaille notamment les mesures de confinement, d'investigation et de remédiation utilisées lors des incidents [H51].

## 2. Prévention avant incident

### 2.1 Inventaire et maîtrise des actifs

- tenir à jour la liste des moniteurs, centrales, passerelles, serveurs et postes ;
- identifier fabricant, modèle, version logicielle et propriétaire métier ;
- connaître la fin de support et les procédures de mise à jour ;
- identifier les flux et accès nécessaires ;
- maintenir une cartographie des zones réseau ;
- désactiver les services et comptes inutilisés.

Le rapport CERT Santé recommande de réduire la surface d'attaque, de désactiver les comptes et services inutiles, de corriger les vulnérabilités et de réaliser régulièrement des scans [H51].

### 2.2 Segmentation

- séparer le réseau biomédical du réseau bureautique ;
- isoler les zones de monitorage, télémétrie, maintenance et intégration ;
- ne permettre que les flux explicitement nécessaires ;
- utiliser des pare-feu et ACL ;
- superviser les communications inter-zones ;
- prévoir des procédures pour les connexions tierces.

Cette approche est cohérente avec les documentations GE, Philips et Dräger, ainsi qu'avec les retours d'expérience CERT Santé [H40–H43, H51].

### 2.3 Identité et accès

- comptes individuels ;
- authentification multi-facteur pour les accès distants et comptes privilégiés ;
- droits minimaux selon le rôle ;
- suppression rapide des accès temporaires ;
- contrôle des comptes prestataires ;
- rotation des secrets et clés ;
- journalisation des connexions ;
- accès distant via une passerelle contrôlée et autorisée.

Le rapport CERT Santé 2025 recommande notamment une authentification multi-facteur, en signalant que les identifiants peuvent être récupérés par phishing, force brute ou infostealer et réutilisés sur les accès VPN et applications exposées [H51].

### 2.4 Mises à jour et vulnérabilités

- suivre les alertes éditeurs et CERT ;
- évaluer les vulnérabilités selon les modèles et versions réellement installés ;
- appliquer les correctifs validés par le fabricant ;
- réaliser des tests de compatibilité avant la mise en production ;
- documenter les versions et dates de mise à jour ;
- définir une stratégie pour les dispositifs en fin de support ;
- analyser les journaux même après application d'un correctif lorsqu'une exploitation antérieure est possible.

Les équipements médicaux ne doivent pas être modifiés par des mises à jour génériques ou non validées. Les procédures du fabricant et du service biomédical doivent être suivies.

### 2.5 Sauvegarde et résilience

- sauvegardes indépendantes du domaine principal ;
- copies protégées contre l'altération et le chiffrement par un ransomware ;
- tests réguliers de restauration ;
- sauvegarde des configurations, certificats et bases ;
- procédures de reconstruction des serveurs et annuaires ;
- objectif de reprise défini par service ;
- documentation des dépendances.

RAID1 améliore la tolérance à une panne de disque, mais ne remplace pas une sauvegarde.

## 3. Détection

Les mécanismes à étudier :
- journaux des serveurs et systèmes ;
- alertes antivirus / EDR ;
- supervision réseau ;
- détection de comportements anormaux ;
- inventaire des communications des dispositifs médicaux ;
- surveillance des comptes VPN et comptes privilégiés ;
- détection de connexions inattendues ;
- détection de flux sortants non autorisés ;
- suivi des changements de configuration ;
- alerte sur la désactivation des outils de sécurité.

Le rapport CERT Santé 2025 décrit des interventions où les outils de détection ont permis d'identifier des mouvements latéraux, rançongiciels, infostealers, vers et logiciels espions, puis de bloquer la progression avant des impacts plus importants [H51].

## 4. Réponse à un incident

Le rapport CERT Santé décrit des mesures de réponse possibles :
- isoler les sauvegardes ;
- restreindre les flux entrants et sortants ;
- isoler l'Active Directory compromis ;
- désactiver les comptes compromis ;
- collecter les journaux et preuves numériques ;
- identifier l'origine et le scénario complet ;
- corriger les vulnérabilités exploitées ;
- désinfecter et reconstruire les systèmes affectés ;
- procéder à une reprise progressive et surveillée [H51].

Pour le monitorage, la réponse doit aussi prendre en compte la sûreté clinique :
- informer les responsables médicaux et biomédicaux ;
- vérifier l'état des moniteurs et centrales ;
- déterminer quels affichages, mesures ou alarmes restent fiables ;
- maintenir les fonctions locales indépendantes lorsque cela est autorisé ;
- utiliser des équipements de remplacement et procédures manuelles ;
- ne pas reconnecter un dispositif avant validation.

La notice Dräger VG6.0 recommande d'isoler l'unité concernée, de contacter les équipes biomédicales et informatiques, de mettre les appareils concernés hors service si nécessaire, de collecter les journaux et de ne pas remettre en service avant résolution [H43].

## 5. Continuité clinique

La cybersécurité doit intégrer un plan de fonctionnement dégradé.

Questions à traiter :
- le moniteur local peut-il continuer à mesurer si la centrale est indisponible ?
- comment les alarmes locales restent-elles opérationnelles ?
- existe-t-il un poste central de secours ?
- comment le personnel sait-il qu'un écran n'est plus à jour ?
- comment utiliser un appareil de remplacement ?
- comment transmettre les informations pendant une panne ?
- quelles mesures sont saisies manuellement et comment vérifier leur intégrité ?
- comment reconstituer l'historique après restauration ?

Il ne faut jamais supposer que le fonctionnement local est suffisant : cela dépend de la nature de l'unité, de l'équipement, du patient et du protocole clinique.

## 6. Programme de sécurité pour notre POC

Pour une démonstration académique sans patient réel :
1. utiliser un réseau local isolé ;
2. générer des patients, mesures et identités fictifs ;
3. segmenter logiquement simulateurs, serveur, base et interface ;
4. authentifier les clients simulateurs ;
5. chiffrer les échanges adaptés ;
6. utiliser des comptes utilisateurs avec rôles différents ;
7. journaliser les actions d'administration et les consultations sensibles simulées ;
8. tester perte de connexion, rejeu, duplication et client non autorisé ;
9. simuler une panne serveur ou une indisponibilité de centrale ;
10. vérifier les sauvegardes et restaurations ;
11. construire un tableau de bord de sécurité avec connexions, rejets, erreurs et événements ;
12. rédiger un scénario de réponse à incident.

Les simulations de cyberattaque doivent être non destructives : on simule un compte compromis, un accès refusé, une perte de service ou une exfiltration de données synthétiques dans un environnement contrôlé. Aucun malware réel ni test sur réseau hospitalier ne doit être utilisé.

## 7. Sources

- [H48] ANS — PGSSI-S : https://esante.gouv.fr/securite/politique-generale-de-securite-des-systemes-d-information-de-sante
- [H51] ANS / CERT Santé — Observatoire 2025 : https://cyberveille.esante.gouv.fr/sites/default/files/media/document/2026-05/ANS_CERTSante_Rapport_Public_Observatoire_Signalements_ISSIS_2025_VF_0.pdf
- [H43] Dräger Infinity CentralStation VG6.0 : https://www.draeger.com/Content/Documents/Products/ics-ifu-3736474-fr.pdf
- [H40] GE CARESCAPE Cybersecurity Fundamentals : https://www.gehealthcare.com/-/media/86efd534d0c94edb831beacde0c0f7eb.pdf
- [H41] Philips IntelliVue network security instructions : https://www.documents.philips.com/assets/Instruction%20for%20Use/20241010/7d137e87854a40a5b843b205009e75dc.pdf
