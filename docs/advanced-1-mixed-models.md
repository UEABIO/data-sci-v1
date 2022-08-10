# (PART\*) Advanced topics {.unnumbered}

# Mixed models




## What is mixed modelling and why do we need it?

Ecological and biological data is often complicated and messy. We can have lots of **grouping factors** like populations, data collection sites that mean our data has clusters so that our data points are not truly **independent**. This is where **mixed models** are useful, these combine **fixed** and **random** effects to help us deal with messy data, structured data, and they help us save degrees of freedom. They are incredibly useful, but frequently tricky to implement well! 

### Fixed effects

So far in our statistics we have dealt only with **fixed effects**

**Fixed effects** are variables that are constant, or have a constant effect on the individual. For example we can argue that the effect of species on average body mass is constant, and does not change. It could be argued that these variables *could* change over time, but for research and experimental purposes are constant. We assume that the values of a fixed variable in one study should be the same as values in another study.

### Random effects

**Random effects**, these are the opposite of fixed effects. These variables have *unpredictable* effects, for example this could be the sample sites. It is perfectly plausible that data collected within different sites are more similar to each other than data from different sites. 

Unlike fixed effects we assume these values are samples drawn from a larger population of values. We are often not interested in the explicit effect of this variable, but we expect it to have an effect on the dependent variable and wish to account for it. These could be any of a number of grouping variables, for example:

* Study-site

* Repeated measurements in an individual

* Experimental replications

## The data

We are going to look at bacterial growth in four different growth media. We ran this experiment five times, in five different microbial growth cabinets


```r
head(bacteria)
```

## Simple model

## Covariates

## Mixed model

### Random slopes

Rats data - Exeter



<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
1. Plot a scatterplot of `Alcohol` vs `TotalPhenols` and colour data points by `WineType` </div></div>

<button id="displayTextunnamed-chunk-4" onclick="javascript:toggle('unnamed-chunk-4');">Show Solution</button>

<div id="toggleTextunnamed-chunk-4" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body"><div class="tab"><button class="tablinksunnamed-chunk-4 active" onclick="javascript:openCode(event, 'option1unnamed-chunk-4', 'unnamed-chunk-4');">Base R</button><button class="tablinksunnamed-chunk-4" onclick="javascript:openCode(event, 'option2unnamed-chunk-4', 'unnamed-chunk-4');"><tt>tidyverse</tt></button></div><div id="option1unnamed-chunk-4" class="tabcontentunnamed-chunk-4">

```r
plot(iris)
```

<img src="advanced-1-mixed-models_files/figure-html/unnamed-chunk-6-1.png" width="100%" style="display: block; margin: auto;" />
</div><div id="option2unnamed-chunk-4" class="tabcontentunnamed-chunk-4">

```r
plot(cars)
```

<img src="advanced-1-mixed-models_files/figure-html/unnamed-chunk-7-1.png" width="100%" style="display: block; margin: auto;" />
</div><script> javascript:hide('option2unnamed-chunk-4') </script></div></div></div>





<div class='webex-solution'><button>Solution</button>


Something


</div>




# Generalised Additive Models

# Structural equation modelling

# Unsupervised Machine Learning


