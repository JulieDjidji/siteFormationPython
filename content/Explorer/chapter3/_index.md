---
title: "Chapitre 3 : Manipuler et visualiser des données géographiques"
date: 2019-03-18T15:26:15Z
draft: false
weight: 40
---

Loin d'être exhaustif, ce tutoriel succint sur les données géographiques vise à présenter les bases pour manipuler et visualiser des données géographiques. Pour réaliser ce tutoriel, on s'est essentiellement appuyé sur la librarie *geopandas* dont [documentation officielle](http://geopandas.org/index.html) fournit d'ailleurs de nombreux explications et exemples.

Pour approfondir ce travail sur les données géographiques, vous pouvez notamment vous appuyer sur les tutoriels suivants : ...

Commençons par préalablement installer les packages utiles pour ce tutoriel :


```python
!pip install geopandas mapclassify descartes pysal
```

<ins>Exercice 1</ins> : Charger les données associées aux communes 2019 et celles associées à la population

<script>
function myFunctionGeoApp1() {
    var x = document.getElementById("GeoApp1");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionGeoApp1()">Voir résultat</button>

<div id="GeoApp1" hidden>
<div></div>

```python
import pandas as pd

communes=pd.read_csv("commune2019.csv")
pop=pd.read_excel("base-pop-historiques-1876-2015.xls", header=5, sheet_name="pop_1876_2015")
```
</div>

<ins>Exercice 2</ins> : Créer un *dataframe* propre issu de la fusion des deux bases à partir du code commune

<script>
function myFunctionGeoApp2() {
    var x = document.getElementById("GeoApp2");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionGeoApp2()">Voir résultat</button>

<div id="GeoApp2" hidden>
<div></div>

```python
data=pd.merge(communes, pop, left_on='com', right_on ="CODGEO")
data=data.groupby('dep', as_index=False)[['PMUN15', 'PMUN10']].sum()
```
</div>

Présentons les deux modes principaux de représentation numériques des données spatialisées :

* les images géoréférencées (photographies, images satellitaires …) aussi appelées **rasters**. Pour simplifier, un raster est une grille composée de cellules (ou pixels) organisées sous forme matricielle. Par exemple, une orthophotographie (photographie aérienne) est composée de 3 matrices empilées correspondant aux 3 couleurs primaires (rouges, vert, bleu).
* les **couches vectorielles** s’appuient sur le concept d’objets géométriques (points, lignes, polygones) pour représenter les entités géographiques. Un point est un doublet de coordonnées (longitude, latitude) auquel on rajoute parfois l’altitude. Une ligne est composée d’une suite de points. Un polygone est une ligne fermée. Afin de tenir compte des éventuelles enclaves et exclaves, les découpages territoriaux sont généralement décrits par des multipolygones qui sont des ensembles de polygones. On appelle données attributaires les variables non spatiales (par exemple le code géographique, le libellé, la région d’appartenance) qui décrivent les entités géographiques. En géopandas, [la géométrie](https://en.wikipedia.org/wiki/Simple_Features) est intégrée sous la forme d’une colonne qui se rajoute aux données attributaires.

Vous pouvez télécharger les fonds de cartes (*shapefile*) sur le site [creacartes](http://creacartes.insee.fr/accueil).

Un *shapefile* est un format de stockage des données vectorielles. Il contient généralement les fichiers suivants :

* un fichier d'extension *shp* qui stocke les entités géographiques. Il s'agit du shapefile proprement-dit.
* un fichier d'extension *dbf* qui fichier qui contient les données attributaires relatives aux objets contenus dans le shapefile.
* un fichier d'extension *shx* qui stocke l'index de la géométrie
* un fichier d'extension * prj* qui stocke l'information sur le système de coordonnées

Pour comprendre les différents systèmes de projection, vous pouvez lire cet [article](https://medium.com/@_FrancoisM/introduction-%C3%A0-la-manipulation-de-donn%C3%A9es-cartographiques-23b4e38d8f0f).

<ins>Exercice 3</ins> : Après avoir téléchargé le zip associé au *shapefile* dans l'environnement local, procéder au dézippage de ce dossier (à l'aide du package zipfile)

<script>
function myFunctionGeoApp3() {
    var x = document.getElementById("GeoApp3");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionGeoApp3()">Voir résultat</button>

<div id="GeoApp3" hidden>
<div></div>

```python
import zipfile
with zipfile.ZipFile('dep_francemetro_2018.zip', 'r') as zip_ref:
    zip_ref.extractall()
```
</div>

<ins>Exercice 4</ins> : Charger le fond de cartes (*shapefile*) des départements

<script>
function myFunctionGeoApp4() {
    var x = document.getElementById("GeoApp4");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionGeoApp4()">Voir résultat</button>

<div id="GeoApp4" hidden>
<div></div>

```python
import geopandas as gpd
dep = gpd.read_file('dep_francemetro_2018.shp')
dep.head()
```
</div>

<ins>Exercice 5</ins> : Tracer la carte des départements à partir du shapefile précédent

<script>
function myFunctionGeoApp5() {
    var x = document.getElementById("GeoApp5");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionGeoApp5()">Voir résultat</button>

<div id="GeoApp5" hidden>
<div></div>

```python
dep.plot(figsize=(8, 8))
```
</div>

<ins>Exercice 6</ins> : Tracer la carte des départements du la région Auvergne-Rhône-Alpes

<script>
function myFunctionGeoApp6() {
    var x = document.getElementById("GeoApp6");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionGeoApp6()">Voir résultat</button>

<div id="GeoApp6" hidden>
<div></div>

```python
dep[dep.reg=='84'].plot(figsize=(8, 8))
```
</div>

<ins>Exercice 7</ins> : Fusionner le *shapefile* avec la base de données

<script>
function myFunctionGeoApp7() {
    var x = document.getElementById("GeoApp7");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionGeoApp7()">Voir résultat</button>

<div id="GeoApp7" hidden>
<div></div>

```python
cartes = dep.merge(data, left_on = "code", right_on="dep")
print(cartes.shape)
cartes.head()
```
</div>

<ins>Exercice 8</ins> : Tracer la carte de France indiquant la population par département

<script>
function myFunctionGeoApp8() {
    var x = document.getElementById("GeoApp8");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionGeoApp8()">Voir résultat</button>

<div id="GeoApp8" hidden>
<div></div>

```python
cartes.plot('PMUN10', legend=True, figsize=(8, 8))
```
</div>

<ins>Exercice 9</ins> : Pourquoi cette carte n'est-elle pas pertinente ?

Cette carte n'est-elle pas pertinente pour deux raisons principales :

* Légende peu indicative : le changement de teinte en cartographie est généralement associée à un changement de signes (les couleurs chaudes sont associées aux valeurs positives)
* Cette carte ne réflète pas les différences de densité et est donc sémantiquement et sémiologiquement fausse. Une différence de population peut réfléter une différence d'aires.

<ins>Exercice 10</ins> : Créer des variables relatives à la densité de la population en 2010 et 2015

<script>
function myFunctionGeoApp10() {
    var x = document.getElementById("GeoApp10");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionGeoApp10()">Voir résultat</button>

<div id="GeoApp10" hidden>
<div></div>

```python
cartes['densite_10'] = cartes.PMUN10 / (cartes.geometry.area / 10**6)
cartes['densite_15'] = cartes.PMUN15 / (cartes.geometry.area / 10**6)
```
</div>

<ins>Exercice 11</ins> : Tracer la carte de densité de population par département. Il peut d'ailleurs être plus pertinent de tracer le *log* de la densité de population par département

<script>
function myFunctionGeoApp11() {
    var x = document.getElementById("GeoApp11");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionGeoApp11()">Voir résultat</button>

<div id="GeoApp11" hidden>
<div></div>

```python
cartes.plot('densite_10', legend=True,  cmap='OrRd', scheme='Quantiles', figsize=(8, 8))
```

Pour faciliter la visualisation, les variables quantitatives représentées sont discrétisées :

* soit par la méthode des quantiles (*scheme='Quantiles'*)
* soit par un découpage en intervalles de même taille (scheme='equal_interval')
* soit à l'aide de l'algorithme de Jenks, c'est-à-dire un découpage en classes homogènes (*scheme='Fisher_Jenks'*).

En cartographique, on privilégie généralement la discrétisation selon l'algorithme de Jenks. Néanmoins, cette méthode peut s'avérer particluièrement lente sur des bases de données volumineuses. Dans ce cas, il est possible d'accélérer les calculs en discrétisant sur un échantillon avec l'option *Fisher_Jenks_Sampled*.

</div>

<ins>Exercice 12</ins> : Calculer la différence de densité entre 2010 et 2015 puis calculer l'évolution de densités de population

<script>
function myFunctionGeoApp12() {
    var x = document.getElementById("GeoApp12");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionGeoApp12()">Voir résultat</button>

<div id="GeoApp12" hidden>
<div></div>

```python
cartes['diff_15_10'] = ((cartes['densite_15']- cartes['densite_10']) ) 
cartes['evol_15_10'] = 100* cartes['diff_15_10'] / cartes['densite_10']
```
</div>

<ins>Exercice 13</ins> : Tracer la carte de l'évolution de la densité de population par département entre 2010 et 2015.

<script>
function myFunctionGeoApp13() {
    var x = document.getElementById("GeoApp13");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionGeoApp13()">Voir résultat</button>

<div id="GeoApp13" hidden>
<div></div>

```python
cartes.plot('evol_15_10', legend=True,  cmap='RdYlBu_r', scheme='Quantiles', figsize=(8, 8))
```
</div>

<ins>Exercice 14</ins> : Ajouter le numéro de département à la carte précédente

<script>
function myFunctionGeoApp14() {
    var x = document.getElementById("GeoApp14");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionGeoApp14()">Voir résultat</button>

<div id="GeoApp14" hidden>
<div></div>

```python
ax = cartes.plot('evol_15_10', legend=True,  cmap='RdYlBu_r', scheme='Quantiles', figsize=(8, 8))
label=cartes.apply(lambda x: ax.annotate(s=x.code, xy=x.geometry.centroid.coords[0], ha='center'),axis=1)
```
</div>

<ins>Exercice 15</ins> : Agréger les données des départements pour obtenir celui des régions (incluant les données et la géométrie)

<script>
function myFunctionGeoApp15() {
    var x = document.getElementById("GeoApp15");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionGeoApp15()">Voir résultat</button>

<div id="GeoApp15" hidden>
<div></div>

```python
reg = cartes.dissolve(by='reg', aggfunc=sum).reset_index()
reg.plot(figsize=(8, 8))
```
</div>

<ins>Exercice 16</ins> : Représenter alors la densité de population par région en 2010

<script>
function myFunctionGeoApp16() {
    var x = document.getElementById("GeoApp16");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionGeoApp16()">Voir résultat</button>

<div id="GeoApp16" hidden>
<div></div>

```python
reg['densite_10'] = reg.PMUN10 / (reg.geometry.area / 10**6)
ax = reg.plot('densite_10', legend=True,  cmap='OrRd', scheme='Quantiles', figsize=(8, 8), edgecolor='k')
label=reg.apply(lambda x: ax.annotate(s=x.reg, xy=x.geometry.centroid.coords[0], ha='center'),axis=1)
```
</div>

<ins>Exercice 17</ins> : Télécharger le zip associé au *shapefile* des fleuves français dans l'environnement local puis procéder au dézippage de ce dossier (à l'aide du package zipfile)

<script>
function myFunctionGeoApp17() {
    var x = document.getElementById("GeoApp17");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionGeoApp17()">Voir résultat</button>

<div id="GeoApp17" hidden>
<div></div>

```python
import zipfile
with zipfile.ZipFile('fleuve_francemetro_2018.zip', 'r') as zip_ref:
    zip_ref.extractall()
```
</div>

<ins>Exercice 18</ins> : Charger ce *shapefile*

<script>
function myFunctionGeoApp18() {
    var x = document.getElementById("GeoApp18");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionGeoApp18()">Voir résultat</button>

<div id="GeoApp18" hidden>
<div></div>

```python
fleuve = gpd.read_file('fleuve_francemetro_2018.shp')
fleuve.head(2)
```
</div>

<ins>Exercice 19</ins> : Ne garder que les observations relatives à la Loire et tracer ce fleuve

<script>
function myFunctionGeoApp19() {
    var x = document.getElementById("GeoApp19");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionGeoApp19()">Voir résultat</button>

<div id="GeoApp19" hidden>
<div></div>

```python
loire = fleuve[fleuve.libgeo.str.lower().str.contains("loire")]
loire.plot(figsize=(8, 8))
```
</div>

<ins>Exercice 20</ins> : Tracer la carte des départements que la Loire traverse. Colorer les départements selon leur région d'appartenance.

<script>
function myFunctionGeoApp20() {
    var x = document.getElementById("GeoApp20");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionGeoApp20()">Voir résultat</button>

<div id="GeoApp20" hidden>
<div></div>

Il faut commencer par installer le package *rtree* comme suit :

```python
import os 
os.environ['http_proxy'] = "http://proxy-rie.http.insee.fr:8080" 
os.environ['https_proxy'] = "https://proxy-rie.http.insee.fr:8080"
!conda install -y -c conda-forge rtree
```

On peut alors évaluer l'intersection entre nos données et la Loire.

```python
import rtree
dep_loire = gpd.sjoin(cartes, loire, op='intersects')
```

```python
ax = dep_loire.plot(cmap='tab10', column='reg')
labels=dep_loire.apply(lambda x: ax.annotate(s=x.code, xy=x.geometry.centroid.coords[0], ha='center'),axis=1)
loire.plot(ax=ax, facecolor='none', edgecolor='k', figsize=(8, 8))
```
</div>

<ins>Exercice 21</ins> : Tracer la carte des départements  qui se situent à moins de 10km autour de la Loire.

<script>
function myFunctionGeoApp21() {
    var x = document.getElementById("GeoApp21");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionGeoApp21()">Voir résultat</button>

<div id="GeoApp21" hidden>
<div></div>

On sélectionne les données présentes dans le périmètre de 10 km autour de la Loire.

```python
loire_buffer = gpd.geodataframe.GeoDataFrame(geometry=loire.geometry.buffer(10000))
dep_loire_buffer = gpd.sjoin(cartes, loire_buffer, op='intersects')
```

Puis, on représente la carte des départements concernés.

```python
ax = dep_loire_buffer.plot(cmap='tab10', column='reg')
labels=dep_loire_buffer.apply(lambda x: ax.annotate(s=x.code, xy=x.geometry.centroid.coords[0], ha='center'),axis=1)
loire.plot(ax=ax, facecolor='none', edgecolor='k', figsize=(8, 8))
```
</div>

### Un petit aperçu de *folium* pour des cartes encore plus visuelles

L'objectif de [*folium*](https://python-visualization.github.io/folium/quickstart.html#Choropleth-maps) est de réaliser des cartes dynamiques. Attention, contrairement aux manipulations précédentes, folium impose l'usage du système de projection WGS 84 (https://fr.wikipedia.org/wiki/WGS_84). Par défaut, les fonds de cartes de situation proposés sont issus d'OpenStreetMap.

Il faut commencer par installer et charger le *package folium* :

```python
!pip install folium
```

```python
import folium
```

<ins>Exercice 22</ins> : Produire une carte dynamique centrée sur le bâtiment White (dont les coordonnées en WGS 84 sont [48.816207, 2.308189]).

<script>
function myFunctionGeoApp22() {
    var x = document.getElementById("GeoApp22");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionGeoApp22()">Voir résultat</button>

<div id="GeoApp22" hidden>
<div></div>

```python
m = folium.Map(location=[48.816207, 2.308189], zoom_start=19)
m
```
</div>

<ins>Exercice 23</ins> : Creer une carte avec un marker sur votre lieu préféré.

<script>
function myFunctionGeoApp23() {
    var x = document.getElementById("GeoApp23");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionGeoApp23()">Voir résultat</button>

<div id="GeoApp23" hidden>
<div></div>

```python
m = folium.Map(
    location=[48.816207, 2.308189],
    zoom_start=18
)
folium.Marker([48.816285, 2.307647], popup='<i>SSP_Lab</i>', tooltip='Saurez-vous deviner mon lieu de travail?').add_to(m)
m 
```
</div>

<ins>Exercice 24</ins> : Représenter sur une carte les départements. (Attention : pour l'instant, on est encore obligé de transformer en geojson un fond de carte pour l'intégrer sous folium. Pour mémoire, il faut convertir en WGS 84 avant l'export en geoJson.)

<script>
function myFunctionGeoApp24() {
    var x = document.getElementById("GeoApp24");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionGeoApp24()">Voir résultat</button>

<div id="GeoApp24" hidden>
<div></div>

```python
cartes_json = cartes.to_crs({'init': 'epsg:4326'}).to_json()
```

```python
m = folium.Map(
    location=[48.816207, 2.308189],
    zoom_start=6
)

folium.GeoJson(
    cartes_json,
    name='départements').add_to(m)

m
```

Voici une solution avec des otpions pour permettre l'affichage des noms des départements :

```python
m = folium.Map(
    location=[48.816207, 2.308189],
    zoom_start=6
)

folium.GeoJson(
    cartes_json,
    name='départements',
    show=True,
    style_function=lambda feature: {
            'fillColor': 'red',
            'color': 'black',
            'weight': 1,
            'fillOpacity':0.1
            },   
    highlight_function=lambda x: {'weight':3, 
                                  'color':'black',
                                  'fillOpacity':1},    
    tooltip=folium.features.GeoJsonTooltip(
            fields=['libelle'],
            aliases=['Nom du département:'])
).add_to(m)

folium.LayerControl().add_to(m)
m
```

</div>

<ins>Exercice 25</ins> : Représenter sur une carte l'évolution de la densité entre 2010 et 2015 par département.

<script>
function myFunctionGeoApp25() {
    var x = document.getElementById("GeoApp25");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionGeoApp25()">Voir résultat</button>

<div id="GeoApp25" hidden>
<div></div>

```python
bins = list(cartes['evol_15_10'].quantile([0, 0.25, 0.5, 0.75, 1]))

m = folium.Map(location=[48.816207, 2.308189], zoom_start=5)

folium.Choropleth(
    geo_data=cartes_json,
    data=cartes,
    columns=['code', 'evol_15_10'],
    key_on='feature.properties.code',
    fill_color='RdYlBu_r',
    fill_opacity=0.7,
    line_opacity=0.5,
    bins=bins,
    reset=True
).add_to(m)

m
```
</div>


