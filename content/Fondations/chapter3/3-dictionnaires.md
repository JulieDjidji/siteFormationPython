---
title: "Les dictionnaires"
date: 2017-10-17T15:26:15Z
draft: false
hidden: true
weight: 30
---

Un dictionnaire est un objet qui à chaque clé associe une valeur. 


<ins>**Exercice**</ins> : Importer les données et les charger dans un dictionnaire

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
dico={}
with open('./data/commune2019.csv', 'r') as csvfile:
    file = csv.reader(csvfile, delimiter=',')
    nrow=1
    for row in file:
        if nrow==1:
            nomColonnes=row
            nrow+=1
            continue
        elif nrow==2:
            dico[row[1]]={x[0]:x[1] for x in zip(nomColonnes,row)}
```
</div>



Mettre en évidence l'intérêt du package pprint

