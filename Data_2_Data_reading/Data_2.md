Data_2\_report\_
================
simon_willemin
(24 août, 2022)

-   [Dataset 1](#dataset-1)
-   [Dataset 2](#dataset-2)
-   [Dataset 3](#dataset-3)

``` r
library(knitr)
```

# Dataset 1

Let’s start by importing a classic r dataset : `mtcars`. It originates
from a 1974 car magazine and comprises fuel consumption and 10 aspects
of automobile design and performance for 32 automobiles. Those models
are from 1973-1974.

``` r
library(knitr)
kable(head(mtcars))
```

|                   |  mpg | cyl | disp |  hp | drat |    wt |  qsec |  vs |  am | gear | carb |
|:------------------|-----:|----:|-----:|----:|-----:|------:|------:|----:|----:|-----:|-----:|
| Mazda RX4         | 21.0 |   6 |  160 | 110 | 3.90 | 2.620 | 16.46 |   0 |   1 |    4 |    4 |
| Mazda RX4 Wag     | 21.0 |   6 |  160 | 110 | 3.90 | 2.875 | 17.02 |   0 |   1 |    4 |    4 |
| Datsun 710        | 22.8 |   4 |  108 |  93 | 3.85 | 2.320 | 18.61 |   1 |   1 |    4 |    1 |
| Hornet 4 Drive    | 21.4 |   6 |  258 | 110 | 3.08 | 3.215 | 19.44 |   1 |   0 |    3 |    1 |
| Hornet Sportabout | 18.7 |   8 |  360 | 175 | 3.15 | 3.440 | 17.02 |   0 |   0 |    3 |    2 |
| Valiant           | 18.1 |   6 |  225 | 105 | 2.76 | 3.460 | 20.22 |   1 |   0 |    3 |    1 |

``` r
str(mtcars)
```

    ## 'data.frame':    32 obs. of  11 variables:
    ##  $ mpg : num  21 21 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 ...
    ##  $ cyl : num  6 6 4 6 8 6 8 4 4 6 ...
    ##  $ disp: num  160 160 108 258 360 ...
    ##  $ hp  : num  110 110 93 110 175 105 245 62 95 123 ...
    ##  $ drat: num  3.9 3.9 3.85 3.08 3.15 2.76 3.21 3.69 3.92 3.92 ...
    ##  $ wt  : num  2.62 2.88 2.32 3.21 3.44 ...
    ##  $ qsec: num  16.5 17 18.6 19.4 17 ...
    ##  $ vs  : num  0 0 1 1 0 1 0 1 1 1 ...
    ##  $ am  : num  1 1 1 0 0 0 0 0 0 0 ...
    ##  $ gear: num  4 4 4 3 3 3 3 4 4 4 ...
    ##  $ carb: num  4 4 1 1 2 1 4 2 2 4 ...

We can see here, thanks to the`str` function that each and every one of
those 11 variables are numerical.

Moreover, the `?mtcars` question to R confirms us that is it is case.

“A data frame with 32 observations on 11 (numeric) variables.

\[, 1\] mpg Miles/(US) gallon \[, 2\] cyl Number of cylinders \[, 3\]
disp Displacement (cu.in.) \[, 4\] hp Gross horsepower \[, 5\] drat Rear
axle ratio \[, 6\] wt Weight (1000 lbs) \[, 7\] qsec 1/4 mile time \[,
8\] vs Engine (0 = V-shaped, 1 = straight) \[, 9\] am Transmission (0 =
automatic, 1 = manual) \[,10\] gear Number of forward gears \[,11\] carb
Number of carburetors”

That said, we can however notice that some of those variables are
discrete `number of cylinders` because a car can indeed only have a
whole/discrete number of those - and some others are continuous like the
`Rear axle ratio`.

All in all, it is clear that this data is *quantitative*

# Dataset 2

The second dataset that we will explore was found on
<https://www.kaggle.com/>.

It is a dataset called `Airlines.csv`and it aims at predicting delays of
airplanes based on the data from schedule panel.

``` r
airlines <- read.csv("Airlines.csv")
kable(head(airlines))
```

|  id | Airline | Flight | AirportFrom | AirportTo | DayOfWeek | Time | Length | Delay |
|----:|:--------|-------:|:------------|:----------|----------:|-----:|-------:|------:|
|   1 | CO      |    269 | SFO         | IAH       |         3 |   15 |    205 |     1 |
|   2 | US      |   1558 | PHX         | CLT       |         3 |   15 |    222 |     1 |
|   3 | AA      |   2400 | LAX         | DFW       |         3 |   20 |    165 |     1 |
|   4 | AA      |   2466 | SFO         | DFW       |         3 |   20 |    195 |     1 |
|   5 | AS      |    108 | ANC         | SEA       |         3 |   30 |    202 |     0 |
|   6 | CO      |   1094 | LAX         | IAH       |         3 |   30 |    181 |     1 |

We can easily tell that those variables are of two different kinds,
statistically speaking. There are both qualitative and quantitative
variables.

``` r
str(airlines)
```

    ## 'data.frame':    539383 obs. of  9 variables:
    ##  $ id         : int  1 2 3 4 5 6 7 8 9 10 ...
    ##  $ Airline    : chr  "CO" "US" "AA" "AA" ...
    ##  $ Flight     : int  269 1558 2400 2466 108 1094 1768 2722 2606 2538 ...
    ##  $ AirportFrom: chr  "SFO" "PHX" "LAX" "SFO" ...
    ##  $ AirportTo  : chr  "IAH" "CLT" "DFW" "DFW" ...
    ##  $ DayOfWeek  : int  3 3 3 3 3 3 3 3 3 3 ...
    ##  $ Time       : int  15 15 20 20 30 30 30 30 35 40 ...
    ##  $ Length     : int  205 222 165 195 202 181 220 228 216 200 ...
    ##  $ Delay      : int  1 1 1 1 0 1 0 0 1 1 ...

After a closer analysis with the `str` function, we can tell that there
is in fact two types of variables, speaking in R language. Namely, the
quantitative variables are set to integer, because they holf discrete
values.

`light     : int  269 1558 2400 2466 108 1094 1768 2722 2606 2538`

*or*

`Length     : int  205 222 165 195 202 181 220 228 216 200 ...`

Whereas the other variables are qualitative character variables.

Just like the airports codes for instance

`$ AirportFrom: chr  "SFO" "PHX" "LAX" "SFO" ...`

# Dataset 3

The third data that we will take a look at today regards satellite
launches from 1957 to 2022. So from the very beginning of artificial
satellites with Sputnik to all the modern ones being launched via the
Starlink programm for instance or via the chinese exploration of space
that tried the latest launches early june 2022.

A quick look at this data via `head` informs us that most of the data
will be qualitative even if dates are involved.

``` r
satellites <- read.csv("sattelite launches.csv")
kable(head(satellites))
```

| norad_id | cospar_id | name       | launch_date | flight_ended | status  | destination | owner                                            |
|---------:|:----------|:-----------|:------------|:-------------|:--------|:------------|:-------------------------------------------------|
|        1 | 1957-001A | SL-1 R/B   | 3-Oct-57    | 1-Dec-57     | Decayed |             | Commonwealth of Independent States (former USSR) |
|        2 | 1957-001B | SPUTNIK 1  | 3-Oct-57    | 3-Jan-58     | Decayed |             | Commonwealth of Independent States (former USSR) |
|        3 | 1957-002A | SPUTNIK 2  | 3-Nov-57    | 14-Apr-58    | Decayed |             | Commonwealth of Independent States (former USSR) |
|        4 | 1958-001A | EXPLORER 1 | 1-Feb-58    | 30-Mar-70    | Decayed |             | United States                                    |
|        5 | 1958-002B | VANGUARD 1 | 17-Mar-58   |              |         |             | United States                                    |
|        6 | 1958-003A | EXPLORER 3 | 26-Mar-58   | 27-Jun-58    | Decayed |             | United States                                    |

``` r
kable(tail(satellites))
```

|       | norad_id | cospar_id | name        | launch_date | flight_ended | status      | destination | owner                      |
|:------|---------:|:----------|:------------|:------------|:-------------|:------------|:------------|:---------------------------|
| 52745 |    52797 | 2022-060A | SHENZHOU 14 | 4-Jun-22    |              | Operational |             | People’s Republic of China |
| 52746 |    52798 | 2022-060B | CZ-2F R/B   | 4-Jun-22    |              |             |             | People’s Republic of China |
| 52747 |    52799 | 2022-060C | OBJECT C    | 4-Jun-22    | 6-Jun-22     | Decayed     |             | People’s Republic of China |
| 52748 |    52800 | 2022-060D | OBJECT D    | 4-Jun-22    | 7-Jun-22     | Decayed     |             | People’s Republic of China |
| 52749 |    52801 | 2022-060E | OBJECT E    | 4-Jun-22    | 11-Jun-22    | Decayed     |             | People’s Republic of China |
| 52750 |    52802 | 2022-060F | OBJECT F    | 4-Jun-22    | 11-Jun-22    | Decayed     |             | People’s Republic of China |

``` r
str(satellites)
```

    ## 'data.frame':    52750 obs. of  8 variables:
    ##  $ norad_id    : int  1 2 3 4 5 6 7 8 9 10 ...
    ##  $ cospar_id   : chr  "1957-001A" "1957-001B" "1957-002A" "1958-001A" ...
    ##  $ name        : chr  "SL-1 R/B" "SPUTNIK 1" "SPUTNIK 2" "EXPLORER 1" ...
    ##  $ launch_date : chr  "3-Oct-57" "3-Oct-57" "3-Nov-57" "1-Feb-58" ...
    ##  $ flight_ended: chr  "1-Dec-57" "3-Jan-58" "14-Apr-58" "30-Mar-70" ...
    ##  $ status      : chr  "Decayed" "Decayed" "Decayed" "Decayed" ...
    ##  $ destination : chr  "" "" "" "" ...
    ##  $ owner       : chr  "Commonwealth of Independent States (former USSR)" "Commonwealth of Independent States (former USSR)" "Commonwealth of Independent States (former USSR)" "United States" ...

That is confirmed by the `str` analysis that shows us that most of the
data is `character` while one of the variables is integer. The latter is
simply the rank of launch (the order) from the first one in 1957 to the
latest one in 2022.
