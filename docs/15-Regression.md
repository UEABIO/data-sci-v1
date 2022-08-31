# Regression









## Introduction to Regression

So far we have used linear models for analyses between *two* 'categorical' explanatory variables e.g. *t*-tests. But what about when we have a 'continuous' explanatory variable? For that we need to use a regression analysis, luckily this is just another 'special case' of the linear model, so we can use the same `lm()` function we have already been using, and we can interpret the outputs in the same way. 

## Linear regression

Much like the *t*-test we have generating from our linear model, the regression analysis is interpreting the strength of the 'signal' (the change in mean values according to the explanatory variable), vs the amount of 'noise' (variance around the mean). 

We would normally visualise a regression analysis with a scatter plot, with the explanatory (predictor, independent) variable on the x-axis and the response (dependent) variable on the y-axis. Individual data points are plotted, and we attempt to draw a straight-line relationship throught the cloud of data points. This line is the 'mean', and the variability around the mean is captured by calculated standard errors and confidence intervals from the variance. 

The equation for the linear regression model is:

$$ y = a + bx $$
You may also note this is basically identical to the equation for a straight fit line $y = mx +c$. 

Here: 

* *y* is the predicted value of the response variable

* *a* is the regression intercept (the value of *y* when *x* = 0)

* *b* is the slope of the regression line

* *x* is the value of the explanatory variable

This formula explains the mean, you would need to include the unexplained residual error as a term to include our measure of uncertainty

$$ y = a + bx + e $$

The regression uses two values to fit a straight line. First we need a starting point, known as the regression intercept. For categorical predictors this is the mean value of *y* for one of our categories, for a regression this is the mean value of *y* when *x* = 0. We then need a gradient (how the value of *y* changes when the value of *x* changes). This allows us to draw a regression line. 

A linear model analysis estimates the values of the intercept and gradient in order to predict values of *y* for given values of *x*. 

## Data

Here we are going to use example data from the Australian forestry industry, recording the density and hardness of 36 samples of wood from different tree species. Wood density is a fundamental property that is relatively easy to measure, timber hardness, is quantified as the 'the amount of force required to embed a 0.444" steel ball into the wood to half of its diameter'. 

With regression, we can test the biological hypothesis that wood density can be used to predict timber hardness, and use this regression to predict timber hardness for new samples of known density. 

Timber hardness is quantified using the 'Janka scale', and the data we are going to use today comes from an R package 'SemiPar' - once loaded you will then need to call the data using another function `data()` (note this is different to PalmerPenguins where the data was immediately available).




```{=html}
<a href="https://raw.githubusercontent.com/UEABIO/data-sci-v1/main/book/files/janka.csv">
<button class="btn btn-success"><i class="fa fa-save"></i> Download Janka data as csv</button>
</a>
```

<div class="try">
<p>Check the data is imported correctly and make sure it is 'tidy' with no obvious errors or missing data</p>
</div>

<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
Is there any visual evidence for a linear association between wood density and timber hardness? </div></div>

<button id="displayTextunnamed-chunk-7" onclick="javascript:toggle('unnamed-chunk-7');">Show Solution</button>

<div id="toggleTextunnamed-chunk-7" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

```r
janka %>% 
  ggplot(aes(x=dens, y=hardness))+
  geom_point()
```

<img src="15-Regression_files/figure-html/unnamed-chunk-36-1.png" width="100%" style="display: block; margin: auto;" />
</div></div></div>

## Correlation

Wood density and timber hardness appear to be positively related, and the linear appears to be fairly linear. We can look at a simple strength of this association between dens and hardness using correlation

<button id="displayTextunnamed-chunk-8" onclick="javascript:toggle('unnamed-chunk-8');">Show Solution</button>

<div id="toggleTextunnamed-chunk-8" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body"><div class="tab"><button class="tablinksunnamed-chunk-8 active" onclick="javascript:openCode(event, 'option1unnamed-chunk-8', 'unnamed-chunk-8');">Base R</button><button class="tablinksunnamed-chunk-8" onclick="javascript:openCode(event, 'option2unnamed-chunk-8', 'unnamed-chunk-8');"><tt>tidyverse</tt></button></div><div id="option1unnamed-chunk-8" class="tabcontentunnamed-chunk-8">

```r
# cor() does not have a data option so need to use the with() function
with(janka, cor(dens, hardness))
```

```
## [1] 0.9743345
```
</div><div id="option2unnamed-chunk-8" class="tabcontentunnamed-chunk-8">

```r
library(rstatix)

janka %>% 
  cor_test(dens, hardness)
```

<div class="kable-table">

<table>
 <thead>
  <tr>
   <th style="text-align:left;"> var1 </th>
   <th style="text-align:left;"> var2 </th>
   <th style="text-align:right;"> cor </th>
   <th style="text-align:right;"> statistic </th>
   <th style="text-align:right;"> p </th>
   <th style="text-align:right;"> conf.low </th>
   <th style="text-align:right;"> conf.high </th>
   <th style="text-align:left;"> method </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> dens </td>
   <td style="text-align:left;"> hardness </td>
   <td style="text-align:right;"> 0.97 </td>
   <td style="text-align:right;"> 25.23845 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 0.949849 </td>
   <td style="text-align:right;"> 0.9869454 </td>
   <td style="text-align:left;"> Pearson </td>
  </tr>
</tbody>
</table>

</div>
</div><script> javascript:hide('option2unnamed-chunk-8') </script></div></div></div>


Correlation coefficients range from -1 to 1 for perfectly negative to perfectly positive linear relationships. The relationship here appears to be strongly positive. Correlation looks at the **association** between two variables, but we want to go further - we are arguing that wood density *causes* higher values of timber hardness. In order to test that hypothesis we need to go further than correlation and use regression.

## Regression in R

We can fit the regression model in exactly the same way as we fit the linear model for Darwin's maize data. The *only* difference is that here our predictor variable is continuous rather than categorical. 

<div class="warning">
<p>Be careful when ordering variables here:</p>
<ul>
<li><p>the left of the 'tilde' is the response variable,</p></li>
<li><p>on the right is the predictor.</p></li>
</ul>
<p>Get them the wrong way round and it will reverse your hypothesis.</p>
</div>


```r
janka_ls1 <- lm(hardness ~ dens, data = janka) 
```

This linear model will estimate a 'line of best fit' using the method of 'least squares' to minimise the error sums of squares (the average distance between the data points and the regression line). 

We can add a regression line to our ggplots very easily with the function `geom_smooth()`.


```r
janka %>% 
  ggplot(aes(x=dens, y=hardness))+
  geom_point()+
  geom_smooth(method="lm")
```

<img src="15-Regression_files/figure-html/unnamed-chunk-11-1.png" width="100%" style="display: block; margin: auto;" />

```r
  # specify linear model method for line fitting
```

**Q. The blue line represents the regression line, and the shaded interval is the 95% confidence interval band. What do you notice about the width of the interval band as you move along the regression line?**


<div class='webex-solution'><button>Explain this</button>


The 95% confidence interval band is narrowest in the middle and widest at either end of the regression line. But why?

When performing a linear regression, there are **two** types of uncertainty in the prediction.

First is the prediction of the overall mean of the estimate (ie the center of the fit). The second is the uncertainly in the estimate calculating the slope.

So when you combine both uncertainties of the prediction there is a spread between the high and low estimates. The further away from the center of the data you get (in either direction), the uncertainty of the slope becomes a large and more noticeable factor, thus the limits widen.


</div>


### Summary


```r
janka_ls1 %>% 
  broom::tidy()

# base R summary(janka_ls1)
```

<div class="kable-table">

<table>
 <thead>
  <tr>
   <th style="text-align:left;"> term </th>
   <th style="text-align:right;"> estimate </th>
   <th style="text-align:right;"> std.error </th>
   <th style="text-align:right;"> statistic </th>
   <th style="text-align:right;"> p.value </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> (Intercept) </td>
   <td style="text-align:right;"> -1160.49970 </td>
   <td style="text-align:right;"> 108.579605 </td>
   <td style="text-align:right;"> -10.68801 </td>
   <td style="text-align:right;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dens </td>
   <td style="text-align:right;"> 57.50667 </td>
   <td style="text-align:right;"> 2.278534 </td>
   <td style="text-align:right;"> 25.23845 </td>
   <td style="text-align:right;"> 0 </td>
  </tr>
</tbody>
</table>

</div>

This output should look very familiar to you, because it's the same output produced for the analysis of the maize data. Including a column for the coefficient estimates, standard error, *t*-statistic and *P*-value. The first row is the intercept, and the second row is the difference in the mean from the intercept caused by our explanantory variable. 

In many ways the intercept makes more intuitive sense in a regression model than a difference model. Here the intercept describes the value of *y* (timber hardness) when *x* (wood density) = 0. The standard error is standard error of this calculated mean value. The only wrinkle here is that that value of *y* is an impossible value - timber hardness obviously cannot be a negative value (anti-hardness???). This does not affect the fit of our line, it just means a regression line (being an infinite straight line) can move into impossible value ranges.

One way in which the intercept can be made more valuable is to use a technique known as 'centering'. By subtracting the average (mean) value of *x* from every data point, the intercept (when *x* is 0) can effectively be right-shifted into the centre of the data. 

<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
Try it for yourself, use your data manipulation skills to 'center' the values of x then fit a new linear model. </div></div>

<button id="displayTextunnamed-chunk-14" onclick="javascript:toggle('unnamed-chunk-14');">Show Solution</button>

<div id="toggleTextunnamed-chunk-14" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

```r
dens_mean <- janka %>% 
  summarise(mean_dens=mean(dens))
# 45.73333

janka %>% 
  mutate(centered_dens = dens-dens_mean[,1]) %>% 
  lm(hardness ~ centered_dens, data = .) %>% 
  broom::tidy()
```

<div class="kable-table">

<table>
 <thead>
  <tr>
   <th style="text-align:left;"> term </th>
   <th style="text-align:right;"> estimate </th>
   <th style="text-align:right;"> std.error </th>
   <th style="text-align:right;"> statistic </th>
   <th style="text-align:right;"> p.value </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> (Intercept) </td>
   <td style="text-align:right;"> 1469.47222 </td>
   <td style="text-align:right;"> 30.509916 </td>
   <td style="text-align:right;"> 48.16376 </td>
   <td style="text-align:right;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> centered_dens </td>
   <td style="text-align:right;"> 57.50667 </td>
   <td style="text-align:right;"> 2.278534 </td>
   <td style="text-align:right;"> 25.23845 </td>
   <td style="text-align:right;"> 0 </td>
  </tr>
</tbody>
</table>

</div>
</div></div></div>


<div class="info">
<p>Note how the estimate for row 2 - the effect of density on timber hardness <strong>has not</strong> changed, but the intercept now represents the estimated mean timber hardness for the mean wood density e.g. at a density of <span class="math inline">\(\rho\)</span> = 45.73 the average timber hardness on the janka scale is 1469.</p>
</div>

### the second row

The second row is labelled 'dens'. Density is our explanatory variable, and the slope is estimated against it. So if 57.5 is the value of the regression slope (with its standard error) - then the timber hardness is predicted to **increase** by 57.5 on the janka scale for every unit change of density. 

According to our model summary, this estimated change in the mean is statistically significant  - so for this effect size and sample size it is unlikely that we would observe this relationship if the null hypothesis (that we cannot predict timber hardness from wood density) were true. 

### Confidence intervals

Just like with the maize data, we can produce upper and lower bounds of confidence intervals: 


```r
broom::tidy(janka_ls1, conf.int=T, conf.level=0.95)

# base r
# confint(lsmodel1)
```

<div class="kable-table">

<table>
 <thead>
  <tr>
   <th style="text-align:left;"> term </th>
   <th style="text-align:right;"> estimate </th>
   <th style="text-align:right;"> std.error </th>
   <th style="text-align:right;"> statistic </th>
   <th style="text-align:right;"> p.value </th>
   <th style="text-align:right;"> conf.low </th>
   <th style="text-align:right;"> conf.high </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> (Intercept) </td>
   <td style="text-align:right;"> -1160.49970 </td>
   <td style="text-align:right;"> 108.579605 </td>
   <td style="text-align:right;"> -10.68801 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> -1381.16001 </td>
   <td style="text-align:right;"> -939.83940 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dens </td>
   <td style="text-align:right;"> 57.50667 </td>
   <td style="text-align:right;"> 2.278534 </td>
   <td style="text-align:right;"> 25.23845 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 52.87614 </td>
   <td style="text-align:right;"> 62.13721 </td>
  </tr>
</tbody>
</table>

</div>

Here we can say that at $\alpha$ = 0.05 we think there is at least a 52.9 unit increase on the janka scale for every unit increase in density ($\rho$). Because our 95% confidence intervals do not span 0, we know that there is a significant relationship at $\alpha$ = 0.05. 

### Effect size

With a regression model, we can also produce a standardised effect size. The estimate and 95% confidence intervals are the amount of change being observed, but just like with the maize data we can produce a standardised measure of how strong the relationship is. This value is represented by $R^2$ : the proportion of the variation in the data explained by the linear regression analysis. 

The value of $R^2$ can be found in the model summaries as follows


```r
janka_ls1 %>% 
  broom::glance()

# base r
# summary(janka_ls1)
```

<div class="kable-table">

<table>
 <thead>
  <tr>
   <th style="text-align:right;"> r.squared </th>
   <th style="text-align:right;"> adj.r.squared </th>
   <th style="text-align:right;"> sigma </th>
   <th style="text-align:right;"> statistic </th>
   <th style="text-align:right;"> p.value </th>
   <th style="text-align:right;"> df </th>
   <th style="text-align:right;"> logLik </th>
   <th style="text-align:right;"> AIC </th>
   <th style="text-align:right;"> BIC </th>
   <th style="text-align:right;"> deviance </th>
   <th style="text-align:right;"> df.residual </th>
   <th style="text-align:right;"> nobs </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 0.9493278 </td>
   <td style="text-align:right;"> 0.9478374 </td>
   <td style="text-align:right;"> 183.0595 </td>
   <td style="text-align:right;"> 636.9794 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> -237.6061 </td>
   <td style="text-align:right;"> 481.2123 </td>
   <td style="text-align:right;"> 485.9628 </td>
   <td style="text-align:right;"> 1139366 </td>
   <td style="text-align:right;"> 34 </td>
   <td style="text-align:right;"> 36 </td>
  </tr>
</tbody>
</table>

</div>


<table class="table table-striped" style="width: auto !important; ">
<caption>(\#tab:unnamed-chunk-18)R squared effect size</caption>
 <thead>
  <tr>
   <th style="text-align:left;"> Effect size </th>
   <th style="text-align:right;"> r^2 </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> small </td>
   <td style="text-align:right;"> 0.1 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> medium </td>
   <td style="text-align:right;"> 0.3 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> large </td>
   <td style="text-align:right;"> 0.5 </td>
  </tr>
</tbody>
</table>

## Assumptions

Regression models make ALL the same assumptions as all linear models - that the unexplained variation around the regression line (the residuals) is approximately normally distributed, and has constant variance. And we can check this in the same way.

Remember, the residuals are the *difference* between the observed values and the fitted values predicted by the model. Or in other words it is the *vertical* distance between a data point and the fitted value on the regression line. We can take a look at this with another function in the `broom` package `augment()`. This generates the predicted value for each data point according to the regression, and calculates the residuals for each data point. 

<button id="displayTextunnamed-chunk-19" onclick="javascript:toggle('unnamed-chunk-19');">Show Solution</button>

<div id="toggleTextunnamed-chunk-19" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body"><div class="tab"><button class="tablinksunnamed-chunk-19 active" onclick="javascript:openCode(event, 'option1unnamed-chunk-19', 'unnamed-chunk-19');">Base R</button><button class="tablinksunnamed-chunk-19" onclick="javascript:openCode(event, 'option2unnamed-chunk-19', 'unnamed-chunk-19');"><tt>tidyverse</tt></button></div><div id="option1unnamed-chunk-19" class="tabcontentunnamed-chunk-19">

```r
predict(janka_ls1)

resid(janka_ls1)
```

```
##         1         2         3         4         5         6         7         8 
##  259.9152  265.6658  409.4325  472.6899  472.6899  507.1939  581.9525  719.9686 
##         9        10        11        12        13        14        15        16 
##  886.7379 1053.5073 1070.7593 1099.5126 1105.2633 1134.0166 1157.0193 1174.2713 
##        17        18        19        20        21        22        23        24 
## 1180.0220 1180.0220 1306.5366 1473.3060 1536.5633 1611.3220 1801.0940 1801.0940 
##        25        26        27        28        29        30        31        32 
## 1910.3567 2059.8741 2088.6274 2134.6328 2151.8848 2243.8954 2278.3994 2634.9408 
##        33        34        35        36 
## 2715.4502 2795.9595 2813.2115 2813.2115 
##            1            2            3            4            5            6 
##  224.0848370  161.3341695    3.5674826   44.3101404   76.3101404  140.8061355 
##            7            8            9           10           11           12 
##    5.0474583  -15.9685611   92.2620821 -139.5072748   -0.7592772  -79.5126146 
##           13           14           15           16           17           18 
##  104.7367180 -145.0166194    2.9807107 -164.2712918  -80.0219592  -50.0219592 
##           19           20           21           22           23           24 
##  -36.5366437 -293.3060005 -136.5633428  148.6779800  -91.0940467  208.9059533 
##           25           26           27           28           29           30 
##  -30.3567287  -79.8740831 -268.6274205 -114.6327603 -171.8847628   66.1045576 
##           31           32           33           34           35           36 
## -338.3994472  625.0591692  -15.4501754   94.0404799  -73.2115225  326.7884775
```
</div><div id="option2unnamed-chunk-19" class="tabcontentunnamed-chunk-19">

```r
janka_ls1 %>% 
  broom::augment()
```

<div class="kable-table">

<table>
 <thead>
  <tr>
   <th style="text-align:right;"> hardness </th>
   <th style="text-align:right;"> dens </th>
   <th style="text-align:right;"> .fitted </th>
   <th style="text-align:right;"> .resid </th>
   <th style="text-align:right;"> .hat </th>
   <th style="text-align:right;"> .sigma </th>
   <th style="text-align:right;"> .cooksd </th>
   <th style="text-align:right;"> .std.resid </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 484 </td>
   <td style="text-align:right;"> 24.7 </td>
   <td style="text-align:right;"> 259.9152 </td>
   <td style="text-align:right;"> 224.0848370 </td>
   <td style="text-align:right;"> 0.0963176 </td>
   <td style="text-align:right;"> 181.2248 </td>
   <td style="text-align:right;"> 0.0883658 </td>
   <td style="text-align:right;"> 1.2876929 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 427 </td>
   <td style="text-align:right;"> 24.8 </td>
   <td style="text-align:right;"> 265.6658 </td>
   <td style="text-align:right;"> 161.3341695 </td>
   <td style="text-align:right;"> 0.0956674 </td>
   <td style="text-align:right;"> 183.4505 </td>
   <td style="text-align:right;"> 0.0454303 </td>
   <td style="text-align:right;"> 0.9267658 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 413 </td>
   <td style="text-align:right;"> 27.3 </td>
   <td style="text-align:right;"> 409.4325 </td>
   <td style="text-align:right;"> 3.5674826 </td>
   <td style="text-align:right;"> 0.0804200 </td>
   <td style="text-align:right;"> 185.8113 </td>
   <td style="text-align:right;"> 0.0000181 </td>
   <td style="text-align:right;"> 0.0203224 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 517 </td>
   <td style="text-align:right;"> 28.4 </td>
   <td style="text-align:right;"> 472.6899 </td>
   <td style="text-align:right;"> 44.3101404 </td>
   <td style="text-align:right;"> 0.0743247 </td>
   <td style="text-align:right;"> 185.6394 </td>
   <td style="text-align:right;"> 0.0025410 </td>
   <td style="text-align:right;"> 0.2515831 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 549 </td>
   <td style="text-align:right;"> 28.4 </td>
   <td style="text-align:right;"> 472.6899 </td>
   <td style="text-align:right;"> 76.3101404 </td>
   <td style="text-align:right;"> 0.0743247 </td>
   <td style="text-align:right;"> 185.2987 </td>
   <td style="text-align:right;"> 0.0075364 </td>
   <td style="text-align:right;"> 0.4332720 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 648 </td>
   <td style="text-align:right;"> 29.0 </td>
   <td style="text-align:right;"> 507.1939 </td>
   <td style="text-align:right;"> 140.8061355 </td>
   <td style="text-align:right;"> 0.0711580 </td>
   <td style="text-align:right;"> 184.0637 </td>
   <td style="text-align:right;"> 0.0243988 </td>
   <td style="text-align:right;"> 0.7981020 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 587 </td>
   <td style="text-align:right;"> 30.3 </td>
   <td style="text-align:right;"> 581.9525 </td>
   <td style="text-align:right;"> 5.0474583 </td>
   <td style="text-align:right;"> 0.0646795 </td>
   <td style="text-align:right;"> 185.8102 </td>
   <td style="text-align:right;"> 0.0000281 </td>
   <td style="text-align:right;"> 0.0285102 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 704 </td>
   <td style="text-align:right;"> 32.7 </td>
   <td style="text-align:right;"> 719.9686 </td>
   <td style="text-align:right;"> -15.9685611 </td>
   <td style="text-align:right;"> 0.0540949 </td>
   <td style="text-align:right;"> 185.7904 </td>
   <td style="text-align:right;"> 0.0002300 </td>
   <td style="text-align:right;"> -0.0896912 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 979 </td>
   <td style="text-align:right;"> 35.6 </td>
   <td style="text-align:right;"> 886.7379 </td>
   <td style="text-align:right;"> 92.2620821 </td>
   <td style="text-align:right;"> 0.0436864 </td>
   <td style="text-align:right;"> 185.0852 </td>
   <td style="text-align:right;"> 0.0060670 </td>
   <td style="text-align:right;"> 0.5153839 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 914 </td>
   <td style="text-align:right;"> 38.5 </td>
   <td style="text-align:right;"> 1053.5073 </td>
   <td style="text-align:right;"> -139.5072748 </td>
   <td style="text-align:right;"> 0.0358837 </td>
   <td style="text-align:right;"> 184.1590 </td>
   <td style="text-align:right;"> 0.0112103 </td>
   <td style="text-align:right;"> -0.7761397 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1070 </td>
   <td style="text-align:right;"> 38.8 </td>
   <td style="text-align:right;"> 1070.7593 </td>
   <td style="text-align:right;"> -0.7592772 </td>
   <td style="text-align:right;"> 0.0352253 </td>
   <td style="text-align:right;"> 185.8124 </td>
   <td style="text-align:right;"> 0.0000003 </td>
   <td style="text-align:right;"> -0.0042227 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1020 </td>
   <td style="text-align:right;"> 39.3 </td>
   <td style="text-align:right;"> 1099.5126 </td>
   <td style="text-align:right;"> -79.5126146 </td>
   <td style="text-align:right;"> 0.0341899 </td>
   <td style="text-align:right;"> 185.2779 </td>
   <td style="text-align:right;"> 0.0034576 </td>
   <td style="text-align:right;"> -0.4419752 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1210 </td>
   <td style="text-align:right;"> 39.4 </td>
   <td style="text-align:right;"> 1105.2633 </td>
   <td style="text-align:right;"> 104.7367180 </td>
   <td style="text-align:right;"> 0.0339921 </td>
   <td style="text-align:right;"> 184.8841 </td>
   <td style="text-align:right;"> 0.0059621 </td>
   <td style="text-align:right;"> 0.5821251 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 989 </td>
   <td style="text-align:right;"> 39.9 </td>
   <td style="text-align:right;"> 1134.0166 </td>
   <td style="text-align:right;"> -145.0166194 </td>
   <td style="text-align:right;"> 0.0330496 </td>
   <td style="text-align:right;"> 184.0305 </td>
   <td style="text-align:right;"> 0.0110912 </td>
   <td style="text-align:right;"> -0.8056073 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1160 </td>
   <td style="text-align:right;"> 40.3 </td>
   <td style="text-align:right;"> 1157.0193 </td>
   <td style="text-align:right;"> 2.9807107 </td>
   <td style="text-align:right;"> 0.0323514 </td>
   <td style="text-align:right;"> 185.8117 </td>
   <td style="text-align:right;"> 0.0000046 </td>
   <td style="text-align:right;"> 0.0165527 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1010 </td>
   <td style="text-align:right;"> 40.6 </td>
   <td style="text-align:right;"> 1174.2713 </td>
   <td style="text-align:right;"> -164.2712918 </td>
   <td style="text-align:right;"> 0.0318603 </td>
   <td style="text-align:right;"> 183.5255 </td>
   <td style="text-align:right;"> 0.0136862 </td>
   <td style="text-align:right;"> -0.9120117 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1100 </td>
   <td style="text-align:right;"> 40.7 </td>
   <td style="text-align:right;"> 1180.0220 </td>
   <td style="text-align:right;"> -80.0219592 </td>
   <td style="text-align:right;"> 0.0317028 </td>
   <td style="text-align:right;"> 185.2724 </td>
   <td style="text-align:right;"> 0.0032306 </td>
   <td style="text-align:right;"> -0.4442348 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1130 </td>
   <td style="text-align:right;"> 40.7 </td>
   <td style="text-align:right;"> 1180.0220 </td>
   <td style="text-align:right;"> -50.0219592 </td>
   <td style="text-align:right;"> 0.0317028 </td>
   <td style="text-align:right;"> 185.6016 </td>
   <td style="text-align:right;"> 0.0012624 </td>
   <td style="text-align:right;"> -0.2776925 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1270 </td>
   <td style="text-align:right;"> 42.9 </td>
   <td style="text-align:right;"> 1306.5366 </td>
   <td style="text-align:right;"> -36.5366437 </td>
   <td style="text-align:right;"> 0.0290215 </td>
   <td style="text-align:right;"> 185.7003 </td>
   <td style="text-align:right;"> 0.0006131 </td>
   <td style="text-align:right;"> -0.2025497 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1180 </td>
   <td style="text-align:right;"> 45.8 </td>
   <td style="text-align:right;"> 1473.3060 </td>
   <td style="text-align:right;"> -293.3060005 </td>
   <td style="text-align:right;"> 0.0277785 </td>
   <td style="text-align:right;"> 178.4513 </td>
   <td style="text-align:right;"> 0.0377229 </td>
   <td style="text-align:right;"> -1.6249727 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1400 </td>
   <td style="text-align:right;"> 46.9 </td>
   <td style="text-align:right;"> 1536.5633 </td>
   <td style="text-align:right;"> -136.5633428 </td>
   <td style="text-align:right;"> 0.0279887 </td>
   <td style="text-align:right;"> 184.2413 </td>
   <td style="text-align:right;"> 0.0082431 </td>
   <td style="text-align:right;"> -0.7566695 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1760 </td>
   <td style="text-align:right;"> 48.2 </td>
   <td style="text-align:right;"> 1611.3220 </td>
   <td style="text-align:right;"> 148.6779800 </td>
   <td style="text-align:right;"> 0.0287204 </td>
   <td style="text-align:right;"> 183.9473 </td>
   <td style="text-align:right;"> 0.0100411 </td>
   <td style="text-align:right;"> 0.8241045 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1710 </td>
   <td style="text-align:right;"> 51.5 </td>
   <td style="text-align:right;"> 1801.0940 </td>
   <td style="text-align:right;"> -91.0940467 </td>
   <td style="text-align:right;"> 0.0329298 </td>
   <td style="text-align:right;"> 185.1114 </td>
   <td style="text-align:right;"> 0.0043595 </td>
   <td style="text-align:right;"> -0.5060212 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2010 </td>
   <td style="text-align:right;"> 51.5 </td>
   <td style="text-align:right;"> 1801.0940 </td>
   <td style="text-align:right;"> 208.9059533 </td>
   <td style="text-align:right;"> 0.0329298 </td>
   <td style="text-align:right;"> 182.0954 </td>
   <td style="text-align:right;"> 0.0229277 </td>
   <td style="text-align:right;"> 1.1604583 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1880 </td>
   <td style="text-align:right;"> 53.4 </td>
   <td style="text-align:right;"> 1910.3567 </td>
   <td style="text-align:right;"> -30.3567287 </td>
   <td style="text-align:right;"> 0.0368840 </td>
   <td style="text-align:right;"> 185.7344 </td>
   <td style="text-align:right;"> 0.0005467 </td>
   <td style="text-align:right;"> -0.1689754 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1980 </td>
   <td style="text-align:right;"> 56.0 </td>
   <td style="text-align:right;"> 2059.8741 </td>
   <td style="text-align:right;"> -79.8740831 </td>
   <td style="text-align:right;"> 0.0441078 </td>
   <td style="text-align:right;"> 185.2674 </td>
   <td style="text-align:right;"> 0.0045951 </td>
   <td style="text-align:right;"> -0.4462818 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1820 </td>
   <td style="text-align:right;"> 56.5 </td>
   <td style="text-align:right;"> 2088.6274 </td>
   <td style="text-align:right;"> -268.6274205 </td>
   <td style="text-align:right;"> 0.0457371 </td>
   <td style="text-align:right;"> 179.5404 </td>
   <td style="text-align:right;"> 0.0540777 </td>
   <td style="text-align:right;"> -1.5021872 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2020 </td>
   <td style="text-align:right;"> 57.3 </td>
   <td style="text-align:right;"> 2134.6328 </td>
   <td style="text-align:right;"> -114.6327603 </td>
   <td style="text-align:right;"> 0.0485051 </td>
   <td style="text-align:right;"> 184.6829 </td>
   <td style="text-align:right;"> 0.0105045 </td>
   <td style="text-align:right;"> -0.6419678 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1980 </td>
   <td style="text-align:right;"> 57.6 </td>
   <td style="text-align:right;"> 2151.8848 </td>
   <td style="text-align:right;"> -171.8847628 </td>
   <td style="text-align:right;"> 0.0495942 </td>
   <td style="text-align:right;"> 183.2601 </td>
   <td style="text-align:right;"> 0.0242032 </td>
   <td style="text-align:right;"> -0.9631426 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2310 </td>
   <td style="text-align:right;"> 59.2 </td>
   <td style="text-align:right;"> 2243.8954 </td>
   <td style="text-align:right;"> 66.1045576 </td>
   <td style="text-align:right;"> 0.0558739 </td>
   <td style="text-align:right;"> 185.4346 </td>
   <td style="text-align:right;"> 0.0040869 </td>
   <td style="text-align:right;"> 0.3716415 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1940 </td>
   <td style="text-align:right;"> 59.8 </td>
   <td style="text-align:right;"> 2278.3994 </td>
   <td style="text-align:right;"> -338.3994472 </td>
   <td style="text-align:right;"> 0.0584333 </td>
   <td style="text-align:right;"> 175.6154 </td>
   <td style="text-align:right;"> 0.1126168 </td>
   <td style="text-align:right;"> -1.9050740 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 3260 </td>
   <td style="text-align:right;"> 66.0 </td>
   <td style="text-align:right;"> 2634.9408 </td>
   <td style="text-align:right;"> 625.0591692 </td>
   <td style="text-align:right;"> 0.0914121 </td>
   <td style="text-align:right;"> 146.6143 </td>
   <td style="text-align:right;"> 0.6455017 </td>
   <td style="text-align:right;"> 3.5821634 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2700 </td>
   <td style="text-align:right;"> 67.4 </td>
   <td style="text-align:right;"> 2715.4502 </td>
   <td style="text-align:right;"> -15.4501754 </td>
   <td style="text-align:right;"> 0.1005073 </td>
   <td style="text-align:right;"> 185.7908 </td>
   <td style="text-align:right;"> 0.0004424 </td>
   <td style="text-align:right;"> -0.0889902 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2890 </td>
   <td style="text-align:right;"> 68.8 </td>
   <td style="text-align:right;"> 2795.9595 </td>
   <td style="text-align:right;"> 94.0404799 </td>
   <td style="text-align:right;"> 0.1102099 </td>
   <td style="text-align:right;"> 185.0002 </td>
   <td style="text-align:right;"> 0.0183679 </td>
   <td style="text-align:right;"> 0.5446014 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2740 </td>
   <td style="text-align:right;"> 69.1 </td>
   <td style="text-align:right;"> 2813.2115 </td>
   <td style="text-align:right;"> -73.2115225 </td>
   <td style="text-align:right;"> 0.1123680 </td>
   <td style="text-align:right;"> 185.3194 </td>
   <td style="text-align:right;"> 0.0114057 </td>
   <td style="text-align:right;"> -0.4244932 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 3140 </td>
   <td style="text-align:right;"> 69.1 </td>
   <td style="text-align:right;"> 2813.2115 </td>
   <td style="text-align:right;"> 326.7884775 </td>
   <td style="text-align:right;"> 0.1123680 </td>
   <td style="text-align:right;"> 175.7285 </td>
   <td style="text-align:right;"> 0.2272457 </td>
   <td style="text-align:right;"> 1.8947765 </td>
  </tr>
</tbody>
</table>

</div>
</div><script> javascript:hide('option2unnamed-chunk-19') </script></div></div></div>

If we plot this, with a black fitted regression line and red dashed lines representing the residuals:


```r
augmented_ls1 <- janka_ls1 %>% 
  broom::augment()

augmented_ls1 %>% 
    ggplot(aes(x=dens, 
               y=.fitted))+
    geom_line()+ 
  geom_point(aes(x=dens, 
                 y=hardness))+
  geom_segment(aes(x=dens, 
                   xend=dens, 
                   y=.fitted, 
                   yend=hardness), 
               linetype="dashed", colour="red")
```

<img src="15-Regression_files/figure-html/unnamed-chunk-20-1.png" width="100%" style="display: block; margin: auto;" />

We can use this augmented data to really help us understand what residual variance looks like, and how it can be used to diagnose our models. A perfect model would mean that all of our residual values = 0, but this is incredibly unlikely to ever occur. Instead we would like to see 

1) that there is a 'normal distribution' to the residuals e.g. more residuals close to the mean, and fewer further away in a rough z-distribution. 

2) We also want to see homogeneity of the residuals e.g. it would be a bad model if the average error was greater at one end of the model than the other. This might mean we have more uncertainty in the slope of the line for large values over small values or vice versa. 


```r
# A line connecting all the data points in order 
p1 <- augmented_ls1 %>% 
  ggplot(aes(x=dens, y=hardness))+
  geom_line()+
  ggtitle("Full Data")

# Plotting the fitted values against the independent e.g. our regression line
p2 <- augmented_ls1 %>% 
  ggplot(aes(x=dens, y=.fitted))+
  geom_line()+
  ggtitle("Linear trend")

# Plotting the residuals against the fitted values e.g. remaining variance
p3 <- augmented_ls1 %>% 
  ggplot(aes(x=.fitted, y=.resid))+
  geom_hline(yintercept=0, colour="white", size=5)+
  geom_line()+
  ggtitle("Remaining \npattern")


library(patchwork)
p1+p2+p3
```

<img src="15-Regression_files/figure-html/unnamed-chunk-21-1.png" width="100%" style="display: block; margin: auto;" />


<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
The above is an example of functional, but repetitive code - could you make a function that reduces the amount of code needed?

HINT - to make sure your arguments for a ggplot are passed properly use this structure x=.data[[x]] , y = .data[[y]] </div></div>


<button id="displayTextunnamed-chunk-23" onclick="javascript:toggle('unnamed-chunk-23');">Show Solution</button>

<div id="toggleTextunnamed-chunk-23" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

```r
model_plot <- function(data=augmented_ls1, 
                       x="dens", 
                       y="hardness", 
                       title="Full data"){
  ggplot(aes(x=.data[[x]], 
             y=.data[[y]]), 
         data=data)+
  geom_line()+
    theme_bw()+
      ggtitle(title)
}

p1 <- model_plot()
p2 <- model_plot(y=".fitted", title="Linear prediction")
p3 <- model_plot(y=".resid", title="Remaining pattern")
```
</div></div></div>


### Normal distribution

We can use the same model diagnostic plots as we used for the maize data.
Here you can see it is mostly pretty good, with just one or two data points outside of the confidence intervals

<button id="displayTextunnamed-chunk-24" onclick="javascript:toggle('unnamed-chunk-24');">Show Solution</button>

<div id="toggleTextunnamed-chunk-24" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body"><div class="tab"><button class="tablinksunnamed-chunk-24 active" onclick="javascript:openCode(event, 'option1unnamed-chunk-24', 'unnamed-chunk-24');">Base R</button><button class="tablinksunnamed-chunk-24" onclick="javascript:openCode(event, 'option2unnamed-chunk-24', 'unnamed-chunk-24');"><tt>tidyverse</tt></button></div><div id="option1unnamed-chunk-24" class="tabcontentunnamed-chunk-24">

```r
plot(janka_ls1, which=c(2,2))
```

<img src="15-Regression_files/figure-html/unnamed-chunk-39-1.png" width="100%" style="display: block; margin: auto;" />
</div><div id="option2unnamed-chunk-24" class="tabcontentunnamed-chunk-24">

```r
performance::check_model(janka_ls1, check=c("normality","qq"))
```

<img src="15-Regression_files/figure-html/unnamed-chunk-40-1.png" width="100%" style="display: block; margin: auto;" />
</div><script> javascript:hide('option2unnamed-chunk-24') </script></div></div></div>


### Equal variance

We can use the same model diagnostic plots as we used for the maize data. 
You should see that this is similar to the `p3` plot we constructed manually. With the plot we constructed earlier we had the 'raw' residuals as a function of the fitted values. The plot we have produced now is the 'standardized residuals' - this is the raw residual divided by the standard deviation.

Both plots suggests that the residuals **do not** have constant variance, broadly speaking the amount of variance *y* increases as *x* increases. This means we have less confidence in our predictions at high values of density. Later we will see what we can do to improve the fit of this model

<button id="displayTextunnamed-chunk-25" onclick="javascript:toggle('unnamed-chunk-25');">Show Solution</button>

<div id="toggleTextunnamed-chunk-25" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body"><div class="tab"><button class="tablinksunnamed-chunk-25 active" onclick="javascript:openCode(event, 'option1unnamed-chunk-25', 'unnamed-chunk-25');">Base R</button><button class="tablinksunnamed-chunk-25" onclick="javascript:openCode(event, 'option2unnamed-chunk-25', 'unnamed-chunk-25');"><tt>tidyverse</tt></button></div><div id="option1unnamed-chunk-25" class="tabcontentunnamed-chunk-25">

```r
plot(janka_ls1, which=c(1,3))
```

<img src="15-Regression_files/figure-html/unnamed-chunk-41-1.png" width="100%" style="display: block; margin: auto;" /><img src="15-Regression_files/figure-html/unnamed-chunk-41-2.png" width="100%" style="display: block; margin: auto;" />
</div><div id="option2unnamed-chunk-25" class="tabcontentunnamed-chunk-25">

```r
performance::check_model(janka_ls1, check="homogeneity")
```

<img src="15-Regression_files/figure-html/unnamed-chunk-42-1.png" width="100%" style="display: block; margin: auto;" />
</div><script> javascript:hide('option2unnamed-chunk-25') </script></div></div></div>

### Outliers

Here we can see there is just one potential outlier. 

<button id="displayTextunnamed-chunk-26" onclick="javascript:toggle('unnamed-chunk-26');">Show Solution</button>

<div id="toggleTextunnamed-chunk-26" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body"><div class="tab"><button class="tablinksunnamed-chunk-26 active" onclick="javascript:openCode(event, 'option1unnamed-chunk-26', 'unnamed-chunk-26');">Base R</button><button class="tablinksunnamed-chunk-26" onclick="javascript:openCode(event, 'option2unnamed-chunk-26', 'unnamed-chunk-26');"><tt>tidyverse</tt></button></div><div id="option1unnamed-chunk-26" class="tabcontentunnamed-chunk-26">

```r
plot(janka_ls1, which=c(4,5))
```

<img src="15-Regression_files/figure-html/unnamed-chunk-43-1.png" width="100%" style="display: block; margin: auto;" /><img src="15-Regression_files/figure-html/unnamed-chunk-43-2.png" width="100%" style="display: block; margin: auto;" />
</div><div id="option2unnamed-chunk-26" class="tabcontentunnamed-chunk-26">

```r
performance::check_model(janka_ls1, check="outliers")
```

<img src="15-Regression_files/figure-html/unnamed-chunk-44-1.png" width="100%" style="display: block; margin: auto;" />
</div><script> javascript:hide('option2unnamed-chunk-26') </script></div></div></div>


## Prediction

Using the coefficients of the intercept and the slope we can make predictions on new data. 
The estimates of the intercept and the slope are:


```r
coef(janka_ls1)
```

```
## (Intercept)        dens 
## -1160.49970    57.50667
```


Now imagine we have a new wood samples with a density of 65, how can we use the equation for a linear regression to predict what the timber hardness for this wood sample should be?

$$ y = a + bx $$

<button id="displayTextunnamed-chunk-28" onclick="javascript:toggle('unnamed-chunk-28');">Show Solution</button>

<div id="toggleTextunnamed-chunk-28" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

```r
# a + bx

-1160.49970 + 57.50667 * 65
```

```
## [1] 2577.434
```
</div></div></div>


Rather than work out the values manually, we can also use the coefficients of the model directly


```r
coef(janka_ls1)[1] + coef(janka_ls1)[2] * 65
```

```
## (Intercept) 
##    2577.434
```


But most of the time we are unlikely to want to work out predicted values by hand, instead we can use functions like `predict()` and `augment()`

<button id="displayTextunnamed-chunk-30" onclick="javascript:toggle('unnamed-chunk-30');">Show Solution</button>

<div id="toggleTextunnamed-chunk-30" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body"><div class="tab"><button class="tablinksunnamed-chunk-30 active" onclick="javascript:openCode(event, 'option1unnamed-chunk-30', 'unnamed-chunk-30');">Base R</button><button class="tablinksunnamed-chunk-30" onclick="javascript:openCode(event, 'option2unnamed-chunk-30', 'unnamed-chunk-30');"><tt>tidyverse</tt></button></div><div id="option1unnamed-chunk-30" class="tabcontentunnamed-chunk-30">

```r
predict(janka_ls1, newdata=list(dens=c(22,35,65)))
```

```
##         1         2         3 
##  104.6471  852.2339 2577.4342
```
</div><div id="option2unnamed-chunk-30" class="tabcontentunnamed-chunk-30">

```r
broom::augment(janka_ls1, 
               newdata=tibble(dens=c(22,35,65)))
```

<div class="kable-table">

<table>
 <thead>
  <tr>
   <th style="text-align:right;"> dens </th>
   <th style="text-align:right;"> .fitted </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 22 </td>
   <td style="text-align:right;"> 104.6471 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 35 </td>
   <td style="text-align:right;"> 852.2339 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 65 </td>
   <td style="text-align:right;"> 2577.4342 </td>
  </tr>
</tbody>
</table>

</div>
</div><script> javascript:hide('option2unnamed-chunk-30') </script></div></div></div>

### Adding confidence intervals


```r
broom::augment(janka_ls1, newdata = tibble(dens=c(22,35,65), se=TRUE))
```

<div class="kable-table">

<table>
 <thead>
  <tr>
   <th style="text-align:right;"> dens </th>
   <th style="text-align:left;"> se </th>
   <th style="text-align:right;"> .fitted </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 22 </td>
   <td style="text-align:left;"> TRUE </td>
   <td style="text-align:right;"> 104.6471 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 35 </td>
   <td style="text-align:left;"> TRUE </td>
   <td style="text-align:right;"> 852.2339 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 65 </td>
   <td style="text-align:left;"> TRUE </td>
   <td style="text-align:right;"> 2577.4342 </td>
  </tr>
</tbody>
</table>

</div>


```r
broom::augment(janka_ls1, newdata=tibble(dens=c(22,35,65), interval="confidence"))
```

<div class="kable-table">

<table>
 <thead>
  <tr>
   <th style="text-align:right;"> dens </th>
   <th style="text-align:left;"> interval </th>
   <th style="text-align:right;"> .fitted </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 22 </td>
   <td style="text-align:left;"> confidence </td>
   <td style="text-align:right;"> 104.6471 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 35 </td>
   <td style="text-align:left;"> confidence </td>
   <td style="text-align:right;"> 852.2339 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 65 </td>
   <td style="text-align:left;"> confidence </td>
   <td style="text-align:right;"> 2577.4342 </td>
  </tr>
</tbody>
</table>

</div>



<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
can you plot the three new predicted values onto an existing figure to recreate the below?  </div></div>

<button id="displayTextunnamed-chunk-34" onclick="javascript:toggle('unnamed-chunk-34');">Show Solution</button>

<div id="toggleTextunnamed-chunk-34" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

```r
pred_newdata <- broom::augment(janka_ls1, 
               newdata=tibble(dens=c(22,35,65)))

janka %>% 
  ggplot(aes(x=dens, y=hardness))+
  geom_point()+
  geom_smooth(method="lm")+
  geom_point(data=pred_newdata, aes(y=.fitted, x=dens), colour="red")+
  geom_label(data=pred_newdata, (aes(y=(.fitted+10), x=(dens+3), label=round(.fitted, digits=0))))+
  theme_bw()+
  labs(x="Density", y="Timber Hardness")+
  scale_x_continuous(limits=c(20,80), expand=expansion(add=c(0,5)))
```

<img src="15-Regression_files/figure-html/unnamed-chunk-36-1.png" width="100%" style="display: block; margin: auto;" />
</div></div></div>


## Summary

Linear model analyses can extend beyond testing differences of means in categorical groupings to test relationships with continuous variables. This is known as linear regression, where the relationship between the explanatory variable and response variable are modelled with the equation for a straight line. The intercept is the value of *y* when *x* = 0, often this isn't that useful, and we can use 'mean-centered' values if we wish to make the intercept more intuitive. 
As with all linear models, regression assumes that the unexplained variability around the regression line, is normally distributed and has constant variance. 

Once the regression has been fitted it is possible to predict values of *y* from values of *x*, the uncertainty around these predictions can be captured with confidence intervals. 
