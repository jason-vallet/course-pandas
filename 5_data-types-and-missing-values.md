
## Dtypes

Comme nous avons pu en discuter auparavant, pandas nous permet de manipuler des objets de types DataFrame et Series. Comme pour tous les objets python, nous pouvons utiliser la fonction `type` pour récupérer cette information simplement.

```python
type(df_vin)
```

```
<class 'pandas.core.frame.DataFrame'>
```

Cependant, pandas est également capable d'inférer le type d'élément stockés dans chacune des colones d'une DataFrame. Cette information va nous être particulièrement utilie lorsque nous devrons réaliser des opérations de traitement automatique dépendant du type de valeur contenues dans nos variables. Nous utilisons dans ce cas l'attribut `dtypes` sur les DataFrame.

```python
df_vin.dtypes
```

```
country                   object
description               object
designation               object
points                     int64
price                    float64
                          ...   
taster_name               object
taster_twitter_handle     object
title                     object
variety                   object
winery                    object
Length: 13, dtype: object
```

Cette attribut existe aussi pour les Series, ainsi qu'un alias `dtype`.

```python
df_vin.price.dtype
df_vin.price.dtypes
```

```
dtype('float64')
dtype('float64')
```

Le type utilisé nous indique la manière dont les données sont stockées. En l'occurrence, `int64` (ou `float64`) implique que les valeurs sont des entiers (ou des flottants) stockés sur 64 bits.

Nous pouvons remarquer que les valeurs stockant des chaînes de caractères sont déclarées comme des objets et non comme des `str`.

```python
type('azerty')
df_vin.title.dtypes
```

```
<class 'str'>
dtype('O')
```

Lors des opérations d'appel, il est possible de convertir les données considérées avec la méthode `astype` afin de permettre certaines opérations directement.

```python
df_vin.points.astype('float64')
```

```
0         87.0
1         87.0
2         87.0
3         87.0
4         87.0
          ... 
129966    90.0
129967    90.0
129968    90.0
129969    90.0
129970    90.0
Name: points, Length: 129971, dtype: float64
```

Les indexes utilisés ont également un type défini.

```python
df_vin.index.dtype
```

```
dtype('int64')
```

## Données manquantes

Comme entrevu plus tôt, les valeurs des jeux de données ne sont pas toujours complète: certaines peuvent manquer et d'autres peuvent devoir être invalidées (ex: cas statistiques extrêmes). Pour indiquer ces valeurs, python et pandas utilisent la valeur `NaN` (Not a Number).

Si lors de nos analyses nous souhaitons ignorer ces valeurs incomplètes nous devons faire appel à la fonction `notnull`.

```python
df_vin[pandas.notnull(df_vin.country)].shape
```

```
(129908, 13)
```

Ces conditions peuvent être enchaînées pour s'assurer que les données récupérées sont entières et complètes.

```python
df_vin[pandas.notnull(df_vin.country) & pandas.notnull(df_vin.region_2)].shape
```

```
(50511, 13)
```

La fonction `isnull` va nous permettre au contraire de ne récupérer que les lignes contenant des données manquantes. 

```python
df_vin[pandas.isnull(df_vin.country)]
```

```
       country                                        description  \
913        NaN  Amber in color, this wine has aromas of peach ...   
3131       NaN  Soft, fruity and juicy, this is a pleasant, si...   
4243       NaN  Violet-red in color, this semisweet wine has a...   
9509       NaN  This mouthwatering blend starts with a nose of...   
9750       NaN  This orange-style wine has a cloudy yellow-gol...   
...        ...                                                ...   
124176     NaN  This Swiss red blend is composed of four varie...   
129407     NaN  Dry spicy aromas of dusty plum and tomato add ...   
129408     NaN  El Capricho is one of Uruguay's more consisten...   
129590     NaN  A blend of 60% Syrah, 30% Cabernet Sauvignon a...   
129900     NaN  This wine offers a delightful bouquet of black...   

                           designation  points  price province region_1  \
913                     Asureti Valley      87   30.0      NaN      NaN   
3131                          Partager      83    NaN      NaN      NaN   
4243          Red Naturally Semi-Sweet      88   18.0      NaN      NaN   
9509    Theopetra Malagouzia-Assyrtiko      92   28.0      NaN      NaN   
9750         Orange Nikolaevo Vineyard      89   28.0      NaN      NaN   
...                                ...     ...    ...      ...      ...   
124176                    Les Romaines      90   30.0      NaN      NaN   
129407                         Reserve      89   22.0      NaN      NaN   
129408                         Reserve      89   22.0      NaN      NaN   
129590                            Shah      90   30.0      NaN      NaN   
129900                             NaN      91   32.0      NaN      NaN   

       region_2        taster_name taster_twitter_handle  \
913         NaN      Mike DeSimone        @worldwineguys   
3131        NaN         Roger Voss            @vossroger   
4243        NaN      Mike DeSimone        @worldwineguys   
9509        NaN    Susan Kostrzewa         @suskostrzewa   
9750        NaN       Jeff Jenssen        @worldwineguys   
...         ...                ...                   ...   
124176      NaN       Jeff Jenssen        @worldwineguys   
129407      NaN  Michael Schachner           @wineschach   
129408      NaN  Michael Schachner           @wineschach   
129590      NaN      Mike DeSimone        @worldwineguys   
129900      NaN      Mike DeSimone        @worldwineguys   

                                                    title             variety  \
913        Gotsa Family Wines 2014 Asureti Valley Chinuri             Chinuri   
3131                    Barton & Guestier NV Partager Red           Red Blend   
4243    Kakhetia Traditional Winemaking 2012 Red Natur...            Ojaleshi   
9509    Tsililis 2015 Theopetra Malagouzia-Assyrtiko W...         White Blend   
9750    Ross-idi 2015 Orange Nikolaevo Vineyard Chardo...          Chardonnay   
...                                                   ...                 ...   
124176            Les Frères Dutruy 2014 Les Romaines Red           Red Blend   
129407        El Capricho 2015 Reserve Cabernet Sauvignon  Cabernet Sauvignon   
129408               El Capricho 2015 Reserve Tempranillo         Tempranillo   
129590                            Büyülübağ 2012 Shah Red           Red Blend   
129900                                 Psagot 2014 Merlot              Merlot   

                                 winery  
913                  Gotsa Family Wines  
3131                  Barton & Guestier  
4243    Kakhetia Traditional Winemaking  
9509                           Tsililis  
9750                           Ross-idi  
...                                 ...  
124176                Les Frères Dutruy  
129407                      El Capricho  
129408                      El Capricho  
129590                        Büyülübağ  
129900                           Psagot  

[63 rows x 13 columns]
```

Ce filtrage va nous permettre de compléter les données manquantes pour éviter tout problème futur; ce genre d'opérations peut être réalisé simplement avec la méthode `fillna`.


```python
df_vin.region_1.fillna('Unknown')
```

```
0                        Etna
1                     Unknown
2           Willamette Valley
3         Lake Michigan Shore
4           Willamette Valley
                 ...         
129966                Unknown
129967                 Oregon
129968                 Alsace
129969                 Alsace
129970                 Alsace
Name: region_1, Length: 129971, dtype: object
```

Notez qu'il est aussi possible d'utiliser des méthodes de remplissage se basant sur les valeurs se situant avant ou après la valeur manquante (appelée `backfill` ou `forwardfill`).

```python
df_vin.region_1.fillna(method='bfill').value_counts().sort_index()
```

```
Abruzzo                  9
Adelaida District      125
Adelaide                18
Adelaide Hills         139
Adelaide Plains          5
                      ... 
Yolo County             62
York Mountain           12
Yorkville Highlands     99
Yountville             109
Zonda Valley             5
Name: region_1, Length: 1229, dtype: int64
```

Évidemment, le remplissage résultant de ces opérations peut drastiquement changer les distributions de valeurs rencontrées. Il convient donc de faire preuve de circonspection quand aux opérations qu'il convient de réaliser sur les données.

```python
df_vin.region_1.fillna(method='ffill').value_counts().sort_index()
```

```
Abruzzo                  6
Adelaida District      120
Adelaide                22
Adelaide Hills         126
Adelaide Plains          4
                      ... 
Yolo County             66
York Mountain            9
Yorkville Highlands    110
Yountville             107
Zonda Valley             3
Name: region_1, Length: 1229, dtype: int64
```

Il est également possible, si vous le souhaitez, de remplacer des valeurs définies grâce à la méthode `replace`.

```python
df_vin.taster_twitter_handle.replace("@vossroger", "@voss")
```

```
0         @kerinokeefe
1                @voss
2          @paulgwine 
3                  NaN
4          @paulgwine 
              ...     
129966             NaN
129967     @paulgwine 
129968           @voss
129969           @voss
129970           @voss
Name: taster_twitter_handle, Length: 129971, dtype: object
```

Notez que vous ne pouvez pas directement remplacer des valeurs `NaN` avec la méthode `replace`. Il est possible cependant de changer des valeurs précédemment indéfinies et qui sont maintenant identifiées par des valeurs de remplissage.

```python
df_vin.region_1.fillna('Unknown').replace('Unknown', 'Inconnu')
```

```
0                        Etna
1                     Inconnu
2           Willamette Valley
3         Lake Michigan Shore
4           Willamette Valley
                 ...         
129966                Inconnu
129967                 Oregon
129968                 Alsace
129969                 Alsace
129970                 Alsace
Name: region_1, Length: 129971, dtype: object
```


## À vous de jouer

C'est maintenant votre tour de vérifier vos acquis en réalisant les [exercices suivants](./5_exercice.md)

