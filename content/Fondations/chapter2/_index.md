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

<ins>**Test 1**</ins> : tester chacune des trois méthodes

<ins>**Test 2**</ins> : que se passe-t-il quand on effectue deux fois de suite la commande fd.readline()

<ins>**Test 2bis**</ins> : retester fd.readline() après avoir fait fd.seek(0)


fd.seek(0) permet de se repositionnement au début fichier !


<ins>**Test 3**</ins> : à partir de la fonction *with* et de la fonction readline, afficher l'ensemble des lignes


Il est aussi possible d'ouvrir les données avec le package *fileinput* en utilisant le code ci-dessous :

```python
import fileinput
for line in fileinput.input('train.csv'):
    print(line)
fileinput.close()
```

<ins>**Test**</ins> : appliquer cette méthode pour lire un fichier txt



Des modules permettent de lire spécifiquement des fichiers csv ou json :

* le module *csv* :  csv.reader() pour lire les lignes au sein d'un csv
* le module *json* : json.dumps() (nécessaires en cas de json emboîtés) suivi d'un json.loads()


```python
import csv
with open('/home/jovyan/train.csv', 'r') as csvfile:
    spamreader = csv.reader(csvfile, delimiter=',')
    for row in spamreader:
        print(', '.join(row))
```


```python
import json
with open('test.json', 'r') as f:
    print(json.loads(json.dumps(f.read())))
```

    {'maps': [{'id': 'blabla', 'iscategorical': '0'},
                  {'id': 'blabla', 'iscategorical': '0'}],
         'masks': [{'id': 'valore'}],
         'om_points': 'value',
         'parameters': [{'id': 'valore'}]}



```python
import json
with open('test.json', 'r') as f:
    try:
        print(json.loads(f.read()))
    except ValueError:
        with open('test.json', 'r') as f:
            print(json.loads(json.dumps(f.read())))
```

    {'maps': [{'id': 'blabla', 'iscategorical': '0'},
                  {'id': 'blabla', 'iscategorical': '0'}],
         'masks': [{'id': 'valore'}],
         'om_points': 'value',
         'parameters': [{'id': 'valore'}]}

