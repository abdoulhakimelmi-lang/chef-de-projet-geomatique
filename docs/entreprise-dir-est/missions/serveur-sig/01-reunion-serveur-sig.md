# 01 --- Préparation de la réunion : serveur SIG interne

## Contexte

Le Pôle SIG de la DIR Est étudie la mise en place d'un **serveur SIG
interne**. L'objectif est de pouvoir gérer davantage les données, les
accès et les droits en interne.

La réflexion répond à deux enjeux exprimés dans le document de réunion
: - **souveraineté des données** : conserver la capacité de gérer les
données de manière autonome ; - **logique économique** : étudier à moyen
ou long terme la possibilité de réduire la dépendance à l'infogérance
Esri et aux VDI.

## Questions de la réunion

L'étude doit répondre progressivement aux questions suivantes : - Quel
type d'infrastructure mettre en place ? - Quelles ressources prévoir :
CPU, RAM et stockage ? - Quel système d'exploitation utiliser ? - Quels
modes de sauvegarde prévoir ? - Quelle version de PostgreSQL/PostGIS
utiliser ? - Comment garantir la compatibilité avec ArcGIS Enterprise,
ArcGIS Pro et QGIS ? - Quel paramétrage prévoir pour PostGIS et ses
dépendances ? - Peut-on faire cohabiter ArcGIS Server avec GeoServer,
QGIS Server ou MapServer ? - Quels hébergements seraient encore
nécessaires et pour quel coût ? - Quelles opérations de maintenance
planifier ? - Comment permettre l'installation d'ArcGIS Pro sur les
postes ? - Comment migrer si l'infogérance Esri GéoCloud est abandonnée
? - Comment réaliser un audit des données et supprimer les doublons ? -
Existe-t-il des organisations utilisant ArcGIS tout en gérant leurs
données de manière autonome ?

## Démarche

``` text
Besoin
  ↓
Comprendre les notions
  ↓
Collecter l'existant
  ↓
Construire des options
  ↓
Obtenir les informations Esri
  ↓
Intégrer le retour du tuteur
  ↓
Préparer les échanges avec le BSI
```
