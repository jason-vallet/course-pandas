
Les Maps vous permettent de transformer les valeurs dans une DataFrame ou une Series de manière nominale (une à la fois) ou directement sur une colonne ou ligne complète. Il pourrait cependant être intéressant d'agir seulement sur un sous-ensemble des données proposées. Ce genre d'opérations peut être réalisé, parfois difficilement, à l'aide d'un filtrage des éléments. Plus couramment, nous utiliserons la méthode `groupeby` pour déclarer des groupes à partir des valeurs définies.

## Analyse par groupe

La méthode regroupant les données utilise une des colonnes comme pivot pour définir les différents groupes. Par exemple, en groupant les vins en fonction de leur note, nous pouvons facilement identifier leur prix minimum. 

```python
df_vin.groupby('points').price.min()
```

```
points
80      5.0
81      5.0
82      4.0
83      4.0
84      4.0
       ... 
96     20.0
97     35.0
98     50.0
99     44.0
100    80.0
Name: price, Length: 21, dtype: float64
```

Certaines des méthodes que nous avons vu plus tôt peuvent avoir leur comportement recréé par la méthode `groupby`. La méthode `value_counts` nous retourne le résultat suivant pour la colonne `points` (la méthode `sort_index` est utilisée ici à des fins de présentation pour ordonner les données).

```python
df_vin.points.value_counts().sort_index()
```

```
80      397
81      692
82     1836
83     3025
84     6480
       ... 
96      523
97      229
98       77
99       33
100      19
Name: points, Length: 21, dtype: int64
```

Le résultat obtenu est similaire à l'opération de groupe suivante:

```python
df_vin.groupby('points').points.count()
```

```
points
80      397
81      692
82     1836
83     3025
84     6480
       ... 
96      523
97      229
98       77
99       33
100      19
Name: points, Length: 21, dtype: int64
```

Chacun des groupes résultant de l'opération `groupby` peut être considéré comme une partie de la DataFrame originale. Afin d'accéder plus spécifiquement à ces données, nous devons utiliser la méthode `apply` qui nous permettra de manipuler les données comme souhaité.

Par exemple, en groupant en fonction des producteurs de vin, nous pouvons générer une Series contenant le nombre d'éléments et de colonnes considérées.

```python
df_vin.groupby('winery').apply(lambda l: l.shape)
```

```
winery
1+1=3                   (6, 14)
10 Knots                (4, 14)
100 Percent Wine        (3, 14)
1000 Stories            (2, 14)
1070 Green              (1, 14)
                         ...   
Órale                   (1, 14)
Öko                     (2, 14)
Ökonomierat Rebholz     (4, 14)
àMaurice               (40, 14)
Štoka                   (3, 14)
Length: 16757, dtype: object
```

Entre autres, la méthode `agg` peut être utilisée conjointement avec `groupby` pour réaliser une succession d'opérations en même temps. Groupant les informations en fonction des pays, nous pouvons en une seule opération connaître un résumé rapide des données une fois organisées.

```python
df_vin.groupby('country').price.agg([len, min, max])
```

```
                            len   min     max
country                                      
Argentina                3800.0   4.0   230.0
Armenia                     2.0  14.0    15.0
Australia                2329.0   5.0   850.0
Austria                  3345.0   7.0  1100.0
Bosnia and Herzegovina      2.0  12.0    13.0
...                         ...   ...     ...
Switzerland                 7.0  21.0   160.0
Turkey                     90.0  14.0   120.0
US                      54504.0   4.0  2013.0
Ukraine                    14.0   6.0    13.0
Uruguay                   109.0  10.0   130.0

[43 rows x 3 columns]
```

Pour encore plus de contrôle, nous pouvons regrouper les données en fonction de plusieurs colonnes simultanément. Regardons pour chaque pays et province le vin le mieux noté.

```python
df_vin.groupby(['country','province']).apply(lambda l: l.loc[l.points.idxmax()])
```

```
                              country  \
country   province                      
Argentina Mendoza Province  Argentina   
          Other             Argentina   
Armenia   Armenia             Armenia   
Australia Australia Other   Australia   
          New South Wales   Australia   
...                               ...   
Uruguay   Juanico             Uruguay   
          Montevideo          Uruguay   
          Progreso            Uruguay   
          San Jose            Uruguay   
          Uruguay             Uruguay   

                                                                  description  \
country   province                                                              
Argentina Mendoza Province  If the color doesn't tell the full story, the ...   
          Other             Take note, this could be the best wine Colomé ...   
Armenia   Armenia           Deep salmon in color, this wine offers a bouqu...   
Australia Australia Other   Writes the book on how to make a wine filled w...   
          New South Wales   De Bortoli's Noble One is as good as ever in 2...   
...                                                                       ...   
Uruguay   Juanico           This mature Bordeaux-style blend is earthy on ...   
          Montevideo        A rich, heady bouquet offers aromas of blackbe...   
          Progreso          Rusty in color but deep and complex in nature,...   
          San Jose          Baked, sweet, heavy aromas turn earthy with ti...   
          Uruguay           Cherry and berry aromas are ripe, healthy and ...   

                                                        designation  points  \
country   province                                                            
Argentina Mendoza Province                         Nicasia Vineyard      97   
          Other                                             Reserva      95   
Armenia   Armenia                                    Estate Bottled      88   
Australia Australia Other                             Sarah's Blend      93   
          New South Wales                        Noble One Bortytis      94   
...                                                             ...     ...   
Uruguay   Juanico                  Preludio Barrel Select Lote N 77      90   
          Montevideo        Monte Vide Eu Tannat-Merlot-Tempranillo      91   
          Progreso                   Etxe Oneko Fortified Sweet Red      90   
          San Jose                         El Preciado Gran Reserva      87   
          Uruguay                         Blend 002 Limited Edition      91   

                            price          province                 region_1  \
country   province                                                             
Argentina Mendoza Province  120.0  Mendoza Province                  Mendoza   
          Other              90.0             Other                    Salta   
Armenia   Armenia            15.0           Armenia                      NaN   
Australia Australia Other    15.0   Australia Other  South Eastern Australia   
          New South Wales    32.0   New South Wales          New South Wales   
...                           ...               ...                      ...   
Uruguay   Juanico            45.0           Juanico                      NaN   
          Montevideo         60.0        Montevideo                      NaN   
          Progreso           46.0          Progreso                      NaN   
          San Jose           50.0          San Jose                      NaN   
          Uruguay            22.0           Uruguay                      NaN   

                           region_2        taster_name taster_twitter_handle  \
country   province                                                             
Argentina Mendoza Province      NaN  Michael Schachner           @wineschach   
          Other                 NaN  Michael Schachner           @wineschach   
Armenia   Armenia               NaN      Mike DeSimone        @worldwineguys   
Australia Australia Other       NaN                NaN                   NaN   
          New South Wales       NaN     Joe Czerwinski                @JoeCz   
...                             ...                ...                   ...   
Uruguay   Juanico               NaN  Michael Schachner           @wineschach   
          Montevideo            NaN  Michael Schachner           @wineschach   
          Progreso              NaN  Michael Schachner           @wineschach   
          San Jose              NaN  Michael Schachner           @wineschach   
          Uruguay               NaN  Michael Schachner           @wineschach   

                                                                        title  \
country   province                                                              
Argentina Mendoza Province  Bodega Catena Zapata 2006 Nicasia Vineyard Mal...   
          Other                            Colomé 2010 Reserva Malbec (Salta)   
Armenia   Armenia                 Van Ardi 2015 Estate Bottled Rosé (Armenia)   
Australia Australia Other   Marquis Philips 2000 Sarah's Blend Red (South ...   
          New South Wales   De Bortoli 2007 Noble One Bortytis Semillon (N...   
...                                                                       ...   
Uruguay   Juanico           Familia Deicas 2004 Preludio Barrel Select Lot...   
          Montevideo        Bouza 2015 Monte Vide Eu Tannat-Merlot-Tempran...   
          Progreso          Pisano 2007 Etxe Oneko Fortified Sweet Red Tan...   
          San Jose          Castillo Viejo 2005 El Preciado Gran Reserva R...   
          Uruguay           Narbona NV Blend 002 Limited Edition Tannat-Ca...   

                                          variety                winery  \
country   province                                                        
Argentina Mendoza Province                 Malbec  Bodega Catena Zapata   
          Other                            Malbec                Colomé   
Armenia   Armenia                            Rosé              Van Ardi   
Australia Australia Other               Red Blend       Marquis Philips   
          New South Wales                Sémillon            De Bortoli   
...                                           ...                   ...   
Uruguay   Juanico                       Red Blend        Familia Deicas   
          Montevideo                    Red Blend                 Bouza   
          Progreso                         Tannat                Pisano   
          San Jose                      Red Blend        Castillo Viejo   
          Uruguay           Tannat-Cabernet Franc               Narbona   

                             critics  
country   province                    
Argentina Mendoza Province  everyone  
          Other             everyone  
Armenia   Armenia           everyone  
Australia Australia Other   everyone  
          New South Wales   everyone  
...                              ...  
Uruguay   Juanico           everyone  
          Montevideo        everyone  
          Progreso          everyone  
          San Jose          everyone  
          Uruguay           everyone  

[425 rows x 14 columns]
```

## Index multiples

Jusqu'à présent nous n'avons travailler qu'avec des données indexées à l'aide d'une seule valeur. Comme vu ci-dessus, `groupby` permet de changer ce prédicat. Nous nous trouvons ainsi face à des données avec des indexes multiples, ou multi-index. Celà signifie que l'index a maintenant plusieurs niveaux.

```python
df_vin.groupby(['country', 'province']).description.count()
```

```
country    province        
Argentina  Mendoza Province    3264
           Other                536
Armenia    Armenia                2
Australia  Australia Other      245
           New South Wales       85
                               ... 
Uruguay    Juanico               12
           Montevideo            11
           Progreso              11
           San Jose               3
           Uruguay               24
Name: description, Length: 425, dtype: int64
```

Ce type d'organisation des données permet à l'objet créé d'être particulière efficace pour stocker et accéder aux données, cependant ces indexes sont diffcilement utilisables. Le plus couramment, un index multiple est mis "à plat" afin d'être utilisé. Pour cela, nous utilisons la méthode `reset_index`.

```python
df_vin.groupby(['country', 'province']).description.count().reset_index()
```

```
       country          province  description
0    Argentina  Mendoza Province         3264
1    Argentina             Other          536
2      Armenia           Armenia            2
3    Australia   Australia Other          245
4    Australia   New South Wales           85
..         ...               ...          ...
420    Uruguay           Juanico           12
421    Uruguay        Montevideo           11
422    Uruguay          Progreso           11
423    Uruguay          San Jose            3
424    Uruguay           Uruguay           24

[425 rows x 3 columns]
```

## Tri des données

Nous avons vu un peu avant qu'il était possible d'organiser le résultat produit en fonction de l'index grâce à `sort_index`. Ce genre de situation est aussi applicable pour les différentes valeurs à l'aide de `sort_values`. La méthode peut prendre différents paramètres tel que `by` pour spécifier la colonne à considérer pour réordonner les valeurs.

```python
df_vin.groupby(['country', 'province']).description.count().reset_index().sort_values(by='description')
```

```
          country               province  description
179        Greece  Muscat of Kefallonian            1
192        Greece          Sterea Ellada            1
194        Greece                 Thraki            1
354  South Africa             Paardeberg            1
40         Brazil       Serra do Sudeste            1
..            ...                    ...          ...
409            US                 Oregon         5373
227         Italy                Tuscany         5897
118        France               Bordeaux         5941
415            US             Washington         8639
392            US             California        36247

[425 rows x 3 columns]
```

Le paramètre `ascending` quant à lui va demander une valeur Booléene pour définir l'ordre du réarrangement (montant ou descendant).

```python
df_vin.groupby(['country', 'province']).description.count().reset_index().sort_values(by='description', ascending=False)
```

```
          country         province  description
392            US       California        36247
415            US       Washington         8639
118        France         Bordeaux         5941
227         Italy          Tuscany         5897
409            US           Oregon         5373
..            ...              ...          ...
101       Croatia              Krk            1
247   New Zealand        Gladstone            1
357  South Africa  Piekenierskloof            1
63          Chile          Coelemu            1
149        Greece           Beotia            1

[425 rows x 3 columns]
```

Sachez qu'il est également possible de réagencer les valeurs selon les valeurs de plusieurs colonnes en passant des tableaux de valeurs aux différents paramètres.

```python
df_vin.groupby(['country', 'province']).description.count().reset_index().sort_values(by=['country', 'description'], ascending=[True, False])
```

```
       country          province  description
0    Argentina  Mendoza Province         3264
1    Argentina             Other          536
2      Armenia           Armenia            2
5    Australia   South Australia         1349
7    Australia          Victoria          322
..         ...               ...          ...
420    Uruguay           Juanico           12
421    Uruguay        Montevideo           11
422    Uruguay          Progreso           11
418    Uruguay         Atlantida            5
423    Uruguay          San Jose            3

[425 rows x 3 columns]
```


## À vous de jouer

C'est maintenant votre tour de vérifier vos acquis en réalisant les [exercices suivants](./4_exercice.md)

