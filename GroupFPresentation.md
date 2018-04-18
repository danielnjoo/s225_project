Flights in Developed and Developing Countries
========================================================
author: Daniel and Jocelyn
date: 4/24/18
autosize: true

Research Questions
========================================================

- Can we predict the number of flights using average GDP growth?
- Is there a difference in the number of flights between developed and developing countries? Recently developed countries?
- Is there preferential travel to certain locations for developed and developing countires?

Basic Info
========================================================

- Flights are classified as developed if there Per Capita GDP was greater than $12,000
- There are 33,559 flights in our dataset
- 156 unique source and destination countries
- `developed.x` is 1 if the source country is developed, and 0 if developing

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


```

Call:
lm(formula = log_count ~ avg_growth.x, data = normal_minus)

Residuals:
    Min      1Q  Median      3Q     Max 
-4.4549 -1.0849 -0.1135  1.1765  4.5242 

Coefficients:
             Estimate Std. Error t value Pr(>|t|)    
(Intercept)  -5.22043    0.21060 -24.788  < 2e-16 ***
avg_growth.x -0.15224    0.04834  -3.149  0.00181 ** 
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 1.795 on 278 degrees of freedom
Multiple R-squared:  0.03445,	Adjusted R-squared:  0.03098 
F-statistic: 9.919 on 1 and 278 DF,  p-value: 0.001814
```

Parametric Conditions
========================================================

![plot of chunk unnamed-chunk-8](GroupFPresentation-figure/unnamed-chunk-8-1.png)![plot of chunk unnamed-chunk-8](GroupFPresentation-figure/unnamed-chunk-8-2.png)

Non-Parametric Regression
========================================================


```
Call:
rfit.default(formula = log_count ~ avg_growth.x, data = normal)

Coefficients:
              Estimate Std. Error  t.value p.value    
(Intercept)  -5.340557   0.205313 -26.0118 < 2e-16 ***
avg_growth.x -0.143715   0.046648  -3.0808 0.00227 ** 
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Multiple R-squared (Robust): 0.02999173 
Reduction in Dispersion Test: 8.62641 p-value: 0.00359 
```

Regression Results and Comparison
========================================================

- Conditions met for both Parametric and Non-Parametric regression
- Both found that `avg_growth.x` was a significant predictor of `log_count` ($p-value = .00181 & .0005$)
- However, both models suggested that `avg_growth.x` explained very little variability in `log_count` ($R^{2} = .034 & .041$)
- Although `avg_growth.x` is a significant predictor, the model lacks any substantial predicting power.

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
recent_development.x   2  258.7 129.349  51.426 < 2.2e-16 ***
Residuals            282  709.3   2.515                      
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```

Parametric Conditions:
========================================================


```
  recent_development.x        min        Q1    median        Q3       max
1            Developed  -9.127169 -5.807052 -4.799897 -3.804811 -1.504283
2           Developing -10.633726 -7.823550 -6.844428 -5.892568 -1.285613
3   Recently Developed  -8.161533 -7.534035 -6.521690 -6.116737 -1.327252
       mean       sd   n missing
1 -4.812397 1.393995 145       0
2 -6.741624 1.759436 128       0
3 -6.418771 1.817377  12       0
```

![plot of chunk unnamed-chunk-12](GroupFPresentation-figure/unnamed-chunk-12-1.png)

Parametric Multiple Comparisons - Fisher's LSD:
========================================================


```

	Pairwise comparisons using t tests with pooled SD 

data:  log_count and recent_development.x 

                   Developed Developing
Developing         <2e-16    -         
Recently Developed 0.0017    0.5007    

P value adjustment method: holm 
```

Non-Parametric ANOVA
========================================================


```

	Kruskal-Wallis rank sum test

data:  log_count by as.factor(recent_development.x)
Kruskal-Wallis chi-squared = 86.641, df = 2, p-value < 2.2e-16
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
Developing         < 2e-16   -         
Recently Developed 0.00054   0.70699   

P value adjustment method: holm 
```

ANOVA Results and Conclusions
========================================================

- ANOVA results, p-values
- Multiple comparison results
- Comparison - prefer NP due to conditions?

Travel Locations
========================================================

Conclusion and Limitations
========================================================

- Average Per Capita GDP Growth is a significant predictor of the normalized natural log of the number of flights, but lacks any substantial predictive power
- Second Question Conclusion
- Third Question and Conclusion

THE END
========================================================

