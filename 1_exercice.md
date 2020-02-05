## Introduction 

Dans un fichier tiers exécutable en **Python**, saisissez vos commandes afin de résoudre les différentes question posées ci-après.

N'oubliez pas de mettre tout texte additionnel en commentaire (en utilisant le symbole `#`).

## 1.

Créez une DataFrame dans la variable `fruits` contenant les données suivantes:

```
   Bananes  Pommes
0       21      30
```

## 2.

Même question que précédemment mais résultant en l'objet suivant stocké dans la variable `fruits_vente`:

```
            Bananes  Pommes
Vente 2017       21      35
Vente 2018       34      41
```

## 3.

Construisez un objet Series stocké dans la variable `ingredients` tel que suit:

```
Farine     400g
Lait      100mL
Oeufs         2
Jambon     100g
Name: Recette Quiche, dtype: object
```

## 4.

Importez le fichier `winemag-data-130k-v2.csv` dans la DataFrame nommée `info_vin`. Vous utiliserez les options nécessaires pour réaliser cette opération telle que:

* vous ne lirez que les 50 premières lignes,
* vous n'importerez que les colonnes `'description', 'designation', 'title', 'variety', 'winery'`
* vous utiliserez la première colonne comme index de ligne

Note:

Les commandes suivantes

```python
info_vin.shape
info_vin.keys()
```

Doivent vous retourner les résultats suivants

```
(50, 5)
Index(['description', 'designation', 'title', 'variety', 'winery'], dtype='object')
```

## 5.

Sauvegardez le fichier ainsi créé sous le nom `1_exercice_info_vin.csv`


## Continuons

Nous pouvons passer à la [suite du cours](./2_indexing-selecting-assigning.md).
