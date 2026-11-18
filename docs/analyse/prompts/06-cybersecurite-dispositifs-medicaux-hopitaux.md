# 06 — Prompt : rechercher la cybersécurité et les incidents des dispositifs médicaux hospitaliers

## Prompt réutilisable

Tu es chargé d'étudier la cybersécurité des systèmes de monitorage hospitalier et des systèmes d'information hospitaliers, ainsi que les incidents publiquement documentés.

Le but est de comprendre les protections en place, les vulnérabilités publiées, les attaques et fuites confirmées, leurs conséquences et les mesures de prévention. Il s'agit d'un travail défensif et documentaire pour un projet académique.

## Périmètre à séparer

Analyser au moins quatre catégories différentes :
1. vulnérabilités de moniteurs et de dispositifs médicaux ;
2. vulnérabilités des centrales, passerelles et logiciels d'intégration ;
3. attaques contre le SI des hôpitaux ;
4. fuites ou compromissions chez les fabricants, hébergeurs et fournisseurs.

## Sources à rechercher

- CISA, FDA, ICS-CERT, CERT Santé et ANS ;
- ANSSI, CNIL, autorités sanitaires et rapports d'établissement ;
- avis de sécurité des fabricants (Philips, GE, Dräger, Mindray, etc.) ;
- CVE, avis de correctifs, bulletins de sécurité ;
- rapports indépendants de laboratoires de sécurité ;
- PGSSI-S, IEC 80001-1 et référentiels applicables ;
- communiqués de presse officiels et enquêtes post-incident.

## Pour chaque incident

Documenter :
- date de publication et date réelle de l'événement ;
- cible et type de système ;
- vulnérabilité ou vecteur initial, seulement si confirmé ;
- déroulement connu à un niveau défensif ;
- données consultées, volées ou publiées ;
- systèmes et services indisponibles ;
- conséquences opérationnelles ou cliniques connues ;
- mesures de confinement et de remédiation ;
- recommandations et enseignements ;
- statut de preuve et informations inconnues.

## Statuts de preuve obligatoires

Utiliser explicitement :
- vulnérabilité identifiée ;
- exploitation confirmée ;
- tentative d'attaque rapportée ;
- attaque confirmée ;
- fuite confirmée ;
- absence d'incident connu à la date d'un avis ;
- résultat de test en laboratoire ;
- allégation d'un fournisseur ou d'une victime non vérifiée indépendamment.

Ne jamais écrire « appareil attaqué » lorsqu'une vulnérabilité est seulement publiée. Ne jamais présenter une fuite comme confirmée sans source. Ne jamais supposer qu'un incident ransomware a touché des moniteurs cliniques si la source mentionne seulement le SI général.

## Analyse défensive

Pour chaque problème, identifier les contrôles à étudier :
- inventaire et gestion des versions ;
- segmentation des réseaux biomédicaux ;
- filtrage et restrictions des flux ;
- authentification des utilisateurs et dispositifs ;
- MFA et accès distant ;
- chiffrement et gestion des certificats ;
- mises à jour validées par le fabricant ;
- gestion des comptes prestataires et temporaires ;
- journaux, détection, alertes ;
- sauvegardes isolées et restauration ;
- mode dégradé et continuité clinique ;
- réponse à incident et notification appropriée.

Ne pas fournir de procédure offensive, d'exploitation reproductible, de code malveillant ou de test sur une infrastructure réelle.

## Format de sortie

1. Résumé par catégories de menace.
2. Protections annoncées par fabricant, avec flux et versions.
3. Tableau des incidents et vulnérabilités, statuts de preuve.
4. Études de cas détaillées.
5. Enseignements par scénario.
6. Prévention, détection, réponse et continuité.
7. Matrice de menaces.
8. Scénarios de tests défensifs non destructifs pour un environnement de laboratoire.
9. Sources datées, fiables et précises.
10. Limites de l'information publique.

## Paramètres

- Date de recherche : [à compléter]
- Géographie : France, Europe et international pour les alertes fabricants.
- Domaine : dispositifs médicaux connectés, moniteurs, centrales, SI hospitalier.
