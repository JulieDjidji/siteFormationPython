---
title: "Le premier objet python : les listes"
date: 2017-10-17T15:26:15Z
draft: false
hidden: true
weight: 20
---

## Création et manipulation d'une liste

| Action | Fonction python |
|:---------------|------------------------:|
| Creation d'une liste | [] ou *list()* |
| Test de la présence d'un élément dans une liste | *x in liste* |
| Accès à un élément | *liste[i]* |
| Accès à plusieurs éléments | *liste[i:j]* |
| Minimum de la liste | *min(liste)* |
| Maximum de la liste | *max(liste)* |
| Nombre d'éléments d'une liste | *len(liste)* |
| Nombre d’occurrence de l'élément x dans la liste | *liste.count(x)* |

## Insertion et suppression d'éléments d'une liste


| Action | Fonction python |
|:---------------|------------------------:|
| Ajouter un élément v à la fin de la liste | liste.append(v) |
| Ajouter une liste sl à la fin de la liste | liste.extend(sl) |
| Insérer un élément v à l'indice i | liste.insert(i,v) |
| Remplacer l'élément i par une valeur v | *liste[i]=v* |
| Remplacer les éléments d'indices i à j par une sous liste sl | *liste[i:j]=sl* |
| Supprimer le premier élément égal à v | *liste.remove(v)* |
| Supprimer l'élément d'indice i | *liste.pop(i)* |
| Supprimer tous les éléments | *liste.clear()* ou *liste *= 0* ou *liste=[]* |


<ins>**Exercice**</ins> : 





## Les compréhensions de liste

**<ins>Principe</ins> : construire une liste en parcourant tout autre itérable (liste, tuple, chaîne de caractères, ...)**

* la valeur ajoutée à la liste peut résulter d'un calcul (avec ou sans utiliser la valeur de l'élément de l'itérable parcouru)
* une condition optionnelle (if) peut filtrer les éléments de l'itérable parcouru
* une condition (if else) peut permettre d'affecter une valeur différente selon la valeur de l'itérable parcouru

**Pourquoi privilégier les compréhensions de liste ?**

* Code plus synthétique
* Rapidité : allocation de la mémoire avant l'ajout des éléments (plutôt qu'un redimensionnement au fil de l'exécution comme avec la fonction *append*)

<ins>**Exercice**</ins> : A partir d'une list comprehension, ré-écrire la boucle for permettant de calculer le carré des éléments compris entre 1 et 5 et stocker le résultat dans une liste.
