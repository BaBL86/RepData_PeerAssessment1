# Reproducible Research: Peer Assessment 1

## Init directories and load required libraries


```r
setwd('/home/babl/coursera/Reproducible_Research/pa1')
library(data.table)
library(ggplot2)
library(grid)
library(gridExtra)
```

## Loading and preprocessing the data


```r
data<-data.table(read.csv("activity.csv", header=TRUE, na.strings="NA"))
```

## What is mean total number of steps taken per day?

### Make a histogram of the total number of steps taken each day


```r
total_steps_by_date <- aggregate(steps ~ date, data, 'sum', na.rm=TRUE)
mean_steps_by_date <- aggregate(steps ~ date, data, 'mean', na.rm=TRUE)

plot1 <- ggplot(mean_steps_by_date, aes(x=steps)) +
  geom_histogram(binwidth=5, colour="black", fill="white") +
  ggtitle('Mean of the total steps / day')

plot2 <- ggplot(total_steps_by_date, aes(x=steps)) +
  geom_histogram(binwidth=1000, colour="black", fill="white") +
  ggtitle('Total number of steps / day')

grid.arrange(plot1,plot2,ncol=2)
```

![](PA1_template_files/figure-html/unnamed-chunk-3-1.png) 

### Calculate and report the mean and median total number of steps taken per day


```r
mean<-mean(total_steps_by_date$steps,na.rm=TRUE)
median<-median(total_steps_by_date$steps,na.rm=TRUE)
```

```r
print(mean)
```

```
## [1] 10766.19
```

```r
print(median)
```

```
## [1] 10765
```

The mean of total number of steps taken per day are 1.0766189\times 10^{4} and median are 10765.

## What is the average daily activity pattern?


```r
mean_steps_by_interval <- aggregate(steps ~ interval, data, 'mean', na.rm=TRUE)
ggplot(mean_steps_by_interval, aes(x = interval, y = steps)) + geom_line()
```

![](PA1_template_files/figure-html/unnamed-chunk-7-1.png) 


## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
