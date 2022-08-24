Data Wrangling
================
Simon Willemin
24 août 2022

-   [Filtering](#filtering)
-   [Selecting](#selecting)
-   [Arranging](#arranging)
-   [Group by and Summarize](#group-by-and-summarize)
-   [Merging](#merging)
-   [References](#references)

``` r
library(knitr)
library(dplyr)
library(readr)
library(dslabs)
```

## Filtering

Let’s first `filter()` the data for the United States and put them in a
dataframe.

``` r
USA_country_filter <- gapminder %>% 
  filter(country == "United States")
```

Let’s now do that for Switzerland

``` r
Switzerland_country_filter <- gapminder %>% 
  filter(country == "Switzerland")
```

## Selecting

Let’s now `select()` some interesting variable for the USA

``` r
USA_selected <- USA_country_filter %>%
  select(fertility, population, year)
  
str(USA_selected)
```

    ## 'data.frame':    57 obs. of  3 variables:
    ##  $ fertility : num  3.67 3.63 3.48 3.35 3.22 2.93 2.71 2.56 2.47 2.46 ...
    ##  $ population: num  1.86e+08 1.89e+08 1.92e+08 1.95e+08 1.97e+08 ...
    ##  $ year      : int  1960 1961 1962 1963 1964 1965 1966 1967 1968 1969 ...

``` r
head(USA_selected) %>% kable()
```

| fertility | population | year |
|----------:|-----------:|-----:|
|      3.67 |  186176524 | 1960 |
|      3.63 |  189077076 | 1961 |
|      3.48 |  191860710 | 1962 |
|      3.35 |  194513911 | 1963 |
|      3.22 |  197028908 | 1964 |
|      2.93 |  199403532 | 1965 |

``` r
tail(USA_selected) %>% kable()
```

|     | fertility | population | year |
|:----|----------:|-----------:|-----:|
| 52  |      1.90 |  312390368 | 2011 |
| 53  |      1.90 |  314799465 | 2012 |
| 54  |      1.98 |  317135919 | 2013 |
| 55  |      1.97 |  319448634 | 2014 |
| 56  |      1.97 |  321773631 | 2015 |
| 57  |        NA |         NA | 2016 |

And the same for Switzerland

``` r
Switzerland_selected <- Switzerland_country_filter %>%
  select(fertility, population, year)
  
str(Switzerland_selected)
```

    ## 'data.frame':    57 obs. of  3 variables:
    ##  $ fertility : num  2.52 2.55 2.58 2.58 2.56 2.53 2.47 2.4 2.31 2.22 ...
    ##  $ population: num  5296120 5393411 5503000 5618160 5729465 ...
    ##  $ year      : int  1960 1961 1962 1963 1964 1965 1966 1967 1968 1969 ...

``` r
head(Switzerland_selected) %>% kable()
```

| fertility | population | year |
|----------:|-----------:|-----:|
|      2.52 |    5296120 | 1960 |
|      2.55 |    5393411 | 1961 |
|      2.58 |    5503000 | 1962 |
|      2.58 |    5618160 | 1963 |
|      2.56 |    5729465 | 1964 |
|      2.53 |    5829958 | 1965 |

``` r
tail(Switzerland_selected) %>% kable()
```

|     | fertility | population | year |
|:----|----------:|-----------:|-----:|
| 52  |      1.51 |    7925813 | 2011 |
| 53  |      1.52 |    8022628 | 2012 |
| 54  |      1.53 |    8118719 | 2013 |
| 55  |      1.54 |    8211383 | 2014 |
| 56  |      1.55 |    8298663 | 2015 |
| 57  |        NA |         NA | 2016 |

## Arranging

``` r
USA_selected %>%
  arrange(year)
```

    ##    fertility population year
    ## 1       3.67  186176524 1960
    ## 2       3.63  189077076 1961
    ## 3       3.48  191860710 1962
    ## 4       3.35  194513911 1963
    ## 5       3.22  197028908 1964
    ## 6       2.93  199403532 1965
    ## 7       2.71  201629471 1966
    ## 8       2.56  203713082 1967
    ## 9       2.47  205687611 1968
    ## 10      2.46  207599308 1969
    ## 11      2.46  209485807 1970
    ## 12      2.27  211357912 1971
    ## 13      2.01  213219515 1972
    ## 14      1.87  215092900 1973
    ## 15      1.83  217001865 1974
    ## 16      1.77  218963561 1975
    ## 17      1.74  220993166 1976
    ## 18      1.78  223090871 1977
    ## 19      1.75  225239456 1978
    ## 20      1.80  227411604 1979
    ## 21      1.82  229588208 1980
    ## 22      1.81  231765783 1981
    ## 23      1.81  233953874 1982
    ## 24      1.78  236161961 1983
    ## 25      1.79  238404223 1984
    ## 26      1.84  240691557 1985
    ## 27      1.84  243032017 1986
    ## 28      1.87  245425409 1987
    ## 29      1.92  247865202 1988
    ## 30      2.00  250340795 1989
    ## 31      2.07  252847810 1990
    ## 32      2.06  255367160 1991
    ## 33      2.04  257908206 1992
    ## 34      2.02  260527420 1993
    ## 35      2.00  263301323 1994
    ## 36      1.98  266275528 1995
    ## 37      1.98  269483224 1996
    ## 38      1.97  272882865 1997
    ## 39      2.00  276354096 1998
    ## 40      2.01  279730801 1999
    ## 41      2.05  282895741 2000
    ## 42      2.03  285796198 2001
    ## 43      2.02  288470847 2002
    ## 44      2.05  291005482 2003
    ## 45      2.06  293530886 2004
    ## 46      2.06  296139635 2005
    ## 47      2.11  298860519 2006
    ## 48      2.12  301655953 2007
    ## 49      2.07  304473143 2008
    ## 50      2.00  307231961 2009
    ## 51      1.93  309876170 2010
    ## 52      1.90  312390368 2011
    ## 53      1.90  314799465 2012
    ## 54      1.98  317135919 2013
    ## 55      1.97  319448634 2014
    ## 56      1.97  321773631 2015
    ## 57        NA         NA 2016

We can here notice that the overall fertility rates drop over the years,
while the population constantly increases. Interestingly, after a
lower-than-two fertility rate period in the 70’s, it increased again
later on, and stabilized.

``` r
Switzerland_selected %>%
  arrange(year)
```

    ##    fertility population year
    ## 1       2.52    5296120 1960
    ## 2       2.55    5393411 1961
    ## 3       2.58    5503000 1962
    ## 4       2.58    5618160 1963
    ## 5       2.56    5729465 1964
    ## 6       2.53    5829958 1965
    ## 7       2.47    5916911 1966
    ## 8       2.40    5991681 1967
    ## 9       2.31    6056358 1968
    ## 10      2.22    6114719 1969
    ## 11      2.12    6169357 1970
    ## 12      2.02    6221634 1971
    ## 13      1.92    6270112 1972
    ## 14      1.83    6311468 1973
    ## 15      1.74    6341051 1974
    ## 16      1.67    6356178 1975
    ## 17      1.61    6355245 1976
    ## 18      1.57    6341216 1977
    ## 19      1.54    6321583 1978
    ## 20      1.52    6306578 1979
    ## 21      1.51    6303608 1980
    ## 22      1.51    6315799 1981
    ## 23      1.52    6341369 1982
    ## 24      1.53    6376791 1983
    ## 25      1.54    6416275 1984
    ## 26      1.54    6455680 1985
    ## 27      1.54    6493442 1986
    ## 28      1.55    6531160 1987
    ## 29      1.55    6571461 1988
    ## 30      1.55    6618268 1989
    ## 31      1.55    6673920 1990
    ## 32      1.54    6739995 1991
    ## 33      1.54    6814186 1992
    ## 34      1.53    6890300 1993
    ## 35      1.53    6959860 1994
    ## 36      1.52    7017042 1995
    ## 37      1.50    7059633 1996
    ## 38      1.49    7090176 1997
    ## 39      1.47    7113505 1998
    ## 40      1.45    7136813 1999
    ## 41      1.44    7165581 2000
    ## 42      1.43    7200945 2001
    ## 43      1.42    7242034 2002
    ## 44      1.42    7289901 2003
    ## 45      1.42    7345299 2004
    ## 46      1.43    7408608 2005
    ## 47      1.44    7480317 2006
    ## 48      1.46    7560141 2007
    ## 49      1.47    7646542 2008
    ## 50      1.49    7737316 2009
    ## 51      1.50    7830534 2010
    ## 52      1.51    7925813 2011
    ## 53      1.52    8022628 2012
    ## 54      1.53    8118719 2013
    ## 55      1.54    8211383 2014
    ## 56      1.55    8298663 2015
    ## 57        NA         NA 2016

Whereas in Switzerland, it was at first (in the 1960’s) lower than in
the US at the same period. However, it shrank more regularly and is now
at a low since the 1980’s already !

## Group by and Summarize

``` r
na.omit(gapminder) %>%
  group_by(country) %>%
  summarize(total_fertility = sum (fertility)) %>%
  arrange(desc(total_fertility)) %>%
  head()
```

    ## # A tibble: 6 × 2
    ##   country       total_fertility
    ##   <fct>                   <dbl>
    ## 1 Rwanda                   376.
    ## 2 Burundi                  374.
    ## 3 Malawi                   357.
    ## 4 Zambia                   349.
    ## 5 Burkina Faso             347.
    ## 6 Cote d'Ivoire            345.

``` r
na.omit(gapminder) %>%
  group_by(country) %>%
  summarize(total_fertility = sum (fertility)) %>%
  arrange(desc(total_fertility)) %>%
  tail()
```

    ## # A tibble: 6 × 2
    ##   country                total_fertility
    ##   <fct>                            <dbl>
    ## 1 Czech Republic                    30.4
    ## 2 Slovenia                          29.3
    ## 3 Montenegro                        26.5
    ## 4 Estonia                           24.9
    ## 5 Bosnia and Herzegovina            24.0
    ## 6 Ireland                           23.8

We can here usprisingly notice that the most fertile country (over the
years) is an african country, namely Rwanda. Also, the least fertile one
is Ireland.

## Merging

We could for instance merge the `results_us_election_2016` and `murders`
datasets.

``` r
head(full_join(results_us_election_2016, murders)) %>% kable()
```

    ## Joining, by = "state"

| state        | electoral_votes | clinton | trump | others | abb | region        | population | total |
|:-------------|----------------:|--------:|------:|-------:|:----|:--------------|-----------:|------:|
| California   |              55 |    61.7 |  31.6 |    6.7 | CA  | West          |   37253956 |  1257 |
| Texas        |              38 |    43.2 |  52.2 |    4.5 | TX  | South         |   25145561 |   805 |
| Florida      |              29 |    47.8 |  49.0 |    3.2 | FL  | South         |   19687653 |   669 |
| New York     |              29 |    59.0 |  36.5 |    4.5 | NY  | Northeast     |   19378102 |   517 |
| Illinois     |              20 |    55.8 |  38.8 |    5.4 | IL  | North Central |   12830632 |   364 |
| Pennsylvania |              20 |    47.9 |  48.6 |    3.6 | PA  | Northeast     |   12702379 |   457 |

# References

Jennifer Bryan (NA). gapminder: Data from Gapminder.
<https://github.com/jennybc/gapminder>,
<http://www.gapminder.org/data/>, <https://doi.org/10.5281/>

Rogers, S. (2011, October 5). The murder map of London’s boroughs. The
Guardian.
<http://www.theguardian.com/news/datablog/interactive/2011/oct/05/murder-london-map>

WIlliams, Jack, 2022, “Elections Performance Index 2016”,
<https://doi.org/10.7910/DVN/TSUQOA>, Harvard Dataverse, V2,
UNF:6:p1RbweyWRBJUm7A957ZaAQ== \[fileUNF\]
