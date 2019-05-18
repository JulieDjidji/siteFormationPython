---
title: "Les sets"
date: 2019-03-18T15:26:15Z
draft: false
hidden: true
weight: 40
---

Un ensemble (*set*) est une collection non ordonnée d'éléments **uniques**.

<ins>**Exercice 1**</ins> : Reprendre le dernier exemple créé dans la <a href="/fondations/chapter3/2-listes">section sur les listes</a>, créer et convertir cette liste en ensemble. Que constatez-vous ?

<script>
function myFunction1() {
    var x = document.getElementById("exercice1");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction1()">Voir résultat</button>

<div id="exercice1" hidden>
<div></div>

```python
set([i**2 for i in [1,2,3,4,5]]+[i**2 for i in [1,2,3,4,5]])
```

On constate que les éléments dupliqués sont supprimés. Cette fonctionnalité des ensembles peut faciliter la manipulation de données lorsqu'on souhaite obtenir les différentes modalités d'une variable par exemple. On verra dans la section sur la <a href="/explorer/chapter1/">manipulation de données</a> qu'il est aussi possible de récuper la sous-liste des éléments uniques d'une liste avec le package *numpy* avec la commande : *np.unique*.
</div>


<ins>**Exercice 2**</ins> : Créer deux ensembles : le premier constitué des cinq premières lettres de l'alphabet et le second des dix premières lettres de l'alphabet

<script>
function myFunction2() {
    var x = document.getElementById("exercice2");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction2()">Voir résultat</button>

<div id="exercice2" hidden>
<div></div>

```python
import string
ens1=set(string.ascii_lowercase[0:5])
ens2=set(string.ascii_lowercase[0:10])
```
</div>

<ins>**Exercice 3**</ins> : Vérifier que ces deux ensembles ne sont pas disjoints

<script>
function myFunction3() {
    var x = document.getElementById("exercice3");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction3()">Voir résultat</button>

<div id="exercice3" hidden>
<div></div>

```python
ens1.isdisjoint(ens2)
```
</div>

<ins>**Exercice 4**</ins> : Afficher l'intersection de ces deux ensembles

<script>
function myFunction4() {
    var x = document.getElementById("exercice4");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction4()">Voir résultat</button>

<div id="exercice4" hidden>
<div></div>

```python
ens1.intersection(ens2)
```
</div>

<ins>**Exercice 5**</ins> : Afficher la différence entre ces deux ensembles

<script>
function myFunction5() {
    var x = document.getElementById("exercice5");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction5()">Voir résultat</button>

<div id="exercice5" hidden>
<div></div>

```python
ens1.difference(ens2)
```
</div>

