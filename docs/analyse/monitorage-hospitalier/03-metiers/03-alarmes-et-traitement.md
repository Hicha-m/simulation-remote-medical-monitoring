# Métier 03 — Alarmes, événements et traitement

**Version :** 0.1 — **Date :** 18 novembre 2026

## 1. Une alarme n'est pas une simple notification

Dans un environnement de monitorage, il faut séparer :
- la détection d'une condition par un appareil ;
- le signal local (sonore ou visuel) ;
- le report vers une centrale ;
- la notification vers un autre poste ou un terminal ;
- la réception par une personne ;
- la vérification de l'événement ;
- la réponse humaine ;
- la documentation et la clôture.

La technologie peut signaler une condition, mais le traitement par le professionnel est un processus organisationnel distinct.

## 2. Familles d'événements à différencier

| Famille | Exemple | Signification |
|---|---|---|
| Alarme physiologique | Paramètre surveillé hors limite configurée. | Condition physiologique signalée par le moniteur. |
| Alarme de rythme / événement ECG | Événement détecté par l'analyse ECG de l'appareil. | Événement à vérifier par le personnel compétent. |
| Alarme technique | Électrode débranchée, capteur absent, défaut du dispositif. | Le signal ou l'appareil ne fonctionne pas comme attendu. |
| Événement réseau | Moniteur non joignable, liaison radio perdue. | La centrale peut ne plus recevoir les informations. |
| Événement de batterie | Batterie faible ou autonomie insuffisante. | Risque d'interruption du dispositif. |
| Événement organisationnel | Alarme non acquittée, absence de réponse, transfert non réalisé. | Le workflow ou l'organisation doit être vérifié. |

Il ne faut jamais traiter une donnée absente comme une mesure physiologique normale.

## 3. Priorités et signaux d'alarme

La norme IEC 60601-1-8 définit des exigences de sécurité et de performance essentielle pour les systèmes d'alarme des appareils et systèmes électromédicaux. Elle définit des catégories de priorité selon le degré d'urgence, des signaux cohérents et des états de contrôle [H28].

La norme ne décide pas à elle seule :
- si un équipement doit avoir une alarme ;
- quelle condition précise doit déclencher une alarme ;
- quelle priorité clinique attribuer à chaque condition ;
- par quel mécanisme technique le signal est généré.

Ces points sont décrits dans le champ de la norme elle-même et dépendent des équipements et de leur destination [H28]. Les règles cliniques ne doivent donc pas être reconstituées arbitrairement dans un POC.

## 4. Le report d'alarme dans un service de soins critiques

La HAS identifie plusieurs destinations possibles :
- moniteur local du patient ;
- centrale d'alarme au poste de soins ;
- moniteurs d'autres chambres (inter-chevet) ;
- répétiteurs dans les zones de circulation ;
- terminaux portatifs affectés à un professionnel ou un secteur.

Elle demande également des procédures relatives au paramétrage patient, à l'utilisation du report d'alarme, à la réduction de la pollution sonore, à la vérification lors des admissions et des relèves, et à la présence de personnel près de la centrale [H02].

Cela montre que l'alarme doit être conçue comme une chaîne de notification et de réponse, pas comme un simple bouton rouge dans une interface.

## 5. Workflow de traitement à analyser

1. **Détection** — un appareil identifie une condition selon sa configuration.
2. **Qualification technique** — le système identifie l'appareil, le patient, la source et la catégorie d'événement.
3. **Signalement local** — le dispositif avertit selon ses propres règles.
4. **Report** — la centrale ou un système de notification reçoit l'événement.
5. **Attribution** — l'événement est rattaché à l'équipe ou au secteur responsable.
6. **Prise de connaissance** — un professionnel voit ou acquitte l'alarme.
7. **Évaluation** — la personne compétente vérifie la situation.
8. **Réponse** — une action est prise selon le protocole de service.
9. **Transmission** — l'événement est communiqué à l'équipe concernée si nécessaire.
10. **Clôture** — résultat et statut sont documentés.

Ce workflow est un modèle fonctionnel pour la discussion, pas un protocole clinique.

## 6. Pourquoi la gestion des alarmes est un sujet métier majeur

Une revue de cadrage de 2025 portant sur la gestion des alarmes en soins intensifs analyse 23 études et regroupe les stratégies observées autour de l'ajustement des paramètres d'alarme, de la formation du personnel, de la standardisation de l'utilisation des dispositifs, des outils d'assistance et des procédures de réponse [H29].

Une étude de télémétrie hospitalière a évalué un mécanisme rappelant aux infirmiers de réexaminer les limites d'alarme des patients générant un nombre particulièrement élevé d'alarmes. Elle rapporte une réduction de la durée moyenne des alarmes après intervention [H15].

Les études montrent donc que le volume, la pertinence et la réponse aux alarmes sont des problèmes d'organisation et d'usage, pas uniquement de programmation.

## 7. Besoins métier candidats

- définir les catégories d'événements ;
- distinguer alarme physiologique et alarme technique ;
- attribuer une priorité sans inventer de seuil médical ;
- diffuser chaque événement vers les postes appropriés ;
- identifier le patient, le lit et l'appareil ;
- afficher l'heure de survenue et l'heure de réception ;
- gérer l'acquittement séparément de la résolution ;
- permettre la transmission d'une alerte à un autre professionnel ;
- conserver les actions et les changements de statut ;
- analyser les volumes, répétitions, durées et événements non traités ;
- permettre la gestion de paramètres adaptée par personnel habilité ;
- détecter l'indisponibilité du chemin d'alarme.

## 8. Indicateurs observables à mesurer dans un POC

Ces indicateurs sont techniques ou organisationnels ; ils ne mesurent pas une performance clinique.

- nombre d'événements produits par type ;
- nombre d'événements transmis et reçus ;
- délai détection → centrale ;
- délai centrale → notification ;
- délai réception → prise de connaissance ;
- délai de traitement et clôture ;
- nombre d'événements répétés ;
- nombre d'alarmes sans acquittement ;
- nombre d'alarmes techniques ;
- nombre d'alarmes simultanées ;
- nombre d'événements perdus ou dupliqués ;
- durée de perte du réseau ;
- nombre de changements de priorité ou de configuration.

## 9. Sources

- **[H02]** HAS, Flash Sécurité Patient — surveillance des patients en soins critiques : https://www.has-sante.fr/jcms/p_3511526/fr/flash-securite-patient-surveillance-des-patients-en-service-de-soins-critiques-une-veille-sans-faille-pour-qu-aucun-patient-ne-defaille
- **[H15]** Technological Intervention to Improve Alarm Management in Acute Care Telemetry Units, 2023 : https://pubmed.ncbi.nlm.nih.gov/37343111/
- **[H28]** IEC 60601-1-8, ISO catalogue — exigences et guidance sur les alarmes électromédicales : https://www.iso.org/standard/41986.html
- **[H29]** Clinical alarm management in intensive care units: A scoping review, 2025 : https://pubmed.ncbi.nlm.nih.gov/40289413/
