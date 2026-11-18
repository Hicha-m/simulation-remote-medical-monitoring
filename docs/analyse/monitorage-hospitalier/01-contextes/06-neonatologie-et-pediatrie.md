# Environnement 06 — Néonatologie et pédiatrie

**Version :** 0.1 — **Date :** 18 novembre 2026  
**Statut :** premier repérage ; à approfondir avec un professionnel de néonatologie ou de pédiatrie.

## 1. Pourquoi ce contexte mérite une étude séparée

Le monitorage d'un nouveau-né ou d'un enfant ne peut pas être traité comme une simple copie du monitorage adulte avec un autre nom de patient.

Les paramètres, accessoires, tailles de capteurs, populations, réglages et alarmes peuvent varier selon l'âge, la maturité et la pathologie. Les sources scientifiques sur les unités néonatales décrivent notamment la surveillance cardiorespiratoire continue et un volume important d'alarmes, avec des problématiques spécifiques de charge sonore et de fatigue des équipes [H31, H32].

## 2. Éléments documentés en France

L'arrêté du 25 avril 2000 relatif aux unités de néonatologie et de réanimation néonatale décrit des équipements de surveillance cardiorespiratoire, hémodynamique, de saturation et de ventilation, avec des dispositifs adaptés au nouveau-né. Il prévoit également des procédures de transfert et de transmissions d'informations entre unités [H30].

**Précaution réglementaire :** la source Légifrance consultée affiche la version initiale de cet arrêté. Son état consolidé et son articulation avec les textes plus récents doivent être vérifiés avant toute conclusion sur les obligations actuellement en vigueur. Les descriptions suivantes l'utilisent comme un repère documentaire historique, pas comme une validation exhaustive du droit applicable en 2026.

## 3. Paramètres et dispositifs étudiés

La littérature sur les unités de soins intensifs néonatals décrit notamment :
- ECG et activité cardiaque ;
- plethysmogramme et SpO₂ ;
- fréquence respiratoire ;
- pression artérielle dans certains cas ;
- paramètres de ventilation ;
- alarmes cardiorespiratoires et de saturation [H31, H32].

Des appareils indépendants peuvent également être présents dans l'environnement du nouveau-né : ventilateurs, pompes à perfusion, incubateurs et dispositifs de thermorégulation. Leur intégration dans une centrale dépend du système et du service ; il ne faut pas supposer que tous sont connectés au même moniteur.

## 4. Un besoin métier majeur : les alarmes adaptées à la population

Une revue systématique publiée en 2026 analyse 23 études d'interventions de réduction des alarmes dans des unités pédiatriques : 12 en NICU, 2 en PICU, 8 en unités médicales/chirurgicales et une étude combinée. Les approches observées incluent la formation des équipes, l'adaptation des paramètres selon l'âge ou la condition, l'ajustement des délais et la standardisation des communications relatives au plan de monitorage [H31].

Une étude menée dans une unité néonatale de 18 lits a observé une réduction importante du nombre d'alarmes après l'implémentation d'une solution de gestion des alarmes et une optimisation du workflow et des réglages [H32]. Il s'agit d'une étude de centre unique ; ses résultats ne doivent pas être généralisés sans précaution.

## 5. Besoins métiers candidats

| ID | Besoin | Pourquoi |
|---|---|---|
| NEO-01 | Distinguer les profils nouveau-né, enfant et adulte. | Les besoins de monitorage et les accessoires peuvent différer. |
| NEO-02 | Associer des capteurs adaptés au patient. | L'acquisition dépend de capteurs et de tailles spécifiques. |
| NEO-03 | Conserver le contexte d'âge et de maturité nécessaire à la configuration autorisée. | Les réglages d'alarme peuvent être adaptés à l'âge et à la condition. |
| NEO-04 | Afficher les paramètres cardiorespiratoires et les courbes. | La surveillance décrite dans les sources est multiparamétrique. |
| NEO-05 | Distinguer alarmes répétitives et événements distincts. | Le volume de notifications est un sujet documenté. |
| NEO-06 | Tracer les changements de paramètres d'alarme. | Les réglages sont un élément important de la gestion du risque. |
| NEO-07 | Préserver la continuité lors du transfert vers une autre unité. | Les textes décrivent des procédures de transfert et d'information. |
| NEO-08 | Associer clairement les dispositifs et le patient. | Plusieurs appareils peuvent être présents autour d'un même lit. |

## 6. Scénarios à étudier

- admission d'un nouveau-né et association des équipements ;
- changement de capteur ;
- déconnexion du capteur SpO₂ ;
- alarmes répétitives de saturation ;
- événement cardiorespiratoire simulé ;
- modification contrôlée d'un réglage par rôle autorisé ;
- transfert vers une unité de réanimation néonatale ;
- transfert vers une autre unité spécialisée ;
- consultation de l'historique des alarmes et des réglages.

Les conditions physiologiques et seuils utilisés dans un POC resteraient fictifs et ne doivent pas reproduire des prescriptions réelles sans validation professionnelle.

## 7. Sources

- **[H30]** Légifrance, arrêté du 25 avril 2000 relatif aux dispositifs médicaux et examens pratiqués en néonatologie et réanimation néonatale (version initiale consultée) : https://www.legifrance.gouv.fr/jorf/id/JORFTEXT000000582539
- **[H31]** Interventions to Reduce Monitor Alarms Across Pediatric Inpatient Settings: A Systematic Review, *Hospital Pediatrics*, 2026 : https://pubmed.ncbi.nlm.nih.gov/42442759/
- **[H32]** Optimisation of clinical workflow and monitor settings safely reduces alarms in the NICU, *Acta Paediatrica*, 2021 : https://pmc.ncbi.nlm.nih.gov/articles/PMC7983880/

## 8. Questions à approfondir

- Les besoins de néonatologie/pédiatrie sont-ils dans le périmètre du projet ou doivent-ils rester un scénario d'extension ?
- Quelles différences d'appareils et de capteurs un système actuel doit-il gérer ?
- Qui fixe et révise les réglages d'alarme ?
- Comment sont gérées les alarmes des moniteurs, incubateurs, ventilateurs et pompes ?
- Quelle est l'organisation des alarmes dans les chambres individuelles et les zones ouvertes ?
