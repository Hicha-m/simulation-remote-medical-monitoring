# 03 — Prompt : construire des scénarios et des cas limites

## Prompt réutilisable

À partir d'un sujet de système de télésurveillance ou de monitorage patient, construis une bibliothèque de scénarios réalistes et vérifiables pour un environnement de simulation logicielle.

### Règles

- Ne pas inventer de protocole de soin.
- Ne pas inventer de seuil médical.
- Ne pas présenter les règles d'un scénario de test comme une recommandation clinique.
- Les valeurs physiologiques doivent être synthétiques et les seuils purement démonstratifs tant qu'ils n'ont pas de validation clinique.
- Distinguer les alertes techniques, les événements de qualité de données et les alertes métier ou médicales.
- Préciser le contexte : patient hospitalisé, domicile ou hybride.
- Identifier qui agit et à quel moment.
- Prévoir les situations nominales, les incidents, les pannes et les actions utilisateurs.

### Familles de scénarios à couvrir

1. Création et clôture de suivi.
2. Association et remplacement d'appareil.
3. Transmission périodique et continue.
4. Données manquantes.
5. Déconnexion et reconnexion.
6. Retard, doublon, désordre et rejeu.
7. Mauvais format, mauvaise unité et horodatage incohérent.
8. Artefact ou mauvaise qualité de signal.
9. Plusieurs patients et appareils simultanés.
10. Création, affichage, acquittement, transfert et clôture d'alerte.
11. Relève entre équipes.
12. Indisponibilité serveur, base ou dashboard.
13. Surcharge de messages.
14. Connexion, accès interdit et révocation de droits.
15. Sauvegarde et restauration.

### Format obligatoire par scénario

- Identifiant.
- Nom.
- Contexte d'utilisation.
- Objectif du test.
- Acteur déclencheur.
- Préconditions.
- Événement déclencheur.
- Séquence chronologique.
- Résultat attendu côté serveur.
- Résultat attendu côté interface.
- Données à persister.
- Journaux et métriques à produire.
- Variantes et cas limites.
- Critères de réussite.
- Ce qui reste à valider avec des professionnels.

### Sortie attendue

- Tableau synthétique des scénarios.
- Fiches détaillées des scénarios prioritaires.
- Couverture des risques.
- Dépendances entre scénarios.
- Scénarios qui nécessitent une validation métier ou clinique.

Ne pas choisir les technologies avant d'avoir décrit les échanges et les résultats attendus.
