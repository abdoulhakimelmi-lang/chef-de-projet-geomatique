# TP — Charte projet : SIG pour la ville de Montauban

> Source unique : `TP Charte projet.pdf` — 7 pages. Les repères de page suivent l’ordre du PDF.

## Sujet du TP

<a id="page-1"></a>

### Projet de SIG pour la ville de Montauban

*Source : page 1.*

**Sujet du TP — Parties 1 et 2.**

SYSTEME D’INFORMATION

GEOGRAPHIQUE

Projet de SIG pour la ville de Montauban

Élaboration du Schéma Directeur du Système

D’Information Géographique

<a id="page-2"></a>

### Présentation — Expression des besoins

*Source : page 2.*

Votre société a remporté un projet pour la ville de Montauban et vous a nommé chef du projet.

Dans ce document, vous trouverez l’ensemble des éléments du projet vous permettant de répondre aux questions du TP.

**PREAMBULE**

**1 Territoire de compétence du SIG**

La Collectivité d’agglomération du Grand Montauban qui regroupe 11 communes, couvre 230 km² et représente 76 000 habitants.

La commune de Montauban couvre 135 km² et abrite 62 000 habitants.

Les services de l’agglomération et les services de la ville sont regroupés au sein d’un organigramme commun.

Les compétences exercées sont soit du ressort de la commune, soient de la collectivité soient mutualisées.

**2 Contexte : le SIG existant**

Historiquement rattaché à la direction de l’urbanisme, de l’aménagement et de la prospective, le service SIG est devenu une direction à part entière, rattaché à la Direction générale de l’Attractivité.

La direction de l’attractivité regroupe les directions

- de l’économie et de l’emploi
- du tourisme,
- du développement culturel et du patrimoine
- des projets urbains
- de l’urbanisme, de l’aménagement et de la prospective

Le SIG n’est pas une compétence communautaire et intervient en appui de l’ensemble des directions générales adjointes et des directions qui les composent quelle que soit leurs collectivités de rattachement

Actuellement un seul agent est en charge du SIG.

Il a été réalisé en interne un audit des besoins qu’il est nécessaire de compléter.

Il détaille les aspects administratifs, techniques, données, matériel, diffusion des données et retour sur investissement pour le SIG, mais reste à approfondir et à compléter.


<a id="page-3"></a>

### Expression des besoins (suite)

*Source : page 3.*

- Les outils Actuellement il existe un Web SIG géré en sous traitance.

Ce web SIG est utilisé par les services de l’agglomération, de la ville mais également des communes membres du GMCA.

Au final plus de 250 comptes utilisateurs existent sur cette application.

Les données du Web SIG sont dupliquées quotidiennement dans une base de données interne POSTGRE/POST GIS et sont accessibles principalement à l’agent du SIG.

Par ailleurs il existe différentes versions de Qgis installées, au cas par cas, sans stratégie de déploiement, soit directement par les services soit par l’agent en charge du SIG.

Au-delà de la pluralité des outils utilisés, on constate des problèmes d’interopérabilité avec des systèmes informations plus ou moins déconnecté du SIG (ADS, DIA, ANC).

Ce schéma directeur SIG s’inscrira pleinement dans la politique informatique de la collectivité et de la Direction des systèmes d’informations (DSI) ainsi que la stratégie de Smart City que la collectivité développe.

- Les données Une information géographique très inégale selon les services, de nombreuses données, sont de simples documents DAO/CAO, ou sous format papier, ou sont inexistantes matériellement et reposent sur la mémoire d’agents au sein des services.

Les données concernant les recollements sont très hétérogènes selon les bureaux d’étude et les demandes des services utilisateurs. Ces derniers ayant peu de connaissance sur les formats géographiques nécessaires à l’information géographique. Le schéma directeur devra couvrir l’ensemble des données géographiques ainsi que celle relevant du volet CAO/DAO.

La rareté des outils ne favorise pas le porté à connaissance, auprès de tous, des données existantes sur le territoire de la collectivité. Le futur SIG doit donc apporter une solution cohérente et facilitatrice pour la gestion et la diffusion des métadonnées et des données en interne comme à l’extérieur.

Le schéma directeur devra préconiser un mode de gestion des données, que ce soient des données de référence (cadastre, orthophotos, PLU, …) ou des données métiers (inventaires,…) ainsi que leurs méthodologies d’actualisation via un cycle de vie des données pour chaque grande famille.

La collectivité doit faire face à des obligations règlementaires liées à ses compétences (PLU, PLH, DT/DICT, PCRS, plan de sauvegarde, …) tant dans le suivi de documents cadres que dans la diffusion de ces derniers.

Enfin, le SIG actuel n’est pas en prise avec nos obligations INSPIRE et assure peu voire pas du tout la diffusion de la donnée.

Seules certaines thématiques sont aujourd’hui valorisées par les services (PLH, urbanisme)

Les domaines de la 3D, Atlas, Cartes, schémas directeurs thématiques, analyses sectorielles sont encore inexistants.


<a id="page-4"></a>

### Expression des besoins (suite) — Le projet à réaliser

*Source : page 4.*

- Les ressources Les ressources internes SIG existantes étant assez limitées, le service s’appuie sur son prestataire.

La continuité de service du SIG est aujourd’hui précaire.

- La relation aux communes L’outil de webSIG mis en place est mis à disposition des communes qui peuvent consulter les données.

Il n’y a pas de mise en œuvre d’un véritable service commun à destination des communes.

**3 Le projet à réaliser`**

La collectivité a décidé l’élaboration du « Schéma Directeur du Système d’Information Géographique».

Le projet de schéma directeur s’inscrit dans le cadre d’un besoin d’évolution du SIG vers une nouvelle architecture tant technique que méthodologique, homogène et intégrant des nouveaux besoins et contraintes méthodologiques, légales, législatives et normatives auxquels la collectivité doit se conformer.

Le schéma directeur doit aboutir à la définition du futur SIG de nos collectivités, avec la prise en compte des enjeux d’homogénéisation, de capitalisation et valorisation, de partage et de diffusion de l’information géographique.

**Ce partage se fait sur 3 plans :**

- en interne en direction des différents services,
- en partenariat avec les communes membres, et les autres institutions et les partenaires (institutions, gestionnaires de réseaux, DSP, …)
- en externe à destination des administrés d’une part et des citoyens d’autre part.

Il donne les voies et les moyens pour atteindre cet objectif à partir d’un scénario choisi se basant sur l’analyse des systèmes existants, sur un recueil identifiant les utilisateurs, leurs attentes et fléchant les besoins émergents et futurs et sur les choix des politiques publiques que les élus font.

Ce projet doit éclairer sur les arbitrages fondamentaux en réalisant une synthèse des enjeux et des éléments de contexte. En se basant sur les échanges avec les agents de la collectivité, le retour d’expérience d’autres collectivité de taille similaire et l’expertise propre du prestataire.

Ce travail constitue un préalable à la seconde étape, la refonte du SIG au travers du choix de nouveaux outils.


<a id="page-5"></a>

### Déroulement du projet

*Source : page 5.*

**4 Déroulement du Projet**

Le projet se découpe en 3 phases. Chacune d’elles donne lieu à la livraison d’un rapport détaillé.

Durée du projet Le délai d’exécution de la prestation est de 5 mois à compter de la notification du marché.

Le calendrier envisagé est le suivant

Phase 1 Audit de l’existant et recensement des besoins aout-septembre 2022

En se basant sur le « pré schéma directeur » existant et en complétant les éléments manquants au regard de l’expertise du prestataire.

Une attention particulière sera apportée sur un bilan des obligations légales/règlementaires à remplir par la collectivité

**Phase 2 Diagnostic et proposition de scenarii octobre 2022**

Phase 3 Elaboration du schéma directeur du SIG novembre 2022

Suivi du projet o Le Comité de Pilotage (COPIL)

Il a pour mission d’arbitrer et de valider les propositions faites par l’équipe projet en examinant les orientations techniques, fonctionnelles et organisationnelles proposées au regard des orientations générales de la collectivité.

**Le comité de pilotage sera, à minima, composé de :**

- Un élu
- La Direction Générale (1 DGS + 5 DGA)

**o Le Groupe projet ou COTECH**

Sa mission est d’assurer le pilotage opérationnel du projet. Il assure le relai entre le soumissionnaire et les différents services de la collectivité. Il valide les documents produits et est force de proposition auprès du COPIL.

**A géométrie variable, le groupe projet est composé par :**

- Directeur du SIG
- Groupe d’expertise technique composé, selon les thématiques abordées, de référents au sein des Direction générales, de la Direction des systèmes d’information et complété par les référents des services concernés


<a id="page-6"></a>

### Déroulement du projet (suite)

*Source : page 6.*

**Méthode de travail**

Les travaux de l’étude seront coordonnés par l’équipe projet du prestataire, qui travaillera de façon permanente en liaison avec les services du maître d’ouvrage.

Le prestataire a la charge de la préparation et l’animation des réunions de travail et des COPIL, il sera autonome dans la réalisation des entretiens.

Tous les contacts utiles seront facilités par les services du maître d’ouvrage.

Modalités de remise des documents Avant tout COPIL et COTECH, le prestataire devra établir un support de présentation provisoire pour le soumettre au directeur du SIG qui émettra ses recommandations.

Chaque phase fera de plus l’objet de la rédaction d’une note synthétique ayant pour objet l’information des membres du COPIL.

D’une manière générale chaque réunion fera systématiquement l’objet d’un compte-rendu rédigé et transmis pour validation au maître d’ouvrage sous 10 jours ouvrés. Ces comptes rendus seront diffusés par le chef projet du prestataire aux membres du COPIL et du Groupe Projet.

Les livrables seront envoyés par voie électronique dans un format bureautique classiques modifiables et une version PDF.

**L’ensemble des livrables devra contenir à minima les informations suivantes :**

- Rédacteur : personne en charge de la rédaction du livrable
- Destinataires : personnes destinataires du livrable
- Date de création du livrable
- Tableau de suivi des mises à jour apportées au livrable
- Dernière date de modification du livrable
- Logo de la collectivité
- Numéro de version : les numéros de version devront respecter la forme « classique » telle que :
- V0.x : où x représente le numéro de version du livrable en phase de rédaction
- V1.x : où x représente le numéro de version du livrable en phase de validation

Voici la liste des membres pressentis du COTECH

- Développement durable.
- Communication
- Direction ressources

ü DRH, à minima le service formation.

ü DAJPA : ü DSI ü Finances

- Direction Attractivité

ü SUAP ü Economie


<a id="page-7"></a>

### Documents et modèles (suite)

*Source : page 7.*

ü Culture

- Direction Services technique

ü Bâtiment : BE Eclairage public ü Cycle de l’eau ü DVI ü Espace vert

- Direction Solidarité et action sociale

ü Développement social ü Habitat

- Direction service à la population

ü Vie civile et citoyenne ü Vie des quartiers

Voici la liste des membres pressentis du COPIL

- Elu Chargé de l’aménagement – prospectives et patrimoine
- Elue Chargée du développement durable, de l’environnement, des réseaux publics et des parcs et jardins
- Elu Chargé de la voirie, des espaces publics, du stationnement et des déplacements doux.
- DGS
- Les 5 DGA

