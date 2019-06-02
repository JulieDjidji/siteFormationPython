---
title: "2 - Les conditions if - elif - else"
date: 2019-03-18T15:26:15Z
draft: false
hidden: true
---

Comme dans les autres langages de programmation, des conditions peuvent être effectuées en python en utilisant *if-elif-else*. Les instructions *elif* et *else* sont évidemment facultatives. Comme pour les fonctions, chaque ligne associée à une condition se termine par un deux-points. La notation habituelle de ces conditions est :


```python
if condition1: 
    Bloc d'instruction
elif condition2:
    Bloc d'instruction
else :
    Bloc d'instruction
```

Une condition correspond à un *booléen*. La condition *x==2* vaut *True* et est donc respectée seulement si x est effectivement égal à 2 sinon elle vaut *False* et le bloc d'instruction associée à cette condition n'est pas exécuté.
Il est possible de directement indiquer un booléen dans l'instruction.

<ins>**Petit exemple**</ins>: afficher (avec la fonction print()) la valeur 1 si notre paramètre est inférieur à 10, 2 s'il est compris entre 10 et 20 et 3 sinon.

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

```python
parametre=2
if parametre < 10:
      print(1)
elif 10<=parametre\<20:
    print(2)
else:
    print(3)
```

</div>



Les conditions peuvent être utilisées dans les fonctions. Par exemple, à partir de la fonction précédente, on peut afficher le résultat seulement si la valeur de l'*input* est strictement supérieur à 10. Pour cela, on écrit le code suivant :


```python
def auCarre(x):
    if x>10:
        print(x**2)
    else:
        print("Ce calcul est trop simple, révisez vos tables de multiplication !")
```

<ins>**Autre exemple**</ins>: écrire une fonction qui mutliplie par 1729 seulement si l'*input* est pair et sinon afficher un message d'erreur


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
def fonctionInutile(x):
    if x%2==0:
        print(x*1729)
    else:
        print("L'input est impair")
```

</div>
