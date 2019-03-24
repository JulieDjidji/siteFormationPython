---
title: "3 - Les boucles"
date: 2019-03-18T15:26:15Z
draft: false
hidden: true
---

## Boucle for

Difficile d'aborder les boucles sans évoquer a minima les listes. Pas de panique, on reviendra plus loin sur la manipulation des listes. Prenons pour l'instant une liste [0,1,2,3,4,5]. Ecrivons une première boucle *for* qui à chaque valeur de la liste, affiche son carré.


```python
for n in [0,1,2,3,4,5]:
    print(n**2, ' ', end='')
```

<ins>**Exemple**</ins>: écrire une boucle qui pour les valeurs de 0 à 10 affiche un message qui indique si la valeur est paire ou impaire. Au sein d'un *print*, plusieurs chaînes peuvent être concaténées simplement en écrivant *print(chaine1, chaine2)*.


<script>
function myFunction() {
    var x = document.getElementById("exemple");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction()">Voir résultat</button>

<div id="exemple" hidden>
<div></div>

<ins>Astuce</ins> : On le verra avec la section sur les générateurs mais pour créer une liste entre 0 et 10, on peut simplement utiliser range(11).

```python
for i in range(11):
    if i%2==0:
        print(i, " est pair")
    else:
        print(i, " est impair")
```

</div>


Si les boucles *for* s'effectuent essentiellement sur les listes, il reste néanmoins possible d'itérer sur une chaîne de caractères. Le code suivant parcourt la chaîne 'je code en python' et chaque espace est remplacé par "_".


```python
for car in 'je code en python':
    if car not in ' ':
        print(car,  end='')
    else:
        print('_',  end='')
```

    je_code_en_python

## Boucle while

La boucle *while* qui permet d'exécuter un code tant qu'une condition est satisfaite. L'exemple précédent qui consiste à afficher le carré de l'*input* pour ce dernier compris dans la liste [0,1,2,3,4,5] peut s'écrire :


```python
n=0 # Commencer par initialiser la valeur de n
while n<6:
    print(n**2, ' ', end='')
    n+=1
```

## Instructions **continue** et **break**

Dans les boucles *for* et *while*, deux instructions peuvent être très utiles :

* l'instruction **continue** passe à l'itération suivante de la boucle en cours, les autres instructions du bloc sont négligées.
* l'instruction **break** stoppe complètement la boucle courante en cours


```python
# Pour afficher le carré de l'input si ce dernier est pair (n%2=0)
for n in [0,1,2,3,4,5]:
    if n%2==1:
        continue
    print(n**2, ' ', end='')
```

```python
# Pour afficher le carré de l'input tant que ce dernier n'est pas impair (n%2=1)
for n in [0,1,2,3,4,5]:
    if n%2==1:
        break
    print(n**2, ' ', end='')
```

<ins>**Exemple**</ins> : écrire une boucle qui pour les valeurs de 5 à 15 calcule la valeur du carré seulement si l'input est strictement supérieur à 10

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
for i in range(5,16):
    if i>10:
        print('Carré de ', i, ' : ', i**2)
```
</div>


## Fonctions *enumerate* et *zip*

On souhaite parfois itérer sur un indice plutôt que sur le contenu de l'itérable (liste, chaîne de caractères ...). On peut envisager d'utiliser la fonction *range* entre 0 et le nombre d'éléments de l'itérable mais cette méthode est peu efficace. La fonction *enumerate* permet d'itérer simultanément sur l'indice et la valeur.

<ins>**Exemple**</ins> : Reprenez l'exemple de la boucle sur la chaîne de caractères 'je code en python', afficher à chaque itération l'indice et la valeur du caractère

<script>
function myFunction3() {
    var x = document.getElementById("exemple3");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction3()">Voir résultat</button>

<div id="exemple3" hidden>
<div></div>

```python
for i in enumerate('je code en python'):
    print(i)
```
</div>

On peut aussi souhaiter itérer sur deux listes en parallèle. La fonction *zip* s'avère dans ce cas particulièrement utile.

<ins>**Exemple**</ins> : Créer deux listes de longueur identique, itérer simulatanément ces deux listes et afficher à chaque itération le couple de valeurs

<script>
function myFunction4() {
    var x = document.getElementById("exemple4");
    if (x.style.display === "none") {
        x.style.display = "block";
    } else {
        x.style.display = "none";
    }
}
</script>
 
<button onclick="myFunction4()">Voir résultat</button>

<div id="exemple4" hidden>
<div></div>

```python
for i, j in zip(range(5), range(5,10)):
    print((i,j))
```
</div> 

