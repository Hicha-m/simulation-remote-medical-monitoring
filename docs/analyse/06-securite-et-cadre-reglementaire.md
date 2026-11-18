# 06 — Sécurité et cadre réglementaire

**Version :** 0.1 — **Date :** 18 novembre 2026  
**Statut :** repérage des sujets à examiner ; ce document n'est pas un avis juridique et ne conclut pas à la conformité d'un système.

## 1. Pourquoi la sécurité est un axe central

Le sujet annonce que les données sont sensibles. Des informations physiologiques associées à une personne peuvent révéler son état de santé et relever de la catégorie des données concernant la santé au sens du RGPD. L'article 9 encadre le traitement de catégories particulières de données personnelles, dont les données de santé [S21].

La sécurité doit donc être envisagée dans tout le cycle :

- création du patient et de son identité ;
- association d'un appareil ;
- émission et transmission ;
- réception et stockage ;
- consultation du tableau de bord ;
- création et traitement des alertes ;
- gestion des comptes et des accès ;
- sauvegarde, export, archivage et suppression ;
- maintenance, journalisation et gestion des incidents.

## 2. Périmètre prudent pour un POC académique

Le POC devrait utiliser exclusivement des données synthétiques, produites pour le projet et sans correspondance avec des patients réels.

Les mesures, identités, dossiers, appareils et événements doivent être fictifs. Les scénarios doivent être explicitement présentés comme des simulations, et les seuils utilisés pour déclencher une démonstration ne doivent jamais être présentés comme des seuils médicaux ou des recommandations de prise en charge.

Il est également prudent de ne pas connecter la démonstration à des appareils médicaux réels, à un dossier patient hospitalier ou à un environnement de production sans accord, cadrage et autorisations explicites.

Cette recommandation de prudence ne remplace pas une analyse juridique si le projet évolue vers le traitement de données réelles.

## 3. RGPD et données de santé

### Points de repère

- Les données concernant la santé font partie des catégories particulières visées à l'article 9 du RGPD [S21].
- Le traitement nécessite une base juridique et une condition applicable au traitement des catégories particulières ; elles doivent être déterminées en fonction du contexte.
- Les rôles de responsable de traitement, sous-traitant et éventuels destinataires doivent être identifiés.
- Les finalités, catégories de données, personnes concernées, accès, durées de conservation et sous-traitants doivent être définis.
- Les droits des personnes et les procédures en cas d'incident doivent être étudiés.
- Une analyse d'impact relative à la protection des données peut être requise selon la nature du traitement et ses risques.

Ce document ne détermine aucune base juridique applicable au projet : l'analyse dépendrait de l'organisme, des finalités, des personnes concernées et des traitements réellement mis en œuvre.

## 4. Hébergement de données de santé (HDS)

L'Agence du Numérique en Santé précise que l'obligation de certification HDS vise les entités fournissant un service d'hébergement portant sur des données de santé à caractère personnel recueillies dans le cadre d'activités de prévention, diagnostic, soins ou suivi médico-social, pour le compte du patient ou d'organismes à l'origine du recueil. Les conditions sont cumulatives et l'applicabilité doit être appréciée au cas par cas [S17].

Conséquences pour l'étude :

- le mot « santé » ne suffit pas à conclure automatiquement que tout hébergement est soumis à HDS ;
- le chiffrement ne transforme pas une donnée de santé personnelle en donnée non personnelle ;
- le rôle de l'hébergeur et le fait d'héberger pour le compte d'un tiers doivent être examinés ;
- l'architecture, le prestataire, les accès distants et la localisation des traitements peuvent compter ;
- il faudra vérifier la version du référentiel applicable au moment du projet.

### Évolution HDS v2.1 — point de vigilance daté

Le support de l'Agence du Numérique en Santé présenté au Comité des entreprises du numérique en santé du 30 septembre 2026 indique que le projet d'arrêté et la version 2.1 ont été notifiés à la Commission européenne le 25 août 2026. Ce même support prévoit une publication par arrêté à horizon décembre 2026, puis l'application des nouveaux contrôles trois mois après publication [S18].

Une autre page ANS publiée précédemment annonce une échéance prévisionnelle d'octobre 2026. Les calendriers ont donc évolué. À la date de cette analyse, 18 novembre 2026, la dernière indication datée examinée est le calendrier du 30 septembre qui prévoit décembre 2026 ; il faudra revérifier la publication effective avant toute décision de déploiement [S18].

## 5. Dispositif médical et logiciel de santé

Le règlement européen 2017/745 définit le dispositif médical en fonction de la destination prévue par le fabricant, notamment pour le diagnostic, la prévention, la surveillance, la prédiction, le pronostic ou le traitement d'une maladie [S22].

Il faut donc distinguer :

- un logiciel général de démonstration ou d'administration ;
- un simulateur pédagogique de mesures ;
- un outil d'aide à l'organisation ou à l'affichage ;
- un logiciel destiné à surveiller, prédire ou contribuer à une décision médicale ;
- un dispositif médical numérique de télésurveillance soumis à des règles spécifiques.

Le nom du projet, le langage utilisé ou la présence de mesures physiologiques ne suffisent pas à déterminer son statut réglementaire. La finalité prévue, les fonctionnalités, la documentation et les usages réels doivent être analysés.

Le POC décrit dans ce dossier est étudié comme une simulation pédagogique. Aucune revendication de diagnostic, de traitement, de prévention ou de décision clinique n'est formulée.

## 6. Principes de sécurité à étudier

| Domaine | Question de conception | Exemples de contrôles à envisager |
|---|---|---|
| Identité utilisateur | Qui se connecte ? | Comptes individuels, authentification robuste, gestion des sessions. |
| Habilitations | À quelles données l'utilisateur a-t-il accès ? | Rôles, périmètres patients, moindre privilège et revue des droits. |
| Identité appareil | Quelle source est autorisée à transmettre ? | Identifiant d'appareil, authentification machine, révocation. |
| Transport | Les données sont-elles protégées en transit ? | TLS, validation des certificats et gestion des secrets. |
| Intégrité | Une mesure peut-elle être modifiée ou rejouée ? | Contrôle d'intégrité, identifiant unique, horodatage, détection des rejeux. |
| Stockage | Qui peut lire ou modifier les données persistées ? | Droits minimaux, chiffrement selon le risque, séparation des environnements. |
| Journalisation | Qui a consulté ou modifié quoi ? | Traces d'accès, de modification, d'administration et d'incident. |
| Sauvegardes | Comment restaurer les données ? | Copies protégées, tests de restauration et séparation des accès. |
| Disponibilité | Comment réagir en cas de panne ? | Supervision, files d'attente, procédures de reprise et signalement d'indisponibilité. |
| Interface | Comment éviter les erreurs de contexte ? | Affichage clair du patient, de l'appareil, de l'heure et de la fraîcheur des données. |
| Maintenance | Comment mettre à jour sans introduire de vulnérabilité ? | Dépendances suivies, mises à jour, tests et gestion des secrets. |

## 7. Habilitations et journalisation

La CNIL recommande de limiter les accès aux données nécessaires à la mission de l'utilisateur, notamment au moyen de profils d'habilitation et du principe de moindre privilège [S20].

La CNIL recommande également la traçabilité des opérations : activités métier, interventions techniques, actions d'administration, anomalies et événements de sécurité. Les journaux doivent être protégés contre les accès et modifications non autorisés ; la CNIL donne des précautions sur les données à journaliser et la durée de conservation [S19].

Pour le projet, cela suggère d'étudier au minimum :

- la consultation d'une fiche patient ;
- la consultation d'un historique ;
- l'acquittement et la clôture d'une alerte ;
- la modification d'une configuration ;
- la création, suspension ou révocation d'un compte ;
- les connexions réussies et échouées ;
- les opérations d'administration ;
- les erreurs d'accès et de transmission.

La durée de conservation des journaux ne sera pas fixée ici : elle dépendra du contexte, des obligations et de l'analyse de risque.

## 8. Modèle de menace préliminaire

Les menaces ci-dessous servent de base à une analyse plus détaillée :

| Menace | Impact potentiel | Question de protection |
|---|---|---|
| Usurpation d'un compte soignant | Consultation ou modification non autorisée | Authentification et moindre privilège. |
| Faux appareil | Envoi de mesures attribuées à un patient | Authentification des clients et association contrôlée. |
| Modification de mesure | Information erronée affichée ou conservée | Intégrité, provenance et contrôles. |
| Rejeu de messages | Mesures comptabilisées plusieurs fois | Identifiants uniques et idempotence. |
| Écoute réseau | Divulgation de données | Chiffrement en transit. |
| Exposition de base de données | Divulgation ou altération de dossiers | Segmentation, accès, chiffrement et sauvegardes. |
| Administrateur trop privilégié | Accès étendu aux dossiers | Séparation des rôles et journalisation protégée. |
| Fuite via les logs | Réplication de données sensibles | Minimisation des logs et masquage des secrets. |
| Déni de service | Perte de visibilité sur les données | Limitation de débit, supervision et procédures de continuité. |
| Rançongiciel ou corruption | Indisponibilité ou perte de données | Sauvegardes isolées et restauration vérifiée. |
| Mauvaise association appareil-patient | Mesures attribuées à la mauvaise personne | Cycle de vie des associations et validation. |
| Tableau de bord périmé | Décision fondée sur une information ancienne | Afficher la dernière réception et l'état de fraîcheur. |

## 9. Sécurité fonctionnelle et sécurité clinique

La sécurité informatique ne garantit pas à elle seule la sécurité de l'utilisation médicale.

Exemples de situations à distinguer :

- une mesure absente n'est pas une valeur normale ;
- une mesure reçue n'est pas forcément une mesure fiable ;
- une alerte visible n'est pas forcément acquittée ;
- une alerte acquittée n'est pas forcément résolue ;
- une valeur simulée ne constitue pas une donnée clinique ;
- une règle logicielle de démonstration n'est pas un protocole médical validé.

La simulation devra rendre ces distinctions visibles.

## 10. Références réglementaires et institutionnelles

- [S17] ANS — champ d'application HDS.
- [S18] ANS — Comité ENS du 30 septembre 2026, support relatif à HDS v2.1.
- [S19] CNIL — sécurité : tracer les opérations.
- [S20] CNIL — sécurité : gérer les habilitations.
- [S21] RGPD — règlement (UE) 2016/679.
- [S22] Règlement (UE) 2017/745 relatif aux dispositifs médicaux.

## 11. Questions restantes

1. Le projet utilise-t-il exclusivement des données synthétiques et fictives ?
2. L'environnement restera-t-il local et isolé ?
3. Le projet doit-il démontrer une authentification des clients simulateurs ?
4. Quels rôles nécessitent des droits différents ?
5. Quelles actions doivent être journalisées ?
6. Comment montrer qu'une donnée est ancienne ou qu'un appareil est hors ligne ?
7. Quelle politique de conservation est nécessaire pour le démonstrateur ?
8. Une intégration externe, un hébergement tiers ou des données réelles sont-ils envisagés ?
9. À quelle étape faut-il faire valider les aspects juridiques et réglementaires par un encadrant ou un spécialiste ?

**Aucune conformité HDS, RGPD, CE, ISO 27001 ou autre n'est revendiquée pour le projet.**
