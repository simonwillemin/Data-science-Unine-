Data_7 Linear Models
================
Simon Willemin
(31 août, 2022)

-   [Correlation?](#correlation)
-   [Visual representation](#visual-representation)
-   [General linear model](#general-linear-model)
    -   [Assumptions](#assumptions)
    -   [Check fro normality of the
        distribution](#check-fro-normality-of-the-distribution)
    -   [Linearity](#linearity)
-   [Simple regression](#simple-regression)
-   [Reference](#reference)

``` r
library(tidyverse)
library(knitr)
library(dslabs)
```

#The Dataset

?cars

Let’s get back to our faithful `cars` data.

``` r
str(cars)
```

    ## 'data.frame':    50 obs. of  2 variables:
    ##  $ speed: num  4 4 7 7 8 9 10 10 10 11 ...
    ##  $ dist : num  2 10 4 22 16 10 18 26 34 17 ...

``` r
kable(head(cars))
```

| speed | dist |
|------:|-----:|
|     4 |    2 |
|     4 |   10 |
|     7 |    4 |
|     7 |   22 |
|     8 |   16 |
|     9 |   10 |

This data - which is old (from the 1920’s) - describes the speed of cars
and the distances taken to stop. The dataframe has 50 observations of
only two variables. Namely, the numeric speed (mph) and the stopping
distance (ft).

It is plain and intuitive to see here that speed influences the braking
distance. Hence, speed will be our **explanatory variable**\* and
distance will be our **response variable**

*Scatterplot*

Let’s take a visual lool at our data and plot the distance per speed :

``` r
plot(cars, xlab = "Speed (mph)", ylab = "Stopping distance (ft)")
lines(lowess(cars$speed, cars$dist, f = 2/3, iter = 2), col = "blue")
title(main = "Stopping Distance (ft) / Speed (Mph)")
```

![](Data_7_files/figure-gfm/plot-1.png)<!-- -->

## Correlation?

Now we will take a look at if there is a correlation between speed and
braking distance. In order to do that, we will conduct a Pearson’s
correlation. That is because both our predictor and output variables are
continuous numerical variables.

``` r
correlation <- cor(cars$dist, cars$speed, method = 'pearson')
print(correlation)
```

    ## [1] 0.8068949

The correlation is strong, being *0.8068949*.

## Visual representation

``` r
library(ggplot2)
gg <- ggplot(cars, aes(speed,dist))
gg <- gg + geom_point()
gg <- gg + geom_smooth(alpha=0.3, method="lm")
print(gg)
```

    ## `geom_smooth()` using formula 'y ~ x'

![](Data_7_files/figure-gfm/plot2-1.png)<!-- -->

We know that such positive correlation results do not mean causation,
altough the relationship is quite obvious here. Let’s hence run a
general linear model.

## General linear model

### Assumptions

**Independence of observations** – \> probably present **Normality** –>
we will check it later on **Linearity** –> we will see it in our linear
model **Homoscedasticity** –> “”

### Check fro normality of the distribution

``` r
hist((cars$dist), main="Cars distance",
     xlab ="distance")
```

![](Data_7_files/figure-gfm/normality-1.png)<!-- -->

``` r
hist((cars$speed), main="Cars speed",
      xlab = "speed")
```

![](Data_7_files/figure-gfm/normality-2.png)<!-- -->

It seems to be roughly normally around 20-40

### Linearity

``` r
 plot(speed ~ dist, data = cars)
```

![](Data_7_files/figure-gfm/linearity-1.png)<!-- -->

``` r
normality <- ggplot(cars, aes(speed,dist))
normality <- normality + geom_point()
normality <- normality + geom_smooth(alpha=0.3, method="lm")
print(normality)
```

    ## `geom_smooth()` using formula 'y ~ x'

![](Data_7_files/figure-gfm/linearity-2.png)<!-- -->

## Simple regression

``` r
speed.dist.lm <- lm(speed ~ dist, data = cars)
summary(speed.dist.lm)
```

    ## 
    ## Call:
    ## lm(formula = speed ~ dist, data = cars)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -7.5293 -2.1550  0.3615  2.4377  6.4179 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  8.28391    0.87438   9.474 1.44e-12 ***
    ## dist         0.16557    0.01749   9.464 1.49e-12 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 3.156 on 48 degrees of freedom
    ## Multiple R-squared:  0.6511, Adjusted R-squared:  0.6438 
    ## F-statistic: 89.57 on 1 and 48 DF,  p-value: 1.49e-12

This leads us to conclude that there is a significant positive
relationship between speed and braking distance.

# Reference

Ezekiel, M. (1930) Methods of Correlation Analysis. Wiley
