# Base R vs. Tidyverse {#baser}





```r
library(tidyverse)
```

## Extract variables

<button id="displayTextunnamed-chunk-3" onclick="javascript:toggle('unnamed-chunk-3');">Show Solution</button>

<div id="toggleTextunnamed-chunk-3" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body"><div class="tab"><button class="tablinksunnamed-chunk-3 active" onclick="javascript:openCode(event, 'option1unnamed-chunk-3', 'unnamed-chunk-3');">Base R</button><button class="tablinksunnamed-chunk-3" onclick="javascript:openCode(event, 'option2unnamed-chunk-3', 'unnamed-chunk-3');"><tt>tidyverse</tt></button></div><div id="option1unnamed-chunk-3" class="tabcontentunnamed-chunk-3">

```r
iris$Sepal.Length # single variable
iris[, c("Species", "Petal.Width")] # by name
iris[, c(5, 4)]  # by column index
```
</div><div id="option2unnamed-chunk-3" class="tabcontentunnamed-chunk-3">

```r
select(iris, Species)
select(iris, Species, Petal.Width) # by name
select(iris, 5, 4)  # by column index
```
</div><script> javascript:hide('option2unnamed-chunk-3') </script></div></div></div>


## Make new variables

<button id="displayTextunnamed-chunk-4" onclick="javascript:toggle('unnamed-chunk-4');">Show Solution</button>

<div id="toggleTextunnamed-chunk-4" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body"><div class="tab"><button class="tablinksunnamed-chunk-4 active" onclick="javascript:openCode(event, 'option1unnamed-chunk-4', 'unnamed-chunk-4');">Base R</button><button class="tablinksunnamed-chunk-4" onclick="javascript:openCode(event, 'option2unnamed-chunk-4', 'unnamed-chunk-4');"><tt>tidyverse</tt></button></div><div id="option1unnamed-chunk-4" class="tabcontentunnamed-chunk-4">

```r
iris$Petal.Ratio <- iris$Petal.Length/iris$Petal.Width

iris$Sepal.Ratio <- iris$Sepal.Length/iris$Sepal.Width
```
</div><div id="option2unnamed-chunk-4" class="tabcontentunnamed-chunk-4">

```r
mutate(iris, 
       Petal.Ratio = Petal.Length/Petal.Width,
       Sepal.Ratio = Sepal.Length/Sepal.Width)
```
</div><script> javascript:hide('option2unnamed-chunk-4') </script></div></div></div>


Extract observations (rows)

<button id="displayTextunnamed-chunk-5" onclick="javascript:toggle('unnamed-chunk-5');">Show Solution</button>

<div id="toggleTextunnamed-chunk-5" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body"><div class="tab"><button class="tablinksunnamed-chunk-5 active" onclick="javascript:openCode(event, 'option1unnamed-chunk-5', 'unnamed-chunk-5');">Base R</button><button class="tablinksunnamed-chunk-5" onclick="javascript:openCode(event, 'option2unnamed-chunk-5', 'unnamed-chunk-5');"><tt>tidyverse</tt></button></div><div id="option1unnamed-chunk-5" class="tabcontentunnamed-chunk-5">

```r
# Using [,]
iris[iris$Petal.Width > 0.5 & iris$Species == "setosa", ]

# Using subset (works very much like dplyr::filter)
subset(iris, Petal.Width > 0.5 & Species == "setosa")
```

<div class="kable-table">

<table>
 <thead>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:right;"> Sepal.Length </th>
   <th style="text-align:right;"> Sepal.Width </th>
   <th style="text-align:right;"> Petal.Length </th>
   <th style="text-align:right;"> Petal.Width </th>
   <th style="text-align:left;"> Species </th>
   <th style="text-align:right;"> Petal.Ratio </th>
   <th style="text-align:right;"> Sepal.Ratio </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> 44 </td>
   <td style="text-align:right;"> 5 </td>
   <td style="text-align:right;"> 3.5 </td>
   <td style="text-align:right;"> 1.6 </td>
   <td style="text-align:right;"> 0.6 </td>
   <td style="text-align:left;"> setosa </td>
   <td style="text-align:right;"> 2.666667 </td>
   <td style="text-align:right;"> 1.428571 </td>
  </tr>
</tbody>
</table>

</div><div class="kable-table">

<table>
 <thead>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:right;"> Sepal.Length </th>
   <th style="text-align:right;"> Sepal.Width </th>
   <th style="text-align:right;"> Petal.Length </th>
   <th style="text-align:right;"> Petal.Width </th>
   <th style="text-align:left;"> Species </th>
   <th style="text-align:right;"> Petal.Ratio </th>
   <th style="text-align:right;"> Sepal.Ratio </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> 44 </td>
   <td style="text-align:right;"> 5 </td>
   <td style="text-align:right;"> 3.5 </td>
   <td style="text-align:right;"> 1.6 </td>
   <td style="text-align:right;"> 0.6 </td>
   <td style="text-align:left;"> setosa </td>
   <td style="text-align:right;"> 2.666667 </td>
   <td style="text-align:right;"> 1.428571 </td>
  </tr>
</tbody>
</table>

</div>
</div><div id="option2unnamed-chunk-5" class="tabcontentunnamed-chunk-5">

```r
filter(iris, Petal.Width > 0.5 & Species == "setosa")
```

<div class="kable-table">

<table>
 <thead>
  <tr>
   <th style="text-align:right;"> Sepal.Length </th>
   <th style="text-align:right;"> Sepal.Width </th>
   <th style="text-align:right;"> Petal.Length </th>
   <th style="text-align:right;"> Petal.Width </th>
   <th style="text-align:left;"> Species </th>
   <th style="text-align:right;"> Petal.Ratio </th>
   <th style="text-align:right;"> Sepal.Ratio </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 5 </td>
   <td style="text-align:right;"> 3.5 </td>
   <td style="text-align:right;"> 1.6 </td>
   <td style="text-align:right;"> 0.6 </td>
   <td style="text-align:left;"> setosa </td>
   <td style="text-align:right;"> 2.666667 </td>
   <td style="text-align:right;"> 1.428571 </td>
  </tr>
</tbody>
</table>

</div>
</div><script> javascript:hide('option2unnamed-chunk-5') </script></div></div></div>

## Arrange observations (rows)

<button id="displayTextunnamed-chunk-6" onclick="javascript:toggle('unnamed-chunk-6');">Show Solution</button>

<div id="toggleTextunnamed-chunk-6" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body"><div class="tab"><button class="tablinksunnamed-chunk-6 active" onclick="javascript:openCode(event, 'option1unnamed-chunk-6', 'unnamed-chunk-6');">Base R</button><button class="tablinksunnamed-chunk-6" onclick="javascript:openCode(event, 'option2unnamed-chunk-6', 'unnamed-chunk-6');"><tt>tidyverse</tt></button></div><div id="option1unnamed-chunk-6" class="tabcontentunnamed-chunk-6">

```r
# descending order of species (alphabetic) followed by ascending order of Petal.Width
iris[order(rev(iris$Species), iris$Petal.Width) , ]
```
</div><div id="option2unnamed-chunk-6" class="tabcontentunnamed-chunk-6">

```r
# descending order of species (alphabetic) followed by ascending order of Petal.Width
arrange(iris, desc(Species), Petal.Width) 
```
</div><script> javascript:hide('option2unnamed-chunk-6') </script></div></div></div>


## Summarise observations (rows)

<button id="displayTextunnamed-chunk-7" onclick="javascript:toggle('unnamed-chunk-7');">Show Solution</button>

<div id="toggleTextunnamed-chunk-7" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body"><div class="tab"><button class="tablinksunnamed-chunk-7 active" onclick="javascript:openCode(event, 'option1unnamed-chunk-7', 'unnamed-chunk-7');">Base R</button><button class="tablinksunnamed-chunk-7" onclick="javascript:openCode(event, 'option2unnamed-chunk-7', 'unnamed-chunk-7');"><tt>tidyverse</tt></button></div><div id="option1unnamed-chunk-7" class="tabcontentunnamed-chunk-7">

```r
# Manually create a data.frame
data.frame(Petal.Length.mean = mean(iris$Petal.Length),
           Petal.Length.sd = sd(iris$Petal.Length),
           Sepal.Length.mean = mean(iris$Sepal.Length),
           Sepal.Length.sd = sd(iris$Sepal.Length))
```

<div class="kable-table">

<table>
 <thead>
  <tr>
   <th style="text-align:right;"> Petal.Length.mean </th>
   <th style="text-align:right;"> Petal.Length.sd </th>
   <th style="text-align:right;"> Sepal.Length.mean </th>
   <th style="text-align:right;"> Sepal.Length.sd </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 3.758 </td>
   <td style="text-align:right;"> 1.765298 </td>
   <td style="text-align:right;"> 5.843333 </td>
   <td style="text-align:right;"> 0.8280661 </td>
  </tr>
</tbody>
</table>

</div>
</div><div id="option2unnamed-chunk-7" class="tabcontentunnamed-chunk-7">

```r
summarise(iris, 
          Petal.Length.mean = mean(Petal.Length),
          Petal.Length.sd = sd(Petal.Length),
          Sepal.Length.mean = mean(Sepal.Length),
          Sepal.Length.sd = sd(Sepal.Length))
```

<div class="kable-table">

<table>
 <thead>
  <tr>
   <th style="text-align:right;"> Petal.Length.mean </th>
   <th style="text-align:right;"> Petal.Length.sd </th>
   <th style="text-align:right;"> Sepal.Length.mean </th>
   <th style="text-align:right;"> Sepal.Length.sd </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 3.758 </td>
   <td style="text-align:right;"> 1.765298 </td>
   <td style="text-align:right;"> 5.843333 </td>
   <td style="text-align:right;"> 0.8280661 </td>
  </tr>
</tbody>
</table>

</div>
</div><script> javascript:hide('option2unnamed-chunk-7') </script></div></div></div>


## Grouped operations

<button id="displayTextunnamed-chunk-8" onclick="javascript:toggle('unnamed-chunk-8');">Show Solution</button>

<div id="toggleTextunnamed-chunk-8" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body"><div class="tab"><button class="tablinksunnamed-chunk-8 active" onclick="javascript:openCode(event, 'option1unnamed-chunk-8', 'unnamed-chunk-8');">Base R</button><button class="tablinksunnamed-chunk-8" onclick="javascript:openCode(event, 'option2unnamed-chunk-8', 'unnamed-chunk-8');"><tt>tidyverse</tt></button></div><div id="option1unnamed-chunk-8" class="tabcontentunnamed-chunk-8">

```r
# First operate in the data.frame by group (split-apply)
mtcars_by <- by(mtcars, 
   INDICES = list(mtcars$cyl, mtcars$gear),
   FUN = function(x){
     data.frame(cyl = unique(x$cyl),
                gear = unique(x$gear),
                mpg.mean = mean(x$mpg),
                mpg.sd = sd(x$mpg),
                wt.mean = mean(x$wt),
                wt.sd = sd(x$wt))
   })

# Then combine the results into a data.frame
do.call(rbind, mtcars_by)
```

<div class="kable-table">

<table>
 <thead>
  <tr>
   <th style="text-align:right;"> cyl </th>
   <th style="text-align:right;"> gear </th>
   <th style="text-align:right;"> mpg.mean </th>
   <th style="text-align:right;"> mpg.sd </th>
   <th style="text-align:right;"> wt.mean </th>
   <th style="text-align:right;"> wt.sd </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:right;"> 21.500 </td>
   <td style="text-align:right;"> NA </td>
   <td style="text-align:right;"> 2.465000 </td>
   <td style="text-align:right;"> NA </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:right;"> 19.750 </td>
   <td style="text-align:right;"> 2.3334524 </td>
   <td style="text-align:right;"> 3.337500 </td>
   <td style="text-align:right;"> 0.1732412 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 8 </td>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:right;"> 15.050 </td>
   <td style="text-align:right;"> 2.7743959 </td>
   <td style="text-align:right;"> 4.104083 </td>
   <td style="text-align:right;"> 0.7683069 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:right;"> 26.925 </td>
   <td style="text-align:right;"> 4.8073604 </td>
   <td style="text-align:right;"> 2.378125 </td>
   <td style="text-align:right;"> 0.6006243 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:right;"> 19.750 </td>
   <td style="text-align:right;"> 1.5524175 </td>
   <td style="text-align:right;"> 3.093750 </td>
   <td style="text-align:right;"> 0.4131460 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:right;"> 5 </td>
   <td style="text-align:right;"> 28.200 </td>
   <td style="text-align:right;"> 3.1112698 </td>
   <td style="text-align:right;"> 1.826500 </td>
   <td style="text-align:right;"> 0.4433560 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:right;"> 5 </td>
   <td style="text-align:right;"> 19.700 </td>
   <td style="text-align:right;"> NA </td>
   <td style="text-align:right;"> 2.770000 </td>
   <td style="text-align:right;"> NA </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 8 </td>
   <td style="text-align:right;"> 5 </td>
   <td style="text-align:right;"> 15.400 </td>
   <td style="text-align:right;"> 0.5656854 </td>
   <td style="text-align:right;"> 3.370000 </td>
   <td style="text-align:right;"> 0.2828427 </td>
  </tr>
</tbody>
</table>

</div>
</div><div id="option2unnamed-chunk-8" class="tabcontentunnamed-chunk-8">

```r
mtcars %>% 
  group_by(cyl, gear) %>% 
  summarise(mpg.mean = mean(mpg),
            mpg.sd = sd(mpg),
            wt.mean = mean(wt),
            wt.sd = sd(wt)) %>% 
  ungroup() # remove any groupings from downstream analysis
```

<div class="kable-table">

<table>
 <thead>
  <tr>
   <th style="text-align:right;"> cyl </th>
   <th style="text-align:right;"> gear </th>
   <th style="text-align:right;"> mpg.mean </th>
   <th style="text-align:right;"> mpg.sd </th>
   <th style="text-align:right;"> wt.mean </th>
   <th style="text-align:right;"> wt.sd </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:right;"> 21.500 </td>
   <td style="text-align:right;"> NA </td>
   <td style="text-align:right;"> 2.465000 </td>
   <td style="text-align:right;"> NA </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:right;"> 26.925 </td>
   <td style="text-align:right;"> 4.8073604 </td>
   <td style="text-align:right;"> 2.378125 </td>
   <td style="text-align:right;"> 0.6006243 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:right;"> 5 </td>
   <td style="text-align:right;"> 28.200 </td>
   <td style="text-align:right;"> 3.1112698 </td>
   <td style="text-align:right;"> 1.826500 </td>
   <td style="text-align:right;"> 0.4433560 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:right;"> 19.750 </td>
   <td style="text-align:right;"> 2.3334524 </td>
   <td style="text-align:right;"> 3.337500 </td>
   <td style="text-align:right;"> 0.1732412 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:right;"> 19.750 </td>
   <td style="text-align:right;"> 1.5524175 </td>
   <td style="text-align:right;"> 3.093750 </td>
   <td style="text-align:right;"> 0.4131460 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:right;"> 5 </td>
   <td style="text-align:right;"> 19.700 </td>
   <td style="text-align:right;"> NA </td>
   <td style="text-align:right;"> 2.770000 </td>
   <td style="text-align:right;"> NA </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 8 </td>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:right;"> 15.050 </td>
   <td style="text-align:right;"> 2.7743959 </td>
   <td style="text-align:right;"> 4.104083 </td>
   <td style="text-align:right;"> 0.7683069 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 8 </td>
   <td style="text-align:right;"> 5 </td>
   <td style="text-align:right;"> 15.400 </td>
   <td style="text-align:right;"> 0.5656854 </td>
   <td style="text-align:right;"> 3.370000 </td>
   <td style="text-align:right;"> 0.2828427 </td>
  </tr>
</tbody>
</table>

</div>
</div><script> javascript:hide('option2unnamed-chunk-8') </script></div></div></div>

## Create new columns as calculations

<button id="displayTextunnamed-chunk-9" onclick="javascript:toggle('unnamed-chunk-9');">Show Solution</button>

<div id="toggleTextunnamed-chunk-9" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body"><div class="tab"><button class="tablinksunnamed-chunk-9 active" onclick="javascript:openCode(event, 'option1unnamed-chunk-9', 'unnamed-chunk-9');">Base R</button><button class="tablinksunnamed-chunk-9" onclick="javascript:openCode(event, 'option2unnamed-chunk-9', 'unnamed-chunk-9');"><tt>tidyverse</tt></button></div><div id="option1unnamed-chunk-9" class="tabcontentunnamed-chunk-9">

```r
# First operate in the data.frame by group (split-apply)
iris_by <- by(iris, 
              INDICES = iris$Species, 
              FUN = function(x){
                x$Petal.Width.centered <- x$Petal.Width - mean(x$Petal.Width)
                return(x)
              })

# Then combine the results into a data.frame
do.call(rbind, iris_by)
```
</div><div id="option2unnamed-chunk-9" class="tabcontentunnamed-chunk-9">

```r
iris %>% 
  group_by(Species) %>% 
  mutate(Petal.Width.centered = Petal.Width - mean(Petal.Width)) %>% 
  ungroup() # remove any groupings from downstream analysis
```
</div><script> javascript:hide('option2unnamed-chunk-9') </script></div></div></div>


## Filter rows with conditions evaluated by group

<button id="displayTextunnamed-chunk-10" onclick="javascript:toggle('unnamed-chunk-10');">Show Solution</button>

<div id="toggleTextunnamed-chunk-10" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body"><div class="tab"><button class="tablinksunnamed-chunk-10 active" onclick="javascript:openCode(event, 'option1unnamed-chunk-10', 'unnamed-chunk-10');">Base R</button><button class="tablinksunnamed-chunk-10" onclick="javascript:openCode(event, 'option2unnamed-chunk-10', 'unnamed-chunk-10');"><tt>tidyverse</tt></button></div><div id="option1unnamed-chunk-10" class="tabcontentunnamed-chunk-10">

```r
# First operate in the data.frame by group (split-apply)
widest_petals <- by(iris, 
                    INDICES = iris$Species, 
                    FUN = function(x){
                      x[x$Petal.Width == max(x$Petal.Width), ] 
                    })

# Then combine the results into a data.frame
do.call(rbind, widest_petals)
```

<div class="kable-table">

<table>
 <thead>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:right;"> Sepal.Length </th>
   <th style="text-align:right;"> Sepal.Width </th>
   <th style="text-align:right;"> Petal.Length </th>
   <th style="text-align:right;"> Petal.Width </th>
   <th style="text-align:left;"> Species </th>
   <th style="text-align:right;"> Petal.Ratio </th>
   <th style="text-align:right;"> Sepal.Ratio </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> setosa </td>
   <td style="text-align:right;"> 5.0 </td>
   <td style="text-align:right;"> 3.5 </td>
   <td style="text-align:right;"> 1.6 </td>
   <td style="text-align:right;"> 0.6 </td>
   <td style="text-align:left;"> setosa </td>
   <td style="text-align:right;"> 2.666667 </td>
   <td style="text-align:right;"> 1.428571 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> versicolor </td>
   <td style="text-align:right;"> 5.9 </td>
   <td style="text-align:right;"> 3.2 </td>
   <td style="text-align:right;"> 4.8 </td>
   <td style="text-align:right;"> 1.8 </td>
   <td style="text-align:left;"> versicolor </td>
   <td style="text-align:right;"> 2.666667 </td>
   <td style="text-align:right;"> 1.843750 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> virginica.101 </td>
   <td style="text-align:right;"> 6.3 </td>
   <td style="text-align:right;"> 3.3 </td>
   <td style="text-align:right;"> 6.0 </td>
   <td style="text-align:right;"> 2.5 </td>
   <td style="text-align:left;"> virginica </td>
   <td style="text-align:right;"> 2.400000 </td>
   <td style="text-align:right;"> 1.909091 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> virginica.110 </td>
   <td style="text-align:right;"> 7.2 </td>
   <td style="text-align:right;"> 3.6 </td>
   <td style="text-align:right;"> 6.1 </td>
   <td style="text-align:right;"> 2.5 </td>
   <td style="text-align:left;"> virginica </td>
   <td style="text-align:right;"> 2.440000 </td>
   <td style="text-align:right;"> 2.000000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> virginica.145 </td>
   <td style="text-align:right;"> 6.7 </td>
   <td style="text-align:right;"> 3.3 </td>
   <td style="text-align:right;"> 5.7 </td>
   <td style="text-align:right;"> 2.5 </td>
   <td style="text-align:left;"> virginica </td>
   <td style="text-align:right;"> 2.280000 </td>
   <td style="text-align:right;"> 2.030303 </td>
  </tr>
</tbody>
</table>

</div>
</div><div id="option2unnamed-chunk-10" class="tabcontentunnamed-chunk-10">

```r
iris %>% 
  group_by(Species) %>% 
  filter(Petal.Width == max(Petal.Width))
```

<div class="kable-table">

<table>
 <thead>
  <tr>
   <th style="text-align:right;"> Sepal.Length </th>
   <th style="text-align:right;"> Sepal.Width </th>
   <th style="text-align:right;"> Petal.Length </th>
   <th style="text-align:right;"> Petal.Width </th>
   <th style="text-align:left;"> Species </th>
   <th style="text-align:right;"> Petal.Ratio </th>
   <th style="text-align:right;"> Sepal.Ratio </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 5.0 </td>
   <td style="text-align:right;"> 3.5 </td>
   <td style="text-align:right;"> 1.6 </td>
   <td style="text-align:right;"> 0.6 </td>
   <td style="text-align:left;"> setosa </td>
   <td style="text-align:right;"> 2.666667 </td>
   <td style="text-align:right;"> 1.428571 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 5.9 </td>
   <td style="text-align:right;"> 3.2 </td>
   <td style="text-align:right;"> 4.8 </td>
   <td style="text-align:right;"> 1.8 </td>
   <td style="text-align:left;"> versicolor </td>
   <td style="text-align:right;"> 2.666667 </td>
   <td style="text-align:right;"> 1.843750 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 6.3 </td>
   <td style="text-align:right;"> 3.3 </td>
   <td style="text-align:right;"> 6.0 </td>
   <td style="text-align:right;"> 2.5 </td>
   <td style="text-align:left;"> virginica </td>
   <td style="text-align:right;"> 2.400000 </td>
   <td style="text-align:right;"> 1.909091 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 7.2 </td>
   <td style="text-align:right;"> 3.6 </td>
   <td style="text-align:right;"> 6.1 </td>
   <td style="text-align:right;"> 2.5 </td>
   <td style="text-align:left;"> virginica </td>
   <td style="text-align:right;"> 2.440000 </td>
   <td style="text-align:right;"> 2.000000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 6.7 </td>
   <td style="text-align:right;"> 3.3 </td>
   <td style="text-align:right;"> 5.7 </td>
   <td style="text-align:right;"> 2.5 </td>
   <td style="text-align:left;"> virginica </td>
   <td style="text-align:right;"> 2.280000 </td>
   <td style="text-align:right;"> 2.030303 </td>
  </tr>
</tbody>
</table>

</div>
</div><script> javascript:hide('option2unnamed-chunk-10') </script></div></div></div>


## Pivot data

<button id="displayTextunnamed-chunk-11" onclick="javascript:toggle('unnamed-chunk-11');">Show Solution</button>

<div id="toggleTextunnamed-chunk-11" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body"><div class="tab"><button class="tablinksunnamed-chunk-11 active" onclick="javascript:openCode(event, 'option1unnamed-chunk-11', 'unnamed-chunk-11');">Base R</button><button class="tablinksunnamed-chunk-11" onclick="javascript:openCode(event, 'option2unnamed-chunk-11', 'unnamed-chunk-11');"><tt>tidyverse</tt></button></div><div id="option1unnamed-chunk-11" class="tabcontentunnamed-chunk-11">

```r
reshape(iris, 
        varying = c("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"),
        timevar = "trait",
        idvar = "id",
        v.names = "measurement",
        direction = "long")
```
</div><div id="option2unnamed-chunk-11" class="tabcontentunnamed-chunk-11">

```r
iris %>% 
 pivot_longer(cols = Sepal.Length:Petal.Width, values_to = "measurement", names_to = "trait" )
```
</div><script> javascript:hide('option2unnamed-chunk-11') </script></div></div></div>

