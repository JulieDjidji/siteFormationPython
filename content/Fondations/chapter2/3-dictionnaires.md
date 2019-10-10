---
title: "Les dictionnaires"
date: 2019-03-18T15:26:15Z
draft: false
hidden: true
weight: 30
---

Un **dictionnaire** est une liste qui à chaque clé associe une valeur. Il prend la forme suivante :

<div align="center">{'clé1': 'valeur1', 'clé2': 'valeur2'}</div>

L'indexation (présence d'une clé) facilite la recherche ou la modification d'une valeur. Contrairement aux listes, en raison du principe d'indexation, le temps nécessaire à la recherche d'un élément (avec l'opérateur *in*) ne dépend pas de la longueur de l'objet.

Voici les principales fonctions pour manipuler les dictionnaires :

| Action | Fonction python |
|:---------------|------------------------:|
| Création d'un dictionnaire | {} |
| Accès aux clés du dictionnaire d | d.keys() |
| Accès aux valeurs du dictionnaire d | d.values() |
| Accès à la valeur associée à la clé "clé1" | d.get("clé1") |
| Test présence de la clé "clé1" | d.has_key("clé1") ou "clé1" in d |
| Copie réelle du dictionnaire d | d.copy() |
| Suppression de tous les items du dictionnaire d | d.clear() |
| Suppression de la clé "clé1" du dictionnaire d | d.pop("clé1") |
| Suppression arbitraire d'un item (clé, valeur) du dictionnaire d | d.popitem() |


<ins>**Exercice 1**</ins> : Créer un dictionnaire vide

<script>
function myFunction1() {
    var x = document.getElementById("exercice1");
    if (x.style.display !== "block") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction1()">Voir résultat</button>

<div id="exercice1" hidden>
<div></div>

``` python
d = {}
```
</div>

<ins>**Exercice 2**</ins> : Ajouter votre nom, votre prénom, votre direction et votre service (DG, SSM, ...)

<script>
function myFunction2() {
    var x = document.getElementById("exercice2");
    if (x.style.display !== "block") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction2()">Voir résultat</button>

<div id="exercice2" hidden>
<div></div>

``` python
d["nom"]="Djirig"
d["prenom"]="Julie"
d["direction"]="DMCSI"
d["service"]="SSP-Lab"
```
</div>

<ins>**Exercice 3**</ins> : Faire un réelle copie de ce premier dictionnaire. Modifier le nom dans cette copie et afficher les deux dictionnaires. Que se serait-il passé si on n'avait pas fait une copie indépendante du dictionnaire avant de modifier le nom ?

<script>
function myFunction3() {
    var x = document.getElementById("exercice3");
    if (x.style.display !== "block") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction3()">Voir résultat</button>

<div id="exercice3" hidden>
<div></div>

``` python
d_copie=d.copy()
d_copie['nom']='nouveauNom'
```

Si on n'avait pas fait de copie à l'aide de la fonction *copy* mais simplement *d_copie=d*, les deux variables auraient pointé sur le même objet. La modification de *d_copie* aurait mécaniquement entrainé celle de *d*.
</div>

<ins>**Exercice 4**</ins> : Créer un dictionnaire contenant votre premier dictionnaire et celui de votre voisin

<script>
function myFunction4() {
    var x = document.getElementById("exercice4");
    if (x.style.display !== "block") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction4()">Voir résultat</button>

<div id="exercice4" hidden>
<div></div>

On commence par créer le dictionnaire de notre voisin.

``` python
d2={}
d2["nom"]="Djirig"
d2["prenom"]="Julie"
d2["direction"]="DMCSI"
d2["service"]="SSP-Lab"
```
Puis, on crée le dictionnaire complet en chosissant comme clé, notre identifiant professionnel.

``` python
d_complet={"ev43ru":d, "test":d2}
```
</div>

<ins>**Exercice 5**</ins> : Afficher ce nouveau dictionnaire

<script>
function myFunction5() {
    var x = document.getElementById("exercice5");
    if (x.style.display !== "block") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction5()">Voir résultat</button>

<div id="exercice5" hidden>
<div></div>

Le contenu de ce nouveau dictionnaire peut s'afficher simplement en indiquant le nom du dictionnaire. Toutefois, lorsque le dictionnaire est long, et notamment lorsqu'il provient de l'import d'un fichier *json*, le package *pprint* permet un affichage plus lisible du contenu du dictionnaire : 

``` python
import pprint
pprint(d)
```
</div>

<ins>**Exercice 6**</ins> : Afin de comprendre l'intérêt d'un dictionnaire et sa logique clé-valeur associée, comptez le nombre de fois où chaque lettre de l'alphabet est présente au sein du mot "Saperlipopette".

<script>
function myFunction6() {
    var x = document.getElementById("exercice6");
    if (x.style.display !== "block") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction6()">Voir résultat</button>

<div id="exercice6" hidden>
<div></div>

``` python
mot="Saperlipopette"
dico={}
for i in mot.lower():
    if i in dico.keys():
        dico[i]+=1
    else:
        dico[i]=1
dico
```

Le dictionnaire, qui repose sur l'association clé-valeurs, est dans cet exemple pertinent car il est modifiable, exige qu'un seul parcours du mot et ne nécessite pas de connaître préalablement l'ensemble des lettres présentes dans le mot. Pour faciliter la réutilisation de ce code, il est préférable de créer une fonction.

``` python
mot="Saperlipopette"

def comptage(mot):
    dico={}
    for i in mot.lower():
        if i in dico.keys():
            dico[i]+=1
        else:
            dico[i]=1
    return dico

comptage(mot)
```

</div>




