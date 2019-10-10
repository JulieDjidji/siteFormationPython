---
title: "Chapitre 3 : Lecture, écriture et fermeture des fichiers"
date: 2019-03-18T15:26:15Z
draft: false
weight: 40
---

Commençons avec une solution simple proposée en python pour lire un fichier, par exemple un fichier *csv*. Faites abstraction du chargement de *pandas* dans un premier temps, on reviendra sur cetta librairie plus tard ! 

```python
import pandas as pd
data = pd.read_csv("train.csv", sep=";", header=0)
data.head(2)
```

Ces commandes illustrent la facilité offerte par python pour charger et consulter un jeu de données. Toutefois, avant d'étudier des méthodes d'ouverture et de lecture de fichiers spécifiées dans des packages spécifiques tels que *pandas*, commençons par mettre en oeuvre les fonctions de la librairie standard. En effet, même si elles sont légèrement plus complexes, elles peuvent s'avérer utile. Par exemple, le jeu de données initial peut être trop volumineux pour être entièrement chargé en mémoire. Cette contrainte est pourtant imposée lors du chargement des données avec le package *pandas*.

Ainsi, pour lire ou écrire dans un fichier, il suffit d'utiliser la fonction *open* et de spécifier son action dans le paramètre *mode*. Les modalités de ce paramètre sont précisées dans le tableau ci-dessous : 

| Paramètre mode | Type d'accès associé |
|:---------------|------------------------------------------------------------------:|
| 'r'            | accès en lecture seule ; erreur si le fichier n'existe pas |
| 'w'            | accès en écriture ; si le fichier n'existe pas, il est créé ; s'il existe, son contenu est écrasé |
| 'r+'           | accès en lecture et écriture, permettant de lire et intercaler des données dans le fichier |
| 'a'            | accès en mode ajout (append) ; si le fichier n'existe pas, il est créé ; s'il existe, son contenu est laissé intact, et les écritures s'effectuent à la fin du fichier |


Dans le paramètre *mode*, il est possible de spécifier aussi le type de fichier ('t' pour le mode texte et 'b' pour le mode binaire). Cette lettre doit être concaténée à la lettre précisant le type d'accès souhaité (lecture ou écriture).

Le pendant de la commande *open* est la commande *close*.


```python
# Commençons par ouvrir un fichier (par exemple, un fichier txt ou un csv)
fd = open('train.csv', mode='r')
```

Trois fonctions permettent de parcourir le fichier ouvert : 

* Pour lire une ligne : *fd.readline()*
* Pour lire toutes les lignes (avec la fonction readline()) jusqu'à la fin du fichier et renvoie une liste de lignes : *fd.readlines()*
* Pour lire complètement un bloc : *fd.read()*
Pour ces 3 fonctions, il est possible de passer un nombre d'octets à lire en paramètre.

Attention au type d'encodage du fichier à lire ou à écrire ! Par défaut python est en *utf8*, alors que bien souvent les fichiers créés sous windows sont en *latin1*. 

```python
# Exemples de code avec variable *encoding*
fd1 = open('train1.csv', mode='r',encoding='latin1')
fd2 = open('train2.csv', mode='r',encoding='utf8')
```

<ins>**Test 1**</ins> : Tester chacune des trois méthodes avec le fichier *communes2019.csv*

<script>
function myFunction1() {
    var x = document.getElementById("test1");
    if (x.style.display !== "block") {
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
read=fd.readline()
fd.close()
```

```python
fd = open('./data/commune2019.csv', mode='r')
read=fd.readlines()
fd.close()
```

```python
fd = open('./data/commune2019.csv', mode='r')
fd.read()
fd.close()
```
</div>

<ins>**Test 2**</ins> : Que se passe-t-il quand on effectue deux fois de suite la commande *fd.readline()*

<ins>**Test 2bis**</ins> : Retester *fd.readline()* après avoir fait *fd.seek(0)*

<script>
function myFunction2() {
    var x = document.getElementById("test2");
    if (x.style.display !== "block") {
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
</div>

A chaque *readline()*, on passe à la ligne suivante. Pour rester sur la première ligne, il faut :

* soit ré-éxécuter l'ouverture du fichier (*open*)
* fd.seek(0) permet aussi de se repositionnement au début fichier !

Les manières d'ouvrir les fichiers présentées ci-dessus ne sont pas les plus élégantes, ni les plus efficaces pour travailler avec les fichiers.
Sur la base des commandes déjà présentées, il est plutôt conseillé d'utiliser le code suivant (avec les instructions *try* et *finally* qui prennent en charge les erreurs et la fin de fichier) :

```python
fd = open('./data/commune2019.csv', mode='r')
try:
    print(fd.readline())
finally:
    reader.close()
```

Encore plus élégant (the "pythonic way"), il est préférable ouvrir un fichier avec la fonction *with*.

<ins>**Test 3**</ins> : A partir de l'instruction *with* et de la fonction *readline*, afficher l'ensemble des lignes

<script>
function myFunction3() {
    var x = document.getElementById("test3");
    if (x.style.display !== "block") {
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
</div>

L'instruction *with* implique automatiquement la fermeture du fichier en fin d'itération. Il est préférable d'utiliser systématiquement cette instruction. 

Encore plus élégant (the "most pythonic way"), il est préférable ouvrir un fichier avec la fonction *with* et de parcourir le fichier avec une boucle *for*. Cette méthode est bien plus économe en mémoire car le fichier n'est pas chargé intégralement en mémoire pour être traité, comme avec les fonctions *read*. En effet, seul un bloc de ligne est chargé en mémoire avant d'être traité puis il est remplacé par le bloc suivant.

<ins>**Test 4**</ins> : A partir des instructions *with* et *for*, afficher l'ensemble des lignes

<script>
function myFunction4() {
    var x = document.getElementById("test4");
    if (x.style.display !== "block") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction4()">Voir résultat</button>

<div id="test4" hidden>
<div></div>

```python
with open('./data/commune2019.csv', mode='r') as file:
    for line in file:
        print(line,end='')
```
</div>

<ins>**Test 5**</ins> : Appliquer une méthode pour lire un fichier txt et n'afficher que les deux premières observations, en ne tenant pas compte de la ligne d'entête.

A noter, il est aussi possible de 'sauter' une ligne avec l'instruction *next*. En effet, l'objet créé avec *with open* est un itérateur, et on peut donc passer au suivant avec un *next(itérateur)*.

<script>
function readtxtFunction() {
    var x = document.getElementById("readtxt");
    if (x.style.display !== "block") {
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
    header=next(txtfile)
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
Avec ces méthodes pour lire les données, on lit "un enregistrement". Il faut ensuite le découper en champs à l'aide du séparateur (en règle générale , ou ;).
Pour ce faire, il faut utiliser la fonction *split("séparateur")*.

Par exemple :

with open('commune2019.csv', 'r') as reader:
    for line in reader:
        print(line.strip().split(","))

On a également utilisé la fonction *strip* pour enlever les éventuels blancs inutiles à droite et à gauche de chaque champs.

Des modules permettent de lire spécifiquement des fichiers csv ou json et de faire ce découpage sur le séparateur et retourne le résultat dans une liste :

* le module *csv* :  csv.reader() et csv.writer() pour lire et écrire les lignes au sein d'un csv. Ces commandes acceptent en option le mot-clé *delimiter=* pour préciser le choix du caractère de séparation, par défaut ','
* le module *json* : json.dumps() (nécessaires en cas de json emboîtés) suivi d'un json.loads()

<ins>**Test 6**</ins> : Utiliser le module csv pour importer et afficher le contenu du fichier *communes.csv*

<script>
function readCSVFunction() {
    var x = document.getElementById("readCSV");
    if (x.style.display !== "block") {
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

<ins>**Test 7**</ins> : Nettoyer le fichier commune2019.csv en ne gardant que les communes avec un "typecom"="COM" et les champs "com", "reg", "libelle" et générer un nouveau csv (utf8 et delimiteur ,) avec un format d'enregistrement depcom, libelle, reg

<script>
function myFunction7() {
    var x = document.getElementById("test7");
    if (x.style.display !== "block") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction7()">Voir résultat</button>

<div id="test7" hidden>
<div></div>

``` python
import csv
with open('commune2019.csv', 'r',encoding='utf8') as csvin, open('cog2019-actual.csv', 'w',encoding='utf8') as csvout:
    reader=csv.reader(csvin,delimiter=',')
    writer=csv.writer(csvout,delimiter=',')
    header = ['depcom','libelle','reg']
    writer.writerow(header)
    for line in reader:
        if line[0] == 'COM':
            depcom=line[1]
            reg=line[2]
            libelle=line[8]
            writer.writerow([depcom,libelle,reg])
```
</div>

<ins>**Test 8**</ins> : Charger ce nouveau fichier dans un dictionnaire

<script>
function myFunction8() {
    var x = document.getElementById("test8");
    if (x.style.display !== "block") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction8()">Voir résultat</button>

<div id="test8" hidden>
<div></div>

``` python
import csv
dico={}
with open('cog2019-actual.csv', 'r') as csvfile:
    file = csv.reader(csvfile, delimiter=',')
    nomColonnes=next(file)
    for row in file:
        dico[row[0]]={x[0]:x[1] for x in zip(nomColonnes,row)}
```
autre solution
``` python
dico = {}
communes = csv.DictReader(open('cog2019-actual.csv', 'r',encoding='utf8'), delimiter=',')
for commune in communes:
    dico[commune['depcom']]=[commune['libelle'],commune['reg']]
```
</div>



