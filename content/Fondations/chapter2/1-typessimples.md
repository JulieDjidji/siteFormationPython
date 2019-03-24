---
title: "Les principaux types de données : entiers, flottants, chaînes de caractère"
date: 2019-03-18T15:26:15Z
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

On souhaite parfois insérer des valeurs personnalisées au sein d'une chaîne de caractères. 

```python
nom1="Julie"
nom2="Laurent"
service = "au SSP-Lab"
"On s'appelle %s et %s et on travaille %s."  %  ( nom1 , nom2, service ) 
```

Toutefois, plus le nombre de paramètres personnalisables est élevé, moins le code est lisible. Une solution alternative consiste à recourir à *str.format()* disponible depuis *python 2.6*.


```python
params  =  { 'nom1' :  'Julie' , 'nom2' : "Laurent" , 'service' : "au SSP-Lab"} 
"On s'appelle {nom1} et {nom2} et on travaille {service}." . format ( ** params )
```

Largement plus lisible, cette deuxième solution devient toutefois aussi chargée lorsque le nombre de paramètres augmente fortement. Et depuis *python 3.6*, sont apparues les *f-Strings*. 

```python
f"On s'appelle {nom1} et {nom2} et on travaille {service}." 
```

Il est possible d'effectuer des opérations au sein des chaînes de caractères avec f-strings*.

```python
x=4
f"Nous pouvons faire des calculs : le double de {x} vaut {2 * x}"
```

L'[article](https://realpython.com/python-f-strings/#old-school-string-formatting-in-python) dédié aux *f-strings* sur le site *realpython* détaille les différentes solutions de formatage des chaînes de caractères et les possibilités offertes par f-strings*.




