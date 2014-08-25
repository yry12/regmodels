## Regression Models - Final Prject

### Load data and check variables available 

We load the data from R package (mtcars) and summarize the data. There are 11 variables total, one of this if the oucome of interest "mpg" and the rest are our potential predictos.


```r
opts_chunk$set(cache=TRUE)
```

```r
setwd("C:/coursera/jhudatascience/regmodels")
  require(knitr)
library(datasets)
data(mtcars)
summary(mtcars)
```

```
##       mpg            cyl            disp             hp       
##  Min.   :10.4   Min.   :4.00   Min.   : 71.1   Min.   : 52.0  
##  1st Qu.:15.4   1st Qu.:4.00   1st Qu.:120.8   1st Qu.: 96.5  
##  Median :19.2   Median :6.00   Median :196.3   Median :123.0  
##  Mean   :20.1   Mean   :6.19   Mean   :230.7   Mean   :146.7  
##  3rd Qu.:22.8   3rd Qu.:8.00   3rd Qu.:326.0   3rd Qu.:180.0  
##  Max.   :33.9   Max.   :8.00   Max.   :472.0   Max.   :335.0  
##       drat            wt            qsec            vs       
##  Min.   :2.76   Min.   :1.51   Min.   :14.5   Min.   :0.000  
##  1st Qu.:3.08   1st Qu.:2.58   1st Qu.:16.9   1st Qu.:0.000  
##  Median :3.69   Median :3.33   Median :17.7   Median :0.000  
##  Mean   :3.60   Mean   :3.22   Mean   :17.8   Mean   :0.438  
##  3rd Qu.:3.92   3rd Qu.:3.61   3rd Qu.:18.9   3rd Qu.:1.000  
##  Max.   :4.93   Max.   :5.42   Max.   :22.9   Max.   :1.000  
##        am             gear           carb     
##  Min.   :0.000   Min.   :3.00   Min.   :1.00  
##  1st Qu.:0.000   1st Qu.:3.00   1st Qu.:2.00  
##  Median :0.000   Median :4.00   Median :2.00  
##  Mean   :0.406   Mean   :3.69   Mean   :2.81  
##  3rd Qu.:1.000   3rd Qu.:4.00   3rd Qu.:4.00  
##  Max.   :1.000   Max.   :5.00   Max.   :8.00
```

```r
names(mtcars)
```

```
##  [1] "mpg"  "cyl"  "disp" "hp"   "drat" "wt"   "qsec" "vs"   "am"   "gear"
## [11] "carb"
```

### Look for any potential relation between variables

In order to visualize a relation between mpg and predictors: 1) boxplot, to see the distribution of predictos; and 2) scatter plot, to visualize potential relation 


```r
require(knitr)
par(mfrow = c(1, 2))
with(mtcars, boxplot(mpg/10, disp/50, hp/50, drat, wt, qsec/5, main = "Boxplots - distribution of predictos"), 
    xlab = "", ylab = "")
axisnames <- c("MPG/10", "DISP/50", "HP/50", "drat", "wt", "qsec/5")
axis(1, at = c(1, 2, 3, 4, 5, 6), labels = axisnames, las = 2, cex.axis = 0.9, 
    tck = -0.01)
pairs(mtcars)
```

![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-21.png) ![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-22.png) 

Clearly, we can visualize some relation (positive or negative) between outcome and predictors.

### Regression model of transmission on fuel efficiency

The regression model is estimated as follows:

```r
require(knitr)
mtcarsmodel1 <- lm(mpg ~ am, data = mtcars)
summary(mtcarsmodel1)
```

```
## 
## Call:
## lm(formula = mpg ~ am, data = mtcars)
## 
## Residuals:
##    Min     1Q Median     3Q    Max 
## -9.392 -3.092 -0.297  3.244  9.508 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)    17.15       1.12   15.25  1.1e-15 ***
## am              7.24       1.76    4.11  0.00029 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 4.9 on 30 degrees of freedom
## Multiple R-squared:  0.36,	Adjusted R-squared:  0.338 
## F-statistic: 16.9 on 1 and 30 DF,  p-value: 0.000285
```

The R square resuls show that that automatic transmission explains 36% of the variance in fuel consumption. The intercept shows the mean value of mpg. In both case, the intercept and the predictor as statistical significantntof am show the difference in means between the two groups. 
This means, that the diffrence in means between autotransmission (am=1) and (am=0) is positive (7.245) and significant

##APPENDIX - additional data displays


```r
require(knitr)
data(mtcars)
with(mtcars, table(cyl))
```

```
## cyl
##  4  6  8 
## 11  7 14
```

```r
with(mtcars, table(am))
```

```
## am
##  0  1 
## 19 13
```

```r
with(mtcars, table(gear))
```

```
## gear
##  3  4  5 
## 15 12  5
```

```r
with(mtcars, table(carb))
```

```
## carb
##  1  2  3  4  6  8 
##  7 10  3 10  1  1
```

```r
with(mtcars, table(vs))
```

```
## vs
##  0  1 
## 18 14
```

```r
par(mfrow = c(2, 2))
plot(mtcarsmodel1)
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4.png) 
