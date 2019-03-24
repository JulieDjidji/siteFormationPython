---
title: "Chapitre 2 : Visualiser les données"
date: 2019-03-18T15:26:15Z
draft: false
weight: 30
---

Ce tutoriel vise à explorer différents packages de visualisation sous python se différenciant notamment sur la niveau de facilité pour réaliser, personnaliser et formater les graphiques, sur la diversité des graphiques réalisables et sur le choix entre visualisation statique et visualisation interactive. Sans prétention d'exhaustivité, notre exploration se retreint essentiellement à cinq librairies incontournables :

* la librairie historique de visualisation : <a href="#matplotlib">**matplotlib**</a>
* une surcouche de *matplotlib* : <a href="#seaborn">**seaborn**</a>
* une librairie avec une syntaxe proche de R : <a href="#plotnine">**plotnine**</a>
* un outil de visualisations interactives : <a href="#plotly">**plotly**</a> (ou de façon alternative <a href="#cufflinks">*cufflinks*</a>)
* une librairie de visualisations Web interactives : <a href="#bokeh">**bokeh**</a>

Il pourrait aussi être intéressant de jeter un oeil à la libraire [*altair*](https://altair-viz.github.io/) qui semble proposer une très large palette de belles visualisations. Dans ce tutoriel, on n'abordera ni les librairies *pydot* qui permet essentiellement la génération de graphes, ni la libraire *networkX* qui est très largement axée sur l'analyse des graphes et des réseaux.

**Quoi représenter ? Comment choisir le type de graphique adéquat ?**

<p align="center">
<a href="https://raw.githubusercontent.com/ft-interactive/chart-doctor/master/visual-vocabulary/poster.png">
<img src="/images/visualVocabulary.jpg" alt="VisualVocabulary" width="1400" height="1200"/>
</a>
</p>

Afin d'explorer ces différentes librairies, nous utiliserons un jeu de données restreints que vous allez contruire ! De plus, *a minima*, un graphique (dont un graphique commun représentant les 10 villes avec le patrimoine moyen le plus élevé parmi les villes de plus de 20 000 habitants ayant plus de 50 redevables à l'ISF) sera réalisé avec chacune des librairies afin de faciliter leur comparaison.

<ins>Exercice 1</ins> : A partir des données Excel sur l'impôt sur la fortune (*isfcom2017.xlsx*), construire deux *dataframes* : le premier *patrimoine_top* qui contient les 10 villes avec le patrimoine moyen le plus élevé et le second *impot_top* qui regroupe les 10 villes avec les redevables de l'isf payant en moyenne le plus d'impôt (parmi les villes de plus de 20 000 habitants ayant plus de 50 redevables à l'ISF).

<script>
function myFunction1() {
    var x = document.getElementById("App1");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction1()">Voir résultat</button>

<div id="App1" hidden>
<div></div>

```python
isf=pd.read_excel("isfcom2017.xlsx", sheet_name="définitif_patrimoine", header=1)
print(isf.shape)
isf.head(2)
```

```python
# On fusionne avec la table commune pour récupérer le libellé des communes
import re
communes=pd.read_csv("commune2019.csv")
isf["codeCommune"]=[re.sub(' ','', str(x)) for x in isf["Code commune (INSEE)"]]
isf=pd.merge(communes, isf, left_on="com", right_on="codeCommune", how='inner')
isf=isf[isf.typecom!='COMD']
```

```python
patrimoine_top=isf.sort_values('patrimoine moyen en €', ascending=False).head(10)
impot_top=isf.sort_values('impôt moyen en €', ascending=False).head(10)
```
</div>

<h2 id="matplotlib">La librairie historique de visualisation : <a href="https://matplotlib.org/index.html"><b>matplotlib</b></a></h2>

Quelques mots sur la syntaxe :

* Chargement de la librarie : *import matplotlib.pyplot as plt*
* Création d'une figure vide en fixant des paramètres comme la taille de l'image *fig = plt.figure(figsize=(10,4))* *\[Etape optionnelle\]*
* Alternative pour diviser la fenêtre graphique en sous-fenêtres avec deux graphiques l'un en dessous de l'autre : *f, (ax1, ax2) = plt.subplots(nrows=2,ncols=1, figsize=(15, 10))* *\[Etape optionnelle\]*
* Tracé du graphique avec la commande *plt.nomGraphique* (par exemple, *plt.plot* pour un tracé linéaire, *plt.scatter* pour nuage de points, *plt.bar* pour un graphique à barres ...)
* Ajout de paramètres (titres aevc *plt.*title* ou *ax.set_title*, label de l'axe des abscisses *plt.xlabel* ou *ax.set_xlabel*, ...) *\[Etape optionnelle\]*

Pour réaliser un graphique, référez-vous à la [documentation officielle](https://matplotlib.org/index.html). Le [site](http://www.python-simple.com/python-matplotlib/matplotlib-intro.php) détaille aussi la syntaxe et les options pour réaliser de nombreux types de graphiques avec *matplotlib*. Si vous avez besoin d'un aide mémoire, consultez le [cheat_sheet](https://s3.amazonaws.com/assets.datacamp.com/blog_assets/Python_Matplotlib_Cheat_Sheet.pdf) !

<ins>Exercice 1</ins> : Tracer le diagramme à barres horizontales représentant les 10 villes avec le patrimoine moyen le plus élevé parmi les villes de plus de 20 000 habitants ayant plus de 50 redevables à l'ISF.

<script>
function myFunctionMatplotlib1() {
    var x = document.getElementById("AppMatplotlib1");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionMatplotlib1()">Voir résultat</button>

<div id="AppMatplotlib1" hidden>
<div></div>

```python
fig = plt.figure(figsize=(10,4))
plt.barh(patrimoine_top['libelle'], patrimoine_top['patrimoine moyen en €'], align='center', color='blue', height=0.7)
plt.xlabel('patrimoine moyen en €')
plt.title('Quelles communes habritent les plus hauts patrimoines ?')
```
</div>

<ins>Exercice 2</ins> : Tracer les deux diagrammes à barres horizontales représentant respectivement les 10 villes avec le patrimoine moyen le plus élevé et les 10 villes avec les redevables de l'isf payant en moyenne le plus d'impôt parmi les villes de plus de 20 000 habitants ayant plus de 50 redevables à l'ISF.

<script>
function myFunctionMatplotlib2() {
    var x = document.getElementById("AppMatplotlib2");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionMatplotlib2()">Voir résultat</button>

<div id="AppMatplotlib2" hidden>
<div></div>

```python
f, (ax1, ax2) = plt.subplots(nrows=2,ncols=1, figsize=(15, 10))
ax1.barh(patrimoine_top['libelle'], patrimoine_top['patrimoine moyen en €'], align='center', color='blue',height=0.7)
ax1.set_xlabel('patrimoine moyen en €')
ax1.set_title('Quelles communes habritent les plus hauts patrimoines ?')

ax2.barh(impot_top['libelle'], impot_top['impôt moyen en €'], align='center', color='magenta',height=0.7)
ax2.set_xlabel('impôt moyen en €')
ax2.set_title("Quelles communes habitrent les redevables de l'isf payant le plus d'impôt en moyenne ?")
```
</div>

Votre graphe ne s'affiche pas dans votre *notebook* mais aucune erreur ne se produit ? Assurez-vous que la ligne de code suivante est bien ajoutée dans votre *notebook* :

```python
%matplotlib inline
```

Toutefois, pour avoir un environnement interactif, il peut être préférable d'utiliser la commande suivante :

```python
%matplotlib notebook
```

Il est possible de directement réaliser des graphes à partir d'un *dataframe pandas*. Pour cela, on peut s'appuyer sur la [documentation de pandas](http://pandas.pydata.org/pandas-docs/stable/user_guide/visualization.html).

<ins>Exercice </ins> : Directement à partir du *dataframe* * patrimoine_top*, tracer le diagramme à barres horizontales représentant les 10 villes avec le patrimoine moyen le plus élevé parmi les villes de plus de 20 000 habitants ayant plus de 50 redevables à l'ISF.

<script>
function myFunctionGraphePandas1() {
    var x = document.getElementById("AppGraphePandas1");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionGraphePandas1()">Voir résultat</button>

<div id="AppGraphePandas1" hidden>
<div></div>

```python
patrimoine_top.plot(kind='barh', y='patrimoine moyen en €', x='Commune', figsize=(10,5), facecolor="magenta", 
                    legend=False, title='Quelles communes habritent les plus hauts patrimoines ?', subplots=1)
```
</div>


<h2 id="seaborn">Une surcouche de *matplotlib* : <a href="http://seaborn.pydata.org/"><b>seaborn</b></a></h2>

Une [documentation officielle](http://seaborn.pydata.org/) peut, comme pour *matplotlib* est complétée par le [site](http://www.python-simple.com/python-seaborn/seaborn-general.php). Comme pour *matplotlib*, n'hésitez pas à consulter le [cheat_sheet](https://s3.amazonaws.com/assets.datacamp.com/blog_assets/Python_Seaborn_Cheat_Sheet.pdf) de Seaborn.

* Les plus de Seaborn 
    * Faciliter la visualisation
    * Rendre la visualisation plus attrayante avec notamment une [palette de couleur spécifique](https://seaborn.pydata.org/tutorial/color_palettes.html)

* Un inconvénient principal : Un nombre plus restreint de visualisations possibles dont les principales sont :

<table border="1px">
	<tr>
        <TH>
        <TH>Fonction
        <TH>Résultat
    <tr>
        <TD rowspan="2">Analyse des variables quantitatives
        <TD> sns.scatterplot() ou sns.replot(kind="scatter")
        <TD> Tracé du nuage de points
    <tr>
        <TD> sns.lineplot() ou sns.replot(kind="line")
        <TD> Tracé linéaire entre les points
    <tr>
        <TD rowspan="4">Analyse des variables catégorielles
        <TD> sns.boxplot()
        <TD> Représentation d'un diagramme en boîte mettant en exergue les quantiles de la distribution et les points extrêmes
    <tr>
        <TD> sns.violinplot()
        <TD> Représentation de la courbe de densité de probabilité des différentes valeurs et de la distribution des données
    <tr>
        <TD> sns.barplot()
        <TD> Graphique à barres de longueur proportionnelle à la valeur représentée
    <tr>
        <TD> sns.countplot()
        <TD> Graphique représentant le nombre d'observations associées à une variable donnée
    <tr>
        <TD> Analyse de la distribution des données
        <TD> sns.distplot()
        <TD> Distribution / histogramme avec ou sans représentation de la densité estimée (Kernel Density Estmation - KDE)
</table>


<ins>Exercice 1</ins> : A partir de *seaborn*, tracer le diagramme à barres horizontales représentant les 10 villes avec le patrimoine moyen le plus élevé parmi les villes de plus de 20 000 habitants ayant plus de 50 redevables à l'ISF.

<script>
function myFunctionSeaborn1() {
    var x = document.getElementById("AppSeaborn1");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionSeaborn1()">Voir résultat</button>

<div id="AppSeaborn1" hidden>
<div></div>

```python
import seaborn as sns
fig = plt.figure(figsize=(10,4))
sns.set(style="whitegrid")
bar_plot = sns.barplot(y=patrimoine_top["Commune"],x=patrimoine_top["patrimoine moyen en €"], 
                       palette=sns.color_palette("Blues_d"), errwidth =False)
plt.xticks(rotation=90)
plt.show()
```
</div>

<ins>Exercice 2</ins> : A partir de la table *isf*, tracé le diagramme à barres verticales représentant les nombre de communes parmi les villes de plus de 20 000 habitants ayant plus de 50 redevables à l'ISF.

<script>
function myFunctionSeaborn2() {
    var x = document.getElementById("AppSeaborn2");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionSeaborn2()">Voir résultat</button>

<div id="AppSeaborn2" hidden>
<div></div>

```python
fig = plt.figure(figsize=(20,4))
sns.set(style="whitegrid")
sns.countplot(x="Région", data=isf)
plt.xticks(rotation=90)
```
</div>

<ins>Exercice 3</ins> : A partir de la table *isf*,  représenter l'impôt moyen selon le patrimoine moyen (pour les villes de plus de 20 000 habitants ayant plus de 50 redevables à l'ISF).

<script>
function myFunctionSeaborn3() {
    var x = document.getElementById("AppSeaborn3");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionSeaborn3()">Voir résultat</button>

<div id="AppSeaborn3" hidden>
<div></div>

```python
fig = plt.figure(figsize=(8,5))
sns.set(style="white")
sns.scatterplot(x="patrimoine moyen en €", y='impôt moyen en €', data=isf)
```
</div>

<h2 id="plotnine">Une librairie avec une syntaxe proche de R : <a href="https://plotnine.readthedocs.io/en/stable/"><b>plotnine</b></a></h2>

Si la librairie *ggplot*(http://ggplot.yhathq.com/) propose dès 2014 une version partielle de *ggplot* sous python avec l'ambition de respecter le concept de *Grammar of Graphics*, cette librairie n'est toutefois plus maintenue depusi 2016. Son installation pose d'ailleurs des problèmes de compatibilité avec la version actuelle de *pandas*. La librairie *plotnine*, toujours en cours de développement, constitue une alternative intéressante pour les aficionados de R souhaitant utiliser python !

IL n'est pas forcément utile de réaliser un grand nombre d'exemples notamment en raison de sa grande similarité avec la syntaxe de R, testons la simplement en réalisant le même diagramme que pour les autre librairies. 

<ins>Exercice </ins> : A partir de *plotnine*, tracer le diagramme à barres horizontales représentant les 10 villes avec le patrimoine moyen le plus élevé parmi les villes de plus de 20 000 habitants ayant plus de 50 redevables à l'ISF.

<script>
function myFunctionPlotnine1() {
    var x = document.getElementById("AppPlotnine1");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPlotnine1()">Voir résultat</button>

<div id="AppPlotnine1" hidden>
<div></div>

```python
!pip install plotnine
import plotnine
```

```python
# Pour ordonner les labels par ordre croissant de patrimoine moyen
commune_cat=pd.api.types.CategoricalDtype(patrimoine_top.libelle.tolist(), ordered=True)
patrimoine_top['commune_cat'] = patrimoine_top['libelle'].astype(str).astype(commune_cat)
```

```python
p  =  plotnine.ggplot(patrimoine_top ,  aes( x = patrimoine_top["commune_cat"], y = "patrimoine moyen en €"))  + \
     geom_bar(stat='identity', fill='magenta') + \
     ggtitle("Quelles communes habritent les plus hauts patrimoines ?" ) + \
     ylab("patrimoine moyen en €" )  +   \
     xlab("Commune") + \
    coord_flip() + \
     theme(axis_text_x = element_text( angle = 0 ))   + \
     theme(panel_background=element_rect(fill='white'),
         axis_line_x=element_line(color='black'),
          axis_line_y=element_line(color='black'))
print(p)
```
</div>


<h2 id="plotly">Un outil de visualisations interactives : <a href="https://plot.ly/python/user-guide/"><b>plotly</b></a></h2>

Comme pour les autres librairies, la [documentation officielle](https://plot.ly/python/reference/) de *plotly* est riche : elle présente la syntaxe relative à chaque fonction, notamment à travers une large palette d'exemples. Pour la syntaxe globale, n'hésitez pas aussi à consulter le [cheat_sheet](https://images.plot.ly/plotly-documentation/images/python_cheat_sheet.pdf) !

* Les plus de *plotly* :
    * Création de visualisations interactives construites à l'aide de D3.js (sans même connaître D3.js !)
    * En dehors de python, *plotly* peut être utilisé sans connaissances techniques pour créer des tracés interactifs, via l'interface graphique de plotly
    * Visualisations partageables en ligne avec plusieurs personnes
    * Intégration possible des graphiques interactifs dans des projets ou des sites Web

* L'inconvénient principal :
    * L'utilisation de l'interface graphique de plotly oblige l'utilisateur à rendre ses données publiques qui sont alors consultables par tous.

Comme l'indique la [documentation](https://plot.ly/python/getting-started/#start-plotting-online), *plotly* permet aussi de créer hors ligne :

* avec *plotly.offline.plot()* pour créer et sauvegarder le graphique en html et l'afficher dans le navigateur 
* avec *plotly.offline.iplot()* pour créer et afficher le graphique au sein d'un *jupyter notebook*

<ins>Exercice 1</ins> : A partir de *plotly*, tracer le diagramme à barres horizontales représentant les 10 villes avec le patrimoine moyen le plus élevé parmi les villes de plus de 20 000 habitants ayant plus de 50 redevables à l'ISF.

<script>
function myFunctionPlotly1() {
    var x = document.getElementById("AppPlotly1");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPlotly1()">Voir résultat</button>

<div id="AppPlotly1" hidden>
<div></div>

```python
import plotly.graph_objs as go
```

```python
# Ensemble des données pour la visualisation
data = [
    go.Bar(x=patrimoine_top['patrimoine moyen en €'],
                    y=patrimoine_top['Commune'], orientation = 'h', 
                   marker=dict(color='magenta'))
]
```

```python
# Apparence du graphique 
layout = go.Layout(
    title='Quelles communes habritent les plus hauts patrimoines ?',
    font=go.layout.Font(
        family='Arial', size=10
    ),
    showlegend=False,
    xaxis=dict(
        showgrid=True,
        showline=True,
        showticklabels=True,
        zeroline=True,
        exponentformat='none'
    ),
    yaxis=dict(
        automargin= True
    ),
    bargap=0.1
)

fig = go.Figure(data=data, layout=layout)
plotly.offline.iplot(fig) # Option filename si on souhaite sauvegarder la figure
```
</div>

<p id="cufflinks">
Pour combiner de façon efficiente, il est possible d'utiliser la librairie **cufflinks** qui facilite la réalisation de graphiques avec *plotly* à partir de *dataframes pandas*. Quelques tutoriels sont disponibles sur leur [github](https://github.com/santosjorge/cufflinks) ou sur le [site](https://plot.ly/ipython-notebooks/cufflinks/) de plotly.
</p>

<ins>Exercice 2</ins> : A partir de *cufflinks*, tracer le diagramme à barres horizontales représentant les 10 villes avec le patrimoine moyen le plus élevé parmi les villes de plus de 20 000 habitants ayant plus de 50 redevables à l'ISF.

<script>
function myFunctionPlotly2() {
    var x = document.getElementById("AppPlotly2");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPlotly2()">Voir résultat</button>

<div id="AppPlotly2" hidden>
<div></div>

```python
import cufflinks as cf
```

```python
# Pour permettre un affichage au sein du notebook
cf.go_offline()
```

```python
patrimoine_top[['libelle','patrimoine moyen en €']].iplot(kind='bar', y='patrimoine moyen en €', x='libelle',
                                                          xTitle='patrimoine moyen en €', yTitle='Commune', 
                                                          barmode='group', orientation='h',
                                                          title='Quelles communes habritent les plus hauts patrimoines ?',
                                                         colors='magenta', bargap=0.2, margin=(200,50,50,50))
```

</div>

<ins>Exercice 3</ins> : Comment contrôler l'apparence du graphique (par exemple la taille de la figure) si les paramètres n'existent pas dans la fonction *iplot* de *cufflinks* ? Tracer le diagramme précédent en fixant la taille de la figure.

<script>
function myFunctionPlotly3() {
    var x = document.getElementById("AppPlotly3");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPlotly3()">Voir résultat</button>

<div id="AppPlotly3" hidden>
<div></div>

```python
import cufflinks as cf
```

```python
# Pour permettre un affichage au sein du notebook
cf.go_offline()
```

Afin de modifier plus finement l'apparence du graphique, il est possible d'ajouter ces caractéristiques de mise en forme en paramètre de *layout*. 

```python
layout_cufflinks = cf.Layout(
    height=500,
    width=1000,
    title='Quelles communes habritent les plus hauts patrimoines ?',
    font=cf.layout.Font(
        family='Arial', size=10
    ),
    showlegend=False,
    xaxis=dict(
        showgrid=True,
        showline=True,
        showticklabels=True,
        zeroline=True,
        exponentformat='none'
    ),
    yaxis=dict(
        automargin= True
    ),
    bargap=0.1
)
patrimoine_top[['libelle','patrimoine moyen en €']].iplot(kind='bar', y='patrimoine moyen en €', x='libelle',
                                                          xTitle='patrimoine moyen en €', yTitle='Commune', 
                                                          barmode='group', orientation='h',
                                                          title='Quelles communes habritent les plus hauts patrimoines ?',
                                                         colors='magenta', bargap=0.2, margin=(800,50,50,50), 
                                                         layout=layout_cufflinks.to_plotly_json())
```

</div>

<h2 id="bokeh">Une librairie de visualisations Web interactives : <a href="https://bokeh.pydata.org/en/latest/"><b>bokeh</b></a></h2>

Difficile de présenter *plotly* et d'ignorer complètement *bokeh* ! Pour faciliter la prise en main de *bokeh*, vous pouvez consulter la [documentation officielle](https://bokeh.pydata.org/en/latest/) ou le [cheat_sheet](https://s3.amazonaws.com/assets.datacamp.com/blog_assets/Python_Bokeh_Cheat_Sheet.pdf). *Bokeh* présente toutefois quelques défauts indéniables :

* Moins d'exemples en ligne et documentation parfois insuffisante (essentiellement basée sur des exemples)
* Moins intégré avec *pandas* que *plotly* (*bokeh* s’intègre aux Pandas à l’aide de la *ColumnDataSourceclasse*, cette fonction est présente dans le module *bokeh.models*)

<ins>Exercice </ins> : A partir de *plotly*, tracer le diagramme à barres horizontales représentant les 10 villes avec le patrimoine moyen le plus élevé parmi les villes de plus de 20 000 habitants ayant plus de 50 redevables à l'ISF.

<script>
function myFunctionBokeh1() {
    var x = document.getElementById("AppBokeh1");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionBokeh1()">Voir résultat</button>

<div id="AppBokeh1" hidden>
<div></div>

```python
from bokeh.plotting import figure, show
from bokeh.io import output_notebook
```

```python
output_notebook()
p = figure(plot_width=800, plot_height=400, y_range=patrimoine_top['libelle'].tolist(),
          title="Quelles communes habritent les plus hauts patrimoines ?",)
p.hbar(y='libelle', right='patrimoine moyen en €', height=0.8, alpha=0.7, source=source, color="magenta")
show(p)
```
</div>




