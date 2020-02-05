## Introduction 

Dans un fichier tiers exécutable en **Python**, saisissez vos commandes afin de résoudre les différentes question posées ci-après.

N'oubliez pas de mettre tout texte additionnel en commentaire (en utilisant le symbole `#`).

## 1.

Ouvrez le fichier csv `./datasets/winemag-data-130k-v2.csv` en utilisant en spécificant l'index comme étant la colonne 0. Stockez la DataFrame dans la variable `info_vin`.

## 2.

Stockez le contenu de la colonne `description` dans la variable `desc`.

```
0         Aromas include tropical fruit, broom, brimston...
1         This is ripe and fruity, a wine that is smooth...
2         Tart and snappy, the flavors of lime flesh and...
3         Pineapple rind, lemon pith and orange blossom ...
4         Much like the regular bottling from 2012, this...
                                ...                        
129966    Notes of honeysuckle and cantaloupe sweeten th...
129967    Citation is given as much as a decade of bottl...
129968    Well-drained gravel soil gives this wine its c...
129969    A dry style of Pinot Gris, this is crisp with ...
129970    Big, rich and off-dry, this is powered by inte...
Name: description, Length: 129971, dtype: object
```

## 3.

En utilisant la méthode `iloc`, stockez la première ligne de la DataFrame `info_vin` dans la variable `ligne`.

```
country                                                              Italy
description              Aromas include tropical fruit, broom, brimston...
designation                                                   Vulkà Bianco
points                                                                  87
price                                                                  NaN
                                               ...                        
taster_name                                                  Kerin O’Keefe
taster_twitter_handle                                         @kerinokeefe
title                                    Nicosia 2013 Vulkà Bianco  (Etna)
variety                                                        White Blend
winery                                                             Nicosia
Name: 0, Length: 13, dtype: object
```

## 4.

En utilisant la méthode `loc`, sélectionnez les 10 premières valeurs de la colonne `province` et stockez les dans la variable `prov`.

```
0    Sicily & Sardinia
1                Douro
2               Oregon
3             Michigan
4               Oregon
5       Northern Spain
6    Sicily & Sardinia
7               Alsace
8          Rheinhessen
9               Alsace
Name: province, dtype: object
```

## 5.

Stockez dans la variable `exemple` les lignes de la DataFrame correspondant aux indexes `1`, `2`, `3`, `5` et `8`.

```
    country                                        description  \
1  Portugal  This is ripe and fruity, a wine that is smooth...   
2        US  Tart and snappy, the flavors of lime flesh and...   
3        US  Pineapple rind, lemon pith and orange blossom ...   
5     Spain  Blackberry and raspberry aromas show a typical...   
8   Germany  Savory dried thyme notes accent sunnier flavor...   

            designation  points  price        province             region_1  \
1              Avidagos      87   15.0           Douro                  NaN   
2                   NaN      87   14.0          Oregon    Willamette Valley   
3  Reserve Late Harvest      87   13.0        Michigan  Lake Michigan Shore   
5          Ars In Vitro      87   15.0  Northern Spain              Navarra   
8                 Shine      87   12.0     Rheinhessen                  NaN   

            region_2         taster_name taster_twitter_handle  \
1                NaN          Roger Voss            @vossroger   
2  Willamette Valley        Paul Gregutt           @paulgwine    
3                NaN  Alexander Peartree                   NaN   
5                NaN   Michael Schachner           @wineschach   
8                NaN  Anna Lee C. Iijima                   NaN   

                                               title             variety  \
1      Quinta dos Avidagos 2011 Avidagos Red (Douro)      Portuguese Red   
2      Rainstorm 2013 Pinot Gris (Willamette Valley)          Pinot Gris   
3  St. Julian 2013 Reserve Late Harvest Riesling ...            Riesling   
5  Tandem 2011 Ars In Vitro Tempranillo-Merlot (N...  Tempranillo-Merlot   
8  Heinz Eifel 2013 Shine Gewürztraminer (Rheinhe...      Gewürztraminer   

                winery  
1  Quinta dos Avidagos  
2            Rainstorm  
3           St. Julian  
5               Tandem  
8          Heinz Eifel
```

## 6.

Sélectionnez un sous-ensemble des données tel que ci-après et stockez le dans la variable `sous_ensemble`.

```
      country           province      region_1      region_2
0       Italy  Sicily & Sardinia          Etna           NaN
1    Portugal              Douro           NaN           NaN
10         US         California   Napa Valley          Napa
100        US           New York  Finger Lakes  Finger Lakes
```

## 7.

Stockez dans la variable `variete` le sous-ensemble des données contenant les deux colonnes indiquées ci-après sur les 100 premières lignes.

```
     country                   variety
0      Italy               White Blend
1   Portugal            Portuguese Red
2         US                Pinot Gris
3         US                  Riesling
4         US                Pinot Noir
..       ...                       ...
95    France                     Gamay
96    France                     Gamay
97        US                  Riesling
98     Italy                Sangiovese
99        US  Bordeaux-style Red Blend

[100 rows x 2 columns]
```

## 8.

Stockez dans la variable `vin_hongrois` la liste des vins prevenant de Hongrie et coutant moins de 20€.

## 9.

Stockez dans la variable `vin_oceanie_top` la liste des vins provenant d'Océanie (Australie et Nouvelle Zélande) et ayant une note au moins égale à 95.

## Continuons

Nous pouvons passer à la [suite du cours](./3_summary-functions-and-maps.md).
