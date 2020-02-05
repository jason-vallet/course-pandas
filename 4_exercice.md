## Introduction 

Dans un fichier tiers exécutable en **Python**, saisissez vos commandes afin de résoudre les différentes question posées ci-après.

N'oubliez pas de mettre tout texte additionnel en commentaire (en utilisant le symbole `#`).

Ouvrez le fichier csv `./datasets/winemag-data-130k-v2.csv` en utilisant en spécificant l'index comme étant la colonne 0. Stockez la DataFrame dans la variable `info_vin`.

## 1.

Dans la variable `testeurs`, stockez la liste des différents testeurs de vin en fonction de leur identifiant twitter et comptez le nombre d'avis qu'ils ont soumis. La liste doit être ordonné de manière décroissante en fonction du nombre d'avis (soit en commençant par le testeur le plus prolifique).

```
taster_twitter_handle
@vossroger         25514
@wineschach        15134
@kerinokeefe       10776
@vboone             9537
@paulgwine          9532
                   ...  
@laurbuzz           1835
@suskostrzewa       1085
@worldwineguys      1005
@bkfiona              27
@winewchristina        6
Name: title, Length: 15, dtype: int64
```

## 2.

On cherche à identifer le meilleur vin pour un prix donné. Dans la variable `points_prix`, stockez une Series contenant, pour chaque prix possible, la meilleure note existante. Ordonnez ces valeurs de manière croissante selon le prix proposé.

```
price
4.0       86
5.0       87
6.0       88
7.0       91
8.0       91
          ..
1900.0    98
2000.0    97
2013.0    91
2500.0    96
3300.0    88
Name: points, Length: 390, dtype: int64
```

## 3.

Pour chaque variété de vin existant, calculez les prix minimum et maximum possible. Stockez la DataFrame ainsi créée dans la variable `prix_varietes`.

```
              min    max
variety                 
Abouriou     15.0   75.0
Agiorgitiko  10.0   66.0
Aglianico     6.0  180.0
Aidani       27.0   27.0
Airen         8.0   10.0
...           ...    ...
Zinfandel     5.0  100.0
Zlahtina     13.0   16.0
Zweigelt      9.0   70.0
Çalkarası    19.0   19.0
Žilavka      15.0   15.0

[707 rows x 2 columns]
```

## 4.

Copiez dans une nouvelle variable `prix_varietes_tries` le résultat de la question précédente en ordonnant les données de telle manière que le prix minimum soit indiqué de manière décroissante. Réalisez la même modification avec le prix maximum pour différencier les cas où les valeurs minimum sont égales.

```
                                  min    max
variety                                     
Ramisco                         495.0  495.0
Terrantez                       236.0  236.0
Francisa                        160.0  160.0
Rosenmuskateller                150.0  150.0
Tinta Negra Mole                112.0  112.0
...                               ...    ...
Roscetto                          NaN    NaN
Sauvignon Blanc-Sauvignon Gris    NaN    NaN
Tempranillo-Malbec                NaN    NaN
Vital                             NaN    NaN
Zelen                             NaN    NaN

[707 rows x 2 columns]
```

## 5.

Stockez dans la variable `testeur_note_moy` la valeur moyenne des notes attribuées pour chaque testeur.

```
taster_name
Alexander Peartree    85.855422
Anna Lee C. Iijima    88.415629
Anne Krebiehl MW      90.562551
Carrie Dykes          86.395683
Christina Pickard     87.833333
                        ...    
Paul Gregutt          89.082564
Roger Voss            88.708003
Sean P. Sullivan      88.755739
Susan Kostrzewa       86.609217
Virginie Boone        89.213379
Name: points, Length: 19, dtype: float64
```

## 6.

Dans la variable `compte_pays_varietes`, stockez pour chaque pays et varieté, le nombre d'occurence dans les données. Triez les valeurs obtenues en ordre décroissant.

```
country    variety                 
US         Pinot Noir                  9885
           Cabernet Sauvignon          7315
           Chardonnay                  6801
France     Bordeaux-style Red Blend    4725
Italy      Red Blend                   3624
                                       ... 
Uruguay    Tempranillo-Tannat             1
Italy      Pignolo                        1
           Muscat                         1
           Moscato di Noto                1
Argentina  Barbera                        1
Length: 1612, dtype: int64
```

## 7.

Suite à la question 2., nous souhaiterions directement connaître le titre du vin considéré comme ayant la meilleure valeur.
Stockez le résultat dans la variable `titre_prix`.

```
price
4.0                           Bandit NV Merlot (California)
5.0       In Situ 2008 Reserva Sauvignon Blanc (Aconcagu...
6.0        Ste. Chapelle 2001 Johannisberg Riesling (Idaho)
7.0       Herdade dos Machados 2012 Toutalga Red (Alente...
8.0       Snoqualmie 2006 Winemaker's Select Riesling (C...
                                ...                        
1900.0                        Château Margaux 2009  Margaux
2000.0                         Château Pétrus 2011  Pomerol
2013.0    Blair 2013 Roger Rose Vineyard Chardonnay (Arr...
2500.0                         Château Pétrus 2014  Pomerol
3300.0                 Château les Ormes Sorbet 2013  Médoc
Length: 390, dtype: object
```

## Continuons

Nous pouvons passer à la [suite du cours](./5_data-types-and-missing-values.md).
