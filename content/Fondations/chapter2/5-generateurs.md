---
title: "Les itérateurs et les générateurs"
date: 2019-03-18T15:26:15Z
draft: false
hidden: true
weight: 50
---

On utilise régulièrement des itérables, c'est-à-dire des séquences que nous parcourons telles que des listes ou des dictionnaires, pour effectuer itérativement des actions à l'aide d'une boucle *for*. Or, le contenu de ces itérables, qui peut pourtant occuper une place importante en mémoire, n'est utile que ponctuellement pour l'action à effectuer lors de l'itération associée à sa valeur. Avant et après l'itération i, la valeur de l'itérable associée à cette itération i ne sert à rien. Tout l'intérêt de l'itérateur est là : il permet *grosso modo* de ne connaître cette valeur qu'au moment de l'itération i !

## Les itérateurs

Les listes, les dictionnaires, les ensembles ou même les chaînes de caractères sont des itérables. On peut en effet itérer selon ces séquences. Un **itérateur** est un curseur permettant de se déplacer d'élément en élément au sein de l'itérable.

Son principal avantage est son faible coût en termes de mémoire. Celui-ci peut par exemple se mesurer dans une faible mesure avec les instructions suivantes :

```python
import sys
n=10000
element=list(range(n))
print(sys.getsizeof(element))
print(sys.getsizeof(iter(element)))
```

Evidemment, plus l'itérable est long/gros, plus les différences de mémoire occupées sont importantes. En revanche, malgré l'augmentation du nombre d'éléments dans l'itérateur, comme ces éléments ne sont pas en mémoire, l'itérateur ne nécessite pas de ressources supplémentaires. Afin d'illustrer ce propos, vous pouvez faire varier n dans le code ci-dessus. Cette différence s'explique par le fait que les éléments de l'itérateur ne sont **pas stockés en mémoire**.

En pratique, quand on réalise une boucle sur la liste *[1,2,3,4,5]*, avant d'exécuter par itération les instructions présentes au sein de la boucle, python commence par transformer cette liste en itérateur avec la commande suivante :

```python
iterateur = iter([1,2,3,4,5])
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
    if (x.style.display !== "block") {
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

Prenons un exemple (certes peu pertinent) qui crée un premier générateur en parcourant une chaîne de caratères :

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
    if (x.style.display !== "block") {
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


