---
title: "Section 9 - R Data Frames"
author: "Victoria"
date: "3/1/2021"
output: html_document
---



# ***Data frames basics***
We can combine different data types in a dataframe, unlike matrices
***Data frames are similar to an Excel spreadsheet***

```r
state.x77 #Data frame with info of the states of the usa
```

```
##                Population Income Illiteracy Life Exp Murder HS Grad Frost   Area
## Alabama              3615   3624        2.1    69.05   15.1    41.3    20  50708
## Alaska                365   6315        1.5    69.31   11.3    66.7   152 566432
## Arizona              2212   4530        1.8    70.55    7.8    58.1    15 113417
## Arkansas             2110   3378        1.9    70.66   10.1    39.9    65  51945
## California          21198   5114        1.1    71.71   10.3    62.6    20 156361
## Colorado             2541   4884        0.7    72.06    6.8    63.9   166 103766
## Connecticut          3100   5348        1.1    72.48    3.1    56.0   139   4862
## Delaware              579   4809        0.9    70.06    6.2    54.6   103   1982
## Florida              8277   4815        1.3    70.66   10.7    52.6    11  54090
## Georgia              4931   4091        2.0    68.54   13.9    40.6    60  58073
## Hawaii                868   4963        1.9    73.60    6.2    61.9     0   6425
## Idaho                 813   4119        0.6    71.87    5.3    59.5   126  82677
## Illinois            11197   5107        0.9    70.14   10.3    52.6   127  55748
## Indiana              5313   4458        0.7    70.88    7.1    52.9   122  36097
## Iowa                 2861   4628        0.5    72.56    2.3    59.0   140  55941
## Kansas               2280   4669        0.6    72.58    4.5    59.9   114  81787
## Kentucky             3387   3712        1.6    70.10   10.6    38.5    95  39650
## Louisiana            3806   3545        2.8    68.76   13.2    42.2    12  44930
## Maine                1058   3694        0.7    70.39    2.7    54.7   161  30920
## Maryland             4122   5299        0.9    70.22    8.5    52.3   101   9891
## Massachusetts        5814   4755        1.1    71.83    3.3    58.5   103   7826
## Michigan             9111   4751        0.9    70.63   11.1    52.8   125  56817
## Minnesota            3921   4675        0.6    72.96    2.3    57.6   160  79289
## Mississippi          2341   3098        2.4    68.09   12.5    41.0    50  47296
## Missouri             4767   4254        0.8    70.69    9.3    48.8   108  68995
## Montana               746   4347        0.6    70.56    5.0    59.2   155 145587
## Nebraska             1544   4508        0.6    72.60    2.9    59.3   139  76483
## Nevada                590   5149        0.5    69.03   11.5    65.2   188 109889
## New Hampshire         812   4281        0.7    71.23    3.3    57.6   174   9027
## New Jersey           7333   5237        1.1    70.93    5.2    52.5   115   7521
## New Mexico           1144   3601        2.2    70.32    9.7    55.2   120 121412
## New York            18076   4903        1.4    70.55   10.9    52.7    82  47831
## North Carolina       5441   3875        1.8    69.21   11.1    38.5    80  48798
## North Dakota          637   5087        0.8    72.78    1.4    50.3   186  69273
## Ohio                10735   4561        0.8    70.82    7.4    53.2   124  40975
## Oklahoma             2715   3983        1.1    71.42    6.4    51.6    82  68782
## Oregon               2284   4660        0.6    72.13    4.2    60.0    44  96184
## Pennsylvania        11860   4449        1.0    70.43    6.1    50.2   126  44966
## Rhode Island          931   4558        1.3    71.90    2.4    46.4   127   1049
## South Carolina       2816   3635        2.3    67.96   11.6    37.8    65  30225
## South Dakota          681   4167        0.5    72.08    1.7    53.3   172  75955
## Tennessee            4173   3821        1.7    70.11   11.0    41.8    70  41328
## Texas               12237   4188        2.2    70.90   12.2    47.4    35 262134
## Utah                 1203   4022        0.6    72.90    4.5    67.3   137  82096
## Vermont               472   3907        0.6    71.64    5.5    57.1   168   9267
## Virginia             4981   4701        1.4    70.08    9.5    47.8    85  39780
## Washington           3559   4864        0.6    71.72    4.3    63.5    32  66570
## West Virginia        1799   3617        1.4    69.48    6.7    41.6   100  24070
## Wisconsin            4589   4468        0.7    72.48    3.0    54.5   149  54464
## Wyoming               376   4566        0.6    70.29    6.9    62.9   173  97203
```

```r
state.area
```

```
##  [1]  51609 589757 113909  53104 158693 104247   5009   2057  58560  58876   6450
## [12]  83557  56400  36291  56290  82264  40395  48523  33215  10577   8257  58216
## [23]  84068  47716  69686 147138  77227 110540   9304   7836 121666  49576  52586
## [34]  70665  41222  69919  96981  45333   1214  31055  77047  42244 267339  84916
## [45]   9609  40815  68192  24181  56154  97914
```

```r
USPersonalExpenditure #info of the US personal expenditure
```

```
##                       1940   1945  1950 1955  1960
## Food and Tobacco    22.200 44.500 59.60 73.2 86.80
## Household Operation 10.500 15.500 29.00 36.5 46.20
## Medical and Health   3.530  5.760  9.71 14.0 21.10
## Personal Care        1.040  1.980  2.45  3.4  5.40
## Private Education    0.341  0.974  1.80  2.6  3.64
```

```r
women #Us women's height and weight
```

```
##    height weight
## 1      58    115
## 2      59    117
## 3      60    120
## 4      61    123
## 5      62    126
## 6      63    129
## 7      64    132
## 8      65    135
## 9      66    139
## 10     67    142
## 11     68    146
## 12     69    150
## 13     70    154
## 14     71    159
## 15     72    164
```
### To get the list of all the data frames (or datasets) available in R, you can do the following

```r
data()
```
### To show only some parts of the data frame

```r
head(state.x77) #it returns only the FIRST 6 rows of data
```

```
##            Population Income Illiteracy Life Exp Murder HS Grad Frost   Area
## Alabama          3615   3624        2.1    69.05   15.1    41.3    20  50708
## Alaska            365   6315        1.5    69.31   11.3    66.7   152 566432
## Arizona          2212   4530        1.8    70.55    7.8    58.1    15 113417
## Arkansas         2110   3378        1.9    70.66   10.1    39.9    65  51945
## California      21198   5114        1.1    71.71   10.3    62.6    20 156361
## Colorado         2541   4884        0.7    72.06    6.8    63.9   166 103766
```

```r
tail(state.x77) #it returns only the LAST 6 rows of data
```

```
##               Population Income Illiteracy Life Exp Murder HS Grad Frost  Area
## Vermont              472   3907        0.6    71.64    5.5    57.1   168  9267
## Virginia            4981   4701        1.4    70.08    9.5    47.8    85 39780
## Washington          3559   4864        0.6    71.72    4.3    63.5    32 66570
## West Virginia       1799   3617        1.4    69.48    6.7    41.6   100 24070
## Wisconsin           4589   4468        0.7    72.48    3.0    54.5   149 54464
## Wyoming              376   4566        0.6    70.29    6.9    62.9   173 97203
```

```r
str(state.x77) #it shows the attributes of the structure of the data frame
```

```
##  num [1:50, 1:8] 3615 365 2212 2110 21198 ...
##  - attr(*, "dimnames")=List of 2
##   ..$ : chr [1:50] "Alabama" "Alaska" "Arizona" "Arkansas" ...
##   ..$ : chr [1:8] "Population" "Income" "Illiteracy" "Life Exp" ...
```

```r
summary(state.x77) #it gives a summary of each of the categories of info in the data frame
```

```
##    Population        Income       Illiteracy       Life Exp         Murder      
##  Min.   :  365   Min.   :3098   Min.   :0.500   Min.   :67.96   Min.   : 1.400  
##  1st Qu.: 1080   1st Qu.:3993   1st Qu.:0.625   1st Qu.:70.12   1st Qu.: 4.350  
##  Median : 2838   Median :4519   Median :0.950   Median :70.67   Median : 6.850  
##  Mean   : 4246   Mean   :4436   Mean   :1.170   Mean   :70.88   Mean   : 7.378  
##  3rd Qu.: 4968   3rd Qu.:4814   3rd Qu.:1.575   3rd Qu.:71.89   3rd Qu.:10.675  
##  Max.   :21198   Max.   :6315   Max.   :2.800   Max.   :73.60   Max.   :15.100  
##     HS Grad          Frost             Area       
##  Min.   :37.80   Min.   :  0.00   Min.   :  1049  
##  1st Qu.:48.05   1st Qu.: 66.25   1st Qu.: 36985  
##  Median :53.25   Median :114.50   Median : 54277  
##  Mean   :53.11   Mean   :104.46   Mean   : 70736  
##  3rd Qu.:59.15   3rd Qu.:139.75   3rd Qu.: 81163  
##  Max.   :67.30   Max.   :188.00   Max.   :566432
```
## ***To create our own data frame***

```r
days <- c("Mon","Tue","Wed","Thur","Fri")
temp <- c(22.2,21,23,24.3,25)
rain <- c(T,T,F,F,T)

data.frame(days,temp,rain) #to create our data frame out of vectors!
```

```
##   days temp  rain
## 1  Mon 22.2  TRUE
## 2  Tue 21.0  TRUE
## 3  Wed 23.0 FALSE
## 4 Thur 24.3 FALSE
## 5  Fri 25.0  TRUE
```

```r
df <- data.frame(days,temp,rain)
df
```

```
##   days temp  rain
## 1  Mon 22.2  TRUE
## 2  Tue 21.0  TRUE
## 3  Wed 23.0 FALSE
## 4 Thur 24.3 FALSE
## 5  Fri 25.0  TRUE
```

```r
str(df)
```

```
## 'data.frame':	5 obs. of  3 variables:
##  $ days: chr  "Mon" "Tue" "Wed" "Thur" ...
##  $ temp: num  22.2 21 23 24.3 25
##  $ rain: logi  TRUE TRUE FALSE FALSE TRUE
```

```r
summary(df)
```

```
##      days                temp         rain        
##  Length:5           Min.   :21.0   Mode :logical  
##  Class :character   1st Qu.:22.2   FALSE:2        
##  Mode  :character   Median :23.0   TRUE :3        
##                     Mean   :23.1                  
##                     3rd Qu.:24.3                  
##                     Max.   :25.0
```

# ***Data frames selection and indexing***
First we load the data frame

```r
days <- c("Mon","Tue","Wed","Thur","Fri")
temp <- c(22.2,21,23,24.3,25)
rain <- c(T,T,F,F,T)

data.frame(days,temp,rain) #to create our data frame out of vectors!
```

```
##   days temp  rain
## 1  Mon 22.2  TRUE
## 2  Tue 21.0  TRUE
## 3  Wed 23.0 FALSE
## 4 Thur 24.3 FALSE
## 5  Fri 25.0  TRUE
```

```r
df <- data.frame(days,temp,rain)
df
```

```
##   days temp  rain
## 1  Mon 22.2  TRUE
## 2  Tue 21.0  TRUE
## 3  Wed 23.0 FALSE
## 4 Thur 24.3 FALSE
## 5  Fri 25.0  TRUE
```
Lets start indexing!

```r
df[1,] #all the columns of the 1st row
```

```
##   days temp rain
## 1  Mon 22.2 TRUE
```

```r
df[,1] #all the rows of the first column
```

```
## [1] "Mon"  "Tue"  "Wed"  "Thur" "Fri"
```

```r
df[,"days"]
```

```
## [1] "Mon"  "Tue"  "Wed"  "Thur" "Fri"
```

```r
df[,"rain"]
```

```
## [1]  TRUE  TRUE FALSE FALSE  TRUE
```

```r
df[1:3,c("days","temp")] #rows 1 to 3 and only the columns "days" and "temp"
```

```
##   days temp
## 1  Mon 22.2
## 2  Tue 21.0
## 3  Wed 23.0
```
We can also use another quick notations to grab columns of a data frame as a **VECTOR**

```r
df$days #returns the column of days as a vector
```

```
## [1] "Mon"  "Tue"  "Wed"  "Thur" "Fri"
```

```r
df["days"] #returns the column of days as a data frame
```

```
##   days
## 1  Mon
## 2  Tue
## 3  Wed
## 4 Thur
## 5  Fri
```
Lets learn to use the **subset function**

```r
subset(df,subset = rain==TRUE) #it only returns the values in which rain==TRUE is true
```

```
##   days temp rain
## 1  Mon 22.2 TRUE
## 2  Tue 21.0 TRUE
## 5  Fri 25.0 TRUE
```

```r
subset(df,subset = temp>23)
```

```
##   days temp  rain
## 4 Thur 24.3 FALSE
## 5  Fri 25.0  TRUE
```
We can also **order** a data frame

```r
sorted.temp <- order(df["temp"]) #it creates a vector of the ascending order of the temp column values
sorted.temp
```

```
## [1] 2 1 3 4 5
```

```r
df[sorted.temp,] #it returns the temp values in order from low to high
```

```
##   days temp  rain
## 2  Tue 21.0  TRUE
## 1  Mon 22.2  TRUE
## 3  Wed 23.0 FALSE
## 4 Thur 24.3 FALSE
## 5  Fri 25.0  TRUE
```

```r
# Now in descending order
desc.temp <- order(-df["temp"])
desc.temp
```

```
## [1] 5 4 3 1 2
```

```r
df[desc.temp,]
```

```
##   days temp  rain
## 5  Fri 25.0  TRUE
## 4 Thur 24.3 FALSE
## 3  Wed 23.0 FALSE
## 1  Mon 22.2  TRUE
## 2  Tue 21.0  TRUE
```

# **Overview of Data Frame Operations**
## Creating Data Frames

```r
empty <- data.frame() #to create an empty data frame
c1 <- 1:10 #vector from 1 to 10
c1
```

```
##  [1]  1  2  3  4  5  6  7  8  9 10
```

```r
c2 <- letters #vector of letters from a to z
c2
```

```
##  [1] "a" "b" "c" "d" "e" "f" "g" "h" "i" "j" "k" "l" "m" "n" "o" "p" "q" "r" "s" "t"
## [21] "u" "v" "w" "x" "y" "z"
```

```r
df <- data.frame(col.name.1 = c1, col.name.2 = c2[1:10]) #the col.name.n will be actually the name you want to give to your columns
```

##Working with **CSV files**

```r
#d2 <- read.csv("some_file.csv") #to read and assign the csv file to a variable
write.csv(df,file = "saved_df.csv") #to create a csv file out of a data frame we created here
df2 <- read.csv("saved_df.csv") #now, lets read it
df2
```

```
##     X col.name.1 col.name.2
## 1   1          1          a
## 2   2          2          b
## 3   3          3          c
## 4   4          4          d
## 5   5          5          e
## 6   6          6          f
## 7   7          7          g
## 8   8          8          h
## 9   9          9          i
## 10 10         10          j
```

```r
df
```

```
##    col.name.1 col.name.2
## 1           1          a
## 2           2          b
## 3           3          c
## 4           4          d
## 5           5          e
## 6           6          f
## 7           7          g
## 8           8          h
## 9           9          i
## 10         10          j
```

## Getting information about the data frame

```r
df
```

```
##    col.name.1 col.name.2
## 1           1          a
## 2           2          b
## 3           3          c
## 4           4          d
## 5           5          e
## 6           6          f
## 7           7          g
## 8           8          h
## 9           9          i
## 10         10          j
```

```r
nrow(df) #it tells us how many rows we have
```

```
## [1] 10
```

```r
ncol(df) #it tells us how many columns we have (not including the index column)
```

```
## [1] 2
```

```r
colnames(df) #names of columns
```

```
## [1] "col.name.1" "col.name.2"
```

```r
rownames(df) #names of rows
```

```
##  [1] "1"  "2"  "3"  "4"  "5"  "6"  "7"  "8"  "9"  "10"
```

```r
summary(df)
```

```
##    col.name.1     col.name.2       
##  Min.   : 1.00   Length:10         
##  1st Qu.: 3.25   Class :character  
##  Median : 5.50   Mode  :character  
##  Mean   : 5.50                     
##  3rd Qu.: 7.75                     
##  Max.   :10.00
```

```r
str(df)
```

```
## 'data.frame':	10 obs. of  2 variables:
##  $ col.name.1: int  1 2 3 4 5 6 7 8 9 10
##  $ col.name.2: chr  "a" "b" "c" "d" ...
```

## Referencing cells

```r
df
```

```
##    col.name.1 col.name.2
## 1           1          a
## 2           2          b
## 3           3          c
## 4           4          d
## 5           5          e
## 6           6          f
## 7           7          g
## 8           8          h
## 9           9          i
## 10         10          j
```

```r
df[[5,2]] # to reference the info in the row 5, column 2 in a data frame
```

```
## [1] "e"
```

```r
df[[5,"col.name.2"]]
```

```
## [1] "e"
```
To **re-assign a value inside of a made data frame**

```r
df[[2,"col.name.1"]] <- 9999 #we changed the value in the referenced position
df
```

```
##    col.name.1 col.name.2
## 1           1          a
## 2        9999          b
## 3           3          c
## 4           4          d
## 5           5          e
## 6           6          f
## 7           7          g
## 8           8          h
## 9           9          i
## 10         10          j
```
# Referencing rows

```r
df[1,]
```

```
##   col.name.1 col.name.2
## 1          1          a
```
# Referencing columns

```r
mtcars #an already made data frame
```

```
##                      mpg cyl  disp  hp drat    wt  qsec vs am gear carb performance
## Mazda RX4           21.0   6 160.0 110 3.90 2.620 16.46  0  1    4    4       41.98
## Mazda RX4 Wag       21.0   6 160.0 110 3.90 2.875 17.02  0  1    4    4       38.26
## Datsun 710          22.8   4 108.0  93 3.85 2.320 18.61  1  1    4    1       40.09
## Hornet 4 Drive      21.4   6 258.0 110 3.08 3.215 19.44  1  0    3    1       34.21
## Hornet Sportabout   18.7   8 360.0 175 3.15 3.440 17.02  0  0    3    2       50.87
## Valiant             18.1   6 225.0 105 2.76 3.460 20.22  1  0    3    1       30.35
## Duster 360          14.3   8 360.0 245 3.21 3.570 15.84  0  0    3    4       68.63
## Merc 240D           24.4   4 146.7  62 3.69 3.190 20.00  1  0    4    2       19.44
## Merc 230            22.8   4 140.8  95 3.92 3.150 22.90  1  0    4    2       30.16
## Merc 280            19.2   6 167.6 123 3.92 3.440 18.30  1  0    4    4       35.76
## Merc 280C           17.8   6 167.6 123 3.92 3.440 18.90  1  0    4    4       35.76
## Merc 450SE          16.4   8 275.8 180 3.07 4.070 17.40  0  0    3    3       44.23
## Merc 450SL          17.3   8 275.8 180 3.07 3.730 17.60  0  0    3    3       48.26
## Merc 450SLC         15.2   8 275.8 180 3.07 3.780 18.00  0  0    3    3       47.62
## Cadillac Fleetwood  10.4   8 472.0 205 2.93 5.250 17.98  0  0    3    4       39.05
## Lincoln Continental 10.4   8 460.0 215 3.00 5.424 17.82  0  0    3    4       39.64
## Chrysler Imperial   14.7   8 440.0 230 3.23 5.345 17.42  0  0    3    4       43.03
## Fiat 128            32.4   4  78.7  66 4.08 2.200 19.47  1  1    4    1       30.00
## Honda Civic         30.4   4  75.7  52 4.93 1.615 18.52  1  1    4    2       32.20
## Toyota Corolla      33.9   4  71.1  65 4.22 1.835 19.90  1  1    4    1       35.42
## Toyota Corona       21.5   4 120.1  97 3.70 2.465 20.01  1  0    3    1       39.35
## Dodge Challenger    15.5   8 318.0 150 2.76 3.520 16.87  0  0    3    2       42.61
## AMC Javelin         15.2   8 304.0 150 3.15 3.435 17.30  0  0    3    2       43.67
## Camaro Z28          13.3   8 350.0 245 3.73 3.840 15.41  0  0    3    4       63.80
## Pontiac Firebird    19.2   8 400.0 175 3.08 3.845 17.05  0  0    3    2       45.51
## Fiat X1-9           27.3   4  79.0  66 4.08 1.935 18.90  1  1    4    1       34.11
## Porsche 914-2       26.0   4 120.3  91 4.43 2.140 16.70  0  1    5    2       42.52
## Lotus Europa        30.4   4  95.1 113 3.77 1.513 16.90  1  1    5    2       74.69
## Ford Pantera L      15.8   8 351.0 264 4.22 3.170 14.50  0  1    5    4       83.28
## Ferrari Dino        19.7   6 145.0 175 3.62 2.770 15.50  0  1    5    6       63.18
## Maserati Bora       15.0   8 301.0 335 3.54 3.570 14.60  0  1    5    8       93.84
## Volvo 142E          21.4   4 121.0 109 4.11 2.780 18.60  1  1    4    2       39.21
```

```r
head(mtcars)
```

```
##                    mpg cyl disp  hp drat    wt  qsec vs am gear carb performance
## Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4       41.98
## Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4       38.26
## Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1       40.09
## Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1       34.21
## Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2       50.87
## Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1       30.35
```

```r
# To return a column as a VECTOR
mtcars$mpg 
```

```
##  [1] 21.0 21.0 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 17.8 16.4 17.3 15.2 10.4 10.4
## [17] 14.7 32.4 30.4 33.9 21.5 15.5 15.2 13.3 19.2 27.3 26.0 30.4 15.8 19.7 15.0 21.4
```

```r
mtcars[,"mpg"]
```

```
##  [1] 21.0 21.0 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 17.8 16.4 17.3 15.2 10.4 10.4
## [17] 14.7 32.4 30.4 33.9 21.5 15.5 15.2 13.3 19.2 27.3 26.0 30.4 15.8 19.7 15.0 21.4
```

```r
mtcars[,1]
```

```
##  [1] 21.0 21.0 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 17.8 16.4 17.3 15.2 10.4 10.4
## [17] 14.7 32.4 30.4 33.9 21.5 15.5 15.2 13.3 19.2 27.3 26.0 30.4 15.8 19.7 15.0 21.4
```

```r
mtcars[["mpg"]]
```

```
##  [1] 21.0 21.0 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 17.8 16.4 17.3 15.2 10.4 10.4
## [17] 14.7 32.4 30.4 33.9 21.5 15.5 15.2 13.3 19.2 27.3 26.0 30.4 15.8 19.7 15.0 21.4
```

```r
# To return a column as a DATA FRAME
mtcars["mpg"]
```

```
##                      mpg
## Mazda RX4           21.0
## Mazda RX4 Wag       21.0
## Datsun 710          22.8
## Hornet 4 Drive      21.4
## Hornet Sportabout   18.7
## Valiant             18.1
## Duster 360          14.3
## Merc 240D           24.4
## Merc 230            22.8
## Merc 280            19.2
## Merc 280C           17.8
## Merc 450SE          16.4
## Merc 450SL          17.3
## Merc 450SLC         15.2
## Cadillac Fleetwood  10.4
## Lincoln Continental 10.4
## Chrysler Imperial   14.7
## Fiat 128            32.4
## Honda Civic         30.4
## Toyota Corolla      33.9
## Toyota Corona       21.5
## Dodge Challenger    15.5
## AMC Javelin         15.2
## Camaro Z28          13.3
## Pontiac Firebird    19.2
## Fiat X1-9           27.3
## Porsche 914-2       26.0
## Lotus Europa        30.4
## Ford Pantera L      15.8
## Ferrari Dino        19.7
## Maserati Bora       15.0
## Volvo 142E          21.4
```

```r
mtcars[1]
```

```
##                      mpg
## Mazda RX4           21.0
## Mazda RX4 Wag       21.0
## Datsun 710          22.8
## Hornet 4 Drive      21.4
## Hornet Sportabout   18.7
## Valiant             18.1
## Duster 360          14.3
## Merc 240D           24.4
## Merc 230            22.8
## Merc 280            19.2
## Merc 280C           17.8
## Merc 450SE          16.4
## Merc 450SL          17.3
## Merc 450SLC         15.2
## Cadillac Fleetwood  10.4
## Lincoln Continental 10.4
## Chrysler Imperial   14.7
## Fiat 128            32.4
## Honda Civic         30.4
## Toyota Corolla      33.9
## Toyota Corona       21.5
## Dodge Challenger    15.5
## AMC Javelin         15.2
## Camaro Z28          13.3
## Pontiac Firebird    19.2
## Fiat X1-9           27.3
## Porsche 914-2       26.0
## Lotus Europa        30.4
## Ford Pantera L      15.8
## Ferrari Dino        19.7
## Maserati Bora       15.0
## Volvo 142E          21.4
```

```r
# To return multiple columns as a DATA FRAME
head(mtcars[c("mpg","cyl")])
```

```
##                    mpg cyl
## Mazda RX4         21.0   6
## Mazda RX4 Wag     21.0   6
## Datsun 710        22.8   4
## Hornet 4 Drive    21.4   6
## Hornet Sportabout 18.7   8
## Valiant           18.1   6
```
## Adding rows

```r
df2 <- data.frame(col.name.1 = 2000,col.name.2 = "new") #we create a chunk of data frame that we want to add to the previous data frame df
df
```

```
##    col.name.1 col.name.2
## 1           1          a
## 2        9999          b
## 3           3          c
## 4           4          d
## 5           5          e
## 6           6          f
## 7           7          g
## 8           8          h
## 9           9          i
## 10         10          j
```

```r
dfnew <- rbind(df,df2) #we bind the new row
dfnew
```

```
##    col.name.1 col.name.2
## 1           1          a
## 2        9999          b
## 3           3          c
## 4           4          d
## 5           5          e
## 6           6          f
## 7           7          g
## 8           8          h
## 9           9          i
## 10         10          j
## 11       2000        new
```
## Adding columns

```r
df$newcol <- 2*df$col.name.1 # we add a new column with the value of 2 times the col.name.1 of df
df
```

```
##    col.name.1 col.name.2 newcol
## 1           1          a      2
## 2        9999          b  19998
## 3           3          c      6
## 4           4          d      8
## 5           5          e     10
## 6           6          f     12
## 7           7          g     14
## 8           8          h     16
## 9           9          i     18
## 10         10          j     20
```

```r
df$newcol.copy <- df$newcol #we created another col
df
```

```
##    col.name.1 col.name.2 newcol newcol.copy
## 1           1          a      2           2
## 2        9999          b  19998       19998
## 3           3          c      6           6
## 4           4          d      8           8
## 5           5          e     10          10
## 6           6          f     12          12
## 7           7          g     14          14
## 8           8          h     16          16
## 9           9          i     18          18
## 10         10          j     20          20
```

```r
# we can also do this
df[,"newcol.copy2"] <- df$newcol
```

## Setting column names

```r
ncol(df)
```

```
## [1] 5
```

```r
colnames(df) <- c("col1","col2","col3","col4","col5")

# To name a specific column
colnames(df)[1] <- "new col name" #we just want to rename the 1st column
```

## Selecting multiple rows
Conditioning with $ symbol

```r
df[1:10,] #to select the rows 1 to 10
```

```
##    new col name col2  col3  col4  col5
## 1             1    a     2     2     2
## 2          9999    b 19998 19998 19998
## 3             3    c     6     6     6
## 4             4    d     8     8     8
## 5             5    e    10    10    10
## 6             6    f    12    12    12
## 7             7    g    14    14    14
## 8             8    h    16    16    16
## 9             9    i    18    18    18
## 10           10    j    20    20    20
```

```r
df[1:3,]
```

```
##   new col name col2  col3  col4  col5
## 1            1    a     2     2     2
## 2         9999    b 19998 19998 19998
## 3            3    c     6     6     6
```

```r
head(df,7) #to return the first 7 rows
```

```
##   new col name col2  col3  col4  col5
## 1            1    a     2     2     2
## 2         9999    b 19998 19998 19998
## 3            3    c     6     6     6
## 4            4    d     8     8     8
## 5            5    e    10    10    10
## 6            6    f    12    12    12
## 7            7    g    14    14    14
```

```r
df[-2,] #to select EVERYTHING BUT THE 2ND ROW
```

```
##    new col name col2 col3 col4 col5
## 1             1    a    2    2    2
## 3             3    c    6    6    6
## 4             4    d    8    8    8
## 5             5    e   10   10   10
## 6             6    f   12   12   12
## 7             7    g   14   14   14
## 8             8    h   16   16   16
## 9             9    i   18   18   18
## 10           10    j   20   20   20
```

```r
#Filtering the rows that we want to get
head(mtcars)
```

```
##                    mpg cyl disp  hp drat    wt  qsec vs am gear carb performance
## Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4       41.98
## Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4       38.26
## Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1       40.09
## Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1       34.21
## Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2       50.87
## Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1       30.35
```

```r
mtcars[mtcars$mpg > 20,] #to return only therows in which mpg value is greather than 20
```

```
##                 mpg cyl  disp  hp drat    wt  qsec vs am gear carb performance
## Mazda RX4      21.0   6 160.0 110 3.90 2.620 16.46  0  1    4    4       41.98
## Mazda RX4 Wag  21.0   6 160.0 110 3.90 2.875 17.02  0  1    4    4       38.26
## Datsun 710     22.8   4 108.0  93 3.85 2.320 18.61  1  1    4    1       40.09
## Hornet 4 Drive 21.4   6 258.0 110 3.08 3.215 19.44  1  0    3    1       34.21
## Merc 240D      24.4   4 146.7  62 3.69 3.190 20.00  1  0    4    2       19.44
## Merc 230       22.8   4 140.8  95 3.92 3.150 22.90  1  0    4    2       30.16
## Fiat 128       32.4   4  78.7  66 4.08 2.200 19.47  1  1    4    1       30.00
## Honda Civic    30.4   4  75.7  52 4.93 1.615 18.52  1  1    4    2       32.20
## Toyota Corolla 33.9   4  71.1  65 4.22 1.835 19.90  1  1    4    1       35.42
## Toyota Corona  21.5   4 120.1  97 3.70 2.465 20.01  1  0    3    1       39.35
## Fiat X1-9      27.3   4  79.0  66 4.08 1.935 18.90  1  1    4    1       34.11
## Porsche 914-2  26.0   4 120.3  91 4.43 2.140 16.70  0  1    5    2       42.52
## Lotus Europa   30.4   4  95.1 113 3.77 1.513 16.90  1  1    5    2       74.69
## Volvo 142E     21.4   4 121.0 109 4.11 2.780 18.60  1  1    4    2       39.21
```

```r
mtcars[(mtcars$mpg>20) & (mtcars$cyl == 6),c("mpg","cyl","hp")] #to get only the selected filtered rows and columns
```

```
##                 mpg cyl  hp
## Mazda RX4      21.0   6 110
## Mazda RX4 Wag  21.0   6 110
## Hornet 4 Drive 21.4   6 110
```
Conditioning with **Subset function**

```r
subset(mtcars, mpg>20 & cyl == 6)
```

```
##                 mpg cyl disp  hp drat    wt  qsec vs am gear carb performance
## Mazda RX4      21.0   6  160 110 3.90 2.620 16.46  0  1    4    4       41.98
## Mazda RX4 Wag  21.0   6  160 110 3.90 2.875 17.02  0  1    4    4       38.26
## Hornet 4 Drive 21.4   6  258 110 3.08 3.215 19.44  1  0    3    1       34.21
```

## Selecting multiple columns

```r
head(mtcars)
```

```
##                    mpg cyl disp  hp drat    wt  qsec vs am gear carb performance
## Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4       41.98
## Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4       38.26
## Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1       40.09
## Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1       34.21
## Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2       50.87
## Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1       30.35
```

```r
mtcars[,c(1,2,3)]
```

```
##                      mpg cyl  disp
## Mazda RX4           21.0   6 160.0
## Mazda RX4 Wag       21.0   6 160.0
## Datsun 710          22.8   4 108.0
## Hornet 4 Drive      21.4   6 258.0
## Hornet Sportabout   18.7   8 360.0
## Valiant             18.1   6 225.0
## Duster 360          14.3   8 360.0
## Merc 240D           24.4   4 146.7
## Merc 230            22.8   4 140.8
## Merc 280            19.2   6 167.6
## Merc 280C           17.8   6 167.6
## Merc 450SE          16.4   8 275.8
## Merc 450SL          17.3   8 275.8
## Merc 450SLC         15.2   8 275.8
## Cadillac Fleetwood  10.4   8 472.0
## Lincoln Continental 10.4   8 460.0
## Chrysler Imperial   14.7   8 440.0
## Fiat 128            32.4   4  78.7
## Honda Civic         30.4   4  75.7
## Toyota Corolla      33.9   4  71.1
## Toyota Corona       21.5   4 120.1
## Dodge Challenger    15.5   8 318.0
## AMC Javelin         15.2   8 304.0
## Camaro Z28          13.3   8 350.0
## Pontiac Firebird    19.2   8 400.0
## Fiat X1-9           27.3   4  79.0
## Porsche 914-2       26.0   4 120.3
## Lotus Europa        30.4   4  95.1
## Ford Pantera L      15.8   8 351.0
## Ferrari Dino        19.7   6 145.0
## Maserati Bora       15.0   8 301.0
## Volvo 142E          21.4   4 121.0
```

```r
mtcars[,c("mpg","cyl")]
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

## Dealing with missing data
Missing data = NA :(

```r
is.na(mtcars) #it returns FALSE if nothing is missing
```

```
##                       mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear
## Mazda RX4           FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Mazda RX4 Wag       FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Datsun 710          FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Hornet 4 Drive      FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Hornet Sportabout   FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Valiant             FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Duster 360          FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Merc 240D           FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Merc 230            FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Merc 280            FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Merc 280C           FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Merc 450SE          FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Merc 450SL          FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Merc 450SLC         FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Cadillac Fleetwood  FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Lincoln Continental FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Chrysler Imperial   FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Fiat 128            FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Honda Civic         FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Toyota Corolla      FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Toyota Corona       FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Dodge Challenger    FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## AMC Javelin         FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Camaro Z28          FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Pontiac Firebird    FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Fiat X1-9           FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Porsche 914-2       FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Lotus Europa        FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Ford Pantera L      FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Ferrari Dino        FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Maserati Bora       FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Volvo 142E          FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##                      carb performance
## Mazda RX4           FALSE       FALSE
## Mazda RX4 Wag       FALSE       FALSE
## Datsun 710          FALSE       FALSE
## Hornet 4 Drive      FALSE       FALSE
## Hornet Sportabout   FALSE       FALSE
## Valiant             FALSE       FALSE
## Duster 360          FALSE       FALSE
## Merc 240D           FALSE       FALSE
## Merc 230            FALSE       FALSE
## Merc 280            FALSE       FALSE
## Merc 280C           FALSE       FALSE
## Merc 450SE          FALSE       FALSE
## Merc 450SL          FALSE       FALSE
## Merc 450SLC         FALSE       FALSE
## Cadillac Fleetwood  FALSE       FALSE
## Lincoln Continental FALSE       FALSE
## Chrysler Imperial   FALSE       FALSE
## Fiat 128            FALSE       FALSE
## Honda Civic         FALSE       FALSE
## Toyota Corolla      FALSE       FALSE
## Toyota Corona       FALSE       FALSE
## Dodge Challenger    FALSE       FALSE
## AMC Javelin         FALSE       FALSE
## Camaro Z28          FALSE       FALSE
## Pontiac Firebird    FALSE       FALSE
## Fiat X1-9           FALSE       FALSE
## Porsche 914-2       FALSE       FALSE
## Lotus Europa        FALSE       FALSE
## Ford Pantera L      FALSE       FALSE
## Ferrari Dino        FALSE       FALSE
## Maserati Bora       FALSE       FALSE
## Volvo 142E          FALSE       FALSE
```

```r
any(is.na(mtcars)) #it checks QUICKLY if there's any TRUE in the NA check of all the data frame
```

```
## [1] FALSE
```

```r
any(is.na(mtcars$mpg))
```

```
## [1] FALSE
```
TO replace missing data

```r
df[is.na(df)] <- 0
mtcars$mpg[is.na(mtcars$mpg)] <- mean(mtcars$mpg) #only replaces the missing values of a column
```

#**...Data frames exercises...**
Ex 1: Recreate the following dataframe by creating vectors and using the data.frame function:


```r
name <- c("Sam","Frank","Amy")
age <- c(22,25,26)
weight <- c(150,165,120)
sex <- c("M","M","F")

adults.info <- data.frame(name,age,weight,sex)
adults.info
```

```
##    name age weight sex
## 1   Sam  22    150   M
## 2 Frank  25    165   M
## 3   Amy  26    120   F
```
Ex 2: Check if mtcars is a dataframe using is.data.frame()

```r
is.data.frame(mtcars)
```

```
## [1] TRUE
```
Ex 3: Use as.data.frame() to convert a matrix into a dataframe:

```r
mat <- matrix(1:25, nrow = 5)
mat.df <- as.data.frame(mat)
```
Ex 4: Set the built-in data frame mtcars as a variable df. We'll use this df variable for the rest of the exercises.

```r
df <- mtcars
```
Ex 5: Display the first 6 rows of df

```r
head(df)
```

```
##                    mpg cyl disp  hp drat    wt  qsec vs am gear carb performance
## Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4       41.98
## Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4       38.26
## Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1       40.09
## Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1       34.21
## Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2       50.87
## Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1       30.35
```
Ex 6: What is the average mpg value for all the cars?

```r
mean(mtcars$mpg)
```

```
## [1] 20.09062
```
Ex 7: Select the rows where all cars have 6 cylinders (cyl column)

```r
# 2 ways of doing it
subset(mtcars, mtcars$cyl == 6)
```

```
##                 mpg cyl  disp  hp drat    wt  qsec vs am gear carb performance
## Mazda RX4      21.0   6 160.0 110 3.90 2.620 16.46  0  1    4    4       41.98
## Mazda RX4 Wag  21.0   6 160.0 110 3.90 2.875 17.02  0  1    4    4       38.26
## Hornet 4 Drive 21.4   6 258.0 110 3.08 3.215 19.44  1  0    3    1       34.21
## Valiant        18.1   6 225.0 105 2.76 3.460 20.22  1  0    3    1       30.35
## Merc 280       19.2   6 167.6 123 3.92 3.440 18.30  1  0    4    4       35.76
## Merc 280C      17.8   6 167.6 123 3.92 3.440 18.90  1  0    4    4       35.76
## Ferrari Dino   19.7   6 145.0 175 3.62 2.770 15.50  0  1    5    6       63.18
```

```r
mtcars[mtcars$cyl == 6,]
```

```
##                 mpg cyl  disp  hp drat    wt  qsec vs am gear carb performance
## Mazda RX4      21.0   6 160.0 110 3.90 2.620 16.46  0  1    4    4       41.98
## Mazda RX4 Wag  21.0   6 160.0 110 3.90 2.875 17.02  0  1    4    4       38.26
## Hornet 4 Drive 21.4   6 258.0 110 3.08 3.215 19.44  1  0    3    1       34.21
## Valiant        18.1   6 225.0 105 2.76 3.460 20.22  1  0    3    1       30.35
## Merc 280       19.2   6 167.6 123 3.92 3.440 18.30  1  0    4    4       35.76
## Merc 280C      17.8   6 167.6 123 3.92 3.440 18.90  1  0    4    4       35.76
## Ferrari Dino   19.7   6 145.0 175 3.62 2.770 15.50  0  1    5    6       63.18
```
Ex 8: Select the columns am,gear, and carb.

```r
mtcars[,c("am","gear","carb")]
```

```
##                     am gear carb
## Mazda RX4            1    4    4
## Mazda RX4 Wag        1    4    4
## Datsun 710           1    4    1
## Hornet 4 Drive       0    3    1
## Hornet Sportabout    0    3    2
## Valiant              0    3    1
## Duster 360           0    3    4
## Merc 240D            0    4    2
## Merc 230             0    4    2
## Merc 280             0    4    4
## Merc 280C            0    4    4
## Merc 450SE           0    3    3
## Merc 450SL           0    3    3
## Merc 450SLC          0    3    3
## Cadillac Fleetwood   0    3    4
## Lincoln Continental  0    3    4
## Chrysler Imperial    0    3    4
## Fiat 128             1    4    1
## Honda Civic          1    4    2
## Toyota Corolla       1    4    1
## Toyota Corona        0    3    1
## Dodge Challenger     0    3    2
## AMC Javelin          0    3    2
## Camaro Z28           0    3    4
## Pontiac Firebird     0    3    2
## Fiat X1-9            1    4    1
## Porsche 914-2        1    5    2
## Lotus Europa         1    5    2
## Ford Pantera L       1    5    4
## Ferrari Dino         1    5    6
## Maserati Bora        1    5    8
## Volvo 142E           1    4    2
```
Ex 9: Create a new column called performance, which is calculated by hp/wt.


```r
mtcars$performance <- mtcars$hp / mtcars$wt
mtcars
```

```
##                      mpg cyl  disp  hp drat    wt  qsec vs am gear carb performance
## Mazda RX4           21.0   6 160.0 110 3.90 2.620 16.46  0  1    4    4    41.98473
## Mazda RX4 Wag       21.0   6 160.0 110 3.90 2.875 17.02  0  1    4    4    38.26087
## Datsun 710          22.8   4 108.0  93 3.85 2.320 18.61  1  1    4    1    40.08621
## Hornet 4 Drive      21.4   6 258.0 110 3.08 3.215 19.44  1  0    3    1    34.21462
## Hornet Sportabout   18.7   8 360.0 175 3.15 3.440 17.02  0  0    3    2    50.87209
## Valiant             18.1   6 225.0 105 2.76 3.460 20.22  1  0    3    1    30.34682
## Duster 360          14.3   8 360.0 245 3.21 3.570 15.84  0  0    3    4    68.62745
## Merc 240D           24.4   4 146.7  62 3.69 3.190 20.00  1  0    4    2    19.43574
## Merc 230            22.8   4 140.8  95 3.92 3.150 22.90  1  0    4    2    30.15873
## Merc 280            19.2   6 167.6 123 3.92 3.440 18.30  1  0    4    4    35.75581
## Merc 280C           17.8   6 167.6 123 3.92 3.440 18.90  1  0    4    4    35.75581
## Merc 450SE          16.4   8 275.8 180 3.07 4.070 17.40  0  0    3    3    44.22604
## Merc 450SL          17.3   8 275.8 180 3.07 3.730 17.60  0  0    3    3    48.25737
## Merc 450SLC         15.2   8 275.8 180 3.07 3.780 18.00  0  0    3    3    47.61905
## Cadillac Fleetwood  10.4   8 472.0 205 2.93 5.250 17.98  0  0    3    4    39.04762
## Lincoln Continental 10.4   8 460.0 215 3.00 5.424 17.82  0  0    3    4    39.63864
## Chrysler Imperial   14.7   8 440.0 230 3.23 5.345 17.42  0  0    3    4    43.03087
## Fiat 128            32.4   4  78.7  66 4.08 2.200 19.47  1  1    4    1    30.00000
## Honda Civic         30.4   4  75.7  52 4.93 1.615 18.52  1  1    4    2    32.19814
## Toyota Corolla      33.9   4  71.1  65 4.22 1.835 19.90  1  1    4    1    35.42234
## Toyota Corona       21.5   4 120.1  97 3.70 2.465 20.01  1  0    3    1    39.35091
## Dodge Challenger    15.5   8 318.0 150 2.76 3.520 16.87  0  0    3    2    42.61364
## AMC Javelin         15.2   8 304.0 150 3.15 3.435 17.30  0  0    3    2    43.66812
## Camaro Z28          13.3   8 350.0 245 3.73 3.840 15.41  0  0    3    4    63.80208
## Pontiac Firebird    19.2   8 400.0 175 3.08 3.845 17.05  0  0    3    2    45.51365
## Fiat X1-9           27.3   4  79.0  66 4.08 1.935 18.90  1  1    4    1    34.10853
## Porsche 914-2       26.0   4 120.3  91 4.43 2.140 16.70  0  1    5    2    42.52336
## Lotus Europa        30.4   4  95.1 113 3.77 1.513 16.90  1  1    5    2    74.68605
## Ford Pantera L      15.8   8 351.0 264 4.22 3.170 14.50  0  1    5    4    83.28076
## Ferrari Dino        19.7   6 145.0 175 3.62 2.770 15.50  0  1    5    6    63.17690
## Maserati Bora       15.0   8 301.0 335 3.54 3.570 14.60  0  1    5    8    93.83754
## Volvo 142E          21.4   4 121.0 109 4.11 2.780 18.60  1  1    4    2    39.20863
```

```r
head(mtcars)
```

```
##                    mpg cyl disp  hp drat    wt  qsec vs am gear carb performance
## Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4    41.98473
## Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4    38.26087
## Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1    40.08621
## Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1    34.21462
## Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2    50.87209
## Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1    30.34682
```
Ex 10: Your performance column will have several decimal place precision. Figure out how to use round() (check help(round)) to reduce this accuracy to only 2 decimal places.

```r
mtcars$performance <- round(mtcars$hp / mtcars$wt, digits = 2)
mtcars
```

```
##                      mpg cyl  disp  hp drat    wt  qsec vs am gear carb performance
## Mazda RX4           21.0   6 160.0 110 3.90 2.620 16.46  0  1    4    4       41.98
## Mazda RX4 Wag       21.0   6 160.0 110 3.90 2.875 17.02  0  1    4    4       38.26
## Datsun 710          22.8   4 108.0  93 3.85 2.320 18.61  1  1    4    1       40.09
## Hornet 4 Drive      21.4   6 258.0 110 3.08 3.215 19.44  1  0    3    1       34.21
## Hornet Sportabout   18.7   8 360.0 175 3.15 3.440 17.02  0  0    3    2       50.87
## Valiant             18.1   6 225.0 105 2.76 3.460 20.22  1  0    3    1       30.35
## Duster 360          14.3   8 360.0 245 3.21 3.570 15.84  0  0    3    4       68.63
## Merc 240D           24.4   4 146.7  62 3.69 3.190 20.00  1  0    4    2       19.44
## Merc 230            22.8   4 140.8  95 3.92 3.150 22.90  1  0    4    2       30.16
## Merc 280            19.2   6 167.6 123 3.92 3.440 18.30  1  0    4    4       35.76
## Merc 280C           17.8   6 167.6 123 3.92 3.440 18.90  1  0    4    4       35.76
## Merc 450SE          16.4   8 275.8 180 3.07 4.070 17.40  0  0    3    3       44.23
## Merc 450SL          17.3   8 275.8 180 3.07 3.730 17.60  0  0    3    3       48.26
## Merc 450SLC         15.2   8 275.8 180 3.07 3.780 18.00  0  0    3    3       47.62
## Cadillac Fleetwood  10.4   8 472.0 205 2.93 5.250 17.98  0  0    3    4       39.05
## Lincoln Continental 10.4   8 460.0 215 3.00 5.424 17.82  0  0    3    4       39.64
## Chrysler Imperial   14.7   8 440.0 230 3.23 5.345 17.42  0  0    3    4       43.03
## Fiat 128            32.4   4  78.7  66 4.08 2.200 19.47  1  1    4    1       30.00
## Honda Civic         30.4   4  75.7  52 4.93 1.615 18.52  1  1    4    2       32.20
## Toyota Corolla      33.9   4  71.1  65 4.22 1.835 19.90  1  1    4    1       35.42
## Toyota Corona       21.5   4 120.1  97 3.70 2.465 20.01  1  0    3    1       39.35
## Dodge Challenger    15.5   8 318.0 150 2.76 3.520 16.87  0  0    3    2       42.61
## AMC Javelin         15.2   8 304.0 150 3.15 3.435 17.30  0  0    3    2       43.67
## Camaro Z28          13.3   8 350.0 245 3.73 3.840 15.41  0  0    3    4       63.80
## Pontiac Firebird    19.2   8 400.0 175 3.08 3.845 17.05  0  0    3    2       45.51
## Fiat X1-9           27.3   4  79.0  66 4.08 1.935 18.90  1  1    4    1       34.11
## Porsche 914-2       26.0   4 120.3  91 4.43 2.140 16.70  0  1    5    2       42.52
## Lotus Europa        30.4   4  95.1 113 3.77 1.513 16.90  1  1    5    2       74.69
## Ford Pantera L      15.8   8 351.0 264 4.22 3.170 14.50  0  1    5    4       83.28
## Ferrari Dino        19.7   6 145.0 175 3.62 2.770 15.50  0  1    5    6       63.18
## Maserati Bora       15.0   8 301.0 335 3.54 3.570 14.60  0  1    5    8       93.84
## Volvo 142E          21.4   4 121.0 109 4.11 2.780 18.60  1  1    4    2       39.21
```

```r
head(mtcars)
```

```
##                    mpg cyl disp  hp drat    wt  qsec vs am gear carb performance
## Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4       41.98
## Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4       38.26
## Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1       40.09
## Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1       34.21
## Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2       50.87
## Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1       30.35
```
Ex 10: What is the average mpg for cars that have more than 100 hp AND a wt value of more than 2.5.

```r
mean(mtcars[mtcars$hp > 100 & mtcars$wt > 2.5,"mpg"])
```

```
## [1] 16.86364
```
Ex 11: What is the mpg of the Hornet Sportabout?

```r
mtcars["Hornet Sportabout","mpg"]
```

```
## [1] 18.7
```

