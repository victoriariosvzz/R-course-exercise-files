---
title: 'Section 14: Data Manipulation with R'
author: "Victoria"
date: "7/1/2021"
output: html_document
---



#**Guide to using Dplyr**

```r
 #dataset we're gonna play with
library(dplyr)
library(nycflights13)
```
Lets start playing with the data

```r
head(flights)
```

```
## # A tibble: 6 x 19
##    year month   day dep_time
##   <int> <int> <int>    <int>
## 1  2013     1     1      517
## 2  2013     1     1      533
## 3  2013     1     1      542
## 4  2013     1     1      544
## 5  2013     1     1      554
## 6  2013     1     1      554
## # ... with 15 more variables:
## #   sched_dep_time <int>,
## #   dep_delay <dbl>, arr_time <int>,
## #   sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>,
## #   flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>,
## #   air_time <dbl>, distance <dbl>,
## #   hour <dbl>, minute <dbl>,
## #   time_hour <dttm>
```

```r
summary(flights)
```

```
##       year          month       
##  Min.   :2013   Min.   : 1.000  
##  1st Qu.:2013   1st Qu.: 4.000  
##  Median :2013   Median : 7.000  
##  Mean   :2013   Mean   : 6.549  
##  3rd Qu.:2013   3rd Qu.:10.000  
##  Max.   :2013   Max.   :12.000  
##                                 
##       day           dep_time   
##  Min.   : 1.00   Min.   :   1  
##  1st Qu.: 8.00   1st Qu.: 907  
##  Median :16.00   Median :1401  
##  Mean   :15.71   Mean   :1349  
##  3rd Qu.:23.00   3rd Qu.:1744  
##  Max.   :31.00   Max.   :2400  
##                  NA's   :8255  
##  sched_dep_time   dep_delay      
##  Min.   : 106   Min.   : -43.00  
##  1st Qu.: 906   1st Qu.:  -5.00  
##  Median :1359   Median :  -2.00  
##  Mean   :1344   Mean   :  12.64  
##  3rd Qu.:1729   3rd Qu.:  11.00  
##  Max.   :2359   Max.   :1301.00  
##                 NA's   :8255     
##     arr_time    sched_arr_time
##  Min.   :   1   Min.   :   1  
##  1st Qu.:1104   1st Qu.:1124  
##  Median :1535   Median :1556  
##  Mean   :1502   Mean   :1536  
##  3rd Qu.:1940   3rd Qu.:1945  
##  Max.   :2400   Max.   :2359  
##  NA's   :8713                 
##    arr_delay          carrier         
##  Min.   : -86.000   Length:336776     
##  1st Qu.: -17.000   Class :character  
##  Median :  -5.000   Mode  :character  
##  Mean   :   6.895                     
##  3rd Qu.:  14.000                     
##  Max.   :1272.000                     
##  NA's   :9430                         
##      flight       tailnum         
##  Min.   :   1   Length:336776     
##  1st Qu.: 553   Class :character  
##  Median :1496   Mode  :character  
##  Mean   :1972                     
##  3rd Qu.:3465                     
##  Max.   :8500                     
##                                   
##     origin              dest          
##  Length:336776      Length:336776     
##  Class :character   Class :character  
##  Mode  :character   Mode  :character  
##                                       
##                                       
##                                       
##                                       
##     air_time        distance   
##  Min.   : 20.0   Min.   :  17  
##  1st Qu.: 82.0   1st Qu.: 502  
##  Median :129.0   Median : 872  
##  Mean   :150.7   Mean   :1040  
##  3rd Qu.:192.0   3rd Qu.:1389  
##  Max.   :695.0   Max.   :4983  
##  NA's   :9430                  
##       hour           minute     
##  Min.   : 1.00   Min.   : 0.00  
##  1st Qu.: 9.00   1st Qu.: 8.00  
##  Median :13.00   Median :29.00  
##  Mean   :13.18   Mean   :26.23  
##  3rd Qu.:17.00   3rd Qu.:44.00  
##  Max.   :23.00   Max.   :59.00  
##                                 
##    time_hour                  
##  Min.   :2013-01-01 05:00:00  
##  1st Qu.:2013-04-04 13:00:00  
##  Median :2013-07-03 10:00:00  
##  Mean   :2013-07-03 05:22:54  
##  3rd Qu.:2013-10-01 07:00:00  
##  Max.   :2013-12-31 23:00:00  
## 
```
##How to use dplyr to easily manipulate our data
FUnctions inside of dplyr to use
###Filter():to select a set of rows in a df

```r
head(filter(flights,month==11,day==3,carrier=="AA")) #with "filter" function
```

```
## # A tibble: 6 x 19
##    year month   day dep_time
##   <int> <int> <int>    <int>
## 1  2013    11     3      538
## 2  2013    11     3      556
## 3  2013    11     3      604
## 4  2013    11     3      624
## 5  2013    11     3      625
## 6  2013    11     3      653
## # ... with 15 more variables:
## #   sched_dep_time <int>,
## #   dep_delay <dbl>, arr_time <int>,
## #   sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>,
## #   flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>,
## #   air_time <dbl>, distance <dbl>,
## #   hour <dbl>, minute <dbl>,
## #   time_hour <dttm>
```
###Slice(): to select rows by position

```r
slice(flights,1:10) #we select the row 1 to 10
```

```
## # A tibble: 10 x 19
##     year month   day dep_time
##    <int> <int> <int>    <int>
##  1  2013     1     1      517
##  2  2013     1     1      533
##  3  2013     1     1      542
##  4  2013     1     1      544
##  5  2013     1     1      554
##  6  2013     1     1      554
##  7  2013     1     1      555
##  8  2013     1     1      557
##  9  2013     1     1      557
## 10  2013     1     1      558
## # ... with 15 more variables:
## #   sched_dep_time <int>,
## #   dep_delay <dbl>, arr_time <int>,
## #   sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>,
## #   flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>,
## #   air_time <dbl>, distance <dbl>,
## #   hour <dbl>, minute <dbl>,
## #   time_hour <dttm>
```
###arrange(): re-orders the rows of a df in ascending order

```r
head(arrange(flights,year,month,day,arr_time)) #it orders the rows in the written columns in ascending order
```

```
## # A tibble: 6 x 19
##    year month   day dep_time
##   <int> <int> <int>    <int>
## 1  2013     1     1     1929
## 2  2013     1     1     2121
## 3  2013     1     1     2058
## 4  2013     1     1     2120
## 5  2013     1     1     2134
## 6  2013     1     1     2312
## # ... with 15 more variables:
## #   sched_dep_time <int>,
## #   dep_delay <dbl>, arr_time <int>,
## #   sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>,
## #   flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>,
## #   air_time <dbl>, distance <dbl>,
## #   hour <dbl>, minute <dbl>,
## #   time_hour <dttm>
```

```r
head(arrange(flights,year,month,day,desc(arr_time)))
```

```
## # A tibble: 6 x 19
##    year month   day dep_time
##   <int> <int> <int>    <int>
## 1  2013     1     1     2209
## 2  2013     1     1     1952
## 3  2013     1     1     2025
## 4  2013     1     1     2119
## 5  2013     1     1     2052
## 6  2013     1     1     2030
## # ... with 15 more variables:
## #   sched_dep_time <int>,
## #   dep_delay <dbl>, arr_time <int>,
## #   sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>,
## #   flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>,
## #   air_time <dbl>, distance <dbl>,
## #   hour <dbl>, minute <dbl>,
## #   time_hour <dttm>
```
###select(): allows to only show specific columns in df

```r
head(select(flights,carrier))
```

```
## # A tibble: 6 x 1
##   carrier
##   <chr>  
## 1 UA     
## 2 UA     
## 3 AA     
## 4 B6     
## 5 DL     
## 6 UA
```

```r
head(select(flights,carrier,dep_time))
```

```
## # A tibble: 6 x 2
##   carrier dep_time
##   <chr>      <int>
## 1 UA           517
## 2 UA           533
## 3 AA           542
## 4 B6           544
## 5 DL           554
## 6 UA           554
```
##rename(): it lets us rename the columns of a df

```r
head(rename(flights,airline_carrier = carrier)) #new name = old name
```

```
## # A tibble: 6 x 19
##    year month   day dep_time
##   <int> <int> <int>    <int>
## 1  2013     1     1      517
## 2  2013     1     1      533
## 3  2013     1     1      542
## 4  2013     1     1      544
## 5  2013     1     1      554
## 6  2013     1     1      554
## # ... with 15 more variables:
## #   sched_dep_time <int>,
## #   dep_delay <dbl>, arr_time <int>,
## #   sched_arr_time <int>,
## #   arr_delay <dbl>,
## #   airline_carrier <chr>,
## #   flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>,
## #   air_time <dbl>, distance <dbl>,
## #   hour <dbl>, minute <dbl>,
## #   time_hour <dttm>
```
##distinct(): allows us to select the unique values in a column or table

```r
distinct(select(flights,carrier)) #it only shows the different unique values (doesn't show the repetition)
```

```
## # A tibble: 16 x 1
##    carrier
##    <chr>  
##  1 UA     
##  2 AA     
##  3 B6     
##  4 DL     
##  5 EV     
##  6 MQ     
##  7 US     
##  8 WN     
##  9 VX     
## 10 FL     
## 11 AS     
## 12 9E     
## 13 F9     
## 14 HA     
## 15 YV     
## 16 OO
```
##mutate(): to create new columns

```r
head(mutate(flights,new_col = arr_delay - dep_delay))
```

```
## # A tibble: 6 x 20
##    year month   day dep_time
##   <int> <int> <int>    <int>
## 1  2013     1     1      517
## 2  2013     1     1      533
## 3  2013     1     1      542
## 4  2013     1     1      544
## 5  2013     1     1      554
## 6  2013     1     1      554
## # ... with 16 more variables:
## #   sched_dep_time <int>,
## #   dep_delay <dbl>, arr_time <int>,
## #   sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>,
## #   flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>,
## #   air_time <dbl>, distance <dbl>,
## #   hour <dbl>, minute <dbl>,
## #   time_hour <dttm>, new_col <dbl>
```
##transmute(): it creates a new column and ONLY returns this new column

```r
head(transmute(flights,new_col = arr_delay - dep_delay))
```

```
## # A tibble: 6 x 1
##   new_col
##     <dbl>
## 1       9
## 2      16
## 3      31
## 4     -17
## 5     -19
## 6      16
```
##summarize(): allows us to collapse dataframes in single rows

```r
summarise(flights,avg_air_time = mean(air_time,na.rm = TRUE)) #it returns one result as a row
```

```
## # A tibble: 1 x 1
##   avg_air_time
##          <dbl>
## 1         151.
```

```r
summarise(flights,total_air_time = sum(air_time,na.rm = TRUE))
```

```
## # A tibble: 1 x 1
##   total_air_time
##            <dbl>
## 1       49326610
```

##sample()

```r
sample_n(flights,10) #returns 10 random rows of the df
```

```
## # A tibble: 10 x 19
##     year month   day dep_time
##    <int> <int> <int>    <int>
##  1  2013     8    18     1120
##  2  2013     1    29     1455
##  3  2013     3    25     1600
##  4  2013     2    18     2038
##  5  2013     5    13     1645
##  6  2013     9    19       NA
##  7  2013     5    23     1156
##  8  2013     7    30     1400
##  9  2013     8    19     1618
## 10  2013     8     8      827
## # ... with 15 more variables:
## #   sched_dep_time <int>,
## #   dep_delay <dbl>, arr_time <int>,
## #   sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>,
## #   flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>,
## #   air_time <dbl>, distance <dbl>,
## #   hour <dbl>, minute <dbl>,
## #   time_hour <dttm>
```

```r
sample_frac(flights,0.1) #returns a fraction of the rows (in this case it returns the 10% of the rows)
```

```
## # A tibble: 33,678 x 19
##     year month   day dep_time
##    <int> <int> <int>    <int>
##  1  2013    10    18     1047
##  2  2013    12     8     1646
##  3  2013    10    21     1854
##  4  2013     5     8     1400
##  5  2013     3     4     1638
##  6  2013     7     7     1049
##  7  2013     6    24     2102
##  8  2013    10     3     2010
##  9  2013    12    12     1324
## 10  2013     5    28      656
## # ... with 33,668 more rows, and 15
## #   more variables:
## #   sched_dep_time <int>,
## #   dep_delay <dbl>, arr_time <int>,
## #   sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>,
## #   flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>,
## #   air_time <dbl>, distance <dbl>,
## #   hour <dbl>, minute <dbl>,
## #   time_hour <dttm>
```

# **Pipe Operator %>%**
It allows us to make sequential operations like: data %>% op1 %>% op2...

```r
library(dplyr)

df <- mtcars

#Nesting
result <- arrange(sample_n(filter(df,mpg>20),size=5),desc(mpg))
print(result)
```

```
##                 mpg cyl  disp  hp drat
## Fiat X1-9      27.3   4  79.0  66 4.08
## Merc 230       22.8   4 140.8  95 3.92
## Hornet 4 Drive 21.4   6 258.0 110 3.08
## Mazda RX4      21.0   6 160.0 110 3.90
## Mazda RX4 Wag  21.0   6 160.0 110 3.90
##                   wt  qsec vs am gear
## Fiat X1-9      1.935 18.90  1  1    4
## Merc 230       3.150 22.90  1  0    4
## Hornet 4 Drive 3.215 19.44  1  0    3
## Mazda RX4      2.620 16.46  0  1    4
## Mazda RX4 Wag  2.875 17.02  0  1    4
##                carb
## Fiat X1-9         1
## Merc 230          2
## Hornet 4 Drive    1
## Mazda RX4         4
## Mazda RX4 Wag     4
```

```r
#the same but using Pipe operator
result.pipe <- df %>% filter(mpg>20) %>% sample_n(size=5) %>% arrange(desc(mpg))

print(result.pipe)
```

```
##                 mpg cyl  disp  hp drat
## Lotus Europa   30.4   4  95.1 113 3.77
## Fiat X1-9      27.3   4  79.0  66 4.08
## Merc 230       22.8   4 140.8  95 3.92
## Hornet 4 Drive 21.4   6 258.0 110 3.08
## Volvo 142E     21.4   4 121.0 109 4.11
##                   wt  qsec vs am gear
## Lotus Europa   1.513 16.90  1  1    5
## Fiat X1-9      1.935 18.90  1  1    4
## Merc 230       3.150 22.90  1  0    4
## Hornet 4 Drive 3.215 19.44  1  0    3
## Volvo 142E     2.780 18.60  1  1    4
##                carb
## Lotus Europa      2
## Fiat X1-9         1
## Merc 230          2
## Hornet 4 Drive    1
## Volvo 142E        2
```

#**..Dplyr exercises..**

```r
library(dplyr)
head(mtcars)
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
Return rows of cars that have an mpg value greater than 20 and 6 cylinders.

```r
res <- filter(mtcars,mpg>20,cyl==6)
head(res)
```

```
##                 mpg cyl disp  hp drat
## Mazda RX4      21.0   6  160 110 3.90
## Mazda RX4 Wag  21.0   6  160 110 3.90
## Hornet 4 Drive 21.4   6  258 110 3.08
##                   wt  qsec vs am gear
## Mazda RX4      2.620 16.46  0  1    4
## Mazda RX4 Wag  2.875 17.02  0  1    4
## Hornet 4 Drive 3.215 19.44  1  0    3
##                carb
## Mazda RX4         4
## Mazda RX4 Wag     4
## Hornet 4 Drive    1
```

Reorder the Data Frame by cyl first, then by descending wt.

```r
res <- arrange(mtcars,cyl,desc(wt))
head(res)
```

```
##                mpg cyl  disp  hp drat
## Merc 240D     24.4   4 146.7  62 3.69
## Merc 230      22.8   4 140.8  95 3.92
## Volvo 142E    21.4   4 121.0 109 4.11
## Toyota Corona 21.5   4 120.1  97 3.70
## Datsun 710    22.8   4 108.0  93 3.85
## Fiat 128      32.4   4  78.7  66 4.08
##                  wt  qsec vs am gear
## Merc 240D     3.190 20.00  1  0    4
## Merc 230      3.150 22.90  1  0    4
## Volvo 142E    2.780 18.60  1  1    4
## Toyota Corona 2.465 20.01  1  0    3
## Datsun 710    2.320 18.61  1  1    4
## Fiat 128      2.200 19.47  1  1    4
##               carb
## Merc 240D        2
## Merc 230         2
## Volvo 142E       2
## Toyota Corona    1
## Datsun 710       1
## Fiat 128         1
```

Select the columns mpg and hp

```r
res <- select(mtcars,mpg,hp)
head(res)
```

```
##                    mpg  hp
## Mazda RX4         21.0 110
## Mazda RX4 Wag     21.0 110
## Datsun 710        22.8  93
## Hornet 4 Drive    21.4 110
## Hornet Sportabout 18.7 175
## Valiant           18.1 105
```

Select the distinct values of the gear column.

```r
distinct(select(mtcars,gear))
```

```
##                gear
## Mazda RX4         4
## Hornet 4 Drive    3
## Porsche 914-2     5
```

Create a new column called "Performance" which is calculated by hp divided by wt.

```r
res <- mutate(mtcars, Performance = hp/wt)
head(res)
```

```
##    mpg cyl disp  hp drat    wt  qsec
## 1 21.0   6  160 110 3.90 2.620 16.46
## 2 21.0   6  160 110 3.90 2.875 17.02
## 3 22.8   4  108  93 3.85 2.320 18.61
## 4 21.4   6  258 110 3.08 3.215 19.44
## 5 18.7   8  360 175 3.15 3.440 17.02
## 6 18.1   6  225 105 2.76 3.460 20.22
##   vs am gear carb Performance
## 1  0  1    4    4    41.98473
## 2  0  1    4    4    38.26087
## 3  1  1    4    1    40.08621
## 4  1  0    3    1    34.21462
## 5  0  0    3    2    50.87209
## 6  1  0    3    1    30.34682
```

Find the mean mpg value using dplyr.

```r
summarize(mtcars,avg_mpg = mean(mpg,na.rm = TRUE))
```

```
##    avg_mpg
## 1 20.09062
```

Use pipe operators to get the mean hp value for cars with 6 cylinders.

```r
res <- mtcars %>% filter(cyl==6) %>% summarise(std_hp = mean(hp,na.rm = TRUE))
print(res)
```

```
##     std_hp
## 1 122.2857
```

#**Tidyr**
It's a function that helps us to clean data, this means, that each column is a property or variable, and each row is a vehicle with values
##Data table = Data frame, but the data table has some extra features, and it's faster to process than a df

```r
library(tidyr)
library(data.table)
```

```
## data.table 1.13.6 using 1 threads (see ?getDTthreads).  Latest news: r-datatable.com
```

```
## 
## Attaching package: 'data.table'
```

```
## The following objects are masked from 'package:dplyr':
## 
##     between, first, last
```
##gather(): it gathers different columns into one single column

```r
#First, we create fake data to process it
comp <- c(1,1,1,2,2,2,3,3,3)
yr <- c(1998,1999,2000,1998,1999,2000,1998,1999,2000)
q1 <- runif(9, min=0, max=100) # random 9 numbers from 0 to 100
q2 <- runif(9, min=0, max=100)
q3 <- runif(9, min=0, max=100)
q4 <- runif(9, min=0, max=100)

df <- data.frame(comp=comp,year=yr,Qtr1 = q1,Qtr2 = q2,Qtr3 = q3,Qtr4 = q4)

gather(df,Quarter,Revenue,Qtr1:Qtr4) #we gather all the information of the Qtr1,2,3... into 2 columns: key = Quarter and value = Revenue
```

```
##    comp year Quarter   Revenue
## 1     1 1998    Qtr1 40.301260
## 2     1 1999    Qtr1 12.792484
## 3     1 2000    Qtr1 87.420440
## 4     2 1998    Qtr1 99.235266
## 5     2 1999    Qtr1 38.508282
## 6     2 2000    Qtr1 97.948422
## 7     3 1998    Qtr1 52.989006
## 8     3 1999    Qtr1 68.908272
## 9     3 2000    Qtr1 58.867038
## 10    1 1998    Qtr2 55.403749
## 11    1 1999    Qtr2 17.402785
## 12    1 2000    Qtr2  5.619767
## 13    2 1998    Qtr2 76.696808
## 14    2 1999    Qtr2 44.689254
## 15    2 2000    Qtr2 87.827053
## 16    3 1998    Qtr2 59.498146
## 17    3 1999    Qtr2  8.770810
## 18    3 2000    Qtr2 89.280977
## 19    1 1998    Qtr3 57.673619
## 20    1 1999    Qtr3 73.662920
## 21    1 2000    Qtr3 70.465606
## 22    2 1998    Qtr3 65.132257
## 23    2 1999    Qtr3 48.449021
## 24    2 2000    Qtr3 45.393177
## 25    3 1998    Qtr3 73.113269
## 26    3 1999    Qtr3  3.977183
## 27    3 2000    Qtr3 35.057756
## 28    1 1998    Qtr4  2.185884
## 29    1 1999    Qtr4 19.963483
## 30    1 2000    Qtr4 45.528869
## 31    2 1998    Qtr4 54.259061
## 32    2 1999    Qtr4 90.139223
## 33    2 2000    Qtr4 96.219187
## 34    3 1998    Qtr4 70.570271
## 35    3 1999    Qtr4 75.929407
## 36    3 2000    Qtr4 16.660352
```

```r
df %>% gather(Quarter,Revenue,Qtr1:Qtr4) #it does the same
```

```
##    comp year Quarter   Revenue
## 1     1 1998    Qtr1 40.301260
## 2     1 1999    Qtr1 12.792484
## 3     1 2000    Qtr1 87.420440
## 4     2 1998    Qtr1 99.235266
## 5     2 1999    Qtr1 38.508282
## 6     2 2000    Qtr1 97.948422
## 7     3 1998    Qtr1 52.989006
## 8     3 1999    Qtr1 68.908272
## 9     3 2000    Qtr1 58.867038
## 10    1 1998    Qtr2 55.403749
## 11    1 1999    Qtr2 17.402785
## 12    1 2000    Qtr2  5.619767
## 13    2 1998    Qtr2 76.696808
## 14    2 1999    Qtr2 44.689254
## 15    2 2000    Qtr2 87.827053
## 16    3 1998    Qtr2 59.498146
## 17    3 1999    Qtr2  8.770810
## 18    3 2000    Qtr2 89.280977
## 19    1 1998    Qtr3 57.673619
## 20    1 1999    Qtr3 73.662920
## 21    1 2000    Qtr3 70.465606
## 22    2 1998    Qtr3 65.132257
## 23    2 1999    Qtr3 48.449021
## 24    2 2000    Qtr3 45.393177
## 25    3 1998    Qtr3 73.113269
## 26    3 1999    Qtr3  3.977183
## 27    3 2000    Qtr3 35.057756
## 28    1 1998    Qtr4  2.185884
## 29    1 1999    Qtr4 19.963483
## 30    1 2000    Qtr4 45.528869
## 31    2 1998    Qtr4 54.259061
## 32    2 1999    Qtr4 90.139223
## 33    2 2000    Qtr4 96.219187
## 34    3 1998    Qtr4 70.570271
## 35    3 1999    Qtr4 75.929407
## 36    3 2000    Qtr4 16.660352
```
## spread(): it's a opposite of gather

```r
stocks <- data.frame(
  time = as.Date('2009-01-01') + 0:9,
  X = rnorm(10, 0, 1),
  Y = rnorm(10, 0, 2),
  Z = rnorm(10, 0, 4)
)
stocks
```

```
##          time          X          Y
## 1  2009-01-01 -0.1560102 -2.6276726
## 2  2009-01-02 -1.5139283 -0.8858126
## 3  2009-01-03  0.1536469 -1.5278682
## 4  2009-01-04  1.6372447  2.8805258
## 5  2009-01-05 -0.1892681  2.6923725
## 6  2009-01-06  0.6131810  3.5029766
## 7  2009-01-07  0.2580381 -6.0900552
## 8  2009-01-08 -0.5631126 -2.2925150
## 9  2009-01-09  1.3227416  0.8457395
## 10 2009-01-10  0.4361890  0.6101168
##            Z
## 1  -2.095574
## 2   2.126793
## 3   1.672490
## 4  -6.858634
## 5   0.434352
## 6   4.007035
## 7  -4.255953
## 8   6.581375
## 9   4.687913
## 10  3.552710
```

```r
#lets use GATHER()
stocks.gathered <- stocks %>% gather(stock,price,X,Y,Z) #key = stock and value = price (X,Y,Z)
head(stocks.gathered)
```

```
##         time stock      price
## 1 2009-01-01     X -0.1560102
## 2 2009-01-02     X -1.5139283
## 3 2009-01-03     X  0.1536469
## 4 2009-01-04     X  1.6372447
## 5 2009-01-05     X -0.1892681
## 6 2009-01-06     X  0.6131810
```

```r
#lets use SPREAD()
stocks.gathered %>% spread(stock,price) #we spread putting (key,values)
```

```
##          time          X          Y
## 1  2009-01-01 -0.1560102 -2.6276726
## 2  2009-01-02 -1.5139283 -0.8858126
## 3  2009-01-03  0.1536469 -1.5278682
## 4  2009-01-04  1.6372447  2.8805258
## 5  2009-01-05 -0.1892681  2.6923725
## 6  2009-01-06  0.6131810  3.5029766
## 7  2009-01-07  0.2580381 -6.0900552
## 8  2009-01-08 -0.5631126 -2.2925150
## 9  2009-01-09  1.3227416  0.8457395
## 10 2009-01-10  0.4361890  0.6101168
##            Z
## 1  -2.095574
## 2   2.126793
## 3   1.672490
## 4  -6.858634
## 5   0.434352
## 6   4.007035
## 7  -4.255953
## 8   6.581375
## 9   4.687913
## 10  3.552710
```

```r
stocks.gathered %>% spread(time,price) #we can also do this, but it is not really tidy
```

```
##   stock 2009-01-01 2009-01-02
## 1     X -0.1560102 -1.5139283
## 2     Y -2.6276726 -0.8858126
## 3     Z -2.0955742  2.1267932
##   2009-01-03 2009-01-04 2009-01-05
## 1  0.1536469   1.637245 -0.1892681
## 2 -1.5278682   2.880526  2.6923725
## 3  1.6724902  -6.858634  0.4343520
##   2009-01-06 2009-01-07 2009-01-08
## 1   0.613181  0.2580381 -0.5631126
## 2   3.502977 -6.0900552 -2.2925150
## 3   4.007035 -4.2559532  6.5813754
##   2009-01-09 2009-01-10
## 1  1.3227416  0.4361890
## 2  0.8457395  0.6101168
## 3  4.6879133  3.5527101
```
## separate(): it transforms a single character column into multiple columns

```r
df <- data.frame(new.col=c(NA,"a.x","b.y","c.z"))
df
```

```
##   new.col
## 1    <NA>
## 2     a.x
## 3     b.y
## 4     c.z
```

```r
separate(df,new.col,c("ABC","XYZ")) #it separates non alphanumerical elements to create columns (like - , . / etc...)
```

```
##    ABC  XYZ
## 1 <NA> <NA>
## 2    a    x
## 3    b    y
## 4    c    z
```
## unite(): the opposite of separate

```r
df <- data.frame(new.col=c(NA,"a.x","b.y","c.z"))
df.sep <- separate(df,new.col,c("ABC","XYZ")) 

unite(df.sep, new.joined.col, ABC, XYZ, sep = "---") #it unites the columns ABC and XYZ as a new column new.joined.col
```

```
##   new.joined.col
## 1        NA---NA
## 2          a---x
## 3          b---y
## 4          c---z
```

