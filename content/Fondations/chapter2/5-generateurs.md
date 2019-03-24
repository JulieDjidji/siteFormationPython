---
title: "Les itérateurs et les générateurs"
date: 2019-03-18T15:26:15Z
draft: false
hidden: true
weight: 50
---

## Les itérateurs

Les listes, les dictionnaires, les ensembles ou même les chaînes de caractères sont des itérables. On peut en effet itérer selon ces séquences. Un **itérateur** est un curseur permettant de se déplacer d'élément en élément au sein de l'itérable.

Son principal avantage est son faible coût en termes de mémoire. Celui peut par exemple se mesurer dans une moindre mesure avec les instructions suivantes :

```python
import sys
print(sys.getsizeof([1,2,3,4,5]))
print(sys.getsizeof(iter([1,2,3,5,5])))
```

Evidemment, plus l'itérable est long/gros, plus les différences de mémoire occupées sont importantes. En revanche, malgré l'augmentation du nombre d'éléments dans l'itérateur, comme ces éléments ne sont pas en mémoire, l'itérateur ne nécessite pas de ressources supplémentaires. 

```python
print(sys.getsizeof([0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99]
))
print(sys.getsizeof(iter([0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99]
)))
```

Cette différence s'explique par le fait que les éléments de l'itérateur ne sont pas stockés en mémoire.

En pratique, quand on réalise une boucle sur la liste *[1,2,5,3,5,4]*, avant d'exécuter par itération les instructions présentes au sein de la boucle, python commence par transformer cette liste en itérateur avec la commande suivante :

```python
iterateur = iter([1,2,3])
```

On peut d'ailleurs parcourir les éléments de l'itérateur avec la fonction *next*. Faites alors tourner 4 fois l'instruction suivante : 

```python
next(iterateur)
```

Lorsque l'itérateur est complètement parcouru, l'instruction *next* lève une exception de type *StopIteration*. On n'a donc pas besoin de connaître le nombre d'éléments de l'itérateur pour le parcourir au sein d'une boucle *for*. Toutefois, un itérateur peut être parcouru une seule fois.

L'itérateur le plus connu : **range** ! Il permet de parcourir une séquences d'entiers en précisant le premier élément, le dernier et le pas d'incrémentation.

<ins>Exemple 1</ins> : Créer une liste d'entiers de 4 à 16 inclus avec seulement les chiffres pairs. Visualiser cette liste.

<script>
function myFunction1() {
    var x = document.getElementById("exemple1");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction1()">Voir résultat</button>

<div id="exemple1" hidden>
<div></div>

```python
pairs=range(4,17,2)
```

```python
for i in pairs :
    print(i, end=' ')
```
</div>

## Les générateurs

Un **générateur** permet de créer facilement un itérateur. Au sein d'une fonction, il suffit en apparence de remplacer le *return* par le terme *yield*. Seulement en apparence toutefois ! En effet, si un *return* renvoie une valeur ou un ensemble de valeurs et termine la fonction, un *yield* retourne la valeur et se met en pause jusqu'à l'appel suivant. Ainsi, à chaque appel d'un élément du générateur avec la fonction *next*, le code est exécuté jusqu'au prochain *yield*.

Comme les itérateurs, les générateurs consomment peu de ressources mémoire car une valeur est générée dès qu'elle est demandée au générateur (avec la fonction *next* par exemple) et elle sera retournée. Rien n'est stocké en mémoire.

Prenons un exemple (certes peu pertinent) qui crée un premier générateur en parcourant une chaîne de caratère

```python
def voyelle(chaine) :
    for i in chaine:
        if i.lower() in ['a','e','i','o','u','y']:
            yield i
```

```python
for i in voyelle("Je fais mon premier test d'itérateur pour comprendre comment cela marche au cours de la formation python"):
    print(i)
```


<ins>Exemple 2</ins> : Créer un générateur qui extraie les mots d'une chaîne de caractères. Supprimer les apostrophes et les points et passer en minuscule. Afficher le résultat du générateur pour observer le résultat.

<script>
function myFunction2() {
    var x = document.getElementById("exemple2");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction2()">Voir résultat</button>

<div id="exemple2" hidden>
<div></div>

```python
def decoupage_mot(chaine) :
    for i in chaine.split():
        if re.search("'", i):
            yield i.replace(".","").lower().split("'")[1]
        else:
            yield i.replace(".","").lower()
```

```python
mot=decoupage_mot("Je fais mon premier test d'itérateur pour comprendre comment cela marche au cours de la formation python.")
next(mot)
```

```python
for i in decoupage_mot("Je fais mon premier test d'itérateur pour comprendre comment cela marche au cours de la formation python."):
    print(i)
```
</div>


