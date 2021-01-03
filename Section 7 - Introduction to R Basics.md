---
title: "Video's notes"
author: "Victoria"
date: "2/1/2021"
output: html_document
---



# ***Basic arithmetic***

### Addition

```r
1 + 1
```

```
## [1] 2
```

### Subtraction

```r
5 - 3
```

```
## [1] 2
```

### Division

```r
2/3
```

```
## [1] 0.6666667
```

### Power

```r
2^3
```

```
## [1] 8
```

### Product

```r
2 * 3
```

```
## [1] 6
```

### Remainder (Modulus)

```r
3 %% 2
```

```
## [1] 1
```

# ***Variables***

```r
variable <- 100 #to assign it
variable #to print it
```

```
## [1] 100
```

```r
bank <- 1000
bank
```

```
## [1] 1000
```

```r
#This are good practices to name variables:
bank.account <-123
bankAccount <-133

#Assigning results into variables
deposit <- 100
total <- bank.account + deposit
total #printing the result
```

```
## [1] 223
```

# ***Data types***

```r
1 #integer
```

```
## [1] 1
```

```r
1.5 #float or decimals
```

```
## [1] 1.5
```

```r
"hello" #character
```

```
## [1] "hello"
```

```r
TRUE #logical or boolean
```

```
## [1] TRUE
```

```r
class(deposit) #to check the class of a variable
```

```
## [1] "numeric"
```

# ***Vector***

```r
nvec <- c(1,2,3,4,5) #a vector is created using the "combination function" [c()], each number represents a column
nvec #we print it
```

```
## [1] 1 2 3 4 5
```

```r
cvec <- c("U","S","A")
cvec
```

```
## [1] "U" "S" "A"
```

```r
lvec <- c(T, F)
lvec
```

```
## [1]  TRUE FALSE
```

### Combining data types in a vector
Rule: **never combine** different data types in a vector, or it will forcefully change them to the same data type, e.g. TRUE in a numeric vector changes to "1".

```r
v <- c(TRUE, 20, 40)
v
```

```
## [1]  1 20 40
```

```r
class(v)
```

```
## [1] "numeric"
```

### Vector names
We can assign a name to **each value in a vector**, for example, to associate days with a vector of temps values

```r
temps <- c(72,71,68,73,69,75,23)
temps
```

```
## [1] 72 71 68 73 69 75 23
```

```r
names(temps) <- c("Mon","Tue","Wed","Thu","Fri","Sat","Sun")
temps #now the vector has a name for each value
```

```
## Mon Tue Wed Thu Fri Sat Sun 
##  72  71  68  73  69  75  23
```
Another way to do it, faster, is by creating the names vector independently and then use it

```r
days <- c("Mon","Tue","Wed","Thu","Fri","Sat","Sun")
names(temps) <- days
temps
```

```
## Mon Tue Wed Thu Fri Sat Sun 
##  72  71  68  73  69  75  23
```

# ***Vector operations***

```r
v1 <- c(1,2,3)
v2 <- c(5,6,7)
v1 + v2 #It will make the operation ELEMENT BY ELEMENT
```

```
## [1]  6  8 10
```

```r
v1 * v2
```

```
## [1]  5 12 21
```

```r
v1 - v2
```

```
## [1] -4 -4 -4
```

```r
v1 / v2
```

```
## [1] 0.2000000 0.3333333 0.4285714
```

```r
# To sum all the elements in a numeric vector
sum(v1)
```

```
## [1] 6
```

```r
sum.of.v1 <- sum(v1)
sum.of.v1
```

```
## [1] 6
```

```r
# mean of a vector
mean(v1)
```

```
## [1] 2
```

```r
# standard deviation of a vector
sd(v1)
```

```
## [1] 1
```

```r
# maximum value
max(v1)
```

```
## [1] 3
```

```r
# minimum value
min(v1)
```

```
## [1] 1
```

```r
# product of all the elements in a vector
prod(v1)
```

```
## [1] 6
```

# ***Comparison operators***
They will return a TRUE or FALSE according to the operation

```r
5 > 6
```

```
## [1] FALSE
```

```r
5 < 6
```

```
## [1] TRUE
```

```r
5 <= 6
```

```
## [1] TRUE
```

```r
2 == 3 #equality
```

```
## [1] FALSE
```

```r
2 != 4 #inequality
```

```
## [1] TRUE
```

```r
my.var <- 2
my.var > 5
```

```
## [1] FALSE
```

When comparing vector values, it will return a **vector result** filled with TRUE and FALSE

```r
v <- c(1,2,3,4,5)
v < 2 # Comparison is done ELEMENT BY ELEMENT
```

```
## [1]  TRUE FALSE FALSE FALSE FALSE
```

```r
v == 3
```

```
## [1] FALSE FALSE  TRUE FALSE FALSE
```

We can also compare two vectors

```r
v2 <- c(10, 20, 30, 40, 50)
v < v2
```

```
## [1] TRUE TRUE TRUE TRUE TRUE
```

# ***Vector indexing and slicing***
NOTE: Indexing starts at number 1

```r
v1 <- c(100,200,300)
v2 <- c("a","b","c")
v1
```

```
## [1] 100 200 300
```

```r
v2
```

```
## [1] "a" "b" "c"
```

```r
#Lets start indexing values from the vectors
v1[1]
```

```
## [1] 100
```

```r
v1[3]
```

```
## [1] 300
```

```r
v2[3]
```

```
## [1] "c"
```
Slicing means we're gonna take multiple items from a vector at the same time

```r
#Lets start slicing
v1[c(1,2)] #to grab the 1st and 2nd element
```

```
## [1] 100 200
```

```r
v2[c(1,3)] #to grab a and c
```

```
## [1] "a" "c"
```

```r
#to grab continuous elements
v <- c(1,2,3,4,5,6,7,8,9,10)
v
```

```
##  [1]  1  2  3  4  5  6  7  8  9 10
```

```r
v[2:5] #To grab from the 2nd element till the 5th element of the vector
```

```
## [1] 2 3 4 5
```

```r
v[7:10]
```

```
## [1]  7  8  9 10
```

Lets assign names to the values of our slice, and **we can actually index it as the name given instead of the number of element**

```r
v.slice <- v[7:10]
v.slice
```

```
## [1]  7  8  9 10
```

```r
v.names <- c("a","b","c","d")

names(v.slice) <- v.names #names assigned
v.slice
```

```
##  a  b  c  d 
##  7  8  9 10
```

```r
# We can index the values as the names given
v.slice[2]
```

```
## b 
## 8
```

```r
v.slice["b"]
```

```
## b 
## 8
```

```r
v.slice[c("c","a","d")]
```

```
##  c  a  d 
##  9  7 10
```

To grab only values greater than 2

```r
v
```

```
##  [1]  1  2  3  4  5  6  7  8  9 10
```

```r
v.labels <- c("a","b","c","d","e","f","g","h","i","j")
names(v) <- v.labels

v[v>2] # it returns only the values that are greater than 2
```

```
##  c  d  e  f  g  h  i  j 
##  3  4  5  6  7  8  9 10
```

```r
# Another way to do it
my.filter <- v>2
v[my.filter]
```

```
##  c  d  e  f  g  h  i  j 
##  3  4  5  6  7  8  9 10
```
# ***To search for help and info about terms and funcitons in R***

```r
help("vector")
??vector
help.search("vector")
```

# ***....R Basics Exercises...***
What is 2 to the power of 5

```r
2^5
```

```
## [1] 32
```
Create a vector called stock.prices with the following data points: 23,27,23,21,34

```r
stock.prices <- c(23,27,23,21,34)
```
Assign names to the price data points relating to the day of the week, starting with Mon, Tue, Wed, etc...

```r
stock.names <- c("Mon","Tue","Wed","Thu","Fri")
names(stock.prices) <- stock.names
stock.prices
```

```
## Mon Tue Wed Thu Fri 
##  23  27  23  21  34
```
What was the average (mean) stock price for the week? (You may need to reference a built-in function)

```r
mean(stock.prices)
```

```
## [1] 25.6
```
Create a vector called over.23 consisting of logicals that correspond to the days where the stock price was more than $23

```r
over.23 <- stock.prices[stock.prices>23]
```

Use the over.23 vector to filter out the stock.prices vector and only return the day and prices where the price was over $23


```r
over.23
```

```
## Tue Fri 
##  27  34
```

Use a built-in function to find the day the price was the highest

```r
max(stock.prices)
```

```
## [1] 34
```

