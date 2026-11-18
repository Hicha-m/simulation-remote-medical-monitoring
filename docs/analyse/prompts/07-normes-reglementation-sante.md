# 07 — Prompt : rechercher les normes, textes réglementaires et recommandations en santé

## Prompt réutilisable

Tu conduis une recherche documentaire sur les normes, réglementations et recommandations applicables à un système de monitorage hospitalier multiparamétrique.

Le projet étudié est un POC académique de simulation logicielle. Il ne s'agit pas de commercialiser ou d'exploiter un dispositif médical, sauf indication contraire explicite.

## Objectifs

1. Identifier les normes relatives aux moniteurs multiparamétriques, ECG, SpO2, pression artérielle et alarmes.
2. Identifier les normes de gestion des risques, cycle de vie logiciel, facteurs humains, réseau médical et cybersécurité des logiciels de santé.
3. Identifier les standards d'interopérabilité et de représentation des données.
4. Identifier les règlements européens et les cadres français pertinents.
5. Identifier les recommandations HAS, ANSM, ANS, CNIL et CERT Santé.
6. Séparer ce qui est juridiquement obligatoire de ce qui constitue une norme volontaire, une guidance ou une recommandation.

## Sources à privilégier

- IEC Webstore, ISO, CENELEC et listes de normes harmonisées publiées au Journal officiel de l'Union européenne.
- EUR-Lex, Légifrance et Commission européenne / MDCG.
- ANS, PGSSI-S, CI-SIS, HDS, programme CaRE.
- HAS, ANSM, CNIL, ANSSI, CERT Santé.
- Publications et guides techniques des organismes de normalisation et autorités compétentes.

## Pour chaque référence

Collecter :
- numéro complet et intitulé ;
- organisme émetteur ;
- édition, amendements et corrigenda ;
- date de publication ;
- statut actuel et éventuelle révision en cours ;
- domaine d'application précis ;
- type de produit ou d'acteur concerné ;
- caractère obligatoire, volontaire, harmonisé, contractuel ou recommandé ;
- pertinence pour le monitorage hospitalier ;
- pertinence pour un simulateur académique ;
- conséquences possibles pour les exigences et tests ;
- URL officielle et date de consultation.

## Règles strictes

- Ne pas confondre IEC et EN IEC.
- Ne pas déclarer une norme harmonisée sans vérifier la référence publiée au Journal officiel.
- Ne pas supposer que toute norme médicale s'applique à un simulateur logiciel.
- Ne pas affirmer qu'une norme est obligatoire sans identifier le texte qui la rend pertinente.
- Vérifier les versions et amendements à la date de recherche.
- Distinguer la qualification réglementaire d'un logiciel de son apparence ou de son nom.
- Pour le MDR, vérifier la finalité prévue et la règle de classification logicielle applicable.
- Pour HDS, vérifier le rôle de l'hébergeur, le type de données et les conditions de l'article L.1111-8.
- Indiquer explicitement les informations qui restent à faire valider juridiquement.

## Format de sortie

1. Résumé des textes et normes prioritaires.
2. Tableau des normes matérielles.
3. Tableau des normes logicielles et qualité.
4. Tableau des standards réseau, sécurité et interopérabilité.
5. Tableau des obligations réglementaires.
6. Tableau des recommandations institutionnelles.
7. Matrice d'applicabilité au POC.
8. Questions ouvertes.
9. Bibliographie avec versions et dates.

## Paramètres

- Date de recherche : [à compléter]
- Domaine : monitorage hospitalier
- Géographie : France et Union européenne
- Finalité du projet : [simulation académique / dispositif médical / autre]
