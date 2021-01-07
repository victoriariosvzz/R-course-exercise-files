---
title: "Section 13 - Advanced R Programming"
author: "Victoria"
date: "6/1/2021"
output: html_document
---



#**Built-in R Features and Functions**
## Seq(): Create a sequence

```r
seq(0,100,by=2) #creates a vector from 0 to 100, with a step-size of 2
```

```
##  [1]   0   2   4   6   8  10  12  14  16  18  20  22  24  26  28  30  32  34  36  38
## [21]  40  42  44  46  48  50  52  54  56  58  60  62  64  66  68  70  72  74  76  78
## [41]  80  82  84  86  88  90  92  94  96  98 100
```

```r
seq(0,24,by=10)
```

```
## [1]  0 10 20
```
## Sort(): Sort a vector

```r
v <- c(1,4,7,2,13,3,11)
v
```

```
## [1]  1  4  7  2 13  3 11
```

```r
sort(v) #it sorts the values in ascending order
```

```
## [1]  1  2  3  4  7 11 13
```

```r
sort(v,decreasing = TRUE) #it sorts the values in descending order
```

```
## [1] 13 11  7  4  3  2  1
```

```r
cv <- c("a","c","d")
sort(cv)
```

```
## [1] "a" "c" "d"
```
## rev(): Reverse elements in object

```r
v <- 1:10
v
```

```
##  [1]  1  2  3  4  5  6  7  8  9 10
```

```r
rev(v)
```

```
##  [1] 10  9  8  7  6  5  4  3  2  1
```
## append(): Merge objects together (works on vectors and lists)

```r
v <- 1:10
v2 <- 35:40
append(v,v2) #it merges them together
```

```
##  [1]  1  2  3  4  5  6  7  8  9 10 35 36 37 38 39 40
```
## Checking the **Data type** in R

```r
v <- c(1,2,3)

is.vector(v) #we check if it's a vector or not
```

```
## [1] TRUE
```

```r
is.data.frame(mtcars)
```

```
## [1] TRUE
```
## To **convert into another Data type**

```r
v <- 1:3

as.list(v)
```

```
## [[1]]
## [1] 1
## 
## [[2]]
## [1] 2
## 
## [[3]]
## [1] 3
```

```r
as.matrix(v)
```

```
##      [,1]
## [1,]    1
## [2,]    2
## [3,]    3
```

#**Apply**
##Sample function: to sample objects from a vector

```r
sample(x = 1:100,1) #we get a certain sample of random numbers from a vector x
```

```
## [1] 97
```
##Apply function: to apply a function over all the values in a vector or list

```r
v <- c(1,2,3,4,5)

addrand <- function(x){
  ran <- sample(1:100,1)
  return(x+ran)
}

print(addrand(10))
```

```
## [1] 64
```

```r
result <- lapply(v,addrand) #as a list
print(result)
```

```
## [[1]]
## [1] 95
## 
## [[2]]
## [1] 4
## 
## [[3]]
## [1] 19
## 
## [[4]]
## [1] 54
## 
## [[5]]
## [1] 59
```

```r
result <- sapply(v,addrand) #as a vector
print(result)
```

```
## [1] 32 61 58 45 59
```
Another example

```r
v <- 1:5

times2 <- function(num){
  return(num*2)
}
print(v)
```

```
## [1] 1 2 3 4 5
```

```r
result <- sapply(v,times2)
print(result)
```

```
## [1]  2  4  6  8 10
```
##Anonymous functions

```r
v <- 1:5

result <- sapply(v,function(num){num*2}) #we just created the anonymous function and used it
print(result)
```

```
## [1]  2  4  6  8 10
```


```r
v <- 1:5

add_choice <- function(num,choice){
  return(num+choice)
}

print(sapply(v,add_choice,choice=100))
```

```
## [1] 101 102 103 104 105
```
# **Math functions in R**
##abs():absolute value

```r
abs(-2)
```

```
## [1] 2
```

```r
abs(2)
```

```
## [1] 2
```

```r
v <- c(-1,-2,-3)
abs(v)
```

```
## [1] 1 2 3
```
##sum(): the sum of a vector

```r
sum(v)
```

```
## [1] -6
```
##mean(): the mean of a vector

```r
mean(v)
```

```
## [1] -2
```
##round(): round values (additional arguments to nearest)

```r
round(2.88887,digits = 0)
```

```
## [1] 3
```
**TIP: Google "R reference card" for the most useful cheat sheet of functions in R**

#**Regular Expressions**
##grepl: returns a logical
##grep: returns an index

```r
text <- "Hi there, how are you?"
text
```

```
## [1] "Hi there, how are you?"
```

```r
grepl("how",text) #to check if there's that element in the variable
```

```
## [1] TRUE
```

```r
grepl("dog",text)
```

```
## [1] FALSE
```

```r
v <- c("a","b","c","d")
grepl("b",v) #to find if the statement is true or false
```

```
## [1] FALSE  TRUE FALSE FALSE
```

```r
grep("b",v) #returns the indexes in which the value appears
```

```
## [1] 2
```

#**Date and Timestamps**
## Dates

```r
Sys.Date() #year-month-day
```

```
## [1] "2021-01-07"
```

```r
today <- Sys.Date()
class(today)
```

```
## [1] "Date"
```

We normally get the input date as a character, so we need to transfrom it into a date object in the **STANDARD DATE FORMAT!**

```r
c <- "1990-01-01"
class(c)
```

```
## [1] "character"
```

```r
c.Date <- as.Date(c)
class(c.Date)
```

```
## [1] "Date"
```
sometimes we don't get the dates in the needed format

```r
## This will give NA(s) in some locales; setting the C locale
## as in the commented lines will overcome this on most systems.
## lct <- Sys.getlocale("LC_TIME"); Sys.setlocale("LC_TIME", "C")
x <- c("1jan1960", "2jan1960", "31mar1960", "30jul1960")
z <- as.Date(x, "%d%b%Y")
## Sys.setlocale("LC_TIME", lct)

my.date <- as.Date("Nov-03-90",format = "%b-%d-%y")
my.date
```

```
## [1] "1990-11-03"
```

```r
my.date1 <- as.Date("June,01,2002",format="%B,%d,%Y")
my.date1
```

```
## [1] "2002-06-01"
```
**as.Date format code list:**
- %d Day (decimal)  
- %m Month (decimal)  
- %b Month (abbreviated)  
- %B Month (full name)  
- %y Year (2 digit)  
- %Y Year (4 digit)  

## **Time information**
R stores time info in POSIXct class

```r
#to convert strings into data type for time stamp information
as.POSIXct("11:02:03",format="%H:M:%S") #we actually don't use this, we use the following instead:
```

```
## [1] NA
```

```r
help("strptime") #here we find all the glossary of conversion from string to time info
strptime("11:02:03",format="%H:%M:%S") #now, it is a time data!!
```

```
## [1] "2021-01-07 11:02:03 CST"
```

