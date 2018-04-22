<style>
.reveal pre code {
  font-size: 1em;
}
.section .reveal .state-background {
  background-image: url('http://ichef.bbci.co.uk/images/ic/1600xn/p03vfmdq.jpg')
}
</style>



Flights in Developed and Developing Countries
========================================================
class: first
author: Daniel and Jocelyn
date: 4/24/18
autosize: true
transition: rotate
transition-speed: fast

Research Questions
========================================================
incremental: true
1. Can we predict the number of flights using average GDP growth?
2. Is there a difference in the number of flights between developed and developing countries? Recently developed countries?
3. Is there preferential travel to certain locations for developed and developing countires?

Data Summary
========================================================
incremental: true

- Flight data from the Flight Route Database (Kaggle)
- Flights are classified as developed if there Per Capita GDP was greater than $12,000
- There are 33,559 flights in our dataset
- 156 unique source and destination countries
- `developed.x` is 1 if the source country is developed, and 0 if developing

1. Predicting flights using average GDP growth
========================================================

Number of Flights per Country
========================================================

![plot of chunk unnamed-chunk-1](GroupFPresentation-figure/unnamed-chunk-1-1.png)


Distribution of Per Capita GDP
========================================================

![plot of chunk unnamed-chunk-2](GroupFPresentation-figure/unnamed-chunk-2-1.png)

Distribution of Per Capita GDP Growth
========================================================

![plot of chunk unnamed-chunk-3](GroupFPresentation-figure/unnamed-chunk-3-1.png)

Number of Flights vs. Average GDP Growth
========================================================

- Explore the relationship between the Number of Flights and Average Per Capita GDP Growth via scatterplots and smoothing
- Transformation and Normalization
- Parametric and Non-Parametric Regression

Linear Fit and Loess Smoother
========================================================

![plot of chunk unnamed-chunk-4](GroupFPresentation-figure/unnamed-chunk-4-1.png)![plot of chunk unnamed-chunk-4](GroupFPresentation-figure/unnamed-chunk-4-2.png)

Normalization of Flights by Population
========================================================

![plot of chunk unnamed-chunk-5](GroupFPresentation-figure/unnamed-chunk-5-1.png)![plot of chunk unnamed-chunk-5](GroupFPresentation-figure/unnamed-chunk-5-2.png)

Log Transformation of Counts
========================================================

![plot of chunk unnamed-chunk-6](GroupFPresentation-figure/unnamed-chunk-6-1.png)![plot of chunk unnamed-chunk-6](GroupFPresentation-figure/unnamed-chunk-6-2.png)

Parametric Regression: log_count ~ avg_growth.x
========================================================
class: small-code


```

Call:
lm(formula = log_count ~ avg_growth.x, data = normal_minus)

Residuals:
    Min      1Q  Median      3Q     Max 
-5.2537 -0.9822  0.0758  1.4343  3.7856 

Coefficients:
             Estimate Std. Error t value Pr(>|t|)    
(Intercept)  -4.29517    0.28235 -15.212  < 2e-16 ***
avg_growth.x -0.17234    0.06482  -2.659  0.00871 ** 
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 1.738 on 147 degrees of freedom
Multiple R-squared:  0.04588,	Adjusted R-squared:  0.03939 
F-statistic: 7.069 on 1 and 147 DF,  p-value: 0.008712
```

Parametric Conditions
========================================================
class: small-code

![plot of chunk unnamed-chunk-8](GroupFPresentation-figure/unnamed-chunk-8-1.png)![plot of chunk unnamed-chunk-8](GroupFPresentation-figure/unnamed-chunk-8-2.png)

Non-Parametric Regression
========================================================


```
Call:
rfit.default(formula = log_count ~ avg_growth.x, data = normal_minus)

Coefficients:
              Estimate Std. Error  t.value   p.value    
(Intercept)  -4.193363   0.312363 -13.4246 < 2.2e-16 ***
avg_growth.x -0.178268   0.064666  -2.7567  0.006578 ** 
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Multiple R-squared (Robust): 0.04850027 
Reduction in Dispersion Test: 7.49295 p-value: 0.00696 
```

Regression Results and Comparison
========================================================

- Both found that `avg_growth.x` was a significant predictor of `log_count` ($p-value = .00871 & .00658$)
- However, both models suggested that `avg_growth.x` explained very little variability in `log_count` ($R^{2} = .0458 & .0485$)
- Although `avg_growth.x` is a significant predictor, the model lacks any substantial predicting power.

2. Investigating differences in travel patterns by development status
========================================================

Has Travel Increased in Recently Developed Countries?
========================================================

- Identified 7 countries that were developing in 2010, but were developed in 2016:
  - China
  - Mongolia
  - Bosnia and Herzegovina
  - Nauru
  - Peru
  - Sri Lanka
  - Turkmenistan
  
Development Status
========================================================

![plot of chunk unnamed-chunk-10](GroupFPresentation-figure/unnamed-chunk-10-1.png)

Parametric ANOVA:
========================================================


```
Analysis of Variance Table

Response: log_count
                      Df Sum Sq Mean Sq F value    Pr(>F)    
recent_development.x   2 147.34  73.670  32.734 1.551e-12 ***
Residuals            151 339.84   2.251                      
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```

Parametric Conditions:
========================================================
class: small-code


```
  recent_development.x        min        Q1    median        Q3       max
1            Developed  -8.509555 -4.827407 -3.744171 -3.087010 -1.424241
2           Developing -10.633726 -6.731752 -6.073666 -5.092774 -1.285613
3   Recently Developed  -8.161533 -6.468207 -5.653310 -5.442111 -1.327252
       mean       sd  n missing
1 -3.886392 1.205375 75       0
2 -5.866088 1.702840 72       0
3 -5.566104 2.099361  7       0
```

![plot of chunk unnamed-chunk-12](GroupFPresentation-figure/unnamed-chunk-12-1.png)

Parametric Multiple Comparisons - Fisher's LSD:
========================================================


```

	Pairwise comparisons using t tests with pooled SD 

data:  log_count and recent_development.x 

                   Developed Developing
Developing         9.2e-13   -         
Recently Developed 0.01      0.61      

P value adjustment method: holm 
```

Non-Parametric ANOVA
========================================================


```

	Kruskal-Wallis rank sum test

data:  log_count by as.factor(recent_development.x)
Kruskal-Wallis chi-squared = 52.653, df = 2, p-value = 3.686e-12
```

Non-Parametric Conditions - Shift Model:
========================================================

![plot of chunk unnamed-chunk-15](GroupFPresentation-figure/unnamed-chunk-15-1.png)

Non-Parametric Multiple Comparisons - Wilcoxon Rank Sum
========================================================


```

	Pairwise comparisons using Wilcoxon rank sum test 

data:  log_count and recent_development.x 

                   Developed Developing
Developing         3.5e-12   -         
Recently Developed 0.0091    0.7627    

P value adjustment method: holm 
```

ANOVA Results and Conclusions
========================================================

- Both tests found that there was a least one significant difference in means and medians of flight between different development status (p-values $< 0.0001$).
- Fisher's LSD and Pairwise Wilcoxon Rank Sums found a significant differences between:
  - Developed and Developing (p-values $<0.0001$)
  - Developed and Recently Developed (p-value $= 0.01$ & p-value = $= 0.0091$)
- Recently developed countries are more similar to developing than developed countries

<<<<<<< HEAD
3. Do developing countries fly to popular developed nation destinations?
========================================================

Travel Locations - Outside Own Country
=======
Normalized Travel Locations 
>>>>>>> 787d4c7fdecc24488cf686a2a1b1be415427ac1c
========================================================

- Most popular destinations for Developed:
  - Antigua and Barbuda
  - Iceland
  - St. Kitts and Nevis
  - Bermuda
  - Austria
- Most popular destinations for Developing:
  - Antigua and Barbuda
  - Nauru
  - Tuvalu
  - Palau
  - Maldives
  
Travel Locations - Developed
========================================================

![plot of chunk unnamed-chunk-17](GroupFPresentation-figure/unnamed-chunk-17-1.png)

Travel Locations - Developing
========================================================

![plot of chunk unnamed-chunk-18](GroupFPresentation-figure/unnamed-chunk-18-1.png)


Non-Normalized Travel Locations:
========================================================

- Most popular destinations for Developed:
  - Great Britain
  - Germany
  - Spain
  - Italy
  - France
- Most popular destinations for Developing:
  - United Arab Emirate
  - Singapore
  - Japan
  - France
  - China

Parametric - Two Proportion Z-test
========================================================










```
Error in melt(.) : could not find function "melt"
```
