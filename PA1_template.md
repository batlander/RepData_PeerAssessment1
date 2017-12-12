---
title: "Assigment 2nd week"
output: 
  html_document: 
    keep_md: yes
---
# Read file


```r
library(tidyverse)
```

```
## ── Attaching packages ────────────────────────────────── tidyverse 1.2.1 ──
```

```
## ✔ ggplot2 2.2.1     ✔ purrr   0.2.4
## ✔ tibble  1.3.4     ✔ dplyr   0.7.4
## ✔ tidyr   0.7.2     ✔ stringr 1.2.0
## ✔ readr   1.1.1     ✔ forcats 0.2.0
```

```
## ── Conflicts ───────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
```

```r
library(readr)
library(knitr)
library(readr)
library(lubridate)
```

```
## 
## Attaching package: 'lubridate'
```

```
## The following object is masked from 'package:base':
## 
##     date
```

```r
activity <- read_csv("./activity.csv", col_names = TRUE)
```

```
## Parsed with column specification:
## cols(
##   steps = col_integer(),
##   date = col_date(format = ""),
##   interval = col_integer()
## )
```

# Histogram


```r
hist <- group_by(activity, date) %>% summarise(sum(steps))
names(hist) <-c("Date", "Steps")
plot(hist$Steps, type = "h", xlab = " Days", ylab = "Steps")
```

![](Assigment_2nd_week_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

# Mean and Median


```r
mean <- na.omit(hist$Steps)
mean <- mean (mean)
median <- na.omit(hist$Steps)
median <- median(median)
```

The mean is 1.0766189\times 10^{4} and the median is 10765.

# Activity Pattern


```r
timeplot <- group_by(activity, interval) %>% summarise(mean(steps, na.rm = TRUE))
plot(timeplot, type ="l", xlab = "Interval", ylab = " Average Steps")
```

![](Assigment_2nd_week_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

```r
max <- max(timeplot)
```

The biggest step interval is 2355.

# Missing Data


```r
# NAs number
missing <- sum(is.na(activity$steps))

# Dataset without NAs

histna <- hist
histna[is.na(histna)]<-mean

# Plot

plot(histna$Steps, type = "h", xlab = " Days", ylab = "Steps")
```

![](Assigment_2nd_week_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

```r
# Mean and median

media <- mean(histna$Steps)
mediana <- median(histna$Steps)
meandif <- abs(mean-media)
mediandif <- abs (median - mediana)
```

Tne number of NAs is 2304.

The new mean is 1.0766189\times 10^{4}and the new median is 1.0766189\times 10^{4}. And the diferences are 0 and 1.1886792.

# Weekdays and weekends comparison


```r
week <- histna[wday(histna$Date) %in% 1:5,]
wend <- histna[wday(histna$Date) %in% 6:7,]

par(mfrow = c(2,1))
plot(week, type ="l", xlab = "Weekdays", ylab = " Average Steps", col = "blue")
plot(wend, type ="l", xlab = "Weekend", ylab = " Average Steps", col = "red")
```

![](Assigment_2nd_week_files/figure-html/unnamed-chunk-6-1.png)<!-- -->







