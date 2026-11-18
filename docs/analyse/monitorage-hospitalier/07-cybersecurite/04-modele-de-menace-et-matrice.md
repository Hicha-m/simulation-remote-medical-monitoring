# Cybersécurité 04 — Modèle de menace et matrice de risques

**Version :** 0.1 — **Date :** 18 novembre 2026  
**Statut :** modèle de travail pour la simulation, pas analyse de risque validée d'un système réel.

## 1. Actifs à protéger

- données physiologiques ;
- identité patient et informations d'affectation ;
- moniteurs et transmetteurs ;
- centrale et serveurs ;
- intégration SIH ;
- utilisateurs et comptes techniques ;
- clés, certificats et secrets ;
- configuration des appareils ;
- alarmes et événements ;
- disponibilité du réseau ;
- journaux et sauvegardes.

## 2. Acteurs et sources de menace

- attaquant externe ;
- cybercriminel de type rançongiciel ;
- utilisateur interne malveillant ou négligent ;
- prestataire ou compte distant compromis ;
- fournisseur ou chaîne d'approvisionnement compromise ;
- logiciel malveillant ;
- appareil non autorisé ;
- erreur de configuration ou de maintenance.

## 3. Matrice des scénarios

| ID | Scénario de menace | Actif | Conséquence | Contrôles à étudier |
|---|---|---|---|---|
| TH-01 | Compte soignant compromis | Utilisateurs / centrale | Accès non autorisé aux données | MFA, RBAC, sessions, journaux. |
| TH-02 | Compte administrateur ancien réactivé | SI / serveurs | Prise de contrôle et ransomware | Cycle de vie des comptes, approbation et audit. |
| TH-03 | Identifiants VPN prestataire volés | Accès distant | Intrusion et propagation | MFA, bastion, accès limités et révocation. |
| TH-04 | Moniteur non autorisé connecté | Réseau médical | Fausse source de données | Identité appareil, segmentation et contrôle d'admission. |
| TH-05 | Flux intercepté | Réseau | Divulgation de données | Chiffrement adapté, isolation et contrôle des chemins. |
| TH-06 | Donnée modifiée | Mesures | Altération de l'information affichée | Intégrité, authentification source, provenance. |
| TH-07 | Centrale indisponible | Application clinique | Perte de vue multi-patients | Continuité, mode local, redondance et procédure. |
| TH-08 | Congestion ou tempête réseau | Réseau | Retard des alarmes / mesures | QoS, isolation, supervision et tests. |
| TH-09 | Firmware vulnérable | Moniteur | Contrôle ou altération potentielle | Inventaire, suivi CVE, correctifs validés, isolement. |
| TH-10 | Rançongiciel sur serveurs | Infrastructure | Indisponibilité et perte de données | EDR, segmentation, sauvegardes et reprise. |
| TH-11 | Exfiltration depuis un service annexe | Partage / intégration | Fuite de données | Contrôle des accès, minimisation et surveillance sortante. |
| TH-12 | Mise à jour non vérifiée | Moniteur / centrale | Corruption ou panne | Packages signés, validation et procédure fabricant. |
| TH-13 | Perte de clés ou certificats | Identité appareil | Perte de connexion ou usurpation | Gestion de cycle de vie, sauvegarde sécurisée et révocation. |
| TH-14 | Journalisation désactivée | Tous | Incident non détecté ou non explicable | Protection des logs et alertes sur désactivation. |
| TH-15 | Mauvaise association patient-moniteur | Identité / mesure | Données du mauvais patient | Vérifications, historique d'affectation et double contrôle. |

## 4. Scénarios de test cyber sûrs pour le POC

| Test | Simulation non destructive | Résultat attendu |
|---|---|---|
| TST-SEC-01 | Tentative de connexion avec un compte invalide. | Accès refusé et événement journalisé. |
| TST-SEC-02 | Utilisateur essaie d'ouvrir un patient hors de son périmètre. | Accès refusé et journal d'audit. |
| TST-SEC-03 | Client simulateur inconnu essaie de publier une mesure. | Message rejeté. |
| TST-SEC-04 | Message synthétique altéré ou avec signature invalide. | Rejet ou mise en quarantaine. |
| TST-SEC-05 | Compte technique désactivé puis utilisé. | Accès bloqué et événement de sécurité. |
| TST-SEC-06 | Serveur d'ingestion arrêté volontairement. | Données marquées indisponibles, alarme technique et procédure dégradée simulée. |
| TST-SEC-07 | Centrale déconnectée du serveur. | Fraîcheur affichée, indicateur hors ligne, historique préservé. |
| TST-SEC-08 | Rejeu de messages synthétiques. | Doublons détectés et non comptés deux fois. |
| TST-SEC-09 | Sauvegarde restaurée dans un environnement isolé. | Cohérence des mesures, utilisateurs et événements vérifiée. |
| TST-SEC-10 | Flux sortant non autorisé simulé. | Blocage et événement de sécurité. |

Aucun test ne doit tenter d'accéder à un système hospitalier, à un appareil réel ou à un réseau tiers.

## 5. Échelles de maturité à comparer

| Domaine | Démonstrateur local | POC avancé | Système de santé exploité |
|---|---|---|---|
| Identité | Comptes de démonstration | RBAC et clients authentifiés | Gouvernance d'identité, MFA et revue des droits. |
| Réseau | Segmentation locale | Flux autorisés et chiffrés | Architecture cloisonnée, supervision et contrôle industriel. |
| Journaux | Logs applicatifs | Audit utilisateur et sécurité | Centralisation, corrélation et conservation encadrée. |
| Vulnérabilités | Dépendances suivies | Scans et mises à jour testées | Programme produit, CERT, correctifs validés et maintenance. |
| Sauvegardes | Export local | Restauration vérifiée | Copies isolées, PRA/PCA et exercices. |
| Incidents | Scénarios fictifs | Playbook documenté | Cellule de crise, CERT, autorités et procédures cliniques. |
| Continuité | Indication hors ligne | Mode dégradé simulé | Procédure clinique validée et matériel de secours. |

## 6. Sources de référence

- [H48] PGSSI-S, ANS : https://esante.gouv.fr/securite/politique-generale-de-securite-des-systemes-d-information-de-sante
- [H51] Observatoire CERT Santé 2025 : https://cyberveille.esante.gouv.fr/sites/default/files/media/document/2026-05/ANS_CERTSante_Rapport_Public_Observatoire_Signalements_ISSIS_2025_VF_0.pdf
- [H52] CISA Contec CMS8000 : https://www.cisa.gov/sites/default/files/2025-02/fact-sheet-contec-cms8000-contains-a-backdoor-508c_0.pdf
- [H56] BSI ManiMed : https://www.bsi.bund.de/SharedDocs/Downloads/DE/BSI/DigitaleGesellschaft/ManiMed_Abschlussbericht_EN.pdf
