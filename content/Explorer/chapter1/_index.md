---
title: "Chapitre 1 : Manipuler les données"
date: 2019-03-18T15:26:15Z
draft: false
weight: 20
---

<a href="#numpy">**Numpy**</a> : bibliothèque python de bas niveau utilisée pour le calcul scientifique :

* Permet notamment de travailler avec des tableaux et matrices multidimensionnels et volumineux homogènes (c'est-à-dire de même type).
* Dont l'objet principal est le ndarray (un type de tableau à N dimensions)

<a href="#pandas">**Pandas**</a> : package de manipulation de données pour manipuler des données de haut niveau construits sur *numpy*

* La série est le principal élément constitutif des pandas. Une série est un tableau unidimensionnel basé sur *numpy ndarray*. Dans un *dataframe*, une série correspond à une colonne.
* Un *dataframe* est un tableau de données étiquetée en 2 dimensions dont les colonnes sont constituées par un *ndarray*, une série ou un autre *dataframe*.

<h2 id="numpy"><b>Numpy</b></h2>

*Numpy* est le package incontournable pour effectuer du calcul scientifique en python, en facilitant notamment la gestion des tableaux et des matrices de grande dimension. La documentation officielle est disponible via ce [lien](https://docs.scipy.org/doc/numpy/user/quickstart.html).

*Numpy* permet de **manipuler des arrays** ou des matrices, pouvant être par exemple construites à partir d'arrays. Un *array* correspond à un tableau de **valeurs du même type**. Les opérations mathématiques sont facilitées par un ensemble de fonctions accessibles dans le package *numpy*. Le [site](http://www.python-simple.com/python-numpy-scipy/creation-numpy.php) offre un large panorama des fonctionnalités de *numpy*. 

<ins>NB</ins> : L'*alias* np est très souvent utilisé pour désigner *numpy*

<ins> Petit rappel</ins> : en python, les indices commencent à zéro. Le premier élément de l'*array* s'obtient donc avec la commande *a\[0\]*

<ins>**App 1**</ins> : Charger *numpy*

```python
import numpy as np
```

<ins>**App 2**</ins> : Créer un array de longueur 10 constitué que de 1 et un autre que de 0

<script>
function myFunctionNumpyApp2() {
    var x = document.getElementById("NumpyApp2");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionNumpyApp2()">Voir résultat</button>

<div id="NumpyApp2" hidden>
<div></div>

```python
np.ones(10)
np.zeros(10)
```
</div>

<ins>**App 3**</ins> : Créer un array de longueur 10 avec des éléments parcourant 0 à 10 inclus de 2 en 2

<script>
function myFunctionNumpyApp3() {
    var x = document.getElementById("NumpyApp3");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionNumpyApp3()">Voir résultat</button>

<div id="NumpyApp3" hidden>
<div></div>

```python
np.arange(0,11,2)
```
</div>

<ins>**App 4**</ins> : Concaténer l'*array* précédent avec un array contenant les entiers de 0 à 5 inclus

<script>
function myFunctionNumpyApp4() {
    var x = document.getElementById("NumpyApp4");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionNumpyApp4()">Voir résultat</button>

<div id="NumpyApp4" hidden>
<div></div>

```python
# Solution 1
np.concatenate([np.arange(0,11,2),np.arange(6)])

# Solution 2
np.hstack([np.arange(0,11,2),np.arange(6)])
```
</div>

<ins>**App 5**</ins> : Concaténer verticalement (pour former un array de listes) l'*array* précédent avec un array contenant les entiers de 0 à 5 inclus

<script>
function myFunctionNumpyApp5() {
    var x = document.getElementById("NumpyApp5");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionNumpyApp5()">Voir résultat</button>

<div id="NumpyApp5" hidden>
<div></div>

```python
# Solution 1
np.vstack([np.arange(0,11,2),np.arange(6)])

# Solution 2 : si la concaténation horizontale des deux arrays est déjà affectée à una variable, il peut être intéressant de simplement la reformater
x=np.hstack([np.arange(0,11,2),np.arange(6)])
x.reshape(2,6)
```
</div>


<ins>**App 6**</ins> : Vérifier que tous les éléments de l'array contenant les entiers de 0 à 5 inclus sont inférieurs à 10

<script>
function myFunctionNumpyApp6() {
    var x = document.getElementById("NumpyApp6");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionNumpyApp6()">Voir résultat</button>

<div id="NumpyApp6" hidden>
<div></div>

```python
np.all(np.arange(6)<10)
```
</div>


<ins>**App 7**</ins> : Vérifier que l'un des éléments de l'array contenant les entiers de 0 à 5 inclus est supérieur strictement à 4

<script>
function myFunctionNumpyApp7() {
    var x = document.getElementById("NumpyApp7");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionNumpyApp7()">Voir résultat</button>

<div id="NumpyApp7" hidden>
<div></div>

```python
np.any(np.arange(6)>4)
```
</div>

<h2 id="pandas"><b>Pandas</b></h2>

Le package *pandas* fournit de nombreux outils pour faciliter la manipulation des données. *Pandas* permet notamment de :

* importer et exporter des données depuis divers formars (*csv*, *Excel*, *HTML*, *json*, *parquet* ...)
* définir des *dataframes* cad des tableaux de données variables (colonnes) x individus (lignes)
* manipuler des *dataframes* (gestion des valeurs manquantes, création de variables, filtre selon les variables ou les individus, fusion de différents *dataframes*)
* effectuer des statistiques descriptives (comptage et agrégation de données par groupe)
* tracer directement des graphes grâce à l'intégration dans *pandas* d'objets *matplotlib*

La documentation officielle est disponible via ce [lien](http://pandas.pydata.org/pandas-docs/stable/user_guide/index.html). Le [site](http://www.python-simple.com/python-pandas/panda-intro.php) fournit aussi un large éventail d'exemples.


<ins>**App 1**</ins> : Charger *pandas*

```python
import pandas as pd
```

<ins>**App 2**</ins> : Lire les données de population du fichier Excel *base-pop-historiques-1876-2015.xls* et afficher les 4 premières lignes

<script>
function myFunctionPandasApp2() {
    var x = document.getElementById("PandasApp2");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPandasApp2()">Voir résultat</button>

<div id="PandasApp2" hidden>
<div></div>

```python
pop=pd.read_excel("base-pop-historiques-1876-2015.xls", sheet_name="pop_1876_2015", header=5)
pop.head(4)
```
</div>


<ins>**App 3**</ins> : Afficher les dimensions de la table pop

<script>
function myFunctionPandasApp3() {
    var x = document.getElementById("PandasApp3");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPandasApp3()">Voir résultat</button>

<div id="PandasApp3" hidden>
<div></div>

```python
pop.shape
```
</div>

<ins>**App 4**</ins> : Afficher les nom de colonnes de la table *pop*

<script>
function myFunctionPandasApp4() {
    var x = document.getElementById("PandasApp4");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPandasApp4()">Voir résultat</button>

<div id="PandasApp4" hidden>
<div></div>

```python
pop.columns
```
</div>


<ins>**App 5**</ins> : Lire les données de population du fichier csv *commune2019.csv* et afficher les 2 premières lignes

<script>
function myFunctionPandasApp5() {
    var x = document.getElementById("PandasApp5");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPandasApp5()">Voir résultat</button>

<div id="PandasApp5" hidden>
<div></div>

```python
communes=pd.read_csv("commune2019.csv", sep=",", header=0)
communes.head(2)
```
</div>


<ins>**App 6**</ins> : Compter le nombre de valeurs na et non na pour la variable "comparent"

<script>
function myFunctionPandasApp6() {
    var x = document.getElementById("PandasApp6");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPandasApp6()">Voir résultat</button>

<div id="PandasApp6" hidden>
<div></div>

```python
communes.comparent.isna().value_counts()
```
</div>

<ins>**App 7**</ins> : Afficher la fréquence de chaque modalité de la variable "typecom" 

<script>
function myFunctionPandasApp7() {
    var x = document.getElementById("PandasApp7");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPandasApp7()">Voir résultat</button>

<div id="PandasApp7" hidden>
<div></div>

```python
communes.typecom.value_counts()
```
</div>

<ins>**App 8**</ins> : Afficher le type des variables de la table communes

<script>
function myFunctionPandasApp8() {
    var x = document.getElementById("PandasApp8");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPandasApp8()">Voir résultat</button>

<div id="PandasApp8" hidden>
<div></div>

```python
communes.dtypes

# Pour obtenir des informations plus détaillées
communes.info()
```
</div>

<ins>**App 9**</ins> : Si aucun typage n'a été imposé dans le read_csv, on constate que les régions (reg) sont considérées comme float alors que les départements (dep) sont considérés comme un objet. Pourquoi la variable reg n'est pas perçue comme un entier ? Pourquoi la variable dep est interprétée comme un objet ?

<script>
function myFunctionPandasApp9() {
    var x = document.getElementById("PandasApp9");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPandasApp9()">Voir résultat</button>

<div id="PandasApp9" hidden>
<div></div>

La variable relative à la région (*reg*) est considérée comme un *float* et non comme un entier car elle contient des valeurs manquantes. La variable relative au département (*dep*) est interprétée comme un objet python car elle contient des caractères de type *string* en raison de la présence de la Corse ("2A" et "2B").

</div>

<ins>**NB**</ins> : A quoi correspond le type object ?

Le type Objet de python est le type de base qui s'appuie sur la classe parente de toutes les classes.


<ins>**App 10**</ins> : Afficher les observations relatives à la ville de Lyon

<script>
function myFunctionPandasApp10() {
    var x = document.getElementById("PandasApp10");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPandasApp10()">Voir résultat</button>

<div id="PandasApp10" hidden>
<div></div>

```python
# Solution 1 :
communes[communes.libelle=='Lyon']

# Solution 2 (surtout utile si on souhaite chercher plusieurs libellés) :
communes[communes.libelle.isin(['Lyon'])]
```
</div>

<ins>**App 11**</ins> : Etes vous sûrs d'afficher toutes les observations associées à la ville de Lyon ? Afficher les observations contenant "yon"

<script>
function myFunctionPandasApp11() {
    var x = document.getElementById("PandasApp11");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPandasApp11()">Voir résultat</button>

<div id="PandasApp11" hidden>
<div></div>

```python
# Première solution avec la fonction find
libelle_yon=communes[communes.libelle.str.find('yon')!=-1].libelle
print(libelle_yon)

# Deuxième solution avec la fonction contains
libelle_yon_regex=communes[communes.libelle.str.contains('yon')]
print(libelle_yon_regex)
```
</div>

<ins>**App 12**</ins> : Afficher maintenant les observations contenant 'lyon' en gérant la casse

<script>
function myFunctionPandasApp12() {
    var x = document.getElementById("PandasApp12");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPandasApp12()">Voir résultat</button>

<div id="PandasApp12" hidden>
<div></div>

```python
libelle_lyon=communes[communes.libelle.str.lower().str.find('lyon')!=-1].libelle
```
</div>

<ins>**App 13**</ins> : Afficher maintenant les libellés présents dans les deux listes (ceux contenant *lyon* et ceux contenant *yon*)

<script>
function myFunctionPandasApp13() {
    var x = document.getElementById("PandasApp13");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPandasApp13()">Voir résultat</button>

<div id="PandasApp13" hidden>
<div></div>

```python
# Solution 1
set(libelle_lyon) & set(libelle_yon)

# Solution 2
set(libelle_lyon).intersection(libelle_yon) 
```
</div>

<ins>**App 14**</ins> : Afficher maintenant les libellés de la liste associée à *lyon* et pas à la liste associée à *yon*

<script>
function myFunctionPandasApp14() {
    var x = document.getElementById("PandasApp14");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPandasApp14()">Voir résultat</button>

<div id="PandasApp14" hidden>
<div></div>

```python
set(libelle_yon).difference(libelle_lyon)
```
</div>

<ins>**App 15**</ins> : Importer l'onglet "définitif_patrimoine" du fichier Excel *isfcom2017* 

<script>
function myFunctionPandasApp15() {
    var x = document.getElementById("PandasApp15");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPandasApp15()">Voir résultat</button>

<div id="PandasApp15" hidden>
<div></div>

```python
isf=pd.read_excel("isfcom2017.xlsx", sheet_name="définitif_patrimoine", header=1)
print(isf.shape)
isf.head(2)
```
</div>

<ins>**App 16**</ins> : Afficher le nom des colonnes de ce *dataframe*

<script>
function myFunctionPandasApp16() {
    var x = document.getElementById("PandasApp16");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPandasApp16()">Voir résultat</button>

<div id="PandasApp16" hidden>
<div></div>

```python
isf.columns
```
</div>

<ins>**App 17**</ins> : Fusionner la table des communes avec cette nouvelle table en ne conservant que les observations communes

<script>
function myFunctionPandasApp17() {
    var x = document.getElementById("PandasApp17");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPandasApp17()">Voir résultat</button>

<div id="PandasApp17" hidden>
<div></div>

Si vous avez tenté de fusionner les tables sans nettoyer la variable relative au code Insee dans le *dataframe isf*, vous avez du constater que peu d'observations ont matché. On constate que le code Insee dans *isf* contient des espaces qu'il faut préalablement supprimer.

```python
isf["codeCommune"]=isf["Code commune (INSEE)"].str.replace(" ", "")

# Plutôt privilégier (car cela permet de se prémunir des cas de double espaces)
import re
isf["codeCommune"]=[re.sub(' ','', str(x)) for x in isf["Code commune (INSEE)"]]
```
Les **expressions régulières** permettent de repérer des schémas ou des ensembles de séquences de caractères semblables dans une chaîne de caractères. Le package [*re*](https://docs.python.org/fr/3/library/re.html) regroupe un ensemble d'opérations réalisables à partir d'expressions réguières. Ce [tutoriel](http://www.xavierdupre.fr/app/teachpyx/helpsphinx/c_regex/regex.html#a-quoi-ca-sert) permet par exemple de s'exercer à leur utilisation. Certes ? Mais commment puis-je être vérifier que j'ai écrit la bonne expression régulière ? Vous pouvez notamment tester les expressions régulières avec ce [site](https://regex101.com/).

A partir de là, vous pouvez procéder à la fusion !

```python
isf_communes=pd.merge(communes, isf, left_on="com", right_on="codeCommune", how='inner')
print(isf_communes.shape)
isf_communes.head(2)
```

Vous auriez pu directement nommer le code Insee nettoyé avec le même nom que celui présent dans la table *communes* (cad *com*). Dans ce cas, il suffit de directement indiquer *on="com"* dans la fonction *merge*.
</div>

<ins>**App 18**</ins> : Pourquoi le nombre de lignes de *isf_communes* est supérieur à celui de *isf*

<script>
function myFunctionPandasApp18() {
    var x = document.getElementById("PandasApp18");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPandasApp18()">Voir résultat</button>

<div id="PandasApp18" hidden>
<div></div>

On peut notamment constater que des villes sont présentes plusieurs fois dans la table *communes*.

```python
isf_communes[isf_communes.libelle.isin(list(isf_communes.libelle.value_counts().index[isf_communes.libelle.value_counts()==2]))]
```
</div>

<ins>**App 19**</ins> : Supprimer les observations associées aux communes déléguées (*typecom* égal à COMD)

<script>
function myFunctionPandasApp19() {
    var x = document.getElementById("PandasApp19");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPandasApp19()">Voir résultat</button>

<div id="PandasApp19" hidden>
<div></div>

```python
# On vérifie au préalable la répartition de la variable *typecom*
isf_communes.typecom.value_counts()
```

```python
isf_communes=isf_communes[isf_communes.typecom!="COMD"]
isf_communes.shape
```
</div>

<ins>**App 20**</ins> : Vérifier que la ville issue de chaque table est identique dans la base fusionnée

<script>
function myFunctionPandasApp20() {
    var x = document.getElementById("PandasApp20");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPandasApp20()">Voir résultat</button>

<div id="PandasApp20" hidden>
<div></div>

```python
# Solution 1 : utiliser l'opérateur &
probleme=isf_communes[(isf_communes.ncc.str.lower()!=isf_communes.Commune.str.lower().str.replace('-'," ")) & \
                     (isf_communes.libelle.str.lower()!=isf_communes.Commune.str.lower().str.replace('-'," "))]
probleme.head(4)

# Solution 2 : utiliser numpy (np.all)
probleme=isf_communes[np.all([isf_communes.ncc.str.lower()!=isf_communes.Commune.str.lower().str.replace('-'," "), 
        isf_communes.libelle.str.lower()!=isf_communes.Commune.str.lower().str.replace('-'," ")], axis=0)]
probleme.head(4)
```

Regardons la répartition des observations posant problème selon la variable *typecom*

```python
probleme.typecom.value_counts()
```

Les observations relatives aux arrondissements sont correctes, la précision de l'arrodissement dans l'un des libellés et non dans l'autre entraîne mécaniquement la détection de ces observations.

On peut alors visualiser les observations restantes. Des problèmes d'accentuation sont à l'orgine des différeces entre les libellés issus des deux tables.

```python
probleme[probleme.typecom=="COM"][['ncc', 'libelle', 'Commune', 'Région', 'Départements']]
```
</div>

<ins>**App 21**</ins> : Afficher, par ordre décroissant, le nombre total de redevables par région

<script>
function myFunctionPandasApp21() {
    var x = document.getElementById("PandasApp21");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPandasApp21()">Voir résultat</button>

<div id="PandasApp21" hidden>
<div></div>

```python
isf_communes.groupby('Région')['nombre de redevables'].sum().sort_values(ascending=False)
```
</div>

<ins>**App 22**</ins> : Afficher, par ordre décroissant, le nombre moyen de redevables par département pour les départements où ce nombre moyen dépasse 500

<script>
function myFunctionPandasApp22() {
    var x = document.getElementById("PandasApp22");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPandasApp22()">Voir résultat</button>

<div id="PandasApp22" hidden>
<div></div>

```python
nb_isf_dep=isf_communes.groupby('Région', as_index=False)['nombre de redevables'].sum().sort_values(by='nombre de redevables', ascending=False)
nb_isf_dep[nb_isf_dep['nombre de redevables']>500]
```

Le *as_index=False* permet de ne pas passer la variable du *by* en index (les libellés des colonnes utilisées pour le regroupement sont conservées au sein d'un *dataframe*). Au delà du caractère esthétique, ce paramètre qui assure que le résultat du *group_by* reste un *dataframe* est particulièrement utile lorsque le *dataframe* final souhaite être réploité en python. Dans certains cas, on retrouve aussi la fonction *reset_index*.

</div>

<ins>**App 23**</ins> : Afficher le nombre moyen de redevables par région x département

<script>
function myFunctionPandasApp23() {
    var x = document.getElementById("PandasApp23");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPandasApp23()">Voir résultat</button>

<div id="PandasApp23" hidden>
<div></div>

```python
nb_moyen_regDep=isf_communes.groupby(['Région', 'Départements'], as_index=False)['nombre de redevables'].mean()
nb_moyen_regDep.head(4)
```
</div>

<ins>**App 24**</ins> : Afficher le nombre moyen de redevables par région x département x typecom en créant une colonne par typecom

<script>
function myFunctionPandasApp24() {
    var x = document.getElementById("PandasApp24");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPandasApp24()">Voir résultat</button>

<div id="PandasApp24" hidden>
<div></div>

```python
nb_moyen_regDepTypeCom=pd.crosstab(index=[isf_communes['Région'], isf_communes['Départements']], columns=isf_communes.typecom, values =isf_communes['nombre de redevables'], aggfunc =np.mean).reset_index()
nb_moyen_regDepTypeCom.head(4)
```
</div>

<ins>**App 25**</ins> : Transposer la table *isf_communes* pour que les trois variables 'nombre de redevables','patrimoine moyen en €','impôt moyen en €' soient au sein d'une même variable en tant que modalité et les valeurs associées dans une seule colonne

<script>
function myFunctionPandasApp25() {
    var x = document.getElementById("PandasApp25");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunctionPandasApp25()">Voir résultat</button>

<div id="PandasApp25" hidden>
<div></div>

```python
isf_transpose=isf_communes.melt(id_vars=list(set(isf_communes.columns).difference(set(['nombre de redevables', 'patrimoine moyen en €', 'impôt moyen en €']))))
isf_transpose.head(2)
```

Pour reformater les données, il peut être utile de recourir aux fonctions *pivot*, *stack* ou *unstack*. Pour cela, vous pouvez vous reporter à l'[aide](http://pandas.pydata.org/pandas-docs/stable/user_guide/reshaping.html) fournie sur le site officiel de pandas.
</div>



