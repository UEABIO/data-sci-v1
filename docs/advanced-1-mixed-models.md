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

# Survival models

# Unsupervised Machine Learning

# Power analysis

However we may also see reports describing "large", "medium" or "small" effect sizes, how do we know if we are looking at a result with a "large" effect size? The answer is to use a method of standardisation. Interestingly there are lots of these, but we will look at one of the most common **Cohen's D**. It is simply a measure of standardising effect sizes across experiments according to the standard deviations of the differences.

<table class="table table-striped" style="width: auto !important; ">
<caption>(\#tab:unnamed-chunk-5)Cohen's D</caption>
 <thead>
  <tr>
   <th style="text-align:left;"> Effect size </th>
   <th style="text-align:right;"> d </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> very small </td>
   <td style="text-align:right;"> 0.01 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> small </td>
   <td style="text-align:right;"> 0.20 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> medium </td>
   <td style="text-align:right;"> 0.50 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> large </td>
   <td style="text-align:right;"> 0.80 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> very large </td>
   <td style="text-align:right;"> 1.20 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> huge </td>
   <td style="text-align:right;"> 2.00 </td>
  </tr>
</tbody>
</table>

For the unpaired *t*-test and then the paired *t*-test (lsmodel1, lsmodel2), see if you can use the following equations to manually calculate *d*. 

Unpaired *t*-test - the difference in means divided by the pooled standard deviation:

$$ \frac{difference}{\frac{(s^2_1+s^2_2)}{2}}$$

Paired *t*-test:

$$ \frac{t}{\sqrt(N)}$$
<details><summary> **What do you calculate as the effect size for these two analyses? Click-me for answer**</summary>

unpaired *t*-test: 0.92

paired *t*-test: 0.45

There is also a package with functions to help you calculate a range of common standardised effect size measures - it also provides confidence intervals on a standardised scale (where 0 would be no effect): 

```r
library(effectsize)


t_to_d(2.437, df_error = 28, paired = F)

t_to_d(2.456, df_error=27, paired=T)
```

<div class="kable-table">

<table>
 <thead>
  <tr>
   <th style="text-align:right;"> d </th>
   <th style="text-align:right;"> CI </th>
   <th style="text-align:right;"> CI_low </th>
   <th style="text-align:right;"> CI_high </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 0.9210994 </td>
   <td style="text-align:right;"> 0.95 </td>
   <td style="text-align:right;"> 0.1349189 </td>
   <td style="text-align:right;"> 1.692417 </td>
  </tr>
</tbody>
</table>

</div><div class="kable-table">

<table>
 <thead>
  <tr>
   <th style="text-align:right;"> d </th>
   <th style="text-align:right;"> CI </th>
   <th style="text-align:right;"> CI_low </th>
   <th style="text-align:right;"> CI_high </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 0.4726574 </td>
   <td style="text-align:right;"> 0.95 </td>
   <td style="text-align:right;"> 0.0712072 </td>
   <td style="text-align:right;"> 0.8662385 </td>
  </tr>
</tbody>
</table>

</div>
</details>

### Power


```r
library(pwr)
library(simr)
```

You don't necessarily need to report effect sizes in a write-up, it is fairly rare to see them included in a paper. It will be more useful for you to report confidence intervals on the original measurement scale. But it does provide two important pieces of information. 

1) All experiments/statistical analyses will become *statistically significant* if you make the sample size large enough. In this respect it shows how misleading a significant result can be. It is not that interesting if a result is statistically significant, but the effect size is tiny. Even without reporting *d* you can start thinking about whether confidence intervals indicate your result is *interesting*.

2) Type 2 errors. Statistical tests provide you with the probability of making a Type 1 error (rejecting the null hypothesis incorrectly) in the form of *P*. But what about Type 2 errors? Keeping the null hypothesis, when we should be rejecting it? Or not finding an effect.

The probability of making a Type 2 error is known as $1-\beta$, where $\beta$ refers to your statistical 'power'. Working out statistical power is is very straightforward for simple tests, and then becomes rapidly more diffcult as the complexity of your analysis increases... but it is an important concept to understand. 

There are two potential uses for Power analysis

1) Working out what the statistical power of you analysis was *post hoc* to determine how likely it was you missed an effect ( but see[This useful paper](https://gpsych.bmj.com/content/32/4/e100069).

2) Working out what sample size you *need* before an experiment to make sure you reach the desired power. Often a common $\beta$ value is 0.8, in much the same way that a common $\alpha$ is 0.05, it is an arbitrary target, but here means we can tolerate a risk of failing to reject the null when we should have in 20% of our experiments that do not produce a significant result. 




```r
# for n, d, sig.level and power - put values for three of the arguments and it will return the value of the fourth e.g. can you work out the power of our two sample t-test above? 
pwr.t.test(n = NULL, d = NULL, sig.level = 0.05, power = NULL,
type = c("two.sample"),
alternative = c("two.sided"))
```

**Now you know how the pwr.t.test() function works - Can you make a simple iteration to check the power for a lower effect size (d) of 0.2 for a two-sided t-test at sample sizes from 0-1000 increasing by 10 each time?**


```r
sample_size <- seq(0,1000, by=10)

output <- list(length(sample_size))



for (i in 1:length(sample_size)) { 
  
  sample <- pwr.t.test(n=sample_size[i], d=0.2, sig.level=0.05)
  output[[i]] <- sample
  
      if(i %% 1==0){    # The %% operator is the remainder, this handy if line prints a number every time it completes a loop
    print(i)
    }
}

sample_list <- as.list(sample_size)

names(output) <- sample_size

#  now you should be able to call any sample size and check statistical power!

# output$`30`
```

```
## [1] 1
## [1] 2
## [1] 3
## [1] 4
## [1] 5
## [1] 6
## [1] 7
## [1] 8
## [1] 9
## [1] 10
## [1] 11
## [1] 12
## [1] 13
## [1] 14
## [1] 15
## [1] 16
## [1] 17
## [1] 18
## [1] 19
## [1] 20
## [1] 21
## [1] 22
## [1] 23
## [1] 24
## [1] 25
## [1] 26
## [1] 27
## [1] 28
## [1] 29
## [1] 30
## [1] 31
## [1] 32
## [1] 33
## [1] 34
## [1] 35
## [1] 36
## [1] 37
## [1] 38
## [1] 39
## [1] 40
## [1] 41
## [1] 42
## [1] 43
## [1] 44
## [1] 45
## [1] 46
## [1] 47
## [1] 48
## [1] 49
## [1] 50
## [1] 51
## [1] 52
## [1] 53
## [1] 54
## [1] 55
## [1] 56
## [1] 57
## [1] 58
## [1] 59
## [1] 60
## [1] 61
## [1] 62
## [1] 63
## [1] 64
## [1] 65
## [1] 66
## [1] 67
## [1] 68
## [1] 69
## [1] 70
## [1] 71
## [1] 72
## [1] 73
## [1] 74
## [1] 75
## [1] 76
## [1] 77
## [1] 78
## [1] 79
## [1] 80
## [1] 81
## [1] 82
## [1] 83
## [1] 84
## [1] 85
## [1] 86
## [1] 87
## [1] 88
## [1] 89
## [1] 90
## [1] 91
## [1] 92
## [1] 93
## [1] 94
## [1] 95
## [1] 96
## [1] 97
## [1] 98
## [1] 99
## [1] 100
## [1] 101
```



