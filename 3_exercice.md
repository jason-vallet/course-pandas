## Introduction 

Dans un fichier tiers exécutable en **Python**, saisissez vos commandes afin de résoudre les différentes question posées ci-après.

N'oubliez pas de mettre tout texte additionnel en commentaire (en utilisant le symbole `#`).

Ouvrez le fichier csv `./datasets/winemag-data-130k-v2.csv` en utilisant en spécificant l'index comme étant la colonne 0. Stockez la DataFrame dans la variable `info_vin`.

## 1.

Stockez dans la variable `prix_mediane` la valeur médiane du prix des vins proposés.

```
25.0
```

## 2.

Stockez dans la variable `liste_pays` la liste des pays existants dans le jeu de données (sans duplicat).

## 3.

Stockez dans la variable `compte_pays` la liste des pays existants et leur nombre d'occurence.

## 4.

Créez la variable `ecart_prix_median` contenant pour chaque ligne l'écart entre le prix courant et le prix médian.

## 5.

Je souhaite trouver le meilleur vin possible pour le prix le plus bas comment faire?

Stockez dans la variable `meilleur_vin` le titre du vin correspondant 

## 6.

Est-ce qu'un vin est plutôt fruité ou tropical? Créez une nouvelle Series nommée `compteur` indiquant le nombre de vin décrit par chacun de ces adjectifs.

```
tropical    3607
fruity      9090
dtype: int64
```

## 7.

Le système de notation utilisant des notes entre 80 et 100 est inhabituel aussi allons changé ces valeurs pour des notes équivalentes en étoiles:

* si la note est supérieure à 95, le vin reçoit 4 étoiles,
* si la note est comprise entre 90 et 95, le vin reçoit 3 étoiles,
* si la note est comprise entre 85 et 90, le vin reçoit 2 étoiles,
* si la note est inférieure à 85, le vin reçoit 1 étoiles.

Nous avons également reçu beaucoup d'argent de la part du Canada pour faire apparaître leurs vins sous un meilleur jour. Nous allons donc donner automatiquement une note d'au moins 3 étoiles à leurs vins.

Stockez la Series crée dans la variable `vin_canada`.


## Continuons

Nous pouvons passer à la [suite du cours](./4_grouping-and-sorting.md).
