## Introduction


Dans ce cours, nous allons voir comment créer nos propre données ainsi que la manière de travailler à partir de données déjà existantes.

## Pour commencer

Pour importer la librairie **pandas**, nous avons juste à entrer la ligne de commande suivante:

```python
import pandas
```

## Créer des données

Pandas utilise deux objets centraux: **DataFrame** et **Series**.

### DataFrame

Une Dataframe est une table contenant des *entrées* individuelles, chacune ayant une certaine *valeur*. Chaque entrée correspond à une *ligne* et une *colonne*.

Par exemple, nous pouvons définir la DataFrame suivante:

```python
pandas.DataFrame({'Yes': [50, 21], 'No': [131, 2]})
```

```
    No  Yes
0  131   50
1    2   21

```

Notez que les ensembles de valeurs définis pour chaque catégorie sont stockés sous forme de colonne de valeurs.

Les données que l'on peut passer en entrées ne sont pas limitées aux entiers. Nous pouvons par exemple utiliser à la place des chaînes de caractères:

```python
pandas.DataFrame({'Alice': ["J'adore.", 'Minable.'], 'Bob': ['Sympa.', 'Quelconque.']})
```

```
      Alice          Bob
0  J'adore.       Sympa.
1  Minable.  Quelconque.
```

Nous utilisons le constructeur de DataFrame pour généer les objets voulus. L'object passé en paramètre est un *dictionnaire* ayant pour *clés* les noms des colonnes et pour *valeur* les listes correspondantes.

On peut observer que les valeurs données pour chaque lignes sont classées par un *index* débutant à 0. Il est égalmeent possible de définir des valeurs d'index plus explicite au besoin en définissant le paramètre `index` lors de la déclaration:

```python
pandas.DataFrame({'Alice': ["J'adore.", 'Minable.'], 
                  'Bob': ['Sympa.', 'Quelconque.']}, 
                  index=['Produit A', 'Produit B'])
```

```
              Alice          Bob
Produit A  J'adore.       Sympa.
Produit B  Minable.  Quelconque.
```

### Series

Un objet Series peut être vu comme une séquence de *valeurs*. Plus simplement, si une DataFrame est considérée comme un tableau, une Series est plutôt une liste de valeurs.

Par exemple, dans sa forme la plus simple, nous pouvons définir l'objet tel que:

```python
pandas.Series([1, 2, 3, 4, 5])
```

Les Series sont utilisées comme des colonnes uniques comme celles définie dans une DataFrame. Nous pouvons donc y rattacher des valeurs d'indexes particulières ainsi que des noms pour définir les Series:

```python
pandas.Series(["J'adore.", 'Minable.'], index=['Produit A', 'Produit B'], name='Alice')
```

```
Produit A    J'adore.
Produit B    Minable.
Name: Alice, dtype: object
```

Les Series peuvent être définies indépendemment les unes des autres pour être ensuite rassemblées dans une DataFrame.

```python
a_s = pandas.Series(["J'adore.", 'Minable.'], index=['Produit A', 'Produit B'], name='Alice')
b_s = pandas.Series(['Sympa.', 'Quelconque.'], index=['Produit A', 'Produit B'], name='Bob')
pandas.DataFrame({a_s.name: a_s, b_s.name: b_s})
```

```
              Alice          Bob
Produit A  J'adore.       Sympa.
Produit B  Minable.  Quelconque.
```

## Lire des fichiers de données

La librairie pandas permet de lire différents types de fichiers, cependant nous allons nous concentrer sur les fichiers de type *csv* (*comma separated values*). Pour rappel, un fichier *csv* est un fichier texte qui contient un tableau mis en forme par des virgules, démarquant les colonnes, et des sauts de ligne, pour indiquer les fins de lignes.

```
Champs 1,Champs 2,Champs 3
AA,21,9
B,34,1
C,11,11
```

Pour ouvrir ce fichier, nous allons utiliser la fonction `read.csv` de pandas qui lira le fichier et stockera son contenu dans une DataFrame.

```python
df_vin = pandas.read_csv('./datasets/winemag-data-130k-v2.csv')
```

En quelques instants, pandas va lire le fichier et classifier les données contenues dans différentes Series. 

Nous pouvons maintenant accéder au contenu de la DataFrame stockée dans la variable `df_vin`. Par exemple, le paramètre `shape` rattaché à l'objet va nous indiquer la taille des données considérées.

```python
df_vin.shape
```

```
(129971, 14)
```

Soit 129971 lignes et 14 colonnes; il est également possible d'avoir un aperçu du contenu du tableau à l'aide de la fonction `head`.

```python
df_vin.head()
```

```
   Unnamed: 0   country                                        description  \
0           0     Italy  Aromas include tropical fruit, broom, brimston...   
1           1  Portugal  This is ripe and fruity, a wine that is smooth...   
2           2        US  Tart and snappy, the flavors of lime flesh and...   
3           3        US  Pineapple rind, lemon pith and orange blossom ...   
4           4        US  Much like the regular bottling from 2012, this...   

                          designation  points  price           province  \
0                        Vulkà Bianco      87    NaN  Sicily & Sardinia   
1                            Avidagos      87   15.0              Douro   
2                                 NaN      87   14.0             Oregon   
3                Reserve Late Harvest      87   13.0           Michigan   
4  Vintner's Reserve Wild Child Block      87   65.0             Oregon   

              region_1           region_2         taster_name  \
0                 Etna                NaN       Kerin O’Keefe   
1                  NaN                NaN          Roger Voss   
2    Willamette Valley  Willamette Valley        Paul Gregutt   
3  Lake Michigan Shore                NaN  Alexander Peartree   
4    Willamette Valley  Willamette Valley        Paul Gregutt   

  taster_twitter_handle                                              title  \
0          @kerinokeefe                  Nicosia 2013 Vulkà Bianco  (Etna)   
1            @vossroger      Quinta dos Avidagos 2011 Avidagos Red (Douro)   
2           @paulgwine       Rainstorm 2013 Pinot Gris (Willamette Valley)   
3                   NaN  St. Julian 2013 Reserve Late Harvest Riesling ...   
4           @paulgwine   Sweet Cheeks 2012 Vintner's Reserve Wild Child...   

          variety               winery  
0     White Blend              Nicosia
1  Portuguese Red  Quinta dos Avidagos
2      Pinot Gris            Rainstorm
3        Riesling           St. Julian
4      Pinot Noir         Sweet Cheeks
```

Nous entrerons davantage dans les détails concernant l'accés aux données stockées dans une DataFrame. Notez cependant que vous pouvez accéder aux entêtes des colones grâce à la fonction `keys`.

```python
df_vin.keys()
```

```
Index(['Unnamed: 0', 'country', 'description', 'designation', 'points',
       'price', 'province', 'region_1', 'region_2', 'taster_name',
       'taster_twitter_handle', 'title', 'variety', 'winery'],
      dtype='object')
```

La fonction `read_csv` contient de [nombreux paramètres optionnels](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html#pandas.read_csv) pour améliorer la catégorisation des données dans la DataFrame. N'hésitez pas à consulter la [documentation de Pandas](https://pandas.pydata.org/pandas-docs/stable/reference/index.html) pour plus d'informations sur les différentes fonctions vues par la suite.

## À vous de jouer

C'est maintenant votre tour de vérifier vos acquis en réalisant les [exercices suivants](./1_exercice.md)
