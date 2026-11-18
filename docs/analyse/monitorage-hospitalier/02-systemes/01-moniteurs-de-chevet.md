# Système 01 — Moniteurs de chevet et moniteurs multiparamétriques

**Version :** 0.1 — **Date :** 18 novembre 2026

## 1. Rôle du moniteur de chevet

Le moniteur de chevet est un équipement placé à proximité du patient. Il reçoit des signaux de capteurs ou de modules, calcule ou affiche des paramètres et signale des conditions d'alarme selon sa configuration.

Il peut fonctionner de façon autonome ou être relié à un système de surveillance central. Le type de paramètres, le nombre de courbes, la capacité de stockage et les options dépendent du modèle et des modules présents.

## 2. Paramètres couramment proposés

| Paramètre / signal | Origine possible | Type de représentation |
|---|---|---|
| ECG / fréquence cardiaque | Électrodes ECG | Courbes et valeur numérique. |
| SpO₂ / pouls | Oxymètre de pouls | Valeur et pléthysmogramme. |
| Pression artérielle non invasive (PNI) | Brassard | Mesure ponctuelle ou périodique. |
| Pression artérielle invasive | Cathéter et transducteur | Courbe et valeurs dérivées. |
| Respiration | Impédance thoracique, capteur ou appareil | Courbe et fréquence. |
| CO₂ / capnographie | Capteur respiratoire | Courbe et valeur. |
| Température | Sonde | Valeur, parfois plusieurs sites. |
| Paramètres ventilatoires | Ventilateur connecté selon système | Valeurs, courbes et alarmes externes. |

Cette liste est illustrative : les paramètres disponibles dépendent de la destination, du modèle, des modules et des options.

## 3. Exemples de gammes commercialisées

### Philips IntelliVue

La gamme française présente les modèles MX750 et MX850 pour les soins intensifs et l'anesthésie, le X3 pour les soins intensifs et le transport, et le MX100 comme moniteur portable autonome utilisable pendant le transport [H06].

### GE HealthCare CARESCAPE

GE documente une famille de moniteurs multiparamétriques configurables selon les zones de soins et les profils patients. La documentation B450 cite des usages dans de nombreuses unités de soins et le transport intrahospitalier [H07].

### Dräger Infinity M540

Dräger présente un moniteur de chevet qui peut être retiré de sa station d'accueil pour le transport, avec transmission sans fil au réseau de monitorage et récupération des données au retour sur station d'accueil. Le fabricant annonce 72 heures de tendances et d'événements accessibles à l'accrochage, et des fonctions de continuité dans son système [H10].

### Mindray BeneVision

Mindray classe ses gammes selon les environnements d'acuité élevée, moyenne ou faible et le transport. La famille TM80 est dédiée à la télémétrie portable plutôt qu'au seul monitorage fixe [H09, H21].

## 4. Besoins fonctionnels autour d'un moniteur

- identifier l'appareil et son modèle ;
- identifier le patient et le lieu de soin ;
- connecter et surveiller les capteurs ;
- afficher les paramètres et courbes disponibles ;
- enregistrer les mesures, tendances et événements ;
- gérer les limites et priorités d'alarme configurées ;
- signaler les défauts techniques (capteur débranché, batterie, réseau, etc.) ;
- conserver les données en cas de transport ou de perte temporaire de connectivité selon les capacités du système ;
- permettre la consultation de données historiques ;
- autoriser les actions de configuration aux rôles habilités.

## 5. Opérations infirmières concrètes à prendre en compte

Une étude de test d'utilisabilité de moniteurs physiologiques décompose les tâches infirmières en plusieurs familles : admission, transport et sortie du patient ; saisie d'informations patient ; branchement de capteurs ; réglage des mesures et limites d'alarme ; analyse ECG ; export d'un ECG 12 dérivations ; résolution de problèmes d'alarmes techniques comme une électrode débranchée [H22].

Ces tâches sont intéressantes pour établir des cas de test. L'étude porte sur des scénarios de simulation et ne prétend pas décrire toutes les organisations hospitalières.

## 6. Sources

- **[H06]** Philips, moniteurs patient IntelliVue : https://www.philips.fr/healthcare/brand/intellivue-patient-monitors
- **[H07]** GE HealthCare, CARESCAPE B450 : https://www.gehealthcare.com/fr-fr/products/patient-monitoring/patient-monitors/carescape-monitor-b450
- **[H09]** Mindray, BeneVision TM80 : https://www.mindray.com/fr/products/patient-monitoring/telemetry-monitoring/benevision-tm80
- **[H10]** Dräger, Infinity M540 : https://www.draeger.com/fr_fr/Products/Infinity-M540-monitor
- **[H21]** Mindray, gamme de surveillance patient : https://www.mindray.com/fr/products/patient-monitoring
- **[H22]** Improving the Safety, Effectiveness, and Efficiency of Clinical Alarm Systems: Simulation-Based Usability Testing of Physiologic Monitors, 2021 : https://nursing.jmir.org/2021/1/e20584

## 7. Questions à approfondir

- Quelles données sont effectivement émises par le moniteur et lesquelles sont uniquement affichées localement ?
- Les courbes brutes sont-elles conservées et pendant combien de temps ?
- Comment un moniteur est-il associé au patient ?
- Comment les alarmes sont-elles configurées et contrôlées ?
- Quels appareils communiquent directement avec les centrales ?
- Quelles données sont reprises au retour d'un transport ?
