---
title: "Section 12 - R Programming Basics"
author: "Victoria"
date: "5/1/2021"
output: html_document
---



#**Logical operators**
AND, OR and NOT

```r
# AND (all should be TRUE to be TRUE)
x <- 10
x < 20 & x > 5 # is x < 20 and x > 5 ?
```

```
## [1] TRUE
```

```r
(x<20) & (x>5) & (x==10)
```

```
## [1] TRUE
```

```r
(x<20) & (x>5) & (x==1)
```

```
## [1] FALSE
```

```r
# OR (all should be FALSE to be FALSE)
(x<20) | (x>5) | (x==1)
```

```
## [1] TRUE
```

```r
# NOT (inverse to what you're writing)
(10 == 1)
```

```
## [1] FALSE
```

```r
!(10 == 1) # is this NOT TRUE?
```

```
## [1] TRUE
```
## Realistic use cases

```r
df <- mtcars
head(df)
```

```
##                    mpg cyl disp  hp
## Mazda RX4         21.0   6  160 110
## Mazda RX4 Wag     21.0   6  160 110
## Datsun 710        22.8   4  108  93
## Hornet 4 Drive    21.4   6  258 110
## Hornet Sportabout 18.7   8  360 175
## Valiant           18.1   6  225 105
##                   drat    wt  qsec vs
## Mazda RX4         3.90 2.620 16.46  0
## Mazda RX4 Wag     3.90 2.875 17.02  0
## Datsun 710        3.85 2.320 18.61  1
## Hornet 4 Drive    3.08 3.215 19.44  1
## Hornet Sportabout 3.15 3.440 17.02  0
## Valiant           2.76 3.460 20.22  1
##                   am gear carb
## Mazda RX4          1    4    4
## Mazda RX4 Wag      1    4    4
## Datsun 710         1    4    1
## Hornet 4 Drive     0    3    1
## Hornet Sportabout  0    3    2
## Valiant            0    3    1
```

```r
df[df$cyl > 4,] #all the rows in which cyl > 4
```

```
##                      mpg cyl  disp  hp
## Mazda RX4           21.0   6 160.0 110
## Mazda RX4 Wag       21.0   6 160.0 110
## Hornet 4 Drive      21.4   6 258.0 110
## Hornet Sportabout   18.7   8 360.0 175
## Valiant             18.1   6 225.0 105
## Duster 360          14.3   8 360.0 245
## Merc 280            19.2   6 167.6 123
## Merc 280C           17.8   6 167.6 123
## Merc 450SE          16.4   8 275.8 180
## Merc 450SL          17.3   8 275.8 180
## Merc 450SLC         15.2   8 275.8 180
## Cadillac Fleetwood  10.4   8 472.0 205
## Lincoln Continental 10.4   8 460.0 215
## Chrysler Imperial   14.7   8 440.0 230
## Dodge Challenger    15.5   8 318.0 150
## AMC Javelin         15.2   8 304.0 150
## Camaro Z28          13.3   8 350.0 245
## Pontiac Firebird    19.2   8 400.0 175
## Ford Pantera L      15.8   8 351.0 264
## Ferrari Dino        19.7   6 145.0 175
## Maserati Bora       15.0   8 301.0 335
##                     drat    wt  qsec
## Mazda RX4           3.90 2.620 16.46
## Mazda RX4 Wag       3.90 2.875 17.02
## Hornet 4 Drive      3.08 3.215 19.44
## Hornet Sportabout   3.15 3.440 17.02
## Valiant             2.76 3.460 20.22
## Duster 360          3.21 3.570 15.84
## Merc 280            3.92 3.440 18.30
## Merc 280C           3.92 3.440 18.90
## Merc 450SE          3.07 4.070 17.40
## Merc 450SL          3.07 3.730 17.60
## Merc 450SLC         3.07 3.780 18.00
## Cadillac Fleetwood  2.93 5.250 17.98
## Lincoln Continental 3.00 5.424 17.82
## Chrysler Imperial   3.23 5.345 17.42
## Dodge Challenger    2.76 3.520 16.87
## AMC Javelin         3.15 3.435 17.30
## Camaro Z28          3.73 3.840 15.41
## Pontiac Firebird    3.08 3.845 17.05
## Ford Pantera L      4.22 3.170 14.50
## Ferrari Dino        3.62 2.770 15.50
## Maserati Bora       3.54 3.570 14.60
##                     vs am gear carb
## Mazda RX4            0  1    4    4
## Mazda RX4 Wag        0  1    4    4
## Hornet 4 Drive       1  0    3    1
## Hornet Sportabout    0  0    3    2
## Valiant              1  0    3    1
## Duster 360           0  0    3    4
## Merc 280             1  0    4    4
## Merc 280C            1  0    4    4
## Merc 450SE           0  0    3    3
## Merc 450SL           0  0    3    3
## Merc 450SLC          0  0    3    3
## Cadillac Fleetwood   0  0    3    4
## Lincoln Continental  0  0    3    4
## Chrysler Imperial    0  0    3    4
## Dodge Challenger     0  0    3    2
## AMC Javelin          0  0    3    2
## Camaro Z28           0  0    3    4
## Pontiac Firebird     0  0    3    2
## Ford Pantera L       0  1    5    4
## Ferrari Dino         0  1    5    6
## Maserati Bora        0  1    5    8
```

```r
subset(df,cyl > 4)
```

```
##                      mpg cyl  disp  hp
## Mazda RX4           21.0   6 160.0 110
## Mazda RX4 Wag       21.0   6 160.0 110
## Hornet 4 Drive      21.4   6 258.0 110
## Hornet Sportabout   18.7   8 360.0 175
## Valiant             18.1   6 225.0 105
## Duster 360          14.3   8 360.0 245
## Merc 280            19.2   6 167.6 123
## Merc 280C           17.8   6 167.6 123
## Merc 450SE          16.4   8 275.8 180
## Merc 450SL          17.3   8 275.8 180
## Merc 450SLC         15.2   8 275.8 180
## Cadillac Fleetwood  10.4   8 472.0 205
## Lincoln Continental 10.4   8 460.0 215
## Chrysler Imperial   14.7   8 440.0 230
## Dodge Challenger    15.5   8 318.0 150
## AMC Javelin         15.2   8 304.0 150
## Camaro Z28          13.3   8 350.0 245
## Pontiac Firebird    19.2   8 400.0 175
## Ford Pantera L      15.8   8 351.0 264
## Ferrari Dino        19.7   6 145.0 175
## Maserati Bora       15.0   8 301.0 335
##                     drat    wt  qsec
## Mazda RX4           3.90 2.620 16.46
## Mazda RX4 Wag       3.90 2.875 17.02
## Hornet 4 Drive      3.08 3.215 19.44
## Hornet Sportabout   3.15 3.440 17.02
## Valiant             2.76 3.460 20.22
## Duster 360          3.21 3.570 15.84
## Merc 280            3.92 3.440 18.30
## Merc 280C           3.92 3.440 18.90
## Merc 450SE          3.07 4.070 17.40
## Merc 450SL          3.07 3.730 17.60
## Merc 450SLC         3.07 3.780 18.00
## Cadillac Fleetwood  2.93 5.250 17.98
## Lincoln Continental 3.00 5.424 17.82
## Chrysler Imperial   3.23 5.345 17.42
## Dodge Challenger    2.76 3.520 16.87
## AMC Javelin         3.15 3.435 17.30
## Camaro Z28          3.73 3.840 15.41
## Pontiac Firebird    3.08 3.845 17.05
## Ford Pantera L      4.22 3.170 14.50
## Ferrari Dino        3.62 2.770 15.50
## Maserati Bora       3.54 3.570 14.60
##                     vs am gear carb
## Mazda RX4            0  1    4    4
## Mazda RX4 Wag        0  1    4    4
## Hornet 4 Drive       1  0    3    1
## Hornet Sportabout    0  0    3    2
## Valiant              1  0    3    1
## Duster 360           0  0    3    4
## Merc 280             1  0    4    4
## Merc 280C            1  0    4    4
## Merc 450SE           0  0    3    3
## Merc 450SL           0  0    3    3
## Merc 450SLC          0  0    3    3
## Cadillac Fleetwood   0  0    3    4
## Lincoln Continental  0  0    3    4
## Chrysler Imperial    0  0    3    4
## Dodge Challenger     0  0    3    2
## AMC Javelin          0  0    3    2
## Camaro Z28           0  0    3    4
## Pontiac Firebird     0  0    3    2
## Ford Pantera L       0  1    5    4
## Ferrari Dino         0  1    5    6
## Maserati Bora        0  1    5    8
```

```r
df[,c("mpg","cyl")]
```

```
##                      mpg cyl
## Mazda RX4           21.0   6
## Mazda RX4 Wag       21.0   6
## Datsun 710          22.8   4
## Hornet 4 Drive      21.4   6
## Hornet Sportabout   18.7   8
## Valiant             18.1   6
## Duster 360          14.3   8
## Merc 240D           24.4   4
## Merc 230            22.8   4
## Merc 280            19.2   6
## Merc 280C           17.8   6
## Merc 450SE          16.4   8
## Merc 450SL          17.3   8
## Merc 450SLC         15.2   8
## Cadillac Fleetwood  10.4   8
## Lincoln Continental 10.4   8
## Chrysler Imperial   14.7   8
## Fiat 128            32.4   4
## Honda Civic         30.4   4
## Toyota Corolla      33.9   4
## Toyota Corona       21.5   4
## Dodge Challenger    15.5   8
## AMC Javelin         15.2   8
## Camaro Z28          13.3   8
## Pontiac Firebird    19.2   8
## Fiat X1-9           27.3   4
## Porsche 914-2       26.0   4
## Lotus Europa        30.4   4
## Ford Pantera L      15.8   8
## Ferrari Dino        19.7   6
## Maserati Bora       15.0   8
## Volvo 142E          21.4   4
```
Using the logical operators

```r
df[(df$mpg > 20) & (df$hp > 100),]
```

```
##                 mpg cyl  disp  hp drat
## Mazda RX4      21.0   6 160.0 110 3.90
## Mazda RX4 Wag  21.0   6 160.0 110 3.90
## Hornet 4 Drive 21.4   6 258.0 110 3.08
## Lotus Europa   30.4   4  95.1 113 3.77
## Volvo 142E     21.4   4 121.0 109 4.11
##                   wt  qsec vs am gear
## Mazda RX4      2.620 16.46  0  1    4
## Mazda RX4 Wag  2.875 17.02  0  1    4
## Hornet 4 Drive 3.215 19.44  1  0    3
## Lotus Europa   1.513 16.90  1  1    5
## Volvo 142E     2.780 18.60  1  1    4
##                carb
## Mazda RX4         4
## Mazda RX4 Wag     4
## Hornet 4 Drive    1
## Lotus Europa      2
## Volvo 142E        2
```

```r
df[(df$mpg > 20) | (df$hp > 100),]
```

```
##                      mpg cyl  disp  hp
## Mazda RX4           21.0   6 160.0 110
## Mazda RX4 Wag       21.0   6 160.0 110
## Datsun 710          22.8   4 108.0  93
## Hornet 4 Drive      21.4   6 258.0 110
## Hornet Sportabout   18.7   8 360.0 175
## Valiant             18.1   6 225.0 105
## Duster 360          14.3   8 360.0 245
## Merc 240D           24.4   4 146.7  62
## Merc 230            22.8   4 140.8  95
## Merc 280            19.2   6 167.6 123
## Merc 280C           17.8   6 167.6 123
## Merc 450SE          16.4   8 275.8 180
## Merc 450SL          17.3   8 275.8 180
## Merc 450SLC         15.2   8 275.8 180
## Cadillac Fleetwood  10.4   8 472.0 205
## Lincoln Continental 10.4   8 460.0 215
## Chrysler Imperial   14.7   8 440.0 230
## Fiat 128            32.4   4  78.7  66
## Honda Civic         30.4   4  75.7  52
## Toyota Corolla      33.9   4  71.1  65
## Toyota Corona       21.5   4 120.1  97
## Dodge Challenger    15.5   8 318.0 150
## AMC Javelin         15.2   8 304.0 150
## Camaro Z28          13.3   8 350.0 245
## Pontiac Firebird    19.2   8 400.0 175
## Fiat X1-9           27.3   4  79.0  66
## Porsche 914-2       26.0   4 120.3  91
## Lotus Europa        30.4   4  95.1 113
## Ford Pantera L      15.8   8 351.0 264
## Ferrari Dino        19.7   6 145.0 175
## Maserati Bora       15.0   8 301.0 335
## Volvo 142E          21.4   4 121.0 109
##                     drat    wt  qsec
## Mazda RX4           3.90 2.620 16.46
## Mazda RX4 Wag       3.90 2.875 17.02
## Datsun 710          3.85 2.320 18.61
## Hornet 4 Drive      3.08 3.215 19.44
## Hornet Sportabout   3.15 3.440 17.02
## Valiant             2.76 3.460 20.22
## Duster 360          3.21 3.570 15.84
## Merc 240D           3.69 3.190 20.00
## Merc 230            3.92 3.150 22.90
## Merc 280            3.92 3.440 18.30
## Merc 280C           3.92 3.440 18.90
## Merc 450SE          3.07 4.070 17.40
## Merc 450SL          3.07 3.730 17.60
## Merc 450SLC         3.07 3.780 18.00
## Cadillac Fleetwood  2.93 5.250 17.98
## Lincoln Continental 3.00 5.424 17.82
## Chrysler Imperial   3.23 5.345 17.42
## Fiat 128            4.08 2.200 19.47
## Honda Civic         4.93 1.615 18.52
## Toyota Corolla      4.22 1.835 19.90
## Toyota Corona       3.70 2.465 20.01
## Dodge Challenger    2.76 3.520 16.87
## AMC Javelin         3.15 3.435 17.30
## Camaro Z28          3.73 3.840 15.41
## Pontiac Firebird    3.08 3.845 17.05
## Fiat X1-9           4.08 1.935 18.90
## Porsche 914-2       4.43 2.140 16.70
## Lotus Europa        3.77 1.513 16.90
## Ford Pantera L      4.22 3.170 14.50
## Ferrari Dino        3.62 2.770 15.50
## Maserati Bora       3.54 3.570 14.60
## Volvo 142E          4.11 2.780 18.60
##                     vs am gear carb
## Mazda RX4            0  1    4    4
## Mazda RX4 Wag        0  1    4    4
## Datsun 710           1  1    4    1
## Hornet 4 Drive       1  0    3    1
## Hornet Sportabout    0  0    3    2
## Valiant              1  0    3    1
## Duster 360           0  0    3    4
## Merc 240D            1  0    4    2
## Merc 230             1  0    4    2
## Merc 280             1  0    4    4
## Merc 280C            1  0    4    4
## Merc 450SE           0  0    3    3
## Merc 450SL           0  0    3    3
## Merc 450SLC          0  0    3    3
## Cadillac Fleetwood   0  0    3    4
## Lincoln Continental  0  0    3    4
## Chrysler Imperial    0  0    3    4
## Fiat 128             1  1    4    1
## Honda Civic          1  1    4    2
## Toyota Corolla       1  1    4    1
## Toyota Corona        1  0    3    1
## Dodge Challenger     0  0    3    2
## AMC Javelin          0  0    3    2
## Camaro Z28           0  0    3    4
## Pontiac Firebird     0  0    3    2
## Fiat X1-9            1  1    4    1
## Porsche 914-2        0  1    5    2
## Lotus Europa         1  1    5    2
## Ford Pantera L       0  1    5    4
## Ferrari Dino         0  1    5    6
## Maserati Bora        0  1    5    8
## Volvo 142E           1  1    4    2
```

#**If, else and ifelse statement**

```r
x <- 10
if(x == 10){
  #code to run if it's true
  print("x is equal to 10!")
}else if(x == 12){
  print("x is equal to 12!")
}else{
  print("x was not equal to 10 or 12")
}
```

```
## [1] "x is equal to 10!"
```

## **..Conditional statements training exercises..**
Example: Write a script that prints "Hello" if the variable x is equal to 1

```r
x <- 1
if(x == 1){
  print("Hello")
}
```

```
## [1] "Hello"
```
Ex 1: Write a script that will print "Even Number" if the variable x is an even number, otherwise print "Not Even":

```r
x <- 1
if (x %% 2 == 0){
  print("Even number")
}else{
  print("Not even")
}
```

```
## [1] "Not even"
```
Ex 2: Write a script that will print 'Is a Matrix' if the variable x is a matrix, otherwise print "Not a Matrix". Hint: You may want to check out help(is.matrix)

```r
x <- matrix(1:25, nrow = 5)
if (is.matrix(x) == TRUE){
  print("Is a Matrix")
}else{
  print("Not a Matrix")
}
```

```
## [1] "Is a Matrix"
```
Ex 3: Create a script that given a numeric vector x with a length 3, will print out the elements in order from high to low. You must use if,else if, and else statements for your logic. (This code will be relatively long)

```r
x <- c(3,7,1)
if (length(x) == 3){
  xorder <- order(x,decreasing = TRUE) #we take the indexes in descending order
  print(x[c(xorder)]) #we print the numbers in order
}
```

```
## [1] 7 3 1
```
Ex 4: Write a script that uses if,else if, and else statements to print the max element in a numeric vector with 
3 elements.

```r
x <- c(20, 10, 1)
if (length(x) == 3){
  print(max(x))
}
```

```
## [1] 20
```

## **While loops**

```r
x <- 0
while(x<10){
  print(paste0("x is: ",x))
  x <- x+1
  
  if (x==5){
    print("x is now equal to 5, break the loop!")
    break
  }
}
```

```
## [1] "x is: 0"
## [1] "x is: 1"
## [1] "x is: 2"
## [1] "x is: 3"
## [1] "x is: 4"
## [1] "x is now equal to 5, break the loop!"
```

##**For loops**

```r
v <- c(1,2,3) #with a vector

for (variable in v) { #it operates with each variable in the vector
  result <- variable + 10
  print(result)
}
```

```
## [1] 11
## [1] 12
## [1] 13
```

```r
my.list <- list(c(1,2,3),mtcars,12) #with a list

for (item in my.list) {
  print(item)
}
```

```
## [1] 1 2 3
##                      mpg cyl  disp  hp
## Mazda RX4           21.0   6 160.0 110
## Mazda RX4 Wag       21.0   6 160.0 110
## Datsun 710          22.8   4 108.0  93
## Hornet 4 Drive      21.4   6 258.0 110
## Hornet Sportabout   18.7   8 360.0 175
## Valiant             18.1   6 225.0 105
## Duster 360          14.3   8 360.0 245
## Merc 240D           24.4   4 146.7  62
## Merc 230            22.8   4 140.8  95
## Merc 280            19.2   6 167.6 123
## Merc 280C           17.8   6 167.6 123
## Merc 450SE          16.4   8 275.8 180
## Merc 450SL          17.3   8 275.8 180
## Merc 450SLC         15.2   8 275.8 180
## Cadillac Fleetwood  10.4   8 472.0 205
## Lincoln Continental 10.4   8 460.0 215
## Chrysler Imperial   14.7   8 440.0 230
## Fiat 128            32.4   4  78.7  66
## Honda Civic         30.4   4  75.7  52
## Toyota Corolla      33.9   4  71.1  65
## Toyota Corona       21.5   4 120.1  97
## Dodge Challenger    15.5   8 318.0 150
## AMC Javelin         15.2   8 304.0 150
## Camaro Z28          13.3   8 350.0 245
## Pontiac Firebird    19.2   8 400.0 175
## Fiat X1-9           27.3   4  79.0  66
## Porsche 914-2       26.0   4 120.3  91
## Lotus Europa        30.4   4  95.1 113
## Ford Pantera L      15.8   8 351.0 264
## Ferrari Dino        19.7   6 145.0 175
## Maserati Bora       15.0   8 301.0 335
## Volvo 142E          21.4   4 121.0 109
##                     drat    wt  qsec
## Mazda RX4           3.90 2.620 16.46
## Mazda RX4 Wag       3.90 2.875 17.02
## Datsun 710          3.85 2.320 18.61
## Hornet 4 Drive      3.08 3.215 19.44
## Hornet Sportabout   3.15 3.440 17.02
## Valiant             2.76 3.460 20.22
## Duster 360          3.21 3.570 15.84
## Merc 240D           3.69 3.190 20.00
## Merc 230            3.92 3.150 22.90
## Merc 280            3.92 3.440 18.30
## Merc 280C           3.92 3.440 18.90
## Merc 450SE          3.07 4.070 17.40
## Merc 450SL          3.07 3.730 17.60
## Merc 450SLC         3.07 3.780 18.00
## Cadillac Fleetwood  2.93 5.250 17.98
## Lincoln Continental 3.00 5.424 17.82
## Chrysler Imperial   3.23 5.345 17.42
## Fiat 128            4.08 2.200 19.47
## Honda Civic         4.93 1.615 18.52
## Toyota Corolla      4.22 1.835 19.90
## Toyota Corona       3.70 2.465 20.01
## Dodge Challenger    2.76 3.520 16.87
## AMC Javelin         3.15 3.435 17.30
## Camaro Z28          3.73 3.840 15.41
## Pontiac Firebird    3.08 3.845 17.05
## Fiat X1-9           4.08 1.935 18.90
## Porsche 914-2       4.43 2.140 16.70
## Lotus Europa        3.77 1.513 16.90
## Ford Pantera L      4.22 3.170 14.50
## Ferrari Dino        3.62 2.770 15.50
## Maserati Bora       3.54 3.570 14.60
## Volvo 142E          4.11 2.780 18.60
##                     vs am gear carb
## Mazda RX4            0  1    4    4
## Mazda RX4 Wag        0  1    4    4
## Datsun 710           1  1    4    1
## Hornet 4 Drive       1  0    3    1
## Hornet Sportabout    0  0    3    2
## Valiant              1  0    3    1
## Duster 360           0  0    3    4
## Merc 240D            1  0    4    2
## Merc 230             1  0    4    2
## Merc 280             1  0    4    4
## Merc 280C            1  0    4    4
## Merc 450SE           0  0    3    3
## Merc 450SL           0  0    3    3
## Merc 450SLC          0  0    3    3
## Cadillac Fleetwood   0  0    3    4
## Lincoln Continental  0  0    3    4
## Chrysler Imperial    0  0    3    4
## Fiat 128             1  1    4    1
## Honda Civic          1  1    4    2
## Toyota Corolla       1  1    4    1
## Toyota Corona        1  0    3    1
## Dodge Challenger     0  0    3    2
## AMC Javelin          0  0    3    2
## Camaro Z28           0  0    3    4
## Pontiac Firebird     0  0    3    2
## Fiat X1-9            1  1    4    1
## Porsche 914-2        0  1    5    2
## Lotus Europa         1  1    5    2
## Ford Pantera L       0  1    5    4
## Ferrari Dino         0  1    5    6
## Maserati Bora        0  1    5    8
## Volvo 142E           1  1    4    2
## [1] 12
```

```r
mat <- matrix(1:25,nrow=5)
for (num in mat){
  print(num) #its gonna print BY COLUMNS (first ALL column 1, then all column 2, etc.)
}
```

```
## [1] 1
## [1] 2
## [1] 3
## [1] 4
## [1] 5
## [1] 6
## [1] 7
## [1] 8
## [1] 9
## [1] 10
## [1] 11
## [1] 12
## [1] 13
## [1] 14
## [1] 15
## [1] 16
## [1] 17
## [1] 18
## [1] 19
## [1] 20
## [1] 21
## [1] 22
## [1] 23
## [1] 24
## [1] 25
```
Nested For loops

```r
mat <- matrix(1:25,nrow=5)

for (row in 1:nrow(mat)) {
  for (col in 1:ncol(mat)) {
    print(paste0("The element at row: ",row," and col:",col," is ",mat[row,col]))
  }
}
```

```
## [1] "The element at row: 1 and col:1 is 1"
## [1] "The element at row: 1 and col:2 is 6"
## [1] "The element at row: 1 and col:3 is 11"
## [1] "The element at row: 1 and col:4 is 16"
## [1] "The element at row: 1 and col:5 is 21"
## [1] "The element at row: 2 and col:1 is 2"
## [1] "The element at row: 2 and col:2 is 7"
## [1] "The element at row: 2 and col:3 is 12"
## [1] "The element at row: 2 and col:4 is 17"
## [1] "The element at row: 2 and col:5 is 22"
## [1] "The element at row: 3 and col:1 is 3"
## [1] "The element at row: 3 and col:2 is 8"
## [1] "The element at row: 3 and col:3 is 13"
## [1] "The element at row: 3 and col:4 is 18"
## [1] "The element at row: 3 and col:5 is 23"
## [1] "The element at row: 4 and col:1 is 4"
## [1] "The element at row: 4 and col:2 is 9"
## [1] "The element at row: 4 and col:3 is 14"
## [1] "The element at row: 4 and col:4 is 19"
## [1] "The element at row: 4 and col:5 is 24"
## [1] "The element at row: 5 and col:1 is 5"
## [1] "The element at row: 5 and col:2 is 10"
## [1] "The element at row: 5 and col:3 is 15"
## [1] "The element at row: 5 and col:4 is 20"
## [1] "The element at row: 5 and col:5 is 25"
```

##**Functions**

```r
name_of_func <- function(input1,input2,input3=45){
  result <- input1 + input2
  return(result)
}

name_of_func(1,2) #using it
```

```
## [1] 3
```


```r
hello <- function(){
  print("Hello")
}

hello() #we need parenthesis to call a function
```

```
## [1] "Hello"
```

```r
hello1 <- function(name = "Vic"){
  print(paste("Hello",name))
}

hello1("sunshine")
```

```
## [1] "Hello sunshine"
```


```r
add_num <- function(num1,num2){
  my.sum <- num1 + num2
  return(my.sum)
}

result <- add_num(4,5)
result
```

```
## [1] 9
```
Global variables

```r
v <- "I'm a global variable"
stuff <- "I'm a global stuff"

fun <- function(stuff){
  print(v)
  stuff <- "Reassign stuff inside of this function"
  print(stuff)
}

fun(stuff)
```

```
## [1] "I'm a global variable"
## [1] "Reassign stuff inside of this function"
```

#**R Functions Exercises**
EXAMPLE 1: Create a function that takes in a name as a string argument, and prints out "Hello name"

```r
hello_you <- function(name){
  print(paste("Hello",name))
}

hello_you("Vicky")
```

```
## [1] "Hello Vicky"
```

EXAMPLE 2: Create a function that takes in a name as a string argument and returns a string of the form - "Hello name"

```r
hello_you2 <- function(name){
  return(paste("Hello",name))
}
hello_you2("Vicky")
```

```
## [1] "Hello Vicky"
```

Ex 1: Create a function that will return the product of two integers.

```r
prod <- function(in1,in2){
  result <- in1 * in2
  return(result)
}

prod(3,4)
```

```
## [1] 12
```

Ex 2: Create a function that accepts two arguments, an integer and a vector of integers. It returns TRUE if the integer is present in the vector, otherwise it returns FALSE. Make sure you pay careful attention to your placement of the return(FALSE) line in your function!

```r
num_check <- function(int,int.vector){
    if(int %in% int.vector == TRUE){
    return(TRUE)
    }else{
    return(FALSE)
  }
}

i <- 1
iv <- c(1,2,3)
num_check(i,iv)
```

```
## [1] TRUE
```
Ex 3: Create a function that accepts two arguments, an integer and a vector of integers. It returns the count of the number of occurences of the integer in the input vector.

```r
i <- 1
iv <- c(1,1,2,2,3,1,4,5,5,2,2,1,3)

num_count <- function(int,int.v){
  counter <- 0
  for (num.v in int.v) {
    if (i == num.v){
      counter <- counter + 1
    }
  }
  return(counter)
}

num_count(i,iv)
```

```
## [1] 4
```

Ex 4: We want to ship bars of aluminum. We will create a function that accepts an integer representing the requested kilograms of aluminum for the package to be shipped. To fullfill these order, we have small bars (1 kilogram each) and big bars (5 kilograms each). Return the least number of bars needed.

```r
bar_count <- function(bars){
  small <- 1
  big <- 5
  
  needed.big <- as.integer(bars / big)
  needed.small <- bars %% big
  total <- needed.big + needed.small
  
 return(paste("Big bars needed:",needed.big,", small bars needed:",needed.small," in total =",total))
}

bar_count(17)
```

```
## [1] "Big bars needed: 3 , small bars needed: 2  in total = 5"
```

Ex 5: Create a function that accepts 3 integer values and returns their sum. However, if an integer value is evenly divisible by 3, then it does not count towards the sum. Return zero if all numbers are evenly divisible by 3. Hint: You may want to use the append() function.

```r
summer <- function(a,b.c)
  {
  
     out <- c(0)
  
    if (a%%3 != 0){
      out <- append(a,out)
    }
   
    if (b%%3 != 0){
      out <- append(b,out)
    }
   
    if (c%%3 != 0){
      out <- append(c,out)
    }
  
  return(sum(out))
}

#print(summer(1,2,5))
```
Ex 6: Create a function that will return TRUE if an input integer is prime. Otherwise, return FALSE. You may want to look into the any() function.

```r
prime_check <- function(num){
  if (num==2){
    return(TRUE)
  }
  for (x in 2:(num-1)){
    if (num%%x == 0){
      return(FALSE)
    }
  }
  return(TRUE)
}
print(prime_check(2))
```

```
## [1] TRUE
```

