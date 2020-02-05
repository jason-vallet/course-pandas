## Introduction 

Dans un fichier tiers exécutable en **Python**, saisissez vos commandes afin de résoudre les différentes question posées ci-après.

N'oubliez pas de mettre tout texte additionnel en commentaire (en utilisant le symbole `#`).

Ouvrez le fichier csv `./datasets/winemag-data-130k-v2.csv` en utilisant en spécificant l'index comme étant la colonne 0. Stockez la DataFrame dans la variable `info_vin`.

## 1.

Dans la variable `type_points`, stockez le type de la Series correspondant à l'ensemble des valeurs de `points`.

```
dtype('int64')
```

## 2.

Dans la variable `points_chaine`, stockez la Series de `points` convertie sous la forme d'un ensemble de chaînes de caractères.

```
0         87
1         87
2         87
3         87
4         87
          ..
129966    90
129967    90
129968    90
129969    90
129970    90
Name: points, Length: 129971, dtype: object
```

## 3.

Dans la variable `n_prix_manquant`, stockez le nombre de lignes ou les données ne contiennent pas de valeur valide pour la variable `price`.

```
8996
```

## 4.

La valeur dans le champ `region_2` est souvent manquante. Dans la variable `region_2_manquant`, créez une nouvelle Series qui contiendra la liste des valeurs contenues dans le champ `region_2` et dont les valeurs indéterminées auront été remplacées par la chaîne `Unknown`.

```
Unknown             79460
Central Coast       11065
Sonoma               9028
Columbia Valley      8103
Napa                 6814
                    ...  
Long Island           680
North Coast           584
Washington Other      534
South Coast           272
New York Other        231
Name: region_2, Length: 18, dtype: int64
```

## Continuons

Nous pouvons passer à la [suite du cours](./6_renaming-and-combining.md).
