## Les fonctions de résumé

Comme nous avons pu le voir précédemment, pandas peut facilement identifier les différents types de données correspondantes aux valeurs existantes dans les colonnes. De la même manière que **R**, pandas peut proposer des informations de résumé concernant les valeurs des colonnes.

### Valeurs numériques

La méthode de base permettant de récupérer des informations générales sur une colonne est appelée `describe`. Celle-ci nous fourni un ensemble de mesures statistiques sur le contenu de la colonne donnée.

```python
df_vin.points.describe()
```

```
count    129971.000000
mean         88.447138
std           3.039730
min          80.000000
25%          86.000000
50%          88.000000
75%          91.000000
max         100.000000
Name: points, dtype: float64
```

Il est possible d'accéder à chacune de ces mesures de manière indépendante afin de les utiliser dans des filtres ou des opérations tierces.

```python
df_vin.points.mean()
```

```
88.44713820775404
```

### Valeurs alphanumériques

Lorsque nous avons affaire à des valeurs alphanumériques, c'est à dire des chaînes de caractères, les mesures statistiques proposée ci-dessus n'ont que peu d'intérêt. Aussi la méthode `describe` propose des informations relative au type de données visées.

```python
df_vin.taster_name.describe()
```

```
count         103727
unique            19
top       Roger Voss
freq           25514
Name: taster_name, dtype: object
```

Nous voyons ici que pandas réussi à catégoriser les différentes valeurs et à compter leur nombre d'occurence. Là encore, il est possible d'accéder aux différentes valeurs de manière indépendante.

```python
df_vin.taster_name.value_counts()
```

```
Roger Voss            25514
Michael Schachner     15134
Kerin O’Keefe         10776
Virginie Boone         9537
Paul Gregutt           9532
                      ...  
Jeff Jenssen            491
Alexander Peartree      415
Carrie Dykes            139
Fiona Adams              27
Christina Pickard         6
Name: taster_name, Length: 19, dtype: int64
```

La liste des valeurs peut aussi être obtenue directement.

```python
df_vin.taster_name.unique()
```

```
array(['Kerin O’Keefe', 'Roger Voss', 'Paul Gregutt',
       'Alexander Peartree', 'Michael Schachner', 'Anna Lee C. Iijima',
       'Virginie Boone', 'Matt Kettmann', nan, 'Sean P. Sullivan',
       'Jim Gordon', 'Joe Czerwinski', 'Anne Krebiehl\xa0MW',
       'Lauren Buzzeo', 'Mike DeSimone', 'Jeff Jenssen',
       'Susan Kostrzewa', 'Carrie Dykes', 'Fiona Adams',
       'Christina Pickard'], dtype=object)
```

## Mapping des valeurs

Le **mapping** est un terme originaire du domaine des mathématiques. Il sert à décrire une opération qui part d'un ensemble de valeurs et les transforme vers un autre ensemble de valeurs. Ce type de modifications est extrêmement utile lorsque nous avons à modifier de manière automatique un grand nombre d'éléments.

Par exemple, nous souhaitons recentrer les valeurs des scores en fonction du score moyen de notre jeu de données.

Voyons les valeurs existantes dans la colonne.

```python
df_vin.points
```

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
Name: points, Length: 129971, dtype: int64
```

### Méthode `map`

Comme vu ci-dessus, nous pouvons accéder à certaines mesures concernant les valeurs, et notamment la valeur moyenne (`mean`). Une première manière de réaliser ces transformations est d'utiliser la méthode `map` et une expression `lambda`. 

```python
df_vin_mean = df_vin.points.mean()
df_vin.points.map(lambda v: v - df_vin_mean)
```

```
0        -1.447138
1        -1.447138
2        -1.447138
3        -1.447138
4        -1.447138
            ...   
129966    1.552862
129967    1.552862
129968    1.552862
129969    1.552862
129970    1.552862
Name: points, Length: 129971, dtype: float64
```

Nous définissons dans une colonne (ici `points`), une valeur courante `v` que nous modifions à l'aide d'une soustraction. Bien que fonctionnelle et parfois amplement suffisante, cette approche nous limite à ne modifier qu'une colonne à la fois.

### Méthode `apply`

La seconde méthode est plus généraliste et peut nous permettre de modifier toutes les valeurs apparaissant sur une même ligne. Pour cela, nous construisons une fonction qui réalisera la transformation et nous l'appelons à l'aide de la méthode `apply`.


```python
def centre_moyenne_points(row):
    row.points = row.points - df_vin_mean
    return row

df_vin.apply(centre_moyenne_points, axis='columns')
```

```
         country                                        description  \
0          Italy  Aromas include tropical fruit, broom, brimston...   
1       Portugal  This is ripe and fruity, a wine that is smooth...   
2             US  Tart and snappy, the flavors of lime flesh and...   
3             US  Pineapple rind, lemon pith and orange blossom ...   
4             US  Much like the regular bottling from 2012, this...   
...          ...                                                ...   
129966   Germany  Notes of honeysuckle and cantaloupe sweeten th...   
129967        US  Citation is given as much as a decade of bottl...   
129968    France  Well-drained gravel soil gives this wine its c...   
129969    France  A dry style of Pinot Gris, this is crisp with ...   
129970    France  Big, rich and off-dry, this is powered by inte...   

                                   designation    points  price  \
0                                 Vulkà Bianco -1.447138    NaN   
1                                     Avidagos -1.447138   15.0   
2                                          NaN -1.447138   14.0   
3                         Reserve Late Harvest -1.447138   13.0   
4           Vintner's Reserve Wild Child Block -1.447138   65.0   
...                                        ...       ...    ...   
129966  Brauneberger Juffer-Sonnenuhr Spätlese  1.552862   28.0   
129967                                     NaN  1.552862   75.0   
129968                                   Kritt  1.552862   30.0   
129969                                     NaN  1.552862   32.0   
129970           Lieu-dit Harth Cuvée Caroline  1.552862   21.0   

                 province             region_1           region_2  \
0       Sicily & Sardinia                 Etna                NaN   
1                   Douro                  NaN                NaN   
2                  Oregon    Willamette Valley  Willamette Valley   
3                Michigan  Lake Michigan Shore                NaN   
4                  Oregon    Willamette Valley  Willamette Valley   
...                   ...                  ...                ...   
129966              Mosel                  NaN                NaN   
129967             Oregon               Oregon       Oregon Other   
129968             Alsace               Alsace                NaN   
129969             Alsace               Alsace                NaN   
129970             Alsace               Alsace                NaN   

               taster_name taster_twitter_handle  \
0            Kerin O’Keefe          @kerinokeefe   
1               Roger Voss            @vossroger   
2             Paul Gregutt           @paulgwine    
3       Alexander Peartree                   NaN   
4             Paul Gregutt           @paulgwine    
...                    ...                   ...   
129966  Anna Lee C. Iijima                   NaN   
129967        Paul Gregutt           @paulgwine    
129968          Roger Voss            @vossroger   
129969          Roger Voss            @vossroger   
129970          Roger Voss            @vossroger   

                                                    title         variety  \
0                       Nicosia 2013 Vulkà Bianco  (Etna)     White Blend   
1           Quinta dos Avidagos 2011 Avidagos Red (Douro)  Portuguese Red   
2           Rainstorm 2013 Pinot Gris (Willamette Valley)      Pinot Gris   
3       St. Julian 2013 Reserve Late Harvest Riesling ...        Riesling   
4       Sweet Cheeks 2012 Vintner's Reserve Wild Child...      Pinot Noir   
...                                                   ...             ...   
129966  Dr. H. Thanisch (Erben Müller-Burggraef) 2013 ...        Riesling   
129967                  Citation 2004 Pinot Noir (Oregon)      Pinot Noir   
129968  Domaine Gresser 2013 Kritt Gewurztraminer (Als...  Gewürztraminer   
129969      Domaine Marcel Deiss 2012 Pinot Gris (Alsace)      Pinot Gris   
129970  Domaine Schoffit 2012 Lieu-dit Harth Cuvée Car...  Gewürztraminer   

                                          winery   critics  
0                                        Nicosia  everyone  
1                            Quinta dos Avidagos  everyone  
2                                      Rainstorm  everyone  
3                                     St. Julian  everyone  
4                                   Sweet Cheeks  everyone  
...                                          ...       ...  
129966  Dr. H. Thanisch (Erben Müller-Burggraef)  everyone  
129967                                  Citation  everyone  
129968                           Domaine Gresser  everyone  
129969                      Domaine Marcel Deiss  everyone  
129970                          Domaine Schoffit  everyone  

[129971 rows x 14 columns]
```

Nous nous aperçevons que cette deuxième opération n'est pas forcément instantanée. Dans les deux cas, une nouvelle Series ou DataFrame est crée, ce qui laisse notre objet `df_vin` intact et inchangé.

Notez que ce genre de transformation peut aussi être réalisé sur les colonnes au lieu des lignes, il faut alors changer le paramètre `axis` de la méthode `apply` tel que `axis='index'`.


### Méthode direct

Lorsque les opérations à réaliser sont simple comme dans notre exemple, il est aussi possible d'effectuer nos transformations directement:

```python
df_vin.points - df_vin_mean
```

```
0        -1.447138
1        -1.447138
2        -1.447138
3        -1.447138
4        -1.447138
            ...   
129966    1.552862
129967    1.552862
129968    1.552862
129969    1.552862
129970    1.552862
Name: points, Length: 129971, dtype: float64
```

Le résultat est similaire à une opération `map`, mais le principe diffère. Ici, pandas détecte que nosu souhaitons réaliser une opération entre une Series et une variable. Il peut ainsi généraliser le traitement à chacune des valeurs de la liste. Ce type de raccourci ne peut être réalisé que si les deux éléments sujets à l'opération sont de la même taille, ou si l'un d'eux est une valeur simple.

C'est opération peuvent également être réalisées avec des valeurs alphanumériques bien que le résultat sera la concaténation des chaînes de caractères. Essayons avec les colonnes suivantes:

```python
df_vin[['country','region_1','region_2']]
```

```
         country             region_1           region_2
0          Italy                 Etna                NaN
1       Portugal                  NaN                NaN
2             US    Willamette Valley  Willamette Valley
3             US  Lake Michigan Shore                NaN
4             US    Willamette Valley  Willamette Valley
...          ...                  ...                ...
129966   Germany                  NaN                NaN
129967        US               Oregon       Oregon Other
129968    France               Alsace                NaN
129969    France               Alsace                NaN
129970    France               Alsace                NaN

[129971 rows x 3 columns]
```

Nous concaténons les différentes valeurs tel que suit:

```python
df_vin.country + ' - ' + df_vin.region_1 + ', ' + df_vin.region_2
```

```
0                                               NaN
1                                               NaN
2         US - Willamette Valley, Willamette Valley
3                                               NaN
4         US - Willamette Valley, Willamette Valley
                            ...                    
129966                                          NaN
129967                    US - Oregon, Oregon Other
129968                                          NaN
129969                                          NaN
129970                                          NaN
Length: 129971, dtype: object
```

Nous pouvons voir de quel manière les valeurs sont concaténées. Nous pouvons aussi noter de quelle manière les valeurs non définies (`NaN`) sont considérées par ces opérations et comme elles "contaminent" les autres valeurs valides.


## À vous de jouer

C'est maintenant votre tour de vérifier vos acquis en réalisant les [exercices suivants](./3_exercice.md)

