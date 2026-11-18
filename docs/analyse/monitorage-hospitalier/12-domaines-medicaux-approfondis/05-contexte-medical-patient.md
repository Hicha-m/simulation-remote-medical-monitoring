# 05 — Informations médicales associées au patient

**Version :** 1.0 — **Date :** 18 novembre 2026  
**Objectif :** définir les informations nécessaires au monitorage sans reconstruire inutilement l'intégralité du dossier patient informatisé.

## 1. Séparer les objets métier

Le modèle doit distinguer au minimum :

- **Patient** : personne prise en charge ; identité interne stable.
- **Séjour / Encounter** : épisode hospitalier, avec admission, origine, destination et sortie.
- **Mouvement / Location history** : succession des unités, chambres et lits avec dates d'effet.
- **Dispositif** : moniteur, capteur, centrale ou appareil associé.
- **Affectation patient-appareil** : association datée entre un dispositif et un patient/séjour.
- **Session de monitorage** : intervalle durant lequel un patient est surveillé par un ensemble de sources.
- **Observation** : mesure numérique ou valeur dérivée.
- **Segment waveform** : bloc de données brutes avec canal et fréquence.
- **Alarme** : événement et cycle de gestion humain/technique.
- **Contexte clinique** : informations minimales qui expliquent le profil de surveillance.

Ces objets ont des cycles de vie différents. Un patient peut avoir plusieurs séjours, un séjour plusieurs unités, un lit plusieurs occupants au cours du temps et un appareil plusieurs associations successives.

## 2. Informations patient : niveaux de nécessité

| Donnée | Raison possible dans un système de monitorage | Priorité proposée | Règle |
|---|---|---|---|
| Identifiant patient interne | Association fiable de toutes les données | Obligatoire | Identifiant unique et non réutilisé dans le jeu de simulation. |
| Nom affiché fictif / alias | Reconnaissance visuelle pendant la démonstration | Utile | Valeur synthétique clairement signalée. |
| Date de naissance ou âge | Vérifier le profil de population / distinguer adulte et pédiatrique | À confirmer | Préférer une tranche d'âge si la date exacte n'est pas nécessaire. |
| Sexe/traits pertinents | Seulement si un cas d'usage documenté en dépend | À confirmer | Ne pas collecter par défaut. Conserver la provenance du champ. |
| Identifiant de séjour | Lier les observations à un épisode donné | Obligatoire | Séparer du patient. |
| Service, chambre, lit | Situer la surveillance et router l'alarme | Obligatoire si carte/centrale multi-lits | Historiser les transferts. |
| Motif d'admission / type de prise en charge | Aider à construire un scénario cohérent | Utile pour scénarios | Ne pas transformer en diagnostic automatique. |
| Antécédents / facteurs de risque | Peut expliquer un profil de surveillance simulé | Optionnel | Limiter à ce qui est nécessaire au scénario. |
| Allergies | Pertinent pour un dossier patient global, pas forcément pour un monitorage seul | Généralement hors noyau | Ne pas les ajouter sans fonction attendue. |
| Traitements / prescriptions | Contexte pour certains scénarios ou intégration DPI | Optionnel / extension | Ne pas simuler de prescription/administration si hors sujet. |
| Taille, poids | Peut contextualiser un patient et certains équipements/calculs | Optionnel | Valeurs et dates de référence explicites. |
| Directives / statut de réanimation | Donnée extrêmement sensible et dépendante du contexte ; pas nécessaire au premier modèle de monitorage | Hors noyau par défaut | Ne l'ajouter qu'avec justification métier et validation. |

Le projet doit distinguer les données nécessaires à l'identification, celles utiles au scénario, et celles qui relèvent du dossier clinique général.

## 3. Dossier patient français et identitovigilance

Le ministère distingue le volet administratif (état civil, débiteurs, entourage) et le volet médical, et rappelle que le dossier patient est constitué à l'admission [H136]. Le Code de la santé publique décrit le contenu du dossier médical ; la version juridique exacte doit être vérifiée dans sa rédaction consolidée en vigueur au moment d'un éventuel usage réglementaire.

L'Identité Nationale de Santé (INS) et le Référentiel National d'Identitovigilance (RNIV) structurent l'identification et le référencement des données de santé en France [H126, H127]. Ce ne sont pas de simples champs libres à recopier.

Pour notre modèle :
- utiliser des identifiants de démonstration propres au projet ;
- ne jamais fabriquer un NIR/NIA ou une INS ressemblant à un identifiant réel ;
- ne pas collecter nom réel, date de naissance réelle, coordonnées ni pièce d'identité ;
- représenter, si nécessaire, un statut d'identité fictif : provisoire, vérifié dans la simulation, en anomalie ;
- distinguer collision d'identité, doublon, patient inconnu et identité non qualifiée ;
- prévoir que les règles INS/RNIV réelles ne sont pas implémentées simplement en générant un matricule.

## 4. Contexte clinique minimal du scénario

Pour rendre un patient simulé cohérent, le dossier de scénario peut contenir :

- profil de population (adulte/pédiatrique/néonatal) ;
- contexte d'admission ;
- unité et période ;
- facteurs influençant le choix des paramètres monitorés ;
- liste de sources/appareils affectés ;
- état de la surveillance ;
- événements du parcours ;
- règles synthétiques de déclenchement d'événements, clairement identifiées comme simulation.

Il est préférable de créer un **profil de scénario** plutôt que d'inventer un dossier médical complet.

## 5. États du parcours patient

- PLANNED : admission ou transfert prévu.
- ADMITTED : séjour ouvert.
- IN_UNIT : patient affecté à une unité et à un lit.
- IN_TRANSPORT : déplacement en cours, avec surveillance/équipement de transport si scénarisé.
- TRANSFERRED : ancien lieu clos, nouveau lieu ouvert.
- DISCHARGED : séjour terminé.
- IDENTITY_REVIEW : incohérence d'identification à examiner.
- UNKNOWN_PATIENT : observation reçue sans correspondance fiable.

Ces états sont proposés pour le système de simulation et doivent être affinés avec le modèle d'admission/transfert retenu.

## 6. Scénarios critiques d'identité et de contexte

1. Deux patients possèdent des noms affichés semblables mais des identifiants internes distincts.
2. Un appareil reste lié à l'ancien patient après transfert.
3. Une observation arrive avec un patientId inconnu.
4. Deux séjours distincts du même patient sont ouverts à des dates différentes.
5. Un mouvement de transfert arrive après une observation déjà reçue.
6. Un patient sans lit confirmé est visible dans la zone d'admission.
7. Une identité passe de provisoire à vérifiée dans le scénario.
8. Une correction d'identité doit être auditée sans réécrire silencieusement l'historique.

## 7. Références

- [H126] Ministère de la Santé, identitovigilance et dossier patient.
- [H127] Agence du Numérique en Santé, Référentiel INS v2.1, RNIV et guide d'implémentation.
