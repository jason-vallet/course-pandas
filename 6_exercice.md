## Introduction 

Dans un fichier tiers exécutable en **Python**, saisissez vos commandes afin de résoudre les différentes question posées ci-après.

N'oubliez pas de mettre tout texte additionnel en commentaire (en utilisant le symbole `#`).

Ouvrez le fichier csv `./datasets/winemag-data-130k-v2.csv` en utilisant en spécificant l'index comme étant la colonne 0. Stockez la DataFrame dans la variable `info_vin`.

## 1.

Les champs `region_1` et `region_2` manquent de détail. Renommez ces deux colonnes en `region` et `locale` respectivement. Stockez le résultat dans la variable `info_vin_renomme_region`.


```
                                                    title   country  \
0                       Nicosia 2013 Vulkà Bianco  (Etna)     Italy   
1           Quinta dos Avidagos 2011 Avidagos Red (Douro)  Portugal   
2           Rainstorm 2013 Pinot Gris (Willamette Valley)        US   
3       St. Julian 2013 Reserve Late Harvest Riesling ...        US   
4       Sweet Cheeks 2012 Vintner's Reserve Wild Child...        US   
...                                                   ...       ...   
129966  Dr. H. Thanisch (Erben Müller-Burggraef) 2013 ...   Germany   
129967                  Citation 2004 Pinot Noir (Oregon)        US   
129968  Domaine Gresser 2013 Kritt Gewurztraminer (Als...    France   
129969      Domaine Marcel Deiss 2012 Pinot Gris (Alsace)    France   
129970  Domaine Schoffit 2012 Lieu-dit Harth Cuvée Car...    France   

                     region             locale  
0                      Etna                NaN  
1                       NaN                NaN  
2         Willamette Valley  Willamette Valley  
3       Lake Michigan Shore                NaN  
4         Willamette Valley  Willamette Valley  
...                     ...                ...  
129966                  NaN                NaN  
129967               Oregon       Oregon Other  
129968               Alsace                NaN  
129969               Alsace                NaN  
129970               Alsace                NaN  

[129971 rows x 4 columns]
```

## 2.

Dans la variable `info_vin_renomme_index`, stockez une copie de la DataFrame `info_vin` et renommez son index avec le nom `vins`.

```
                                                    title
vins                                                     
0                       Nicosia 2013 Vulkà Bianco  (Etna)
1           Quinta dos Avidagos 2011 Avidagos Red (Douro)
2           Rainstorm 2013 Pinot Gris (Willamette Valley)
3       St. Julian 2013 Reserve Late Harvest Riesling ...
4       Sweet Cheeks 2012 Vintner's Reserve Wild Child...
...                                                   ...
129966  Dr. H. Thanisch (Erben Müller-Burggraef) 2013 ...
129967                  Citation 2004 Pinot Noir (Oregon)
129968  Domaine Gresser 2013 Kritt Gewurztraminer (Als...
129969      Domaine Marcel Deiss 2012 Pinot Gris (Alsace)
129970  Domaine Schoffit 2012 Lieu-dit Harth Cuvée Car...

[129971 rows x 1 columns]
```

## 3.

Chargez les fichiers `CAvideos.csv` et `FRvideos.csv` tel que vu en cours (n'oubliez pas de redéfinir l'index!).

À partir des deux jeux de données sur les vidéos YouTube, utilisez les opérations de jointures pour ne récupérer que les vidéos ayant eu du succès à la fois en France et au Canada. Stockez le résultat dans la variable `videos_communes`.

```
(5545, 28)
```

## 4.

Plusieurs de nos champs ont des valeurs similaires que nous souhaitons rassembler suite à la jointure des ensembles. Pour tous les champs ayant le même nom (nonobstant le suffixe) et de type numérique ou booléen, rassamblez les valeurs soit en choisissant le maximum, soit en prenant la valeur Vrai si l'un des deux ensemble est à vrai. Stockez le résultat dans la variable `video_propre`.




