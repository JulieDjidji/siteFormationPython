---
title: "Les principaux types de données : entiers, flottants, chaînes de caractère"
draft: false
weight: 10
hidden: true
---

## Quelques exercices de manipulation

<ins>**Exercice 1**</ins> : afficher le type de x pour x=3, x="test" et x=3.5

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
x=3
type(x)
```
```python
x='test'
type(x)
```
```python
x=3.5
type(x)
```
</div>

<ins>**Exercice 2**</ins> : Concaténer les chaînes de caractères suivantes "Les deux formateurs sont : ", "Julie", " et ", "Laurent"

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
"Les deux formateurs sont : "+"Julie"+" et "+"Laurent"
```
</div>

<ins>**Exercice 3**</ins> : Compter le nombre de fois où la lettre e est présente dans la chaîne "Je fais un comptage des e."

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
"Je fais un comptage des e.".count('e')
```
</div>

<ins>**Exercice 4**</ins> : Repérer la première position où la lettre e est présente dans la chaîne "Je fais un comptage des e."

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
"Je fais un comptage des e.".find('e')
```
</div>

<ins>**Exercice 5**</ins> : Afficher l'ensemble des méthodes attachées à la chaîne de caractère "Je fais un comptage des e."

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
chaine="Je fais un comptage des e."
dir(chaine)
```
</div>


## Astuce de formatage des chaînes de caractères

* **Les expressions régulières**

Les **expressions régulières** permettent de repérer des schémas ou des ensembles de séquences de caractères semblables dans une chaîne de caractères. Le package [*re*](https://docs.python.org/fr/3/library/re.html) regroupe un ensemble d'opérations réalisables à partir d'expressions réguières. Ce [tutoriel](http://www.xavierdupre.fr/app/teachpyx/helpsphinx/c_regex/regex.html#a-quoi-ca-sert) permet par exemple de s'exercer à leur utilisation. Certes ? Mais commment puis-je être vérifier que j'ai écrit la bonne expression régulière ? Vous pouvez notamment tester les expressions régulières avec ce [site](https://regex101.com/).

* **f_string**

https://cito.github.io/blog/f-strings/
https://www.python.org/dev/peps/pep-0498/#differences-between-f-string-and-str-format-expressions
https://realpython.com/python-f-strings/#old-school-string-formatting-in-python



