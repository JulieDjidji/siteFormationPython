---
title: "Chapitre 4 : Les packages en python"
date: 2017-10-17T15:26:15Z
draft: false
weight: 50
---

## Installation avec le gestionnaire de packages PIP ou le gestionnaire de packages Conda

* Pip, qui signifie Pip Installs Packages, est le gestionnaire de paquets officiellement approuvé par Python. Il est généralement utilisé pour installer des paquets publiés sur PyPI (Python Package Index -repository of software for the Python programming language).

* Conda est un gestionnaire d’environnement multi-plateformes **indépendant du langage**

N'hésitez pas à lire cet [article](https://jakevdp.github.io/blog/2016/08/25/conda-myths-and-misconceptions/) si vous souhaitez quelques éléments supplémentaires sur *conda* !


## Comment télécharger un package ?

Pour télécharger un package :

```python
!pip install nomDuPackage
```

Pour importer le package pandas (l'ajout d'alias est optionnel) :

```python
import pandas as pd
```
Pour importer un module spécifique (par exemple, *pyplot*) d'un package (ici *matplotlib*)

```python
from matplotlib import pyplot
```

## Vue d'ensemble des principaux packages python

![Panorama des principaux packages python](/images/packagesPython.jpeg "packagesPython")

