## Accès aux données

Les objets de base dans Python peuvent permettre de facilement indexer les données, cependant pandas nous permet d'attendre un même résultat de manière plus simple.

Toujours en utilisant notre objet stocké dans la variable `df_vin`, nous pouvons faire appel à chacune des colonnes soit en les appelant comme des attributs:

```python
df_vin.country
```

```
0               Italy
1            Portugal
2                  US
3                  US
4                  US
             ...     
129966        Germany
129967             US
129968         France
129969         France
129970         France
Name: country, Length: 129971, dtype: object
```

Soit en les appelant à l'aide de l'opérateur `[]` comme des valeurs indexées:

```python
df_vin['country']
```

```
0            Italy
1         Portugal
2               US
3               US
4               US
            ...   
129966     Germany
129967          US
129968      France
129969      France
129970      France
Name: country, Length: 129971, dtype: object
```

Ces deux techniques pour accéder aux valeurs sont entièrement équivalentes, cependant, l'utilisation de l'opérateur `[]` nous permet de consulter les colones dont la valeur d'index contient un caractère espace. Une manière simple d'éviter ce genre de souci est d'utiliser le caractère `_` dans les valeurs d'indexes pour indiquer un espace.

```python
df_vin.taster_twitter_handle
```

```
0         @kerinokeefe
1           @vossroger
2          @paulgwine 
3                  NaN
4          @paulgwine 
              ...     
129966             NaN
129967     @paulgwine 
129968      @vossroger
129969      @vossroger
129970      @vossroger
Name: taster_twitter_handle, Length: 129971, dtype: object
```

Une fois que la Series souhaitée est isolée, l'accès à chacun des éléments se fait de nouveau à l'aide de l'interacteur `[]`, où l'index utilisé sera par défaut le numéro de ligne ou la valeur définie comme telle au moment de la création de la DataFrame.

```python
df_vin.taster_twitter_handle[1]
```

```
'@vossroger'
```

De manière assez logique, la méthode d'accès aux données est très similaire à celle que nous utiliserions si les donénes stockées était organisées à l'intérieur d'un dictionnaire contenant des tableaux (voir Lesson 1 pour rappel).


## L'indexation dans pandas

Nous avons pour l'instant vu les méthodes pour récupérer les valeurs à partir des colonnes mais nous pouvons aussi avoir besoin d'accéder aux données directement en fonction des lignes. À cette fin, nous pouvons utiliser les méthodes `.loc`, `.iloc`, `.at` and `.iat`.

Pour l'instant, nous n'utiliserons que les méthodes de localisation, vous pouvez consulter la [documentation](https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#indexing) pour plus d'information sur les autres méthodes d'accés.


### Sélection à partir de valeur d'index

La localisation des valeurs à partir d'`iloc` peut être réalisée de plusieurs manières. Sous sa forme la plus simple, la valeur d'index permet de sélectionner une ligne complète.

```python
df_vin.iloc[0]
```

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

Il est ensuite possible d'accéder directement aux champs grâce aux valeurs d'indexes ou en spécifiant directement le numéro de colonne à considérer.

```python
df_vin.iloc[0].country
df_vin.iloc[0, 0]
```

```
'Italy'
'Italy'
```

Cette manière d'accéder aux données utilise une approche permettant de spécifier la ligne en premier puis la colonne, ce qui est l'inverse des approches habituelles. Nous pouvons également utiliser les modificateurs à base de `:` pour sélectionner des ensembles de valeurs.

```python
df_vin.iloc[:3, 0]
```

```
0       Italy
1    Portugal
2          US
Name: country, dtype: object
```

Il est également possible de passer des tableaux de valeurs pour accéder aux champs spécifiquement voulus.

```python
df_vin.iloc[:3, [1, 4, 6]]
```

```
                                         description  price           region_1
0  Aromas include tropical fruit, broom, brimston...    NaN               Etna
1  This is ripe and fruity, a wine that is smooth...   15.0                NaN
2  Tart and snappy, the flavors of lime flesh and...   14.0  Willamette Valley
```

Et même de commencer directement par la fin du tableau au besoin.

```python
df_vin.iloc[-3:, [1, 4, 6]]
```

```
                                              description  price region_1
129968  Well-drained gravel soil gives this wine its c...   30.0   Alsace
129969  A dry style of Pinot Gris, this is crisp with ...   32.0   Alsace
129970  Big, rich and off-dry, this is powered by inte...   21.0   Alsace
```

### Sélection à partir de valeur de labels

Si l'on souhaite utiliser les labels spécifiés comme valeurs d'index, il faut utiliser la méthode `loc` au lieu d'`iloc`.

```python
df_vin.loc[0, 'country']
```

```
'Italy'
```

Comme précédemment, nous pouvons définir un ensemble de valeurs à partir de l'index des lignes (notez cependant la différence d'indexation de ligne!).

```python
df_vin.loc[:2, 'country']
```

```
0       Italy
1    Portugal
2          US
Name: country, dtype: object
```

Il est également possible d'utiliser des tableaux de labels pour identifier les champs à récupérer.

```python
df_vin.loc[:3, ['description', 'price', 'region_1']]
```

```
                                         description  price  \
0  Aromas include tropical fruit, broom, brimston...    NaN   
1  This is ripe and fruity, a wine that is smooth...   15.0   
2  Tart and snappy, the flavors of lime flesh and...   14.0   
3  Pineapple rind, lemon pith and orange blossom ...   13.0   

              region_1  
0                 Etna  
1                  NaN  
2    Willamette Valley  
3  Lake Michigan Shore  
```

### Choisir `loc` ou `iloc`

Les deux méthodes différencient de part leur approche. Là où `iloc` considère la DataFrame comme une simple matrice à deux dimensions, `loc` se base sur les labels pour récupérer les données. Au final, l'utilisation de l'un ou de l'autre est laissée à la préférence de l'utilisateur. Il est cependant certain que la préférence de l'un ou de l'autre pourra simplifier certains traitement lors d'opérations plus avancées.

La différence de comportement lors du comptage des lignes est également un point important à garder à l'esprit. Simplement, `loc` a un comportement inclusif alors qu'`iloc` suit le comportement habituel des indexes de python.


## Manipulation de l'index

Lors des accès aux valeurs, nous avons utilisé le numéro de ligne comme étant la valeur standard nous rattachant aux données. Il est possible de choisir une autre valeur d'index. Cette valeur devra cependant être unique.

```python
df_tmp = df_vin.set_index('title')
df_tmp.loc['Nicosia 2013 Vulkà Bianco  (Etna)']
```

```
country                                                              Italy
description              Aromas include tropical fruit, broom, brimston...
designation                                                   Vulkà Bianco
points                                                                  87
price                                                                  NaN
                                               ...                        
region_2                                                               NaN
taster_name                                                  Kerin O’Keefe
taster_twitter_handle                                         @kerinokeefe
variety                                                        White Blend
winery                                                             Nicosia
Name: Nicosia 2013 Vulkà Bianco  (Etna), Length: 12, dtype: object
```

## Sélection conditionnelle

Parmi tous les avantages de pandas, la possibilité de filtrer les informations d'un jeu de données rapidement est extrêmement importante pour dégrossir vos données. Ce filtrage prend la forme d'un demande conditionnelle.

Par exemple, recherchons l'ensemble des vins provenant d'Italie.

```python
>>> df_vin.country == 'Italy'
```

```
0          True
1         False
2         False
3         False
4         False
          ...  
129966    False
129967    False
129968    False
129969    False
129970    False
Name: country, Length: 129971, dtype: bool
```

Nous avons ici une Series contenant une liste de valeurs Booléenes (`True`/`False`) que nous pouvons mettre à profit pour isoler l'ensemble des vins nous intéressant.

```python
df_vin_italie = df_vin.loc[df_vin.country == 'Italy']
df_vin_italie.shape
```

```
(19540, 13)
```

Nous avons pu récupérer un sous ensemble de données, plus précisément 19 540 lignes sur les 130 000 initiales. Nous pouvons ajouter davantage de filtres pour récupérer par exemple seulement l'ensemble des vins ayant en moyenne une meilleur note que les autres; cette information est donnée dans la colonne `points`.

```python
df_vin_italie_meilleur = df_vin_italie.loc[(df_vin_italie.points >= df_vin_italie.points.mean())]
df_vin_italie_meilleur.shape
```

```
(8922, 13)
```

Il est possible d'enchaîner les filtres en utilisant le caractère `&` pour indiquer un lien logique `ET`, ainsi que le caractère `|` pour indiquer un lien logique `OU`.

```python
df_vin_filtre = df_vin.loc[(df_vin.country == 'Italy') | (df_vin.points >= df_vin_italie.points.mean())]
df_vin_filtre.shape
```

```
(71889, 13)
```

En cas de conditions multiple sur une même colonne, pandas nous permet d'utiliser plusieurs méthodes. Il est par exeple possible d'utiliser plusieurs filtres liés logiquement:

```python
df_vin_filtre = df_vin.loc[(df_vin.country == 'Italy') | (df_vin.country == 'France')]
df_vin_filtre.shape
```

```
(41633, 13)
```

Ou bie, nous pouvons utiliser certaines méthodes de sélections déjà intégrées à notre DataFrame, en l'occurence, il s'agit ici de la méthode `isin` permettant de spécifier une valeur parmi une liste de possibilités:

```python
df_vin_filtre = df_vin.loc[df_vin.country.isin(['Italy', 'France'])]
df_vin_filtre.shape
```

```
(41633, 13)
```

Certaines de ces méthodes peuvent être particulièrement utiles lorsque nous nous retrouvons face à des données incomplètes qui peuvent impacter nos calculs ou mesures. Nous pouvons utilsier les méthodes `isnull` et `notnull` pour identifier ou ignorer ces valeurs non déterminées.

```python
df_vin.loc[df_vin.price.isnull()].shape
df_vin.loc[df_vin.price.notnull()].shape
```

```
(8996, 13)
(120975, 13)
```

## Ajouter des données

Même si la DataFrame est déjà définie, il est toujours possible de compléter les informations stockées en son sein. Si le label n'existe pas, il est par exemple possible de créer une nouvelle colonne avec une valeur par défaut.

```python
df_vin['critics'] = 'everyone'
```

```
0         everyone
1         everyone
2         everyone
3         everyone
4         everyone
            ...   
129966    everyone
129967    everyone
129968    everyone
129969    everyone
129970    everyone
Name: critics, Length: 129971, dtype: object
```

Ce genre d'opération est également possible à l'aide de valeurs itérables, par exemple pour réaliser une indexation propre:


```python
df_vin_italie['index2'] = range(len(df_vin_italie))
df_vin_italie[['index2']]
```

```
        index2
0            0
6            1
13           2
22           3
24           4
...        ...
129929   19535
129943   19536
129947   19537
129961   19538
129962   19539

[19540 rows x 1 columns]
```


## À vous de jouer

C'est maintenant votre tour de vérifier vos acquis en réalisant les [exercices suivants](./2_exercice.md)

