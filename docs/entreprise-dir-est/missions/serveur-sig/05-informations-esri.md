# 05 --- Informations transmises par Esri

## Pourquoi demander ces informations ?

Ma première collecte ne donnait pas suffisamment d'informations sur les
ressources de la machine actuelle. Des informations complémentaires ont
donc été demandées à Esri afin d'obtenir une référence technique de
l'existant.

## Infrastructure actuelle communiquée

Les informations reçues décrivent **DIREST1**, utilisé pour
l'environnement ArcGIS Enterprise et PostgreSQL.

  Élément                                         Valeur
  ------------------- ----------------------------------
  vCPU                                             **8**
  RAM                                          **32 Go**
  Disque C:                                   **500 Go**
  Système               **Windows Server 2022 Standard**
  ArcGIS Enterprise                             **11.5**
  PostgreSQL                                   **16.15**
  SDE                                           **11.5**
  IIS                                           **10.0**

``` text
DIREST1
├── 8 vCPU
├── 32 Go RAM
├── C: 500 Go
├── ArcGIS Enterprise 11.5
├── PostgreSQL 16.15 / SDE
└── IIS 10
```

Les 8 vCPU, 32 Go de RAM et 500 Go correspondent à la machine décrite,
et non uniquement à PostgreSQL.

## Exploitation actuelle

Les informations reçues montrent aussi des activités de supervision, de
mise à jour et de surveillance de l'environnement. Il faut donc prendre
en compte non seulement le serveur, mais également son exploitation et
sa maintenance.

Le rapport indique également un volume important de services ArcGIS sur
la plateforme.

## Ce que cela apporte

Avant, plusieurs ressources étaient inconnues. Les informations Esri
donnent maintenant une **référence de l'existant**.

Elles ne signifient pas qu'une future infrastructure interne doit
automatiquement reprendre exactement 8 vCPU, 32 Go de RAM et 500 Go. Le
dimensionnement dépendra de l'architecture retenue et des besoins réels.


## Schéma récapitulatif

![Architecture actuelle structurée](images/04-architecture-actuelle.png)
