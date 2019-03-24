---
title: "4 - Contrôler ses codes en termes de mémoire et de temps d'exécution"
date: 2019-03-18T15:26:15Z
draft: false
hidden: true
---

Afin de réaliser des codes efficaces, il peut être utile de mesurer le temps d'exécution d'une instruction ou d'évaluer l'occupation mémoire. Pour cela, vous pouvez recourir aux commandes magiques suivantes, notamment présentées dans le livre *Python Data Science Handbook* dont un résumé est disponible sous ce [lien](https://jakevdp.github.io/PythonDataScienceHandbook/01.07-timing-and-profiling.html) :

* *%timeit* pour évaluer le temps d'exécution d'une instruction
* *%prun* pour profiler un code, c'est-à-dire chronométrer le temps d'exécution de chaque ligne de code
* *%memit* pour mesurer l'occupation mémoire maximale nécessaire lors d'une instruction

Les commandes magiques permettent d'automatiser des tâches courantes et la liste de ces commandes peut d'ailleurs être affichée dans le *notebook* avec la commande *%lsmagic* ou en consultant la documentation de *IPython* via ce [lien](https://ipython.org/ipython-doc/dev/interactive/magics.html) ou ce [lien](https://ipython.readthedocs.io/en/stable/interactive/magics.html).

Au cours de ce chapitre, on s'appuiera sur la fonction suivante qui enregistre dans une liste (cet objet *python* sera présenté dans le chapitre ) le carré de x pour x entre 1 et N.

```python
def auCarre(N):
    liste=[]
    for i in range(N):
        liste.append(i**2)
    return liste
```

## Timer son code 

Pour chronométrer globalement une instruction, avec la fonction *%timeit*, on peut exécuter la commande suivante :

```python
%timeit auCarre(1000000)
```

Si on souhaite connaître le temps d'exécution de chaque commande de la fonction, on peut utiliser la commande *%prun* :

```python
%prun auCarre(1000000)
```

## L'occupation mémoire lors du lancement d'un script

Pour évaluer l'occupation mémoire globale de la fonction *auCarre*, on peut installer le package *memory_profiler* et utiliser la fonction *%memit* :

```python
!pip install memory_profiler
%load_ext memory_profiler
```

```python
%memit auCarre(1000000)
```

Si on souhaite connaître l'occupation mémoire ligne à ligne, on peut l'obtenir en utilisant la fonction *%mprun* en exécutant les commandes suivantes :

```python
%%file mprun_fonction.py
def auCarre(N):
    liste=[]
    for i in range(N):
        liste.append(i**2)
    return liste
```

```python
from mprun_fonction import auCarre
%mprun -f auCarre auCarre(1000000)
```


