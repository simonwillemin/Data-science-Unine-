---
title: "Data_2_report_"
author: "simon_willemin"
date: "(`r format(Sys.time(), '%d %B, %Y')`)"
output:
  github_document:
    toc: true

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```


```{r message=FALSE, warning=FALSE}
library(knitr)

```

# Dataset 1

Let's  start by importing a classic r dataset : `mtcars`. It originates from a 1974 car magazine and comprises fuel consumption and 10 aspects of automobile design and performance for 32 automobiles. Those models are from 1973-1974. 
```{r mtcars}
library(knitr)
kable(head(mtcars))
```

```{r mtcars-data-type}
str(mtcars)
```

We can see here, thanks to the`str` function that each and every one of those 11 variables are numerical. 

Moreover, the `?mtcars` question to R confirms us that is it is case. 

"A data frame with 32 observations on 11 (numeric) variables.

[, 1]	mpg	Miles/(US) gallon
[, 2]	cyl	Number of cylinders
[, 3]	disp	Displacement (cu.in.)
[, 4]	hp	Gross horsepower
[, 5]	drat	Rear axle ratio
[, 6]	wt	Weight (1000 lbs)
[, 7]	qsec	1/4 mile time
[, 8]	vs	Engine (0 = V-shaped, 1 = straight)
[, 9]	am	Transmission (0 = automatic, 1 = manual)
[,10]	gear	Number of forward gears
[,11]	carb	Number of carburetors"



That said, we can however notice that some of those variables are discrete `number of cylinders` because a car can indeed only have a whole/discrete number of those - and some others are continuous like the `Rear axle ratio`.

All in all, it is clear that this data is *quantitative*



# Dataset 2

The second dataset that we will explore was found on  https://www.kaggle.com/. 

It is a dataset called `Airlines.csv`and it aims at predicting delays of airplanes based on the data from schedule panel. 




```{r airlines}
airlines <- read.csv("Airlines.csv")
kable(head(airlines))
```

We can easily tell that those variables are of two different kinds, statistically speaking. There are both qualitative and quantitative variables. 

```{r airlines-data-type}
str(airlines)
```

After a closer analysis with the `str` function, we can tell that there is in fact two types of variables, speaking in R language. Namely, the quantitative variables are set to integer, because they holf discrete values.

`light     : int  269 1558 2400 2466 108 1094 1768 2722 2606 2538`

*or*


`Length     : int  205 222 165 195 202 181 220 228 216 200 ...`



Whereas the other variables are qualitative character variables. 

Just like the airports codes for instance 

`$ AirportFrom: chr  "SFO" "PHX" "LAX" "SFO" ...`


# Dataset 3


The third data that we will take a look at today regards satellite launches from 1957 to 2022. So from the very beginning of artificial satellites with Sputnik to all the modern ones being launched via the Starlink programm for instance or via the chinese exploration of space that tried the latest launches early june 2022. 

A quick look at this data via `head` informs us that most of the data will be qualitative even if dates are involved. 

```{r satellites}
satellites <- read.csv("sattelite launches.csv")
kable(head(satellites))

```



```{r latest satellites}

kable(tail(satellites))

```

```{r satellites-data-type}
str(satellites)
```


That is confirmed by the `str` analysis that shows us that most of the data is `character` while one of the variables is integer. The latter is simply the rank of launch (the order) from the first one in 1957 to the latest one in 2022. 


## R Markdown

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:

```{r cars}
summary(cars)
```

## Including Plots

You can also embed plots, for example:

```{r pressure, echo=FALSE}
plot(pressure)
```

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.
