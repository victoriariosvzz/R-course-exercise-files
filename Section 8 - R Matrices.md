---
title: "Section 8 - R Matrices"
author: "Victoria"
date: "2/1/2021"
output: html_document
---



# ***Creating a matrix***
To create a matrix out of a vector

```r
v <- 1:10 #easy way to create a vector

matrix(v) #creates a matrix with 10 rows and 1 column
```

```
##       [,1]
##  [1,]    1
##  [2,]    2
##  [3,]    3
##  [4,]    4
##  [5,]    5
##  [6,]    6
##  [7,]    7
##  [8,]    8
##  [9,]    9
## [10,]   10
```
To create a matrix from zero

```r
matrix(v,nrow = 2) # I want a matrix with 2 rows and whatever columns with the values of v
```

```
##      [,1] [,2] [,3] [,4] [,5]
## [1,]    1    3    5    7    9
## [2,]    2    4    6    8   10
```

```r
matrix(1:12,byrow = FALSE, nrow = 4) # it starts filling the values vertically
```

```
##      [,1] [,2] [,3]
## [1,]    1    5    9
## [2,]    2    6   10
## [3,]    3    7   11
## [4,]    4    8   12
```

```r
matrix(1:12,byrow = TRUE, nrow = 4) # it starts filling the values horizontally (row by row)
```

```
##      [,1] [,2] [,3]
## [1,]    1    2    3
## [2,]    4    5    6
## [3,]    7    8    9
## [4,]   10   11   12
```


```r
goog <- c(450,451,452,445,468)
msft <- c(230,231,232,233,220)

stocks <-c(goog,msft) #to combine both vectors in one
print(stocks)
```

```
##  [1] 450 451 452 445 468 230 231 232 233 220
```

```r
stock.matrix <- matrix(stocks, byrow = TRUE, nrow = 2)
print(stock.matrix)
```

```
##      [,1] [,2] [,3] [,4] [,5]
## [1,]  450  451  452  445  468
## [2,]  230  231  232  233  220
```

```r
#To name the rows and columns values
days <- c("Mon","Tue","Wed","Thu","Fri")
st.names <- c("GOOG","MSFT")

colnames(stock.matrix) <- days
rownames(stock.matrix) <- st.names
print(stock.matrix)
```

```
##      Mon Tue Wed Thu Fri
## GOOG 450 451 452 445 468
## MSFT 230 231 232 233 220
```

# ***Matrix Arithmetic***
All the operations made to the matrix are made element by element

```r
mat <- matrix(1:25, byrow = TRUE, nrow = 5)
mat
```

```
##      [,1] [,2] [,3] [,4] [,5]
## [1,]    1    2    3    4    5
## [2,]    6    7    8    9   10
## [3,]   11   12   13   14   15
## [4,]   16   17   18   19   20
## [5,]   21   22   23   24   25
```

```r
# Examples of operations
mat * 2
```

```
##      [,1] [,2] [,3] [,4] [,5]
## [1,]    2    4    6    8   10
## [2,]   12   14   16   18   20
## [3,]   22   24   26   28   30
## [4,]   32   34   36   38   40
## [5,]   42   44   46   48   50
```

```r
mat - 2
```

```
##      [,1] [,2] [,3] [,4] [,5]
## [1,]   -1    0    1    2    3
## [2,]    4    5    6    7    8
## [3,]    9   10   11   12   13
## [4,]   14   15   16   17   18
## [5,]   19   20   21   22   23
```

```r
mat / 2
```

```
##      [,1] [,2] [,3] [,4] [,5]
## [1,]  0.5  1.0  1.5  2.0  2.5
## [2,]  3.0  3.5  4.0  4.5  5.0
## [3,]  5.5  6.0  6.5  7.0  7.5
## [4,]  8.0  8.5  9.0  9.5 10.0
## [5,] 10.5 11.0 11.5 12.0 12.5
```

```r
mat^2
```

```
##      [,1] [,2] [,3] [,4] [,5]
## [1,]    1    4    9   16   25
## [2,]   36   49   64   81  100
## [3,]  121  144  169  196  225
## [4,]  256  289  324  361  400
## [5,]  441  484  529  576  625
```

```r
mat > 15
```

```
##       [,1]  [,2]  [,3]  [,4]  [,5]
## [1,] FALSE FALSE FALSE FALSE FALSE
## [2,] FALSE FALSE FALSE FALSE FALSE
## [3,] FALSE FALSE FALSE FALSE FALSE
## [4,]  TRUE  TRUE  TRUE  TRUE  TRUE
## [5,]  TRUE  TRUE  TRUE  TRUE  TRUE
```

```r
#We can also filter out some values of the matrix in a form of a vector
mat.f <- mat[mat>15]
mat.f
```

```
##  [1] 16 21 17 22 18 23 19 24 20 25
```

```r
mat * mat # element by element multiplication
```

```
##      [,1] [,2] [,3] [,4] [,5]
## [1,]    1    4    9   16   25
## [2,]   36   49   64   81  100
## [3,]  121  144  169  196  225
## [4,]  256  289  324  361  400
## [5,]  441  484  529  576  625
```

```r
mat %*% mat # real linear algebra matrix multiplication
```

```
##      [,1] [,2] [,3] [,4] [,5]
## [1,]  215  230  245  260  275
## [2,]  490  530  570  610  650
## [3,]  765  830  895  960 1025
## [4,] 1040 1130 1220 1310 1400
## [5,] 1315 1430 1545 1660 1775
```

# ***Matrix operations***
We start with the previous matrix

```r
goog <- c(450,451,452,445,468)
msft <- c(230,231,232,233,220)

stocks <-c(goog,msft) #to combine both vectors in one
print(stocks)
```

```
##  [1] 450 451 452 445 468 230 231 232 233 220
```

```r
stock.matrix <- matrix(stocks, byrow = TRUE, nrow = 2)
print(stock.matrix)
```

```
##      [,1] [,2] [,3] [,4] [,5]
## [1,]  450  451  452  445  468
## [2,]  230  231  232  233  220
```

```r
#To name the rows and columns values
days <- c("Mon","Tue","Wed","Thu","Fri")
st.names <- c("GOOG","MSFT")

colnames(stock.matrix) <- days
rownames(stock.matrix) <- st.names
print(stock.matrix)
```

```
##      Mon Tue Wed Thu Fri
## GOOG 450 451 452 445 468
## MSFT 230 231 232 233 220
```
Operations on the matrix

```r
colSums(stock.matrix) #it adds all the values on each column
```

```
## Mon Tue Wed Thu Fri 
## 680 682 684 678 688
```

```r
rowSums(stock.matrix) #it adds all the values on each row
```

```
## GOOG MSFT 
## 2266 1146
```

```r
rowMeans(stock.matrix) #mean value of the rows
```

```
##  GOOG  MSFT 
## 453.2 229.2
```

```r
colMeans(stock.matrix) #mean value of the columns
```

```
## Mon Tue Wed Thu Fri 
## 340 341 342 339 344
```
Exercise: Add a vector as a new row of your previous matrix

```r
Fbook <- c(111,112,113,114,115)
# Function rbind
tech.stocks <- rbind(stock.matrix,Fbook) # rbind adds the selected vector as a new row of the selected matrix
tech.stocks
```

```
##       Mon Tue Wed Thu Fri
## GOOG  450 451 452 445 468
## MSFT  230 231 232 233 220
## Fbook 111 112 113 114 115
```

```r
# Function cbind
avg <- rowMeans(tech.stocks)
avg
```

```
##  GOOG  MSFT Fbook 
## 453.2 229.2 113.0
```

```r
tech.stocks <- cbind(tech.stocks,avg) # rbind adds the selected vector as a new column of the selected matrix
tech.stocks
```

```
##       Mon Tue Wed Thu Fri   avg
## GOOG  450 451 452 445 468 453.2
## MSFT  230 231 232 233 220 229.2
## Fbook 111 112 113 114 115 113.0
```

# ***Matrix selection and Indexing***
Creating the matrix

```r
mat <- matrix(1:50, byrow = TRUE, nrow = 5)
mat
```

```
##      [,1] [,2] [,3] [,4] [,5] [,6] [,7] [,8] [,9] [,10]
## [1,]    1    2    3    4    5    6    7    8    9    10
## [2,]   11   12   13   14   15   16   17   18   19    20
## [3,]   21   22   23   24   25   26   27   28   29    30
## [4,]   31   32   33   34   35   36   37   38   39    40
## [5,]   41   42   43   44   45   46   47   48   49    50
```
Lets index!

```r
mat[1,] #all the columns of the 1st row
```

```
##  [1]  1  2  3  4  5  6  7  8  9 10
```

```r
mat[,1] #all the rows of the 1st column
```

```
## [1]  1 11 21 31 41
```

```r
mat[] #all the values of the matrix
```

```
##      [,1] [,2] [,3] [,4] [,5] [,6] [,7] [,8] [,9] [,10]
## [1,]    1    2    3    4    5    6    7    8    9    10
## [2,]   11   12   13   14   15   16   17   18   19    20
## [3,]   21   22   23   24   25   26   27   28   29    30
## [4,]   31   32   33   34   35   36   37   38   39    40
## [5,]   41   42   43   44   45   46   47   48   49    50
```

```r
mat[1:3,] #all the columns of the rows 1 to 3
```

```
##      [,1] [,2] [,3] [,4] [,5] [,6] [,7] [,8] [,9] [,10]
## [1,]    1    2    3    4    5    6    7    8    9    10
## [2,]   11   12   13   14   15   16   17   18   19    20
## [3,]   21   22   23   24   25   26   27   28   29    30
```

```r
mat[1:2,1:3]
```

```
##      [,1] [,2] [,3]
## [1,]    1    2    3
## [2,]   11   12   13
```

```r
mat[,9:10]
```

```
##      [,1] [,2]
## [1,]    9   10
## [2,]   19   20
## [3,]   29   30
## [4,]   39   40
## [5,]   49   50
```

```r
mat[2:3,5:6]
```

```
##      [,1] [,2]
## [1,]   15   16
## [2,]   25   26
```

# ***Factor and categorical matrices***

**Factor function** is useful to create categorical matrices
There are 2 types of categorical variables:

- **Nominal:** There's NO order  
- **Ordinal:** There's order (like numbers, temp, letters a to z)  

Nominal example:

```r
animal <- c("dog","cat","dog","cat","cat")
id <- c(1,2,3,4,5)

factor(animal) # Finds the categories within the values of our vector
```

```
## [1] dog cat dog cat cat
## Levels: cat dog
```

```r
fact.ani <- factor(animal)
```
Ordinal example with temps:

```r
ord.cat <- c("cold","med","hot")
temps <- c("cold","med","hot","hot","hot","cold","med")
temps
```

```
## [1] "cold" "med"  "hot"  "hot"  "hot"  "cold" "med"
```

```r
fact.temp <- factor(temps, ordered = TRUE, levels = c("cold","med","hot")) #we can tell the factor function our levels of categorization
fact.temp
```

```
## [1] cold med  hot  hot  hot  cold med 
## Levels: cold < med < hot
```

We can use this to find the # of times a value appears in a vector

```r
# Summary function
summary(fact.temp) #of the categorized vector
```

```
## cold  med  hot 
##    2    2    3
```

```r
summary(temps) # of the uncategorized vector (not the expected results)
```

```
##    Length     Class      Mode 
##         7 character character
```

# **...R Matrix Exercises...**

Create 2 vectors A and B, where A is (1,2,3) and B is (4,5,6). With these vectors, use the cbind() or rbind() function to create a 2 by 3 matrix from the vectors. You'll need to figure out which of these binding functions is the correct choice.


```r
A <- 1:3
B <- 4:6
matrix.AB <- rbind(A,B)
matrix.AB
```

```
##   [,1] [,2] [,3]
## A    1    2    3
## B    4    5    6
```

Create a 3 by 3 matrix consisting of the numbers 1-9. Create this matrix using the shortcut 1:9 and by specifying the nrow argument in the matrix() function call. Assign this matrix to the variable mat

```r
mat <- matrix(1:9, nrow = 3)
mat
```

```
##      [,1] [,2] [,3]
## [1,]    1    4    7
## [2,]    2    5    8
## [3,]    3    6    9
```
Confirm that mat is a matrix using is.matrix()

```r
is.matrix(mat)
```

```
## [1] TRUE
```

Create a 5 by 5 matrix consisting of the numbers 1-25 and assign it to the variable mat2. The top row should be the numbers 1-5.

```r
mat2 <- matrix(1:25,byrow = TRUE, nrow = 5)
mat2
```

```
##      [,1] [,2] [,3] [,4] [,5]
## [1,]    1    2    3    4    5
## [2,]    6    7    8    9   10
## [3,]   11   12   13   14   15
## [4,]   16   17   18   19   20
## [5,]   21   22   23   24   25
```

Using indexing notation, grab a sub-section of mat2 from the previous exercise that looks like this: 
[7,8]
[12,13]

```r
mat2[2:3,2:3]
```

```
##      [,1] [,2]
## [1,]    7    8
## [2,]   12   13
```
Using indexing notation, grab a sub-section of mat2 from the previous exercise that looks like this:
[19,20]
[24,25]

```r
mat2[4:5,4:5]
```

```
##      [,1] [,2]
## [1,]   19   20
## [2,]   24   25
```
What is the sum of all the elements in mat2?

```r
sum(mat2)
```

```
## [1] 325
```
Ok time for our last exercise! Find out how to use runif() to create a 4 by 5 matrix consisting of 20 random numbers (4*5=20).

```r
v <- runif(20, min = 0, max = 100) #creates a vector of random numbers from min to max
v
```

```
##  [1] 77.585917 90.111945  8.749677 61.439053 32.315146 70.036214 90.982198 37.137448
##  [9] 60.221008 28.183307 66.505413 54.068062  5.948450 17.086280 81.690026 99.355656
## [17]  8.619422 68.605398 79.512132 55.158848
```

```r
v.mat <- matrix(v,byrow = FALSE, nrow = 4)
v.mat
```

```
##           [,1]     [,2]     [,3]     [,4]      [,5]
## [1,] 77.585917 32.31515 60.22101  5.94845  8.619422
## [2,] 90.111945 70.03621 28.18331 17.08628 68.605398
## [3,]  8.749677 90.98220 66.50541 81.69003 79.512132
## [4,] 61.439053 37.13745 54.06806 99.35566 55.158848
```

