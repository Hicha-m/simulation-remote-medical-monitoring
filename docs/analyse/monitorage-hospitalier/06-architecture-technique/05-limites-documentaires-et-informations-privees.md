# Architecture technique 05 — Informations publiques, privées et inconnues

**Version :** 0.1 — **Date :** 18 novembre 2026

## 1. Informations généralement publiques

| Information | Disponibilité typique |
|---|---|
| Gammes de moniteurs et centrales | Publique |
| Paramètres physiologiques proposés | Publique |
| Fonctionnalités générales | Publique |
| Prérequis réseau de base | Souvent publics |
| Protocoles standards annoncés (HL7, NTP, TLS, etc.) | Souvent publics |
| Principes généraux de cybersécurité | Souvent publics |
| Notices d'utilisation | Variable, souvent publiques |
| Alertes de sécurité et CVE | Publiques lorsque publiées par fabricants ou autorités |
| Marchés publics et lots d'achat | Publics sous réserve des documents accessibles |

## 2. Informations souvent réservées ou propres au déploiement

| Information | Pourquoi elle peut être non publique |
|---|---|
| Manuel réseau détaillé du produit | Peut être réservé aux clients, intégrateurs ou mainteneurs. |
| Liste complète des ports et flux | Document d'installation ou sécurité produit. |
| Protocoles propriétaires et détails du format | Propriété industrielle et compatibilité des produits. |
| Topologie réelle du réseau hospitalier | Sensibilité cybersécurité. |
| Plan d'adressage, VLAN et pare-feu | Informations d'infrastructure sensibles. |
| Comptes de service, certificats et clés | Secrets d'exploitation. |
| Configurations et versions exactes | Peuvent être considérées comme informations internes. |
| Rapports d'audit et tests d'intrusion | Peuvent contenir des faiblesses exploitables. |
| Journaux réseau et d'authentification | Données opérationnelles et potentiellement personnelles. |
| Procédures d'incident et de continuité détaillées | Documents internes de sécurité. |

## 3. Ce qu'il est possible de demander légitimement

Dans le cadre d'un entretien, d'un stage ou d'une visite autorisée :
- familles de systèmes utilisées ;
- rôles des centrales et passerelles ;
- processus d'admission et de transfert ;
- flux fonctionnels entre appareils et systèmes ;
- standards d'interopérabilité ;
- principes généraux de segmentation ;
- procédures de maintenance et de mise à jour ;
- organisation du traitement des alarmes ;
- fonctionnement dégradé en cas de panne.

Il n'est pas nécessaire de demander les adresses IP, les règles de pare-feu détaillées, les identifiants, certificats, secrets, ou rapports de vulnérabilités non publiés pour comprendre le fonctionnement métier.

## 4. Comment obtenir davantage de détails

1. Lire les notices d'utilisation et documents de divulgation de sécurité des modèles exacts.
2. Obtenir les documents réseau via un fournisseur ou intégrateur autorisé.
3. Consulter les CCTP et spécifications publiques de marchés hospitaliers.
4. Interroger un ingénieur biomédical sur l'inventaire, les cycles de maintenance et les interfaces.
5. Interroger la DSI sur l'architecture fonctionnelle et la gouvernance, sans demander de secrets.
6. Interroger les professionnels de soins sur la façon dont ils utilisent les systèmes.
7. Comparer plusieurs déploiements et ne pas généraliser le cas d'un seul fabricant.

## 5. Conclusion

Nous disposons de suffisamment d'informations publiques pour construire une architecture conceptuelle et identifier les grandes technologies. Les détails de protocole, de configuration et d'exploitation réels doivent être complétés par des documents autorisés et des entretiens.

Le POC devra simuler des comportements et interfaces documentés, sans prétendre reproduire les configurations internes privées d'un hôpital.
