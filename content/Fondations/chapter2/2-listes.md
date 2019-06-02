---
title: "Le premier objet python : les listes"
date: 2019-03-18T15:26:15Z
draft: false
hidden: true
weight: 20
---

Une **liste** est une collection ordonnée d'élements qui peuvent être de types différents (combinaison possible de listes, de dictionnaires, d'éléments numériques et d'éléments caractères).

## Création et manipulation d'une liste

| Action | Fonction python |
|:---------------|------------------------:|
| Création d'une liste | [] ou *list()* |
| Test de la présence d'un élément dans une liste | *x in liste* |
| Accès à un élément | *liste[i]* |
| Accès à plusieurs éléments | *liste[i:j]* |
| Minimum de la liste | *min(liste)* |
| Maximum de la liste | *max(liste)* |
| Nombre d'éléments d'une liste | *len(liste)* |
| Nombre d’occurrence de l'élément x dans la liste | *liste.count(x)* |

## Insertion et suppression d'éléments d'une liste


| Action | Fonction python |
|:---------------|------------------------:|
| Ajouter un élément v à la fin de la liste | liste.append(v) |
| Ajouter une liste sl à la fin de la liste | liste.extend(sl) |
| Insérer un élément v à l'indice i | liste.insert(i,v) |
| Remplacer l'élément i par une valeur v | *liste[i]=v* |
| Remplacer les éléments d'indices i à j par une sous liste sl | *liste[i:j]=sl* |
| Supprimer le premier élément égal à v | *liste.remove(v)* |
| Supprimer l'élément d'indice i | *liste.pop(i)* |
| Supprimer tous les éléments | *liste.clear()* ou *liste *= 0* ou *liste=[]* |


<ins>**Exercice**</ins> : Importer les données (avec *open* et *csv.reader*) et les charger dans une liste


<script>
function myFunction() {
    var x = document.getElementById("myDIV");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction()">Voir résultat</button>

<div id="myDIV" hidden>
<div></div>

``` python
import csv
liste=[]
with open('./data/commune2019.csv', 'r') as csvfile:
    file = csv.reader(csvfile, delimiter=',')
    for row in file:
    	liste.append(row)
```
</div>



## Gérér le caractère mutable des listes

<ins>**Test**</ins> : Créer une liste l1 et créer l2=l1 puis modifier l1. Afficher ensuite l2. Que constatez-vous ?



<ins>**Test**</ins> : Faire une vraie copie de l1

<script>
function astuceFunction() {
    var x = document.getElementById("astuce");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="astuceFunction()">Astuce</button>
<div id="astuce" hidden>
<div></div>

**Fonction copy et deepcopy**

Le package *copy* contient deux fonctions *copy* et *deepcopy* pour réaliser des copies. Il est préférable d'utiliser *deepcopy* car la fonction *copy* peut réaliser une copie imparfaite dans le cas des listes de listes.
</div>


## Les compréhensions de liste

**<ins>Principe</ins> : construire une liste en parcourant tout autre itérable (liste, tuple, chaîne de caractères, ...)**

* la valeur ajoutée à la liste peut résulter d'un calcul (avec ou sans utiliser la valeur de l'élément de l'itérable parcouru)
* une condition optionnelle (if) peut filtrer les éléments de l'itérable parcouru
* une condition (if else) peut permettre d'affecter une valeur différente selon la valeur de l'itérable parcouru

**Pourquoi privilégier les compréhensions de liste ?**

* Code plus synthétique
* Rapidité : allocation de la mémoire avant l'ajout des éléments (plutôt qu'un redimensionnement au fil de l'exécution comme avec la fonction *append*)

<ins>**Exercice**</ins> : A partir d'une list comprehension, ré-écrire la boucle for permettant de calculer le carré des éléments compris entre 1 et 5 et stocker le résultat dans une liste.

<script>
function myFunction2() {
    var x = document.getElementById("myDIV2");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction2()">Voir résultat</button>

<div id="myDIV2" hidden>
<div></div>

``` python
[i**2 for i in [1,2,3,4,5]]
```
</div>


<ins>**Exercice**</ins> : Dupliquer cette liste pour obtenir une liste contenant les éléments en double

<script>
function myFunction3() {
    var x = document.getElementById("myDIV3");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction3()">Voir résultat</button>

<div id="myDIV3" hidden>
<div></div>

``` python
[i**2 for i in [1,2,3,4,5]]+[i**2 for i in [1,2,3,4,5]]
```
</div>





