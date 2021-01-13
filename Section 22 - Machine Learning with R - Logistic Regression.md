---
title: "Section 22 - Machine Learning with R - Logistic Regression"
author: "Victoria"
date: "12/1/2021"
output: html_document
---



#**Introduction to Logistic Regression**
It's a method for **binary classification**, for example:
- Detecting spam and non-spam e-mails  
- Detecting faulty and non-faulty payments  
We cannot use the Linear Regression Model in binary groups, because the training data is either 1 or 0, and the linear model would give values lower or higher than those values.
##Result: probability between 0 and 1 of belonging to class 1 (for example, class 1 is for values of p > 0.5)

##Model
Using the **confusion matrix**
- Accuracy: (TN + TP)/Total
- Error rate: (FN + FN)/Total
**Type of errors**
- Type I error: False positive
- Type II error: False negative

# Logistic Regression Lecture

```r
df.train <- read.csv("titanic_train.csv")

head(df.train)
```

```
##   PassengerId Survived Pclass
## 1           1        0      3
## 2           2        1      1
## 3           3        1      3
## 4           4        1      1
## 5           5        0      3
## 6           6        0      3
##                                                  Name
## 1                             Braund, Mr. Owen Harris
## 2 Cumings, Mrs. John Bradley (Florence Briggs Thayer)
## 3                              Heikkinen, Miss. Laina
## 4        Futrelle, Mrs. Jacques Heath (Lily May Peel)
## 5                            Allen, Mr. William Henry
## 6                                    Moran, Mr. James
##      Sex Age SibSp Parch           Ticket
## 1   male  22     1     0        A/5 21171
## 2 female  38     1     0         PC 17599
## 3 female  26     0     0 STON/O2. 3101282
## 4 female  35     1     0           113803
## 5   male  35     0     0           373450
## 6   male  NA     0     0           330877
##      Fare Cabin Embarked
## 1  7.2500              S
## 2 71.2833   C85        C
## 3  7.9250              S
## 4 53.1000  C123        S
## 5  8.0500              S
## 6  8.4583              Q
```

```r
str(df.train)
```

```
## 'data.frame':	891 obs. of  12 variables:
##  $ PassengerId: int  1 2 3 4 5 6 7 8 9 10 ...
##  $ Survived   : int  0 1 1 1 0 0 0 0 1 1 ...
##  $ Pclass     : int  3 1 3 1 3 3 1 3 3 2 ...
##  $ Name       : chr  "Braund, Mr. Owen Harris" "Cumings, Mrs. John Bradley (Florence Briggs Thayer)" "Heikkinen, Miss. Laina" "Futrelle, Mrs. Jacques Heath (Lily May Peel)" ...
##  $ Sex        : chr  "male" "female" "female" "female" ...
##  $ Age        : num  22 38 26 35 35 NA 54 2 27 14 ...
##  $ SibSp      : int  1 1 0 1 0 0 0 3 0 1 ...
##  $ Parch      : int  0 0 0 0 0 0 0 1 2 0 ...
##  $ Ticket     : chr  "A/5 21171" "PC 17599" "STON/O2. 3101282" "113803" ...
##  $ Fare       : num  7.25 71.28 7.92 53.1 8.05 ...
##  $ Cabin      : chr  "" "C85" "" "C123" ...
##  $ Embarked   : chr  "S" "C" "S" "S" ...
```
1. Let's check how many missing data we have (using Amelia package)

```r
library(Amelia)

missmap(df.train, main = "Missing map", col = c("yellow","black"), legend = FALSE) #we notice that in the AGE column we have lots of missing spaces
```

![plot of chunk unnamed-chunk-44](figure/unnamed-chunk-44-1.png)

2. Exploring the data

```r
library(ggplot2)

ggplot(df.train, aes(Survived)) + geom_bar()
```

![plot of chunk unnamed-chunk-45](figure/unnamed-chunk-45-1.png)

```r
ggplot(df.train, aes(Pclass)) + geom_bar(aes(fill= factor(Pclass)))
```

![plot of chunk unnamed-chunk-45](figure/unnamed-chunk-45-2.png)

```r
ggplot(df.train, aes(Sex)) + geom_bar(aes(fill= factor(Sex)))
```

![plot of chunk unnamed-chunk-45](figure/unnamed-chunk-45-3.png)

```r
ggplot(df.train, aes(Age)) + geom_histogram(bins=20, alpha=0.5, fill="blue")
```

```
## Warning: Removed 177 rows containing non-finite
## values (stat_bin).
```

![plot of chunk unnamed-chunk-45](figure/unnamed-chunk-45-4.png)

```r
ggplot(df.train, aes(SibSp)) + geom_bar()
```

![plot of chunk unnamed-chunk-45](figure/unnamed-chunk-45-5.png)

```r
ggplot(df.train, aes(Fare)) + geom_histogram(fill="green", color="black")
```

```
## `stat_bin()` using `bins = 30`. Pick
## better value with `binwidth`.
```

![plot of chunk unnamed-chunk-45](figure/unnamed-chunk-45-6.png)
3. Cleaning the data by filling the missing ages with the average ages of their class

```r
library(plotly)

pl <- ggplot(df.train, aes(Pclass, Age)) + geom_boxplot(aes(group=Pclass,fill=factor(Pclass)),alpha=0.4) + scale_y_continuous(breaks = seq(min(0),max(80),by = 2)) + theme_bw()

print(pl)
```

```
## Warning: Removed 177 rows containing non-finite
## values (stat_boxplot).
```

![plot of chunk unnamed-chunk-46](figure/unnamed-chunk-46-1.png)

```r
ggplotly(pl) #we check the median age of each class
```

```
## Warning: Removed 177 rows containing non-finite
## values (stat_boxplot).
```

```
## Error in loadNamespace(name): there is no package called 'webshot'
```

```r
##Imputation of age based on class
impute_age <- function(age, class){
  out <- age
  for (i in 1:length(age)) {
    if (is.na(age[i])) {
      if (class[i]==1) {
        out[i] <- 37
      }else if (class[i]==2) {
        out[i] <- 29
      }else{
        out[i] <- 24
      }
    }else{
      out[i] <- age[i]
    }
  }
  return(out)
}

#####
fixed.ages <- impute_age(df.train$Age,df.train$Pclass)

any(is.na(fixed.ages))
```

```
## [1] FALSE
```

```r
df.train$Age <- fixed.ages #applying it to our data frame
any(is.na(df.train$Age))
```

```
## [1] FALSE
```

```r
missmap(df.train,main = "Imputation check",col = c("yellow","black"),legend = FALSE) #we check for missing values
```

![plot of chunk unnamed-chunk-46](figure/unnamed-chunk-46-2.png)

4.Final clean-up of our data: remove what you won't use and check the data format

```r
str(df.train)
```

```
## 'data.frame':	891 obs. of  12 variables:
##  $ PassengerId: int  1 2 3 4 5 6 7 8 9 10 ...
##  $ Survived   : int  0 1 1 1 0 0 0 0 1 1 ...
##  $ Pclass     : int  3 1 3 1 3 3 1 3 3 2 ...
##  $ Name       : chr  "Braund, Mr. Owen Harris" "Cumings, Mrs. John Bradley (Florence Briggs Thayer)" "Heikkinen, Miss. Laina" "Futrelle, Mrs. Jacques Heath (Lily May Peel)" ...
##  $ Sex        : chr  "male" "female" "female" "female" ...
##  $ Age        : num  22 38 26 35 35 24 54 2 27 14 ...
##  $ SibSp      : int  1 1 0 1 0 0 0 3 0 1 ...
##  $ Parch      : int  0 0 0 0 0 0 0 1 2 0 ...
##  $ Ticket     : chr  "A/5 21171" "PC 17599" "STON/O2. 3101282" "113803" ...
##  $ Fare       : num  7.25 71.28 7.92 53.1 8.05 ...
##  $ Cabin      : chr  "" "C85" "" "C123" ...
##  $ Embarked   : chr  "S" "C" "S" "S" ...
```

```r
library(dplyr)
df.train <- select(df.train,-PassengerId,-Name,-Cabin,-Ticket) #deleting the selected columns
head(df.train)
```

```
##   Survived Pclass    Sex Age SibSp Parch
## 1        0      3   male  22     1     0
## 2        1      1 female  38     1     0
## 3        1      3 female  26     0     0
## 4        1      1 female  35     1     0
## 5        0      3   male  35     0     0
## 6        0      3   male  24     0     0
##      Fare Embarked
## 1  7.2500        S
## 2 71.2833        C
## 3  7.9250        S
## 4 53.1000        S
## 5  8.0500        S
## 6  8.4583        Q
```

```r
str(df.train)
```

```
## 'data.frame':	891 obs. of  8 variables:
##  $ Survived: int  0 1 1 1 0 0 0 0 1 1 ...
##  $ Pclass  : int  3 1 3 1 3 3 1 3 3 2 ...
##  $ Sex     : chr  "male" "female" "female" "female" ...
##  $ Age     : num  22 38 26 35 35 24 54 2 27 14 ...
##  $ SibSp   : int  1 1 0 1 0 0 0 3 0 1 ...
##  $ Parch   : int  0 0 0 0 0 0 0 1 2 0 ...
##  $ Fare    : num  7.25 71.28 7.92 53.1 8.05 ...
##  $ Embarked: chr  "S" "C" "S" "S" ...
```

```r
#We convert some of the int values as factors with levels
df.train$Survived <- factor(df.train$Survived)
df.train$Pclass <- factor(df.train$Pclass)
df.train$Parch <- factor(df.train$Parch)
df.train$SibSp <- factor(df.train$SibSp)

str(df.train)
```

```
## 'data.frame':	891 obs. of  8 variables:
##  $ Survived: Factor w/ 2 levels "0","1": 1 2 2 2 1 1 1 1 2 2 ...
##  $ Pclass  : Factor w/ 3 levels "1","2","3": 3 1 3 1 3 3 1 3 3 2 ...
##  $ Sex     : chr  "male" "female" "female" "female" ...
##  $ Age     : num  22 38 26 35 35 24 54 2 27 14 ...
##  $ SibSp   : Factor w/ 7 levels "0","1","2","3",..: 2 2 1 2 1 1 1 4 1 2 ...
##  $ Parch   : Factor w/ 7 levels "0","1","2","3",..: 1 1 1 1 1 1 1 2 3 1 ...
##  $ Fare    : num  7.25 71.28 7.92 53.1 8.05 ...
##  $ Embarked: chr  "S" "C" "S" "S" ...
```

5. Training the model

```r
log.model <- glm(Survived ~ ., family = binomial(link = "logit"), data = df.train) #logistic regression model

summary(log.model)
```

```
## 
## Call:
## glm(formula = Survived ~ ., family = binomial(link = "logit"), 
##     data = df.train)
## 
## Deviance Residuals: 
##     Min       1Q   Median       3Q  
## -2.8158  -0.6134  -0.4138   0.5808  
##     Max  
##  2.4896  
## 
## Coefficients:
##               Estimate Std. Error z value
## (Intercept)  1.845e+01  1.660e+03   0.011
## Pclass2     -1.079e+00  3.092e-01  -3.490
## Pclass3     -2.191e+00  3.161e-01  -6.930
## Sexmale     -2.677e+00  2.040e-01 -13.123
## Age         -3.971e-02  8.758e-03  -4.534
## SibSp1       8.135e-02  2.245e-01   0.362
## SibSp2      -2.897e-01  5.368e-01  -0.540
## SibSp3      -2.241e+00  7.202e-01  -3.111
## SibSp4      -1.675e+00  7.620e-01  -2.198
## SibSp5      -1.595e+01  9.588e+02  -0.017
## SibSp8      -1.607e+01  7.578e+02  -0.021
## Parch1       3.741e-01  2.895e-01   1.292
## Parch2       3.862e-02  3.824e-01   0.101
## Parch3       3.655e-01  1.056e+00   0.346
## Parch4      -1.586e+01  1.055e+03  -0.015
## Parch5      -1.152e+00  1.172e+00  -0.983
## Parch6      -1.643e+01  2.400e+03  -0.007
## Fare         2.109e-03  2.490e-03   0.847
## EmbarkedC   -1.458e+01  1.660e+03  -0.009
## EmbarkedQ   -1.456e+01  1.660e+03  -0.009
## EmbarkedS   -1.486e+01  1.660e+03  -0.009
##             Pr(>|z|)    
## (Intercept) 0.991134    
## Pclass2     0.000484 ***
## Pclass3     4.20e-12 ***
## Sexmale      < 2e-16 ***
## Age         5.79e-06 ***
## SibSp1      0.717133    
## SibSp2      0.589361    
## SibSp3      0.001862 ** 
## SibSp4      0.027954 *  
## SibSp5      0.986731    
## SibSp8      0.983077    
## Parch1      0.196213    
## Parch2      0.919560    
## Parch3      0.729318    
## Parch4      0.988007    
## Parch5      0.325771    
## Parch6      0.994536    
## Fare        0.397036    
## EmbarkedC   0.992995    
## EmbarkedQ   0.993001    
## EmbarkedS   0.992857    
## ---
## Signif. codes:  
##   0 '***' 0.001 '**' 0.01 '*' 0.05 '.'
##   0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 1186.66  on 890  degrees of freedom
## Residual deviance:  763.41  on 870  degrees of freedom
## AIC: 805.41
## 
## Number of Fisher Scoring iterations: 15
```

6. Let's start with predictions

```r
library(caTools)
set.seed(101)
split <- sample.split(df.train$Survived, SplitRatio = 0.7)

final.train <- subset(df.train, split == TRUE)
final.test <- subset(df.train, split == FALSE)

final.log.model <- glm(Survived ~ ., family = binomial(link = "logit"), data = final.train )
summary(final.log.model)
```

```
## 
## Call:
## glm(formula = Survived ~ ., family = binomial(link = "logit"), 
##     data = final.train)
## 
## Deviance Residuals: 
##     Min       1Q   Median       3Q  
## -2.8288  -0.5607  -0.4096   0.6174  
##     Max  
##  2.4898  
## 
## Coefficients:
##               Estimate Std. Error z value
## (Intercept)  1.777e+01  2.400e+03   0.007
## Pclass2     -1.230e+00  3.814e-01  -3.225
## Pclass3     -2.160e+00  3.841e-01  -5.624
## Sexmale     -2.660e+00  2.467e-01 -10.782
## Age         -3.831e-02  1.034e-02  -3.705
## SibSp1      -2.114e-02  2.755e-01  -0.077
## SibSp2      -4.000e-01  6.463e-01  -0.619
## SibSp3      -2.324e+00  8.994e-01  -2.584
## SibSp4      -1.196e+00  8.302e-01  -1.440
## SibSp5      -1.603e+01  9.592e+02  -0.017
## SibSp8      -1.633e+01  1.004e+03  -0.016
## Parch1       7.290e-01  3.545e-01   2.056
## Parch2       1.406e-01  4.504e-01   0.312
## Parch3       7.919e-01  1.229e+00   0.645
## Parch4      -1.498e+01  1.552e+03  -0.010
## Parch5      -9.772e-03  1.378e+00  -0.007
## Parch6      -1.635e+01  2.400e+03  -0.007
## Fare         3.128e-03  3.091e-03   1.012
## EmbarkedC   -1.398e+01  2.400e+03  -0.006
## EmbarkedQ   -1.387e+01  2.400e+03  -0.006
## EmbarkedS   -1.431e+01  2.400e+03  -0.006
##             Pr(>|z|)    
## (Intercept) 0.994091    
## Pclass2     0.001261 ** 
## Pclass3     1.87e-08 ***
## Sexmale      < 2e-16 ***
## Age         0.000212 ***
## SibSp1      0.938836    
## SibSp2      0.536028    
## SibSp3      0.009765 ** 
## SibSp4      0.149839    
## SibSp5      0.986666    
## SibSp8      0.987019    
## Parch1      0.039771 *  
## Parch2      0.754892    
## Parch3      0.519226    
## Parch4      0.992300    
## Parch5      0.994343    
## Parch6      0.994563    
## Fare        0.311605    
## EmbarkedC   0.995353    
## EmbarkedQ   0.995386    
## EmbarkedS   0.995243    
## ---
## Signif. codes:  
##   0 '***' 0.001 '**' 0.01 '*' 0.05 '.'
##   0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 829.60  on 622  degrees of freedom
## Residual deviance: 530.63  on 602  degrees of freedom
## AIC: 572.63
## 
## Number of Fisher Scoring iterations: 15
```

```r
#Predicting
fitted.probabilities <- predict(final.log.model, final.test, type = "response")

fitted.results <- ifelse(fitted.probabilities>0.5, 1, 0) #to set the categories out of the probabilities values

misClassError <- mean(fitted.results != final.test$Survived) #Error

print(1 - misClassError) #Accuracy
```

```
## [1] 0.7985075
```
7. Let's create our **confussion matrix**

```r
table(final.test$Survived, fitted.probabilities>0.5)
```

```
##    
##     FALSE TRUE
##   0   140   25
##   1    29   74
```

