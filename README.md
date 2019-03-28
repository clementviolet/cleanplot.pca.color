# A propos

Ce repo contient une version modifiée de la fonction `cleanplot.pca()`
dont la version originelle se trouve également dans ce dossier. Cette
nouvelle version, nommée `cleanpot.pca.color()` permet de différencier
les points par couleurs en fonction d’une variable catégorielle (i.e :
un `factor`).

Pour l’utiliser, il suffit d’enregistrer le script
`cleanplot.pca.color.R` dans le répertoire courant dans lequel travaille
`R` (utilisez la fonction `getwd()` pour le trouver).

# Exemple

Je souhaite faire une ACP sur les données du jeu `iris` inclu dans `R`.

``` r
library(vegan)
```

    ## Loading required package: permute

    ## Loading required package: lattice

    ## This is vegan 2.5-3

``` r
source("cleanplot.pca.color.R")

data <- iris

species <- iris$Species
species <- as.factor(species) # Je transforme mes données d

data <- data[, -5]

data_pca <- rda(scale(data))
```

`cleanplot.pca.color()` a de nouveaux arguements qui sont tous
facultatifs :

  - `grouping.factor` Un vecteur contenant les facteurs servant à
    colorer les points (le nombre d’éléments dans votre vecteur doit
    être égal au nombre de ligne du tableau utilisé dans la
    fonction`rda()`);
  - `grouping.title` Le titre de la boite de légende que souhaitez
    donner ;
  - `pos.legend` La position boîte de légende. Doit avoir l’une des
    valeurs suivantes `bottomright`, `bottom`, `bottomleft`, `left`,
    `topleft`, `top`, `topright`, `right` ou `center`.

Par exemple, cela donne quelque chose comme cela :

``` r
cleanplot.pca.color(data_pca, grouping.factor = species, grouping.title = "Espèce", pos.legend = "topleft")
```

![](README_files/figure-gfm/acp-plot-color-1.png)<!-- -->

Si je ne donne pas ces nouveaux arguments, `cleanplot.pca.color()` se
comporte de la même manière que `cleanplot.pca()`.

``` r
cleanplot.pca.color(data_pca)
```

![](README_files/figure-gfm/acp-plot-classic-1.png)<!-- -->
