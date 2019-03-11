---
title: "Chapitre 4 : Les packages en python"
draft: false
weight: 50
---

## Qu'est ce qu'un package ?

Commençons simplement ! Déjà, un **module** est simplement un fichier contenant un ensemble de fonctions python et de variables globales. L'intérêt d'un tel fichier ? En pratique, si des fonctions sont créées dans un *notebook* (ou quelconques éditeurs), celles-ci sont perdues dès la fermeture de celui-ci. Cette encapsulation dans un fichier facilite la programation et notamment le travail collaboratif.

Pour charger les fonctions du fichier *premierModule.py*, il suffit d'exécuter au sein d'un *notebook* (ou dans un éditeur intégré à un IDE tel que Spyder) la commande suivante :

```python
import premierModule
```

Toutefois, le recours à la fonction *premiereFonction* de ce module nécessite de référencer le nom du module selon cette commande : *premierModule.premiereFonction*. Pour charger directement les fonctions, la commande suivante peut être exécutée :

```python
from premierFodule import *
```

Un **package** désigne alors la réunion, au sein d'un même répertoire, de modules chargeables directement avec une seule instruction. Au sein du dossier relatif à un *package*, un fichier d'initialement, obligatoirement nommée *__init__.py*, doit être créé. 

## Installation avec le gestionnaire de packages PIP ou le gestionnaire de packages Conda

* Pip, qui signifie Pip Installs Packages, est le gestionnaire de paquets officiellement approuvé par Python. Il est généralement utilisé pour installer des paquets publiés sur PyPI (Python Package Index -repository of software for the Python programming language).

* Conda est un gestionnaire d’environnement multi-plateformes **indépendant du langage**

N'hésitez pas à lire cet [article](https://jakevdp.github.io/blog/2016/08/25/conda-myths-and-misconceptions/) si vous souhaitez quelques éléments supplémentaires sur *conda* !


## Comment télécharger un package ?

Pour télécharger un package, tapez dans un *jupyter notebook* :

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

