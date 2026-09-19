# 03 --- Première collecte d'informations

## Objectif

Avant de proposer une nouvelle infrastructure, j'ai commencé par
répondre à la question : **qu'avons-nous actuellement ?**

Cette première collecte a servi à identifier l'environnement, les bases
et les informations encore manquantes.

## Éléments identifiés

La collecte faisait apparaître notamment : - 3 VDI VMware Horizon ; -
une VM Windows Server 2022 ; - IIS ; - Portal for ArcGIS ; - ArcGIS
Server fédéré ; - ArcGIS Data Store ; - PostgreSQL ; - Web Adaptors ; -
FTP.

## Bases PostgreSQL observées

  Base             Taille Remarque
  ----------- ----------- -----------------------------------
  `entgdb`          73 Go Géodatabase Enterprise principale
  `amiante`         13 Go Autre base
  **Total**     **86 Go** Données utiles observées

## Connexion PostgreSQL collectée

-   serveur : `postgres.sig-direst.fr` ;
-   port : `5432` ;
-   rôle d'administration observé : `sde` ;
-   connexions maximales observées : `100`.

## Informations qui manquaient encore

À ce moment de la collecte, je cherchais encore : - la RAM de la VM ; -
le nombre de vCPU ; - la capacité totale de stockage ; - l'espace disque
disponible.

## Schéma de ma collecte

![Infos collectées --- serveur
actuel](images/infos-collectees-serveur-actuel.png)

Cette page représente donc **mon état des lieux initial**, avant la
réception des informations complémentaires d'Esri.
