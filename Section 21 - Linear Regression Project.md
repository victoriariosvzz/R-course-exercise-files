---
title: "Section 21 - Linear Regression Project"
author: "Victoria"
date: "12/1/2021"
output: html_document
---



#**Linear Regression Project**
For this project you will be doing the Bike Sharing Demand Kaggle challenge! We won't submit any results to the competition, but feel free to explore Kaggle more in depth. The main point of this project is to get you feeling comfortabe with Exploratory Data Analysis and begin to get an understanding that sometimes certain models are not a good choice for a data set. In this case, we will discover that Linear Regression may not be the best choice given our data!

```r
bike <- read.csv("bikeshare.csv")
head(bike)
```

```
##              datetime season holiday
## 1 2011-01-01 00:00:00      1       0
## 2 2011-01-01 01:00:00      1       0
## 3 2011-01-01 02:00:00      1       0
## 4 2011-01-01 03:00:00      1       0
## 5 2011-01-01 04:00:00      1       0
## 6 2011-01-01 05:00:00      1       0
##   workingday weather temp  atemp
## 1          0       1 9.84 14.395
## 2          0       1 9.02 13.635
## 3          0       1 9.02 13.635
## 4          0       1 9.84 14.395
## 5          0       1 9.84 14.395
## 6          0       2 9.84 12.880
##   humidity windspeed casual registered
## 1       81    0.0000      3         13
## 2       80    0.0000      8         32
## 3       80    0.0000      5         27
## 4       75    0.0000      3         10
## 5       75    0.0000      0          1
## 6       75    6.0032      0          1
##   count
## 1    16
## 2    40
## 3    32
## 4    13
## 5     1
## 6     1
```

**Exploratory Data Analysis**
Create a scatter plot of count vs temp. Set a good alpha value.

```r
library(ggplot2)

ggplot(bike,aes(x=temp, y=count)) + geom_point(alpha = 0.1, aes(color = temp))
```

![plot of chunk unnamed-chunk-54](figure/unnamed-chunk-54-1.png)
Plot count versus datetime as a scatterplot with a color gradient based on temperature. You'll need to convert the datetime column into POSIXct before plotting.

```r
ggplot(bike,aes(x=datetime, y=count)) + geom_point(alpha = 0.1, aes(color = temp)) + scale_colour_gradient(low="blue",high="red")
```

![plot of chunk unnamed-chunk-55](figure/unnamed-chunk-55-1.png)
Hopefully you noticed two things: A seasonality to the data, for winter and summer. Also that bike rental counts are increasing in general. This may present a problem with using a linear regression model if the data is non-linear. Let's have a quick overview of pros and cons right now of Linear Regression:

Pros:

Simple to explain
Highly interpretable
Model training and prediction are fast
No tuning is required (excluding regularization)
Features don't need scaling
Can perform well with a small number of observations
Well-understood
Cons:

Assumes a linear relationship between the features and the response
Performance is (generally) not competitive with the best supervised learning methods due to high bias
Can't automatically learn feature interactions

What is the correlation between temp and count?

```r
cor(bike$temp,bike$count)
```

```
## [1] 0.3944536
```
Let's explore the season data. Create a boxplot, with the y axis indicating count and the x axis begin a box for each season.

```r
ggplot(bike, aes(x=factor(season), y=count)) + geom_boxplot(aes(color=factor(season)))
```

![plot of chunk unnamed-chunk-57](figure/unnamed-chunk-57-1.png)
**Feature Engineering**
A lot of times you'll need to use domain knowledge and experience to engineer and create new features. Let's go ahead and engineer some new features from the datetime column.

Create an "hour" column that takes the hour from the datetime column. You'll probably need to apply some function to the entire datetime column and reassign it. Hint: time.stamp <- bike$datetime[4]
format(time.stamp, "%H")

```r
time.stamp <- bike$datetime

#first, we convert character vector to data type format
time.stamp.dt <- as.POSIXct(time.stamp, format = "%Y-%m-%d %H:%M:%S")
class(time.stamp.dt)
```

```
## [1] "POSIXct" "POSIXt"
```

```r
#then, we can apply format to create a column with only the hour
bike$hour <- format(time.stamp.dt, format = "%H")
```
Now create a scatterplot of count versus hour, with color scale based on temp. Only use bike data where workingday==1.

Optional Additions:

Use the additional layer: scale_color_gradientn(colors=c('color1',color2,etc..)) where the colors argument is a vector gradient of colors you choose, not just high and low.
Use position=position_jitter(w=1, h=0) inside of geom_point() and check out what it does.

```r
bike.working <- subset(bike, workingday == 1)
ggplot(bike.working, aes(x=hour, y=count)) + geom_point(position = position_jitter(w=1,h=0), aes(color = temp), alpha=0.5) + scale_color_gradientn(colors = c("blue", "green", "yellow", "red"))
```

![plot of chunk unnamed-chunk-59](figure/unnamed-chunk-59-1.png)
Now create the same plot for non working days:

```r
bike.notworking <- subset(bike, workingday == 0)
ggplot(bike.notworking, aes(x=hour, y=count)) + geom_point(position = position_jitter(w=1,h=0), aes(color = temp), alpha=0.5) + scale_color_gradientn(colors = c("blue", "green", "yellow", "red"))
```

![plot of chunk unnamed-chunk-60](figure/unnamed-chunk-60-1.png)
**Building the Model**
Use lm() to build a model that predicts count based solely on the temp feature, name it temp.model

```r
temp.data <- bike$temp


library(caTools)

temp.model <- lm(formula = count ~ temp, data = bike)
summary(temp.model)
```

```
## 
## Call:
## lm(formula = count ~ temp, data = bike)
## 
## Residuals:
##     Min      1Q  Median      3Q 
## -293.32 -112.36  -33.36   78.98 
##     Max 
##  741.44 
## 
## Coefficients:
##             Estimate Std. Error
## (Intercept)   6.0462     4.4394
## temp          9.1705     0.2048
##             t value Pr(>|t|)    
## (Intercept)   1.362    0.173    
## temp         44.783   <2e-16 ***
## ---
## Signif. codes:  
##   0 '***' 0.001 '**' 0.01 '*' 0.05
##   '.' 0.1 ' ' 1
## 
## Residual standard error: 166.5 on 10884 degrees of freedom
## Multiple R-squared:  0.1556,	Adjusted R-squared:  0.1555 
## F-statistic:  2006 on 1 and 10884 DF,  p-value: < 2.2e-16
```
How many bike rentals would we predict if the temperature was 25 degrees Celsius? Calculate this two ways:

```r
temps.25 <- subset(bike, temp == 25)
temps.predict <- predict(temp.model, data = temps.25)
mean(temps.predict)
```

```
## [1] 191.5741
```
Use sapply() and as.numeric to change the hour column to a column of numeric values.

```r
bike$hour <- sapply(bike$hour, as.numeric)
class(bike$hour)
```

```
## [1] "numeric"
```
Finally build a model that attempts to predict count based off of the following features. Figure out if theres a way to not have to pass/write all these variables into the lm() function. Hint: StackOverflow or Google may be quicker than the documentation.

```r
model <- lm(count ~ season + holiday + workingday + weather + temp + humidity + windspeed + hour, data = bike)

summary(model)
```

```
## 
## Call:
## lm(formula = count ~ season + holiday + workingday + weather + 
##     temp + humidity + windspeed + hour, data = bike)
## 
## Residuals:
##     Min      1Q  Median      3Q 
## -324.62  -96.90  -31.02   55.29 
##     Max 
##  688.82 
## 
## Coefficients:
##              Estimate Std. Error
## (Intercept)  46.89219    8.45350
## season       21.70478    1.35422
## holiday     -10.28558    8.79170
## workingday   -0.70375    3.14558
## weather      -3.21499    2.49767
## temp          7.01969    0.19138
## humidity     -2.21174    0.09084
## windspeed     0.20275    0.18640
## hour          7.61358    0.21692
##             t value Pr(>|t|)    
## (Intercept)   5.547 2.97e-08 ***
## season       16.027  < 2e-16 ***
## holiday      -1.170    0.242    
## workingday   -0.224    0.823    
## weather      -1.287    0.198    
## temp         36.680  < 2e-16 ***
## humidity    -24.347  < 2e-16 ***
## windspeed     1.088    0.277    
## hour         35.098  < 2e-16 ***
## ---
## Signif. codes:  
##   0 '***' 0.001 '**' 0.01 '*' 0.05
##   '.' 0.1 ' ' 1
## 
## Residual standard error: 147.9 on 10875 degrees of freedom
##   (2 observations deleted due to missingness)
## Multiple R-squared:  0.3343,	Adjusted R-squared:  0.3338 
## F-statistic: 682.6 on 8 and 10875 DF,  p-value: < 2.2e-16
```

You should have noticed that this sort of model doesn't work well given our seasonal and time series data. We need a model that can account for this type of trend, read about Regression Forests for more info if you're interested! For now, let's keep this in mind as a learning experience and move on towards classification with Logistic Regression!

Optional: See how well you can predict for future data points by creating a train/test split. But instead of a random split, your split should be "future" data for test, "previous" data for train.
