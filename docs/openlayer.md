# 1. Cours théorique — OpenLayers

## 1.1 Qu'est-ce qu'OpenLayers ?

OpenLayers est une bibliothèque JavaScript permettant de créer des cartes interactives dans une page Web.

Une bibliothèque JavaScript est un ensemble de fonctions déjà développées que nous pouvons utiliser dans notre propre programme.

Avec OpenLayers, nous pouvons par exemple :

- afficher un fond de carte ;
- afficher des données géographiques ;
- afficher des données GeoJSON ;
- afficher des données provenant d'une base PostgreSQL/PostGIS ;
- gérer plusieurs couches ;
- appliquer une symbologie ;
- récupérer les coordonnées d'un clic ;
- sélectionner un objet ;
- afficher une popup ;
- géolocaliser l'utilisateur ;
- interagir avec la carte.

OpenLayers travaille donc principalement du côté **client**, c'est-à-dire dans le navigateur Web de l'utilisateur.

---

## 1.2 Une application cartographique Web

Une application Web SIG peut faire intervenir plusieurs technologies.

Exemple :

```text
PostgreSQL / PostGIS
        ↓
       PHP
        ↓
     GeoJSON
        ↓
JavaScript / OpenLayers
        ↓
   Navigateur Web
        ↓
      Carte
```

Il faut bien différencier les rôles.

### HTML

HTML permet de construire la structure de la page.

Exemple :

```html
<div id="carte"></div>
```

Ici, nous créons un élément HTML qui recevra notre carte.

---

### CSS

CSS permet de définir l'apparence des éléments HTML.

Exemple :

```css
#carte {
    width:100%;
    height:80%;
}
```

Cela signifie que l'élément `carte` occupe :

- 100 % de la largeur ;
- 80 % de la hauteur.

---

### JavaScript

JavaScript permet de rendre la page dynamique.

C'est avec JavaScript que nous allons utiliser OpenLayers.

Par exemple :

```javascript
var map = new ol.Map({...});
```

---

### OpenLayers

OpenLayers fournit les objets nécessaires pour construire et manipuler la carte.

Par exemple :

```text
ol.Map
ol.View
ol.layer
ol.source
ol.style
ol.Overlay
ol.Geolocation
```

---

## 1.3 Charger OpenLayers dans une page HTML

Pour utiliser OpenLayers, il faut charger la bibliothèque JavaScript et sa feuille de style.

Exemple :

```html
<script src="https://cdn.jsdelivr.net/npm/ol@v10.10.0/dist/ol.js"></script>

<link rel="stylesheet"
href="https://cdn.jsdelivr.net/npm/ol@v10.10.0/ol.css">
```

Le fichier JavaScript contient les fonctionnalités d'OpenLayers.

Le fichier CSS contient les styles nécessaires à l'affichage de la carte et des contrôles OpenLayers.

---

# 1.4 Les principaux objets OpenLayers

Pour comprendre OpenLayers, il faut retenir cette logique :

```text
SOURCE
  ↓
LAYER
  ↓
MAP
  ↓
VIEW
```

En français :

```text
SOURCE = d'où viennent les données ?

LAYER = comment ces données deviennent une couche ?

MAP = quelles couches sont présentes dans la carte ?

VIEW = où regarde-t-on sur la carte ?
```

Ces quatre notions sont fondamentales.

---

# 1.5 La source — `ol.source`

Une source indique à OpenLayers **d'où viennent les données**.

Exemples :

```text
OpenStreetMap
GeoJSON
XYZ
WMS
données vectorielles
```

Pour OpenStreetMap :

```javascript
var source_osm = new ol.source.OSM();
```

Ici :

```text
new
```

permet de créer un nouvel objet.

Et :

```text
ol.source.OSM
```

représente une source OpenStreetMap.

---

# 1.6 La couche — `ol.layer`

Une couche permet d'afficher une source sur la carte.

Par exemple :

```javascript
var couche_osm = new ol.layer.Tile({
    source:new ol.source.OSM()
});
```

Il faut comprendre :

```text
new ol.source.OSM()
        ↓
     SOURCE
        ↓
new ol.layer.Tile()
        ↓
      LAYER
```

`Tile` signifie que la carte est constituée de **tuiles**.

Une tuile est une petite image constituant une partie de la carte.

Lorsque plusieurs tuiles sont assemblées, elles donnent l'impression d'avoir une seule grande carte.

---

# 1.7 La carte — `ol.Map`

La carte principale est créée avec :

```javascript
new ol.Map()
```

Exemple :

```javascript
var map = new ol.Map({
    target:'carte',
    layers:[couche_osm]
});
```

### `target`

```javascript
target:'carte'
```

indique dans quel élément HTML la carte doit être affichée.

Cela correspond à :

```html
<div id="carte"></div>
```

Il y a donc une relation directe :

```text
HTML

<div id="carte"></div>

        ↕

JavaScript

target:'carte'
```

### `layers`

```javascript
layers:[couche_osm]
```

indique les couches qui doivent être ajoutées à la carte.

---

# 1.8 La vue — `ol.View`

Une carte ne suffit pas.

Il faut également préciser **où regarder**.

C'est le rôle de :

```javascript
ol.View
```

Exemple :

```javascript
map.setView(new ol.View({
    center:[709043,6235462],
    zoom:13
}));
```

### `center`

```javascript
center:[709043,6235462]
```

correspond au centre de la carte.

Les deux nombres correspondent à :

```text
X = 709043
Y = 6235462
```

### `zoom`

```javascript
zoom:13
```

détermine le niveau de zoom.

Plus la valeur est élevée, plus nous sommes proches du terrain.

---

# 1.9 Les projections

Une coordonnée n'a de sens que si nous connaissons son système de coordonnées.

Dans notre application OpenLayers, nous utilisons notamment :

```text
EPSG:3857
```

Il s'agit du **Web Mercator**.

C'est une projection très utilisée pour les cartes Web.

Par exemple, les coordonnées :

```text
X = 709043
Y = 6235462
```

sont des coordonnées projetées.

Elles ne correspondent pas directement à une longitude et une latitude exprimées en degrés.

---

# 1.10 Les données vectorielles

OpenLayers permet également d'afficher des données vectorielles.

Une donnée vectorielle peut être :

```text
Point
Ligne
Polygone
```

Exemples :

```text
DAE         → points
Routes      → lignes
Parcelles   → polygones
Bâtiments   → polygones
Communes    → polygones
```

Pour gérer ces données, nous pouvons utiliser :

```javascript
ol.source.Vector
```

et :

```javascript
ol.layer.Vector
```

---

# 1.11 Source vectorielle

Exemple :

```javascript
var donnees_parcelles = new ol.source.Vector({
    url:'...',
    format:new ol.format.GeoJSON()
});
```

Deux informations importantes apparaissent.

### `url`

```javascript
url:'...'
```

indique où OpenLayers doit récupérer les données.

### `format`

```javascript
format:new ol.format.GeoJSON()
```

indique que les données reçues sont au format GeoJSON.

---

# 1.12 Le format GeoJSON

GeoJSON est un format permettant de représenter des données géographiques avec une structure JSON.

Il peut contenir :

- la géométrie ;
- les attributs ;
- plusieurs objets géographiques.

Exemple simplifié :

```json
{
    "type":"Feature",
    "properties":{
        "nom":"DAE mairie"
    },
    "geometry":{
        "type":"Point",
        "coordinates":[709043,6235462]
    }
}
```

Nous retrouvons deux parties importantes :

```text
properties
```

pour les informations attributaires ;

et :

```text
geometry
```

pour la géométrie.

---

# 1.13 Couche vectorielle

Après avoir créé la source, nous pouvons créer la couche.

```javascript
var couche_parcelles = new ol.layer.Vector({
    source:donnees_parcelles
});
```

Puis l'ajouter à la carte :

```javascript
map.addLayer(couche_parcelles);
```

La logique est donc :

```text
URL
 ↓
GeoJSON
 ↓
ol.source.Vector
 ↓
ol.layer.Vector
 ↓
map.addLayer()
 ↓
CARTE
```

---

# 1.14 Style d'une couche vectorielle

OpenLayers permet de modifier l'apparence des objets.

On utilise :

```javascript
ol.style.Style
```

Exemple :

```javascript
style:new ol.style.Style({
    stroke:new ol.style.Stroke({
        color:'black',
        width:1
    }),
    fill:new ol.style.Fill({
        color:'rgba(255,255,255,0.5)'
    })
})
```

---

## Stroke

`Stroke` correspond au contour.

```javascript
stroke:new ol.style.Stroke({
    color:'black',
    width:1
})
```

Nous définissons :

```text
color → couleur
width → épaisseur
```

---

## Fill

`Fill` correspond au remplissage.

```javascript
fill:new ol.style.Fill({
    color:'rgba(255,255,255,0.5)'
})
```

`rgba()` permet de définir :

```text
rouge
vert
bleu
transparence
```

La dernière valeur représente l'opacité.

---

# 1.15 Style d'un point

Pour un point, nous pouvons utiliser :

```javascript
ol.style.Circle
```

Exemple :

```javascript
image:new ol.style.Circle({
    radius:3,
    fill:new ol.style.Fill({
        color:'red'
    }),
    stroke:new ol.style.Stroke({
        color:'black'
    })
})
```

### `radius`

```javascript
radius:3
```

détermine la taille du cercle.

### `fill`

détermine la couleur intérieure.

### `stroke`

détermine le contour.

---

# 1.16 Afficher ou masquer une couche

Une couche peut être visible ou invisible.

```javascript
couche_parcelles.setVisible(false);
```

`false` signifie :

```text
couche cachée
```

Alors que :

```javascript
couche_parcelles.setVisible(true);
```

signifie :

```text
couche visible
```

On peut également récupérer son état :

```javascript
couche_parcelles.getVisible();
```

---

# 1.17 Les propriétés personnalisées d'une couche

Nous pouvons ajouter des propriétés à une couche.

Exemple :

```javascript
var couche_dae = new ol.layer.Vector({
    source:donnees_dae,
    title:'DAE',
    name:'dae'
});
```

Ici :

```text
title
```

peut servir pour l'affichage du nom de la couche.

Et :

```text
name
```

peut servir à identifier la couche dans notre programme.

Nous pouvons ensuite récupérer cette valeur avec :

```javascript
layer.get('name')
```

---

# 1.18 Les événements JavaScript

Une carte interactive doit pouvoir réagir aux actions de l'utilisateur.

Par exemple :

```text
clic
double clic
déplacement
changement
```

Pour écouter un événement dans OpenLayers, nous pouvons utiliser :

```javascript
map.on()
```

Exemple :

```javascript
map.on('singleclick',function(evt){

});
```

Cela signifie :

> Lorsque l'utilisateur effectue un clic simple sur la carte, exécuter cette fonction.

---

# 1.19 L'objet événement `evt`

Dans :

```javascript
map.on('singleclick',function(evt){
});
```

`evt` contient des informations sur l'événement.

Par exemple :

```javascript
evt.coordinate
```

permet de récupérer les coordonnées géographiques du clic.

```javascript
let position=evt.coordinate;
```

Puis :

```javascript
let posx=position[0];
let posy=position[1];
```

Nous obtenons :

```text
position[0] = X
position[1] = Y
```

---

# 1.20 Sélectionner un objet sur la carte

OpenLayers permet de rechercher l'objet qui se trouve sous un pixel.

Une fonction importante est :

```javascript
map.forEachFeatureAtPixel()
```

Principe :

```text
clic utilisateur
      ↓
pixel de l'écran
      ↓
forEachFeatureAtPixel()
      ↓
objet géographique
```

L'objet trouvé est une `Feature`.

---

# 1.21 Feature

Une `Feature` représente un objet géographique.

Par exemple :

```text
une parcelle
un bâtiment
un DAE
une commune
```

Une Feature possède généralement :

```text
une géométrie
+
des attributs
```

Pour récupérer un attribut :

```javascript
objet.get('c_nom')
```

ou :

```javascript
objet.get('numero')
```

Par exemple :

```javascript
let nom=objet.get('c_nom');
```

permet de récupérer le champ `c_nom`.

---

# 1.22 Filtrer les couches lors d'un clic

Lorsqu'il existe plusieurs couches, nous pouvons préciser celles dans lesquelles nous voulons rechercher une Feature.

Exemple :

```javascript
layerFilter:function(layer){
    return layer.get('name') === 'dae';
}
```

Cela signifie :

> Ne rechercher les objets que dans la couche dont la propriété `name` vaut `dae`.

---

# 1.23 Les interactions

OpenLayers possède également des interactions.

Une interaction permet à l'utilisateur d'agir sur la carte.

Par exemple :

```javascript
new ol.interaction.Select()
```

permet de sélectionner une Feature.

Exemple :

```javascript
var selectparcelles = new ol.interaction.Select({
    layers:[couche_parcelles]
});
```

Puis :

```javascript
map.addInteraction(selectparcelles);
```

---

# 1.24 Les Overlay

Un `Overlay` est un élément HTML positionné par-dessus la carte.

Il peut être utilisé pour créer une popup.

Exemple :

```javascript
let popup = new ol.Overlay({
    element:document.getElementById('info')
});
```

Puis :

```javascript
map.addOverlay(popup);
```

Nous avons donc :

```text
DIV HTML
   ↓
ol.Overlay
   ↓
map.addOverlay()
```

---

# 1.25 Positionner une popup

Pour afficher la popup à une position :

```javascript
popup.setPosition(evt.coordinate);
```

La popup apparaît donc à l'endroit du clic.

Pour la fermer :

```javascript
popup.setPosition(null);
```

---

# 1.26 Modifier le contenu HTML avec JavaScript

JavaScript peut récupérer un élément HTML grâce à :

```javascript
document.getElementById()
```

Exemple :

```javascript
document.getElementById('contenu')
```

Puis nous pouvons modifier son contenu :

```javascript
document.getElementById('contenu').innerHTML='Bonjour';
```

La propriété :

```text
innerHTML
```

permet donc de modifier le contenu HTML d'un élément.

---

# 1.27 jQuery

jQuery est une bibliothèque JavaScript.

Elle simplifie certaines opérations JavaScript.

Elle peut être chargée avec :

```html
<script src="https://code.jquery.com/jquery-4.0.0.min.js"></script>
```

Avec jQuery, nous pouvons sélectionner un élément :

```javascript
$('#info')
```

Cela correspond à l'élément :

```html
<div id="info"></div>
```

Puis :

```javascript
$('#info').html('Bonjour');
```

permet de modifier son contenu.

---

# 1.28 AJAX

AJAX permet au JavaScript de communiquer avec le serveur **sans recharger toute la page Web**.

Exemple :

```javascript
$.ajax({
    method:"POST",
    url:"create_point.php",
    data:{
        coordx:posx,
        coordy:posy
    }
});
```

### `method`

```javascript
method:"POST"
```

indique que nous envoyons des informations au serveur.

### `url`

```javascript
url:"create_point.php"
```

indique le script PHP qui recevra les données.

### `data`

```javascript
data:{
    coordx:posx,
    coordy:posy
}
```

correspond aux informations envoyées.

---

# 1.29 Recevoir les données AJAX en PHP

Si JavaScript envoie :

```javascript
data:{
    coordx:posx,
    coordy:posy
}
```

PHP peut récupérer ces informations avec :

```php
$coordonneX=$_POST['coordx'];
$coordonneY=$_POST['coordy'];
```

La correspondance est :

```text
JavaScript                 PHP

coordx       ──────────→   $_POST['coordx']

coordy       ──────────→   $_POST['coordy']
```

---

# 1.30 OpenLayers et PostgreSQL/PostGIS

OpenLayers fonctionne dans le navigateur.

PostgreSQL/PostGIS fonctionne côté serveur.

OpenLayers ne doit donc pas se connecter directement à PostgreSQL avec le mot de passe de la base.

Une architecture possible est :

```text
OpenLayers
    ↓
 AJAX / HTTP
    ↓
   PHP
    ↓
PostgreSQL/PostGIS
```

Pour la lecture des données :

```text
PostGIS
   ↓
 PHP
   ↓
GeoJSON
   ↓
OpenLayers
```

---

# 1.31 Création d'un point PostGIS

Les coordonnées récupérées depuis notre carte OpenLayers sont en EPSG:3857.

Nous pouvons créer un point avec :

```sql
ST_Point(x,y)
```

Puis lui attribuer son système de coordonnées :

```sql
ST_SetSRID(
    ST_Point(x,y),
    3857
)
```

`ST_SetSRID` ne transforme pas les coordonnées.

Il indique simplement :

> Ces coordonnées sont exprimées dans le système EPSG:3857.

---

# 1.32 Transformer une géométrie

Si notre table PostGIS utilise Lambert-93 (`EPSG:2154`), nous devons transformer le point.

```sql
ST_Transform(
    ST_SetSRID(
        ST_Point(x,y),
        3857
    ),
    2154
)
```

Il faut bien distinguer :

```text
ST_SetSRID
    ↓
déclare le système de coordonnées

ST_Transform
    ↓
transforme réellement les coordonnées
```

---

# 1.33 Insérer le point

Exemple :

```sql
INSERT INTO sante.dae_plai (geom)
VALUES (
    ST_Transform(
        ST_SetSRID(
            ST_Point(x,y),
            3857
        ),
        2154
    )
);
```

La logique complète est :

```text
coordonnées OpenLayers
EPSG:3857
      ↓
ST_Point()
      ↓
ST_SetSRID(...,3857)
      ↓
ST_Transform(...,2154)
      ↓
INSERT
      ↓
PostGIS
```

---

# 1.34 `RETURNING`

PostgreSQL permet de récupérer une information immédiatement après un `INSERT`.

Exemple :

```sql
INSERT INTO sante.dae_plai (geom)
VALUES (...)
RETURNING id;
```

Cela permet de connaître l'identifiant du nouvel objet.

En PHP :

```php
$result=pg_query($dbconnect,$sql);

$row=pg_fetch_row($result);
```

Puis :

```php
$row[0]
```

contient l'identifiant retourné.

---

# 1.35 Réponse du serveur AJAX

Après l'appel AJAX :

```javascript
$.ajax({...})
.done(function(msg){

});
```

`msg` contient la réponse envoyée par PHP.

Par exemple, si PHP fait :

```php
echo "Point créé";
```

alors :

```javascript
msg
```

contiendra :

```text
Point créé
```

Nous pouvons ensuite l'afficher :

```javascript
$('#info').html(msg);
```

---

# 1.36 Actualiser une source vectorielle

Après avoir ajouté un objet dans PostGIS, OpenLayers ne connaît pas automatiquement ce nouvel objet.

Nous pouvons demander à la source de recharger les données :

```javascript
donnees_dae.refresh();
```

Le nouveau fonctionnement devient :

```text
INSERT PostGIS
      ↓
réponse PHP
      ↓
AJAX .done()
      ↓
donnees_dae.refresh()
      ↓
nouvelle requête GeoJSON
      ↓
nouveau DAE affiché
```

---

# 1.37 Géolocalisation

OpenLayers permet également d'utiliser la géolocalisation du navigateur.

L'objet utilisé est :

```javascript
ol.Geolocation
```

Exemple :

```javascript
var geolocation = new ol.Geolocation({
    tracking:true,
    projection:map.getView().getProjection()
});
```

### `tracking`

```javascript
tracking:true
```

active le suivi de la position.

### `projection`

```javascript
projection:map.getView().getProjection()
```

demande d'utiliser la même projection que la carte.

Le navigateur doit autoriser l'accès à la position de l'utilisateur.

---

# 1.38 Contrôles OpenLayers

Les contrôles sont des outils placés sur la carte.

OpenLayers possède plusieurs contrôles.

Par exemple :

```text
zoom
échelle
gestion des couches
```

Une échelle peut être ajoutée avec :

```javascript
new ol.control.ScaleLine()
```

Un contrôle doit ensuite être associé à la carte.

---

# 1.39 LayerSwitcher

Un LayerSwitcher permet à l'utilisateur d'afficher ou masquer les différentes couches de la carte.

Les couches peuvent posséder un titre :

```javascript
title:'DAE'
```

ou :

```javascript
title:'Parcelles'
```

Le LayerSwitcher utilise ces informations pour présenter les couches à l'utilisateur.

Il permet donc de transformer une carte contenant plusieurs couches en application plus interactive.

---

# 1.40 Ce qu'il faut retenir

OpenLayers repose sur quelques concepts fondamentaux :

### Carte

```javascript
ol.Map
```

Contient la carte et ses couches.

### Vue

```javascript
ol.View
```

Détermine le centre, le zoom et la projection.

### Source

```javascript
ol.source
```

Indique d'où viennent les données.

### Couche

```javascript
ol.layer
```

Permet d'afficher les données.

### Feature

Représente un objet géographique.

### Style

```javascript
ol.style
```

Détermine l'apparence des objets.

### Interaction

```javascript
ol.interaction
```

Permet à l'utilisateur d'interagir avec les objets.

### Overlay

```javascript
ol.Overlay
```

Permet notamment d'afficher une popup.

### Événement

```javascript
map.on()
```

Permet de réagir aux actions de l'utilisateur.

---

# 1.41 Logique générale à mémoriser

Pour afficher une donnée :

```text
DONNÉES
   ↓
SOURCE
   ↓
LAYER
   ↓
MAP
   ↓
VIEW
   ↓
UTILISATEUR
```

Pour lire des données PostGIS :

```text
PostgreSQL/PostGIS
        ↓
       PHP
        ↓
     GeoJSON
        ↓
ol.source.Vector
        ↓
ol.layer.Vector
        ↓
    OpenLayers
```

Pour créer une donnée :

```text
Utilisateur
     ↓
clic OpenLayers
     ↓
evt.coordinate
     ↓
AJAX
     ↓
PHP
     ↓
requête SQL
     ↓
PostGIS
     ↓
réponse PHP
     ↓
actualisation OpenLayers
```