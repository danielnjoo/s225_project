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
lm(formula = log_count ~ avg_growth.x, data = normal)

Residuals:
   Min     1Q Median     3Q    Max 
-4.583 -1.129 -0.130  1.165  5.593 

Coefficients:
             Estimate Std. Error t value Pr(>|t|)    
(Intercept)  -5.35963    0.20967  -25.56   <2e-16 ***
avg_growth.x -0.10978    0.04732   -2.32   0.0211 *  
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 1.826 on 279 degrees of freedom
  (6 observations deleted due to missingness)
Multiple R-squared:  0.01893,	Adjusted R-squared:  0.01541 
F-statistic: 5.383 on 1 and 279 DF,  p-value: 0.02106
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
- Both found that `avg_growth.x` was a significant predictor of `log_count` ($p-value = .002 & .0005$)
- However, both models suggested that `avg_growth.x` explained very little variability in `log_count` ($R^{2} = .034 & .041$)
- Although `avg_growth.x` is a significant predictor, the model lacks any substantial predicting power.

Conclusion
========================================================

Slide With Plot
========================================================

![plot of chunk unnamed-chunk-10](GroupFPresentation-figure/unnamed-chunk-10-1.png)
