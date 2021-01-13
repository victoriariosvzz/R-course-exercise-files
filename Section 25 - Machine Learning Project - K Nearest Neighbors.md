---
title: "Section 25 - Machine Learning Project - K Nearest Neighbors"
author: "Victoria"
date: "12/1/2021"
output: html_document
---



#**KNN Project**
Since KNN is such a simple algorithm, we will just use this "Project" as a simple exercise to test your understanding of the implementation of KNN. By now you should feel comfortable implementing a machine learning algorithm in R, as long as you know what library to use for it.

So for this project, just follow along with the bolded instructions. It should be very simple, so at the end you'll have an additional optional "bonus" project.

**Get the Data**
Iris Data Set

```r
library(ISLR)
head(iris)
```

```
##   Sepal.Length Sepal.Width
## 1          5.1         3.5
## 2          4.9         3.0
## 3          4.7         3.2
## 4          4.6         3.1
## 5          5.0         3.6
## 6          5.4         3.9
##   Petal.Length Petal.Width Species
## 1          1.4         0.2  setosa
## 2          1.4         0.2  setosa
## 3          1.3         0.2  setosa
## 4          1.5         0.2  setosa
## 5          1.4         0.2  setosa
## 6          1.7         0.4  setosa
```

**Standardize Data**
In this case, the iris data set has all its features in the same order of magnitude, but its good practice (especially with KNN) to standardize features in your data. Lets go ahead and do this even though its not necessary for this data!

Use scale() to standardize the feature columns of the iris dataset. Set this standardized version of the data as a new variable.

```r
standarized.iris <- scale(iris[1:4])
```

Check that the scaling worked by checking the variance of one of the new columns.

```r
standarized.iris <- as.data.frame(standarized.iris)

var(standarized.iris$Sepal.Length)
```

```
## [1] 1
```

```r
var(standarized.iris$Sepal.Width)
```

```
## [1] 1
```
Join the standardized data with the response/target/label column (the column with the species names.

```r
standarized.iris$Species <- iris$Species

head(standarized.iris)
```

```
##   Sepal.Length Sepal.Width
## 1   -0.8976739  1.01560199
## 2   -1.1392005 -0.13153881
## 3   -1.3807271  0.32731751
## 4   -1.5014904  0.09788935
## 5   -1.0184372  1.24503015
## 6   -0.5353840  1.93331463
##   Petal.Length Petal.Width Species
## 1    -1.335752   -1.311052  setosa
## 2    -1.335752   -1.311052  setosa
## 3    -1.392399   -1.311052  setosa
## 4    -1.279104   -1.311052  setosa
## 5    -1.335752   -1.311052  setosa
## 6    -1.165809   -1.048667  setosa
```

**Train and Test Splits**
Use the caTools library to split your standardized data into train and test sets. Use a 70/30 split.

```r
library(caTools)

split <- sample.split(standarized.iris, SplitRatio = 0.7)

train <- subset(standarized.iris, split == TRUE)
test <- subset(standarized.iris, split == FALSE)
```

**Build a KNN model**
Call the class library.

```r
library(class)

predicted.species <- knn(train[1:4], test[1:4], train$Species, k = 1)

head(predicted.species)
```

```
## [1] setosa setosa setosa setosa setosa
## [6] setosa
## 3 Levels: setosa ... virginica
```

What was your misclassification rate?

```r
misclass.error <- mean(predicted.species != test$Species)

print(misclass.error)
```

```
## [1] 0.05
```

**Choosing a K Value**
Although our data is quite small for us to really get a feel for choosing a good K value, let's practice.

Create a plot of the error (misclassification) rate for k values ranging from 1 to 10.

```r
predicted.species <- NULL
error.rate <- NULL

for (i in 1:10) {
  set.seed(101)
  predicted.species <- knn(train[1:4], test[1:4], train$Species, k=i)
  error.rate[i] <- mean(test$Species != predicted.species)
}

## Visualize K elbow method
library(ggplot2)
k.values <- 1:10
error.df <- data.frame(error.rate,k.values)
print(error.df)
```

```
##    error.rate k.values
## 1  0.05000000        1
## 2  0.06666667        2
## 3  0.06666667        3
## 4  0.05000000        4
## 5  0.03333333        5
## 6  0.05000000        6
## 7  0.06666667        7
## 8  0.06666667        8
## 9  0.06666667        9
## 10 0.05000000       10
```

```r
ggplot(error.df, aes(k.values,error.rate)) + geom_point() + geom_line(lty = "dotted", color="red", size=2) + theme_bw() 
```

![plot of chunk unnamed-chunk-8](figure/unnamed-chunk-8-1.png)

