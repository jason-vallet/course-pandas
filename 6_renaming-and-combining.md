
## Renommer les colonnes

Lorsque l'on travaille avec des données provenant de diverses sources, il est possible que les conventions de nommage suivies ne nous conviennent pas. Pour adresser ce problème, nous pouvons utiliser la méthode `rename`.

```python
info_vin[['title', 'points']].rename(columns={'points':'score'})
```

```
                                                    title  score
0                       Nicosia 2013 Vulkà Bianco  (Etna)     87
1           Quinta dos Avidagos 2011 Avidagos Red (Douro)     87
2           Rainstorm 2013 Pinot Gris (Willamette Valley)     87
3       St. Julian 2013 Reserve Late Harvest Riesling ...     87
4       Sweet Cheeks 2012 Vintner's Reserve Wild Child...     87
...                                                   ...    ...
129966  Dr. H. Thanisch (Erben Müller-Burggraef) 2013 ...     90
129967                  Citation 2004 Pinot Noir (Oregon)     90
129968  Domaine Gresser 2013 Kritt Gewurztraminer (Als...     90
129969      Domaine Marcel Deiss 2012 Pinot Gris (Alsace)     90
129970  Domaine Schoffit 2012 Lieu-dit Harth Cuvée Car...     90

[129971 rows x 2 columns]
```

Le paramètre `column` nous permet de préciser la cible de la modification à réaliser. Il est également possible de modifier les valeurs d'indexes au besoin (à utiliser de façon réfléchie!) et de spécifier plusieurs modifications en une seule fois.

```python
info_vin[['title', 'points']].rename(index={0: 'firstEntry', 1: 'secondEntry'})
```

```
                                                         title  points
firstEntry                   Nicosia 2013 Vulkà Bianco  (Etna)      87
secondEntry      Quinta dos Avidagos 2011 Avidagos Red (Douro)      87
2                Rainstorm 2013 Pinot Gris (Willamette Valley)      87
3            St. Julian 2013 Reserve Late Harvest Riesling ...      87
4            Sweet Cheeks 2012 Vintner's Reserve Wild Child...      87
...                                                        ...     ...
129966       Dr. H. Thanisch (Erben Müller-Burggraef) 2013 ...      90
129967                       Citation 2004 Pinot Noir (Oregon)      90
129968       Domaine Gresser 2013 Kritt Gewurztraminer (Als...      90
129969           Domaine Marcel Deiss 2012 Pinot Gris (Alsace)      90
129970       Domaine Schoffit 2012 Lieu-dit Harth Cuvée Car...      90

[129971 rows x 2 columns]
```

De manière plus générale, la définition des indexes se fera plus souvent avec la méthode `set_index`.

Pour des questions de présentations de résultats, il peut parfois être utile de définir des noms exhaustifs pour les indexes des lignes et des colonnes. Ce genre d'action utilise la méthode `rename_axis` et prend en paramètre le nom à attribuer et l'axe à considérer.

```python
info_vin.rename_axis("vins", axis='rows').rename_axis("champs", axis='columns')[['title','points','price']]
```

```
champs                                              title  points  price
vins                                                                    
0                       Nicosia 2013 Vulkà Bianco  (Etna)      87    NaN
1           Quinta dos Avidagos 2011 Avidagos Red (Douro)      87   15.0
2           Rainstorm 2013 Pinot Gris (Willamette Valley)      87   14.0
3       St. Julian 2013 Reserve Late Harvest Riesling ...      87   13.0
4       Sweet Cheeks 2012 Vintner's Reserve Wild Child...      87   65.0
...                                                   ...     ...    ...
129966  Dr. H. Thanisch (Erben Müller-Burggraef) 2013 ...      90   28.0
129967                  Citation 2004 Pinot Noir (Oregon)      90   75.0
129968  Domaine Gresser 2013 Kritt Gewurztraminer (Als...      90   30.0
129969      Domaine Marcel Deiss 2012 Pinot Gris (Alsace)      90   32.0
129970  Domaine Schoffit 2012 Lieu-dit Harth Cuvée Car...      90   21.0

[129971 rows x 3 columns]
```

## Combinaison de données

Pour différentes raisons, vos données à traiter peuvent être distribuées dans plusieurs fichiers. Dans ces cas là, il convient de savoir de quelle manère regrouper vos données avant de réaliser vos analyses. Nous avons vu ci-avant de quelle manière renommer les colonnes, ceci va nous simplifier la tâche en rendant les différents jeux de données "compatibles"; ainsi une colonne `title` dans les données A et une colonne `titre` dans les données B devront être nommées de façon similaire si elles indiquent le même type de contenu dans les deux cas.

Nous allons travailler avec deux ensembles de données regroupant des informations statistiques sur des vidéos hébergée sur YouTube selon leur pays d'origine. Afin de simplifier le problème, nous ne travaillerons qu'avec deux fichiers.

```python
df_yt_fr = pandas.read_csv('./datasets/FRvideos.csv')
df_yt_ca = pandas.read_csv('./datasets/CAvideos.csv')
df_yt_fr
df_yt_ca
```

```
          video_id  ...                                        description
0      Ro6eob0LrCY  ...  Dimanche.\n18h30.\nSoyez présents pour la vidé...
1      Yo84eqYwP98  ...  Le jeu de société: https://goo.gl/hhG1Ta\n\nGa...
2      ceqntSXE-10  ...  Une nouvelle dose de dessins animés français e...
3      WuTFI5qftCE  ...  Nouvel ,épisode de Papy Grenier ! Ce mois-ci o...
4      ee6OFs8TdEg  ...  Sauts à plus de 4 mètres de haut dans un tramp...
...            ...  ...                                                ...
40719  coVXf3Q9xBk  ...  المغرب تخسر تنظيم مونديال كاس العالم 2026 لصال...
40720  _umkjOQJvtw  ...  ملخص ابرز ما حصل في جلسة البرلمان يوم 12/06/20...
40721  nt25ec7nzIM  ...  •● Yozakura Quartet ~Hana no Uta~ ●•☆ S'abonne...
40722  NlxE_QQMRzg  ...  Follow Armenia TV on social platforms:Instagra...
40723  _LgKglfnqlc  ...                                                NaN

[40724 rows x 16 columns]

          video_id  ...                                        description
0      n1WpP7iowLc  ...  Eminem's new track Walk on Water ft. Beyoncé i...
1      0dBIkQ4Mz1M  ...  STill got a lot of packages. Probably will las...
2      5qpjK5DgCt4  ...  WATCH MY PREVIOUS VIDEO ▶ \n\nSUBSCRIBE ► http...
3      d380meD0W0M  ...  I know it's been a while since we did this sho...
4      2Vv-BfVoq4g  ...  🎧: https://ad.gt/yt-perfect\n💰: https://atlant...
...            ...  ...                                                ...
40876  sGolxsMSGfQ  ...  🚨 NEW MERCH! http://amzn.to/annoyingorange 🚨➤ ...
40877  8HNuRNi8t70  ...  ► Retrouvez vos programmes préférés : https://...
40878  GWlKEM3m2EE  ...  Find out more about Kingdom Hearts 3: https://...
40879  lbMKLzQ4cNQ  ...  Peter Navarro isn’t talking so tough now. Ana ...
40880  POTgw38-m58  ...  藝人：李妍瑾、玉兔、班傑、LaLa、小優、少少專家：陳筱屏(律師)、Wendy(心理師)、羅...

[40881 rows x 16 columns]
```

Le premier type d'opération pour combiner les fichiers est une concaténation, réalisée par la méthode `concat`. Le résultat est une simple opération qui va mettre bout à bout les deux ensembles de données considérés.

```python
df_yt_cc = pandas.concat([df_yt_fr, df_yt_ca])
df_yt_cc.shape
```

```
(81605, 16)
```

Cependant, certaines des vidéos sont peut-être présentes dans les deux ensembles de données. Afin de le vérifier, nous pouvons vérifier à l'aide de la méthode `duplicated` qui compare si les lignes sont des duplicats.

```python
df_yt_cc[df_yt_cc.duplicated()].size
```

```
25056
```

Bien que nous puissions supprimer les lignes dupliquées, une manière plus intelligente de rassembler nos données serait d'utiliser l'opération `join`. Nous allons spécifier pour chacun des jeux de données l'index qui nous convient et spécifier à la méthode `join` d'utiliser ces champs comme point de comparaison.

L'identification d'un index valide dans ces cas là est essentiel, heureusement la fonction `set_index` peut nous permettre de vérifier si un choix est valide grâce à l'option `verify_integrity`. Essayons par exemple avec le champ `video_id`.

```python
df_yt_fr.set_index('video_id', verify_integrity=True)
```

```
ValueError: Index has duplicate keys: Index(['Ro6eob0LrCY', 'tsMw-VMUtNU', 'teXaL6GdQRk', 'ceqntSXE-10',
       'Yo84eqYwP98', 'ee6OFs8TdEg', 'WuTFI5qftCE', '2rciAnKuVdM',
       '-ktC_CVGAvs', 'PpECwr15oQQ',
       ...
       'UkwNrJSNEXM', 'kS33gBAGcnQ', 'mGZwZDaPpMc', '05tyrZonnmw',
       'N7V7FVwlRpk', 'Qz-LPtregKk', 'AHO6zvnY08I', 'fODCOUeY0YM',
       'r5Kd7ltWS9w', '_umkjOQJvtw'],
      dtype='object', name='video_id', length=7587)
```

Nous voyons donc que le champ `video_id` n'est pas un index viable. Chacune des lignes correspondant à une occasion où la vidéo a été populaire, nous pouvons utiliser le champ `trending_date` pour tenir compte de cette information.

```python
df_yt_fr.set_index(['video_id', 'trending_date'], verify_integrity=True, inplace=True)
df_yt_fr.shape
```

```
(40724, 14)
```

Vu que l'opération à bien fonctionné, nous répétons le processus avec les données du Canada. Notez que nous utilisons ici le paramètre `inplace` pour stocker le résultat directement dans la variable initiale; ce type de comportement est à limiter aux cas où vous êtes certain de vouloir effacer les valeurs précédentes.

```python
df_yt_ca.set_index(['video_id', 'trending_date'], verify_integrity=True, inplace=True)
```

Il ne nous reste maintenant plus qu'à joindre les deux ensemble de données avec `join`. Cette fonction demande un certain nombre de paramètres tel que des valeurs de suffixes pour différencier les champs existants dans les deux ensembles ainsi qu'une méthode de fusion exprimée par `how`.

```python
tmp = df_yt_fr.join(df_yt_ca, how='outer', lsuffix='_FR', rsuffix='_CA')
tmp.shape
```

```
(76060, 28)
```

Une fois les données regroupés, il reste encore du travail avant d'avoir une DataFrame organisée et utilisable. Il faudra notamment:

* comparer et fusionner les valeurs des colonnes "identiques"
* renommer les colonnes que nous prevoyons d'utiliser
* supprimer les colonnes inutiles
* répéter l'opération autant de fois que nécessaire pour fusionner les autres fichiers restant...
* enfin commencer à réaliser notre analyse!


## À vous de jouer

C'est maintenant votre tour de vérifier vos acquis en réalisant les [exercices suivants](./6_exercice.md)

