
# geOrchestra — Fiche de cours

**Date : 24 septembre 2026**  
**Sujet : comprendre une infrastructure de données spatiales**

> **L’idée principale :** geOrchestra rassemble plusieurs logiciels pour stocker, décrire, publier et consulter des données géographiques, avec une gestion des utilisateurs et des accès.

## 1. Qu’est-ce que geOrchestra ?

**geOrchestra est une infrastructure de données spatiales (IDS), libre, modulaire et interopérable.**

Une **donnée spatiale**, ou donnée géographique, est une information que l’on peut situer sur une carte : une école, une route, une parcelle ou une zone inondable.

Une **infrastructure de données spatiales** est un ensemble d’outils, de services et de règles qui permet d’organiser et de partager ces informations.

**Exemple :** une métropole rassemble les données sur ses pistes cyclables. Les agents peuvent les rechercher, les afficher et les réutiliser pour préparer de nouveaux aménagements.

### Les mots importants

| Mot | Définition simple | Exemple |
|---|---|---|
| **Libre / open source** | Le code peut être consulté, utilisé, modifié et redistribué dans le respect de sa licence. | Une collectivité peut adapter la plateforme à ses besoins. |
| **Modulaire** | La plateforme est composée de plusieurs outils complémentaires. | GeoNetwork gère le catalogue ; GeoServer publie les données. |
| **Interopérable** | Des logiciels différents peuvent échanger grâce à des règles communes. | QGIS peut consulter des services publiés par GeoServer. |
| **OGC** | L’Open Geospatial Consortium définit des standards pour les échanges géographiques. | WMS sert à demander des images de cartes ; WFS permet d’accéder à des objets géographiques et à leurs attributs. |
| **Écosystème** | L’ensemble des outils, organismes, entreprises et personnes qui participent au projet. | Des collectivités et des développeurs partagent leurs améliorations. |

> **Attention :** un logiciel libre peut nécessiter des dépenses d’hébergement, de maintenance et de formation.

*Le mot « foutoir » présent dans les notes initiales reste à clarifier : ce n’est pas un terme technique de geOrchestra.*

## 2. Les acteurs et plateformes cités en cours

Les noms corrigés sont :

- **GéoBretagne** ;
- **CRAIG** ;
- **Rennes Métropole** ;
- **DataGrandEst** ;
- **Géo2France** ;
- **OPenIG** ;
- **Métropole Européenne de Lille (MEL)**.

Ce sont des organismes ou des plateformes liés au partage de l’information géographique. Ils illustrent l’écosystème évoqué en cours ; leurs installations et leurs projets peuvent être différents.

**Exemple concret :** plusieurs organismes d’un même territoire peuvent partager leurs données sur un portail commun au lieu de s’envoyer des fichiers par courriel.

## 3. Les buts et les outils

| But | Outil | Rôle simple | Exemple |
|---|---|---|---|
| **Stocker** | **PostgreSQL + PostGIS** | Conserver et interroger des données géographiques. PostGIS ajoute les fonctions spatiales à PostgreSQL. | Stocker le tracé et la longueur des pistes cyclables. |
| **Cataloguer** | **GeoNetwork** | Décrire les jeux de données et permettre de les retrouver. | Rechercher la fiche « Pistes cyclables », avec sa source et sa date de mise à jour. |
| **Publier et partager** | **GeoServer** | Rendre les données accessibles par des services web. | Fournir une couche consultable dans QGIS ou sur une carte web. |
| **Visualiser des cartes** | **MapStore / mviewer** | Afficher et superposer des couches dans un navigateur. | Voir les pistes cyclables sur un fond de carte. |
| **Créer des tableaux de bord** | **Superset** | Explorer les données et produire des graphiques et indicateurs. | Comparer la longueur des pistes cyclables par commune. |

**Une métadonnée** est une information qui décrit une donnée : son titre, son auteur, sa date, sa précision ou ses conditions d’utilisation.

**À distinguer :** PostGIS sert au **stockage des données**. L’**hébergement** désigne les serveurs et les ressources qui font fonctionner toute la plateforme. Les données peuvent également être conservées dans des fichiers ; elles ne passent pas toutes obligatoirement par PostGIS.

### Schéma simplifié des données

```text
PostGIS                 GeoServer                 MapStore / mviewer
Stocker les données ──► Publier les données ─────► Afficher les cartes
    │
    └───────────────────────────────────────────► Superset
                                                  Tableaux de bord

GeoNetwork : catalogue qui décrit les jeux de données
             et aide à trouver leurs liens d’accès.
```

*Ce schéma explique les rôles. Les connexions exactes dépendent de l’installation.*

## 4. Sécurité, authentification et droits

Ces fonctions concernent l’ensemble de la plateforme.

| Notion | Question à retenir | Exemple |
|---|---|---|
| **Authentification** | Qui es-tu ? | L’utilisateur se connecte avec son compte. |
| **Autorisation / gestion des droits** | Que peux-tu faire ? | Un agent peut modifier une ressource ; un visiteur peut seulement la consulter. |
| **Sécurité** | Comment protéger les services et les données ? | Contrôler les accès, protéger les connexions et maintenir les logiciels à jour. |

### 4.1. Gateway : la porte d’entrée

La **Gateway** reçoit les demandes des utilisateurs et les dirige vers les applications.

- **Reverse proxy, ou proxy inverse :** elle transmet une demande au bon service.
- **Authentification :** elle prend en charge la connexion selon la configuration retenue.
- **Contrôle d’accès :** elle applique des règles d’accès aux applications selon les rôles.
- **Transmission de l’identité :** elle communique aux applications les informations utiles sur l’utilisateur.

**Exemple :** un utilisateur demande à ouvrir la Console. La Gateway contrôle son accès avant de transmettre la demande.

Les applications et des outils spécialisés, comme **GeoFence**, peuvent compléter ce contrôle avec des droits plus précis sur les données.

### 4.2. LDAP : l’annuaire

**LDAP** désigne un protocole d’accès à un annuaire. Dans le cours, « le LDAP » désigne le service d’annuaire utilisé par la plateforme.

Il conserve notamment les comptes, les groupes et les informations sur les organismes. Il peut servir à vérifier les identifiants lors de la connexion.

**Exemple :** le compte d’Amina appartient au groupe « agents ». La plateforme utilise cette appartenance pour appliquer les règles prévues pour ce groupe.

### 4.3. Console : l’administration des comptes

La **Console** est une interface web permettant d’administrer les utilisateurs, les rôles et les organismes.

**Exemple :** un administrateur gère le compte d’Amina et lui attribue le rôle adapté à son travail.

### Schéma simplifié des accès

```text
UTILISATEUR
    │
    ▼
GATEWAY ◄────────────► LDAP
Contrôle l’entrée      Annuaire : comptes et groupes
et oriente                  ▲
    │                       │ gère
    ▼                       │
APPLICATIONS             CONSOLE
Catalogue, cartes…       Interface d’administration
                         accessible via la Gateway
```

> **Mémo :** la Gateway contrôle l’entrée ; LDAP conserve l’annuaire ; la Console permet de l’administrer.

## 5. Déploiement : comment installer la plateforme ?

**Déployer**, c’est installer, configurer et démarrer les composants pour rendre la plateforme utilisable.

Les outils ci-dessous n’ont pas tous le même rôle : certains installent les logiciels, d’autres automatisent les opérations ou organisent les conteneurs.

| Solution | Définition simple | Exemple d’utilisation |
|---|---|---|
| **Paquets Debian** | Paquets logiciels installables sur un système Debian compatible. | Installer les composants directement sur un serveur Linux. |
| **Ansible** | Outil qui automatise l’installation et la configuration à partir de fichiers de tâches appelés *playbooks*. | Reproduire une configuration sur plusieurs serveurs. |
| **Docker Compose** | Outil qui décrit et lance plusieurs conteneurs, généralement sur une même machine. | Démarrer une plateforme de test avec ses différents services. |
| **Docker Swarm** | Outil qui organise des services en conteneurs sur un groupe de machines. | Répartir des services entre plusieurs serveurs. |
| **Kubernetes** | Système qui organise l’exécution de conteneurs sur un ensemble de machines. | Redémarrer un composant défaillant ou gérer plusieurs instances d’un service. |
| **Helm** | Outil qui facilite l’installation et la configuration d’applications dans Kubernetes à l’aide de paquets appelés *charts*. | Utiliser un chart geOrchestra et adapter ses paramètres. |

Un **conteneur** est un environnement isolé qui regroupe une application et ses dépendances. Un **cluster** est un ensemble de machines qui travaillent ensemble.

**Kubernetes fait fonctionner les composants ; Helm aide à les installer et à les configurer.**

La documentation geOrchestra présente notamment Helm, Docker Compose, Ansible et les paquets Debian. Docker Swarm est conservé ici comme notion citée en cours ; il n’est pas présenté comme une procédure officielle équivalente dans le guide consulté. Une configuration de démonstration doit être adaptée avant une utilisation en production.

## 6. Un exemple complet : les pistes cyclables

1. La collectivité prépare un jeu de données sur les pistes cyclables.
2. Elle stocke les tracés et leurs informations dans **PostGIS**.
3. **GeoServer** publie ces données sous forme de services web.
4. Une fiche dans **GeoNetwork** explique leur contenu, leur origine et leur date.
5. Les habitants consultent une carte avec **MapStore** ou **mviewer**.
6. Les agents peuvent utiliser **Superset** pour comparer des indicateurs par commune.
7. Pour les accès réservés, la **Gateway** prend en charge la connexion et le contrôle d’accès ; **LDAP** fournit les informations de compte et de groupe dans cette configuration.
8. L’administrateur utilise la **Console** pour gérer les comptes et les rôles.

*Cet exemple est pédagogique : les modules et les droits sont choisis selon les besoins de l’organisme.*

## 7. Les phrases à retenir

> **geOrchestra est une infrastructure de données spatiales libre, modulaire et interopérable.**
>
> **PostGIS stocke, GeoNetwork catalogue, GeoServer publie, MapStore et mviewer affichent les cartes, Superset présente des indicateurs.**
>
> **L’authentification vérifie qui je suis ; l’autorisation définit ce que je peux faire.**

## 8. Le schéma d’architecture de geOrchestra

![Schéma d’architecture geOrchestra fourni pendant le cours](../../images/architecture-georchestra.png)

Une **architecture** décrit les composants d’un système et leurs relations. Ce schéma donne une vue d’ensemble des services, de l’authentification et des bases de données.

### 8.1. Comment lire le schéma ?

- **À gauche : l’entrée et la connexion.** La Gateway reçoit les demandes. L’authentification peut s’appuyer sur LDAP ou sur un fournisseur externe OAuth2 / OIDC.
- **Au centre : les applications.** La grande zone arrondie regroupe les services accessibles derrière la Gateway : catalogue, cartes, import et administration.
- **À droite : les ressources complémentaires.** On trouve notamment des bases de données, un serveur web et des outils d’import ou de statistiques.
- **Les flèches** indiquent des échanges ou des dépendances. Elles ne représentent pas toutes un déplacement de l’utilisateur entre les écrans.

### 8.2. Les couleurs et les symboles

Selon la légende de cette image :

| Symbole ou couleur | Signification |
|---|---|
| **Violet foncé** | Composant du cœur de la plateforme. |
| **Violet clair** | Module optionnel pris en charge par la communauté geOrchestra. |
| **Jaune / orange** | Module optionnel que cette légende indique comme non pris en charge par la communauté geOrchestra. |
| **Cylindre** | Base de données. |
| **MD** | Métadonnées : informations qui décrivent les données. |
| **SVC** | Service. |

*Cette légende décrit le schéma fourni. Un module optionnel peut être très utile ; tous les modules représentés ne sont pas nécessairement installés sur la plateforme du cours.*

### 8.3. Les composants supplémentaires à comprendre

| Composant | Rôle simple dans ce schéma | Exemple pédagogique |
|---|---|---|
| **Datahub** | Interface pour consulter et rechercher des données et leurs métadonnées, lues depuis GeoNetwork. | Rechercher la fiche d’un jeu de données sur les départements. |
| **Metadata-editor** | Interface pour rédiger et modifier les métadonnées. | Corriger le titre, la description et les mots-clés d’une fiche. |
| **Gn-cloud-ogc-records** | Fournit une interface standard OGC API Records pour accéder au catalogue. | Permettre à une autre application de rechercher des fiches. |
| **Datafeeder** | Outil d’import qui s’appuie sur GeoServer et GeoNetwork. | Introduire un nouveau jeu de données dans la plateforme. |
| **Airflow** | Organise l’exécution des tâches utilisées par Datafeeder. | Enchaîner plusieurs étapes d’un import. |
| **GeoWebCache** | Met en cache des tuiles cartographiques pour accélérer leur affichage. | Réutiliser une portion de carte déjà préparée. |
| **GeoContrib** | Outil de contribution et de signalement collaboratif. | Signaler un problème localisé sur une carte. |
| **Cadastrapp** | Application consacrée à la consultation cadastrale. | Consulter des informations sur une parcelle, selon les droits. |
| **Vrt-bot** | Outil d’import utilisant des descriptions VRT des sources de données. | Alimenter une base à partir de sources configurées. |
| **Analytics CLI / TimescaleDB** | Outil de préparation des données statistiques et base utilisée ici pour les traces d’accès. | Préparer des statistiques de fréquentation. |
| **Superset** | Outil de visualisation de données ; il lit ici les données de TimescaleDB. | Afficher un tableau de bord sur l’utilisation de la plateforme. |

### 8.4. Exemple : retrouver les départements sur une carte

1. L’utilisateur arrive sur la plateforme : ses demandes passent par la **Gateway**.
2. Si une connexion est nécessaire, le système vérifie son identité avec le mécanisme configuré.
3. Dans **Datahub**, il recherche « départements » et consulte une fiche provenant de **GeoNetwork**.
4. Si la fiche propose un lien cartographique, il peut ouvrir les données dans un visualiseur comme **MapStore**.
5. Le visualiseur demande les données ou les cartes aux services de publication, notamment **GeoServer**.

> **La distinction essentielle : GeoNetwork décrit les données ; Datahub présente le catalogue ; GeoServer diffuse les données ; MapStore affiche les cartes.**

*Source de cette section : schéma fourni par l’utilisateur pendant le cours. Les exemples expliquent les rôles ; ils ne constituent pas une vérification de la configuration réelle de la plateforme.*

## Sources pour réviser

- [Présentation geOrchestra — FOSS4G Europe 2017 (SlideShare)](https://fr.slideshare.net/slideshow/ge-orchestra-opensourceinspiresdiprojectstatusfoss4geu2017/78226277) : présentation historique de 2017, à replacer dans le contexte de cette époque.
- [Documentation geOrchestra — Read the Docs](https://georchestra-main-documentation.readthedocs.io/) : lien complémentaire fourni pendant le cours.
- [Présentation et composants de geOrchestra](https://www.georchestra.org/fr/) : définition, modules et fonctions.
- [Projet geOrchestra](https://www.georchestra.org/fr/projet.html) : logiciel libre, interopérabilité et communauté.
- [Documentation générale](https://www.georchestra.org/fr/documentation.html) : accès aux guides des composants.
- [Guide de la Gateway](https://docs.georchestra.org/gateway/en/latest/user_guide/) : authentification, routage et contrôle d’accès.
- [Architecture de la Gateway](https://docs.georchestra.org/gateway/en/latest/arc42/context_view/) : liens avec LDAP et la Console.
- [Guide d’installation](https://docs.georchestra.org/georchestra/install_guide/) : différentes méthodes de déploiement.
- [Démarrage avec Docker](https://github.com/georchestra/docker) : environnement de démarrage à adapter pour la production.
- [Documentation Superset pour geOrchestra](https://docs.georchestra.org/superset/en/latest/) : tableaux de bord et visualisation de données.
- [Communauté geOrchestra](https://www.georchestra.org/fr/communaute.html) : acteurs et projets.
