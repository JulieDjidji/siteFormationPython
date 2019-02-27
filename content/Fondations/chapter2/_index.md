---
title: "Chapitre 2 : Lecture, écriture et fermeture des fichiers"
date: 2017-10-17T15:26:15Z
draft: false
weight: 30
---

Avant d'étudier des méthodes d'ouverture et de lecture de fichiers spécifiées dans des packages spécifiques (*numpy* ou *pandas* par exemple), commençons par mettre en oeuvre les fonctions de la librairie standard. Pour lire ou écrire dans un fichier, il suffit d'utiliser la fonction *open* et de spécifier son action dans le paramètre *mode*. Les modalités de ce paramètre sont précisés dans le tableau ci-dessous : 

| Paramètre mode | Type d'accès associé |
|:---------------|------------------------------------------------------------------:|
| 'r'            | accès en lecture seule ; erreur si le fichier n'existe pas|
| 'w'            | accès en écriture ; si le fichier n'existe pas, il est créé ; s'il existe, son contenu est écrasé|
| 'r+'           | accès en lecture et écriture, permettant de lire et intercaler des données dans le fichier|
| 'a'            | accès en mode ajout (append) ; si le fichier n'existe pas, il est créé ; s'il existe, son contenu est laissé intact, et les écritures s'effectuent à la fin du fichier|


Dans le paramètre *mode*, il est possible de spécifier aussi le type de fichier ('t' pour le mode texte et 'b' pour le mode binaire). Cette lettre doit être concaténée à la lettre précisant le type d'accès souhaité (lecture ou écriture).


```python
# Commençons par ouvrir un fichier (par exemple, un fichier txt ou un csv)
fd = open('train.csv', mode='r')
```

Trois fonctions permettent de lire le fichier :
* Pour lire un ligne : fd.readline()
* Pour lire l'ensemble des lignes en séparant chaque ligne : fd.readlines()
* Pour lire complètement un bloc : fd.read()

<ins>**Test 1**</ins> : tester chacune des trois méthodes avec le fichier *communes.csv*

<script>
function myFunction1() {
    var x = document.getElementById("test1");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction1()">Voir résultat</button>

<div id="test1" hidden>
<div></div>

```python
fd = open('./data/commune2019.csv', mode='r')
fd.readline()
```

```python
fd = open('./data/commune2019.csv', mode='r')
fd.readlines()
```

```python
fd = open('./data/commune2019.csv', mode='r')
fd.read()
```
</div>

<ins>**Test 2**</ins> : que se passe-t-il quand on effectue deux fois de suite la commande fd.readline()

<ins>**Test 2bis**</ins> : retester fd.readline() après avoir fait fd.seek(0)

<script>
function myFunction2() {
    var x = document.getElementById("test2");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction2()">Voir résultat</button>

<div id="test2" hidden>
<div></div>

```python
fd = open('./data/commune2019.csv', mode='r')
print(fd.readline())
print(fd.readline())
```

A chaque readline(), on passe à la ligne suivante. Pour rester sur la première ligne, il faut :

* soit ré-éxécuter l'ouverture du fichier (*open*)
* fd.seek(0) permet aussi de se repositionnement au début fichier !

</div>


<ins>**Test 3**</ins> : à partir de l'instruction *with* et de la fonction readline, afficher l'ensemble des lignes

<script>
function myFunction3() {
    var x = document.getElementById("test3");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction3()">Voir résultat</button>

<div id="test3" hidden>
<div></div>

```python
with open('./data/commune2019.csv', mode='r') as file:
    print(file.readline())
```

L'instruction *with* implique automatiquement la fermeture du fichier. Il est préférable d'utiliser systématiquement cette instruction. 

</div>


<ins>**Test 4**</ins> : appliquer une méthode pour lire un fichier txt et n'afficher que les deux premières observations

<script>
function readtxtFunction() {
    var x = document.getElementById("readtxt");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="readtxtFunction()">Voir résultat</button>

<div id="readtxt" hidden>
<div></div>

```python
with open('france2016.txt', 'r', encoding='latin1') as txtfile:
    print(txtfile.readline())
    print(txtfile.readline())
```

</div>

Il est aussi possible d'ouvrir les données avec le package *fileinput* en utilisant le code ci-dessous :

```python
import fileinput
for line in fileinput.input('train.csv'):
    print(line)
fileinput.close()
```

Des modules permettent de lire spécifiquement des fichiers csv ou json :

* le module *csv* :  csv.reader() pour lire les lignes au sein d'un csv
* le module *json* : json.dumps() (nécessaires en cas de json emboîtés) suivi d'un json.loads()


<ins>**Test**</ins> : Utiliser le module csv pour importer et afficher le contenu du fichier *communes.csv*

<script>
function readCSVFunction() {
    var x = document.getElementById("readCSV");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="readCSVFunction()">Voir résultat</button>

<div id="readCSV" hidden>
<div></div>

```python
import csv
with open('/data/communes.csv', 'r') as csvfile:
    file = csv.reader(csvfile, delimiter=',')
    for row in file:
	print(', '.join(row))
```

</div>



