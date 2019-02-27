---
title: "1 - Les fonctions"
date: 2017-10-17T15:26:15Z
draft: false
hidden: true
---

Pour comprendre l'indentation, prenons l'exemple des fonctions. Pour écrire sa propre fonction, il faut respecter les conventions suivantes :

* il faut définir la fonction avec le terme *def* et la ligne contenant cette instruction se termine par un deux-points selon ce modèle : *def nomFonction(arg1, ...):* 
* des parenthèses après le nom de la fonction contiennent les paramètres de la fonction. En cas d'absence de paramètres, les parenthèses restent vides. 
* il n'y a pas de contrainte sur le nom des fonctions, à l'exception de mots ayant déjà une signification (par exemple, *list* correspond déjà à une fonction python). Il est préférable que le nom des fonctions commence par une minuscule.
* Si on souhaite fixer des valeurs par défaut à certains paramètres de la fonction, il faut que les paramètres sans valeur par défaut soient définis avant au sein des parenthèses.
* Pour renvoyer une valeur à la fonction, il faut la faire figurer dans *return * à la fin de la fonction.


```python
# Fonction pour calculer le carré de x 
def auCarre(x):
    return x**2
```


```python
# Pour appliquer la fonction avec x=4
auCarre(4)
```


    16
