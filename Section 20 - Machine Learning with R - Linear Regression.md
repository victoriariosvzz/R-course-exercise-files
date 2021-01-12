---
title: 'Section 20: Machine Learning with R - Linear Regression'
author: "Victoria"
date: "10/1/2021"
output: html_document
---



# **Using R for Linear Regression**
Formulas in R take the form (y ~ x). To add more variables we use the sign +, for example (y ~ x + z)

##**syntax for linear regression model**
model <- lm(formula, data = dataframe.for.training)
**formula's syntax*: Quantity we want to predict ~ variables that make that prediction (var1 + var2...)
**Once you create your model, it's time to train your model**
dtest$pred_quantity <- predict(model, newdata = data.to.use.in.prediction)

#**Linear Regression with R**
1. Getting the data

```r
df <- read.csv("student-mat.csv",sep = ";") #we indicate the separator is not a comma but a ;
head(df)
```

```
##   school sex age address famsize
## 1     GP   F  18       U     GT3
## 2     GP   F  17       U     GT3
## 3     GP   F  15       U     LE3
## 4     GP   F  15       U     GT3
## 5     GP   F  16       U     GT3
## 6     GP   M  16       U     LE3
##   Pstatus Medu Fedu     Mjob     Fjob
## 1       A    4    4  at_home  teacher
## 2       T    1    1  at_home    other
## 3       T    1    1  at_home    other
## 4       T    4    2   health services
## 5       T    3    3    other    other
## 6       T    4    3 services    other
##       reason guardian traveltime
## 1     course   mother          2
## 2     course   father          1
## 3      other   mother          1
## 4       home   mother          1
## 5       home   father          1
## 6 reputation   mother          1
##   studytime failures schoolsup famsup
## 1         2        0       yes     no
## 2         2        0        no    yes
## 3         2        3       yes     no
## 4         3        0        no    yes
## 5         2        0        no    yes
## 6         2        0        no    yes
##   paid activities nursery higher
## 1   no         no     yes    yes
## 2   no         no      no    yes
## 3  yes         no     yes    yes
## 4  yes        yes     yes    yes
## 5  yes         no     yes    yes
## 6  yes        yes     yes    yes
##   internet romantic famrel freetime
## 1       no       no      4        3
## 2      yes       no      5        3
## 3      yes       no      4        3
## 4      yes      yes      3        2
## 5       no       no      4        3
## 6      yes       no      5        4
##   goout Dalc Walc health absences G1
## 1     4    1    1      3        6  5
## 2     3    1    1      3        4  5
## 3     2    2    3      3       10  7
## 4     2    1    1      5        2 15
## 5     2    1    2      5        4  6
## 6     2    1    2      5       10 15
##   G2 G3
## 1  6  6
## 2  5  6
## 3  8 10
## 4 14 15
## 5 10 10
## 6 15 15
```

```r
summary(df)
```

```
##     school              sex           
##  Length:395         Length:395        
##  Class :character   Class :character  
##  Mode  :character   Mode  :character  
##                                       
##                                       
##                                       
##       age         address         
##  Min.   :15.0   Length:395        
##  1st Qu.:16.0   Class :character  
##  Median :17.0   Mode  :character  
##  Mean   :16.7                     
##  3rd Qu.:18.0                     
##  Max.   :22.0                     
##    famsize            Pstatus         
##  Length:395         Length:395        
##  Class :character   Class :character  
##  Mode  :character   Mode  :character  
##                                       
##                                       
##                                       
##       Medu            Fedu      
##  Min.   :0.000   Min.   :0.000  
##  1st Qu.:2.000   1st Qu.:2.000  
##  Median :3.000   Median :2.000  
##  Mean   :2.749   Mean   :2.522  
##  3rd Qu.:4.000   3rd Qu.:3.000  
##  Max.   :4.000   Max.   :4.000  
##      Mjob               Fjob          
##  Length:395         Length:395        
##  Class :character   Class :character  
##  Mode  :character   Mode  :character  
##                                       
##                                       
##                                       
##     reason            guardian        
##  Length:395         Length:395        
##  Class :character   Class :character  
##  Mode  :character   Mode  :character  
##                                       
##                                       
##                                       
##    traveltime      studytime    
##  Min.   :1.000   Min.   :1.000  
##  1st Qu.:1.000   1st Qu.:1.000  
##  Median :1.000   Median :2.000  
##  Mean   :1.448   Mean   :2.035  
##  3rd Qu.:2.000   3rd Qu.:2.000  
##  Max.   :4.000   Max.   :4.000  
##     failures       schoolsup        
##  Min.   :0.0000   Length:395        
##  1st Qu.:0.0000   Class :character  
##  Median :0.0000   Mode  :character  
##  Mean   :0.3342                     
##  3rd Qu.:0.0000                     
##  Max.   :3.0000                     
##     famsup              paid          
##  Length:395         Length:395        
##  Class :character   Class :character  
##  Mode  :character   Mode  :character  
##                                       
##                                       
##                                       
##   activities          nursery         
##  Length:395         Length:395        
##  Class :character   Class :character  
##  Mode  :character   Mode  :character  
##                                       
##                                       
##                                       
##     higher            internet        
##  Length:395         Length:395        
##  Class :character   Class :character  
##  Mode  :character   Mode  :character  
##                                       
##                                       
##                                       
##    romantic             famrel     
##  Length:395         Min.   :1.000  
##  Class :character   1st Qu.:4.000  
##  Mode  :character   Median :4.000  
##                     Mean   :3.944  
##                     3rd Qu.:5.000  
##                     Max.   :5.000  
##     freetime         goout      
##  Min.   :1.000   Min.   :1.000  
##  1st Qu.:3.000   1st Qu.:2.000  
##  Median :3.000   Median :3.000  
##  Mean   :3.235   Mean   :3.109  
##  3rd Qu.:4.000   3rd Qu.:4.000  
##  Max.   :5.000   Max.   :5.000  
##       Dalc            Walc      
##  Min.   :1.000   Min.   :1.000  
##  1st Qu.:1.000   1st Qu.:1.000  
##  Median :1.000   Median :2.000  
##  Mean   :1.481   Mean   :2.291  
##  3rd Qu.:2.000   3rd Qu.:3.000  
##  Max.   :5.000   Max.   :5.000  
##      health         absences     
##  Min.   :1.000   Min.   : 0.000  
##  1st Qu.:3.000   1st Qu.: 0.000  
##  Median :4.000   Median : 4.000  
##  Mean   :3.554   Mean   : 5.709  
##  3rd Qu.:5.000   3rd Qu.: 8.000  
##  Max.   :5.000   Max.   :75.000  
##        G1              G2       
##  Min.   : 3.00   Min.   : 0.00  
##  1st Qu.: 8.00   1st Qu.: 9.00  
##  Median :11.00   Median :11.00  
##  Mean   :10.91   Mean   :10.71  
##  3rd Qu.:13.00   3rd Qu.:13.00  
##  Max.   :19.00   Max.   :19.00  
##        G3       
##  Min.   : 0.00  
##  1st Qu.: 8.00  
##  Median :11.00  
##  Mean   :10.42  
##  3rd Qu.:14.00  
##  Max.   :20.00
```
2. Cleaning the data

```r
any(is.na(df)) #to check if we have na values
```

```
## [1] FALSE
```

```r
str(df)
```

```
## 'data.frame':	395 obs. of  33 variables:
##  $ school    : chr  "GP" "GP" "GP" "GP" ...
##  $ sex       : chr  "F" "F" "F" "F" ...
##  $ age       : int  18 17 15 15 16 16 16 17 15 15 ...
##  $ address   : chr  "U" "U" "U" "U" ...
##  $ famsize   : chr  "GT3" "GT3" "LE3" "GT3" ...
##  $ Pstatus   : chr  "A" "T" "T" "T" ...
##  $ Medu      : int  4 1 1 4 3 4 2 4 3 3 ...
##  $ Fedu      : int  4 1 1 2 3 3 2 4 2 4 ...
##  $ Mjob      : chr  "at_home" "at_home" "at_home" "health" ...
##  $ Fjob      : chr  "teacher" "other" "other" "services" ...
##  $ reason    : chr  "course" "course" "other" "home" ...
##  $ guardian  : chr  "mother" "father" "mother" "mother" ...
##  $ traveltime: int  2 1 1 1 1 1 1 2 1 1 ...
##  $ studytime : int  2 2 2 3 2 2 2 2 2 2 ...
##  $ failures  : int  0 0 3 0 0 0 0 0 0 0 ...
##  $ schoolsup : chr  "yes" "no" "yes" "no" ...
##  $ famsup    : chr  "no" "yes" "no" "yes" ...
##  $ paid      : chr  "no" "no" "yes" "yes" ...
##  $ activities: chr  "no" "no" "no" "yes" ...
##  $ nursery   : chr  "yes" "no" "yes" "yes" ...
##  $ higher    : chr  "yes" "yes" "yes" "yes" ...
##  $ internet  : chr  "no" "yes" "yes" "yes" ...
##  $ romantic  : chr  "no" "no" "no" "yes" ...
##  $ famrel    : int  4 5 4 3 4 5 4 4 4 5 ...
##  $ freetime  : int  3 3 3 2 3 4 4 1 2 5 ...
##  $ goout     : int  4 3 2 2 2 2 4 4 2 1 ...
##  $ Dalc      : int  1 1 2 1 1 1 1 1 1 1 ...
##  $ Walc      : int  1 1 3 1 2 2 1 1 1 1 ...
##  $ health    : int  3 3 3 5 5 5 3 1 1 5 ...
##  $ absences  : int  6 4 10 2 4 10 0 6 0 0 ...
##  $ G1        : int  5 5 7 15 6 15 12 6 16 14 ...
##  $ G2        : int  6 5 8 14 10 15 12 5 18 15 ...
##  $ G3        : int  6 6 10 15 10 15 11 6 19 15 ...
```
3. Exploring the data with ggplot2 to find correlations

```r
library(ggplot2)
library(ggthemes)
library(dplyr)

#Num only
num.cols <- sapply(df,is.numeric) #we can only use the cor function with numeric values
#Filter
cor.data <- cor(df[,num.cols]) #we find the correlation of the numeric columns
print(cor.data)
```

```
##                     age         Medu
## age         1.000000000 -0.163658419
## Medu       -0.163658419  1.000000000
## Fedu       -0.163438069  0.623455112
## traveltime  0.070640721 -0.171639305
## studytime  -0.004140037  0.064944137
## failures    0.243665377 -0.236679963
## famrel      0.053940096 -0.003914458
## freetime    0.016434389  0.030890867
## goout       0.126963880  0.064094438
## Dalc        0.131124605  0.019834099
## Walc        0.117276052 -0.047123460
## health     -0.062187369 -0.046877829
## absences    0.175230079  0.100284818
## G1         -0.064081497  0.205340997
## G2         -0.143474049  0.215527168
## G3         -0.161579438  0.217147496
##                    Fedu   traveltime
## age        -0.163438069  0.070640721
## Medu        0.623455112 -0.171639305
## Fedu        1.000000000 -0.158194054
## traveltime -0.158194054  1.000000000
## studytime  -0.009174639 -0.100909119
## failures   -0.250408444  0.092238746
## famrel     -0.001369727 -0.016807986
## freetime   -0.012845528 -0.017024944
## goout       0.043104668  0.028539674
## Dalc        0.002386429  0.138325309
## Walc       -0.012631018  0.134115752
## health      0.014741537  0.007500606
## absences    0.024472887 -0.012943775
## G1          0.190269936 -0.093039992
## G2          0.164893393 -0.153197963
## G3          0.152456939 -0.117142053
##               studytime    failures
## age        -0.004140037  0.24366538
## Medu        0.064944137 -0.23667996
## Fedu       -0.009174639 -0.25040844
## traveltime -0.100909119  0.09223875
## studytime   1.000000000 -0.17356303
## failures   -0.173563031  1.00000000
## famrel      0.039730704 -0.04433663
## freetime   -0.143198407  0.09198747
## goout      -0.063903675  0.12456092
## Dalc       -0.196019263  0.13604693
## Walc       -0.253784731  0.14196203
## health     -0.075615863  0.06582728
## absences   -0.062700175  0.06372583
## G1          0.160611915 -0.35471761
## G2          0.135879999 -0.35589563
## G3          0.097819690 -0.36041494
##                  famrel    freetime
## age         0.053940096  0.01643439
## Medu       -0.003914458  0.03089087
## Fedu       -0.001369727 -0.01284553
## traveltime -0.016807986 -0.01702494
## studytime   0.039730704 -0.14319841
## failures   -0.044336626  0.09198747
## famrel      1.000000000  0.15070144
## freetime    0.150701444  1.00000000
## goout       0.064568411  0.28501871
## Dalc       -0.077594357  0.20900085
## Walc       -0.113397308  0.14782181
## health      0.094055728  0.07573336
## absences   -0.044354095 -0.05807792
## G1          0.022168316  0.01261293
## G2         -0.018281347 -0.01377714
## G3          0.051363429  0.01130724
##                   goout         Dalc
## age         0.126963880  0.131124605
## Medu        0.064094438  0.019834099
## Fedu        0.043104668  0.002386429
## traveltime  0.028539674  0.138325309
## studytime  -0.063903675 -0.196019263
## failures    0.124560922  0.136046931
## famrel      0.064568411 -0.077594357
## freetime    0.285018715  0.209000848
## goout       1.000000000  0.266993848
## Dalc        0.266993848  1.000000000
## Walc        0.420385745  0.647544230
## health     -0.009577254  0.077179582
## absences    0.044302220  0.111908026
## G1         -0.149103967 -0.094158792
## G2         -0.162250034 -0.064120183
## G3         -0.132791474 -0.054660041
##                   Walc       health
## age         0.11727605 -0.062187369
## Medu       -0.04712346 -0.046877829
## Fedu       -0.01263102  0.014741537
## traveltime  0.13411575  0.007500606
## studytime  -0.25378473 -0.075615863
## failures    0.14196203  0.065827282
## famrel     -0.11339731  0.094055728
## freetime    0.14782181  0.075733357
## goout       0.42038575 -0.009577254
## Dalc        0.64754423  0.077179582
## Walc        1.00000000  0.092476317
## health      0.09247632  1.000000000
## absences    0.13629110 -0.029936711
## G1         -0.12617921 -0.073172073
## G2         -0.08492735 -0.097719866
## G3         -0.05193932 -0.061334605
##               absences          G1
## age         0.17523008 -0.06408150
## Medu        0.10028482  0.20534100
## Fedu        0.02447289  0.19026994
## traveltime -0.01294378 -0.09303999
## studytime  -0.06270018  0.16061192
## failures    0.06372583 -0.35471761
## famrel     -0.04435409  0.02216832
## freetime   -0.05807792  0.01261293
## goout       0.04430222 -0.14910397
## Dalc        0.11190803 -0.09415879
## Walc        0.13629110 -0.12617921
## health     -0.02993671 -0.07317207
## absences    1.00000000 -0.03100290
## G1         -0.03100290  1.00000000
## G2         -0.03177670  0.85211807
## G3          0.03424732  0.80146793
##                     G2          G3
## age        -0.14347405 -0.16157944
## Medu        0.21552717  0.21714750
## Fedu        0.16489339  0.15245694
## traveltime -0.15319796 -0.11714205
## studytime   0.13588000  0.09781969
## failures   -0.35589563 -0.36041494
## famrel     -0.01828135  0.05136343
## freetime   -0.01377714  0.01130724
## goout      -0.16225003 -0.13279147
## Dalc       -0.06412018 -0.05466004
## Walc       -0.08492735 -0.05193932
## health     -0.09771987 -0.06133460
## absences   -0.03177670  0.03424732
## G1          0.85211807  0.80146793
## G2          1.00000000  0.90486799
## G3          0.90486799  1.00000000
```
4. We digitaliza the data to have an easy interpretation of it

```r
library(corrgram)
library(corrplot)

#using corrplot (we need to filter for only num values and apply cor to the data)
print(corrplot(cor.data, method = "color"))
```

![plot of chunk unnamed-chunk-42](figure/unnamed-chunk-42-1.png)

```
##                     age         Medu
## age         1.000000000 -0.163658419
## Medu       -0.163658419  1.000000000
## Fedu       -0.163438069  0.623455112
## traveltime  0.070640721 -0.171639305
## studytime  -0.004140037  0.064944137
## failures    0.243665377 -0.236679963
## famrel      0.053940096 -0.003914458
## freetime    0.016434389  0.030890867
## goout       0.126963880  0.064094438
## Dalc        0.131124605  0.019834099
## Walc        0.117276052 -0.047123460
## health     -0.062187369 -0.046877829
## absences    0.175230079  0.100284818
## G1         -0.064081497  0.205340997
## G2         -0.143474049  0.215527168
## G3         -0.161579438  0.217147496
##                    Fedu   traveltime
## age        -0.163438069  0.070640721
## Medu        0.623455112 -0.171639305
## Fedu        1.000000000 -0.158194054
## traveltime -0.158194054  1.000000000
## studytime  -0.009174639 -0.100909119
## failures   -0.250408444  0.092238746
## famrel     -0.001369727 -0.016807986
## freetime   -0.012845528 -0.017024944
## goout       0.043104668  0.028539674
## Dalc        0.002386429  0.138325309
## Walc       -0.012631018  0.134115752
## health      0.014741537  0.007500606
## absences    0.024472887 -0.012943775
## G1          0.190269936 -0.093039992
## G2          0.164893393 -0.153197963
## G3          0.152456939 -0.117142053
##               studytime    failures
## age        -0.004140037  0.24366538
## Medu        0.064944137 -0.23667996
## Fedu       -0.009174639 -0.25040844
## traveltime -0.100909119  0.09223875
## studytime   1.000000000 -0.17356303
## failures   -0.173563031  1.00000000
## famrel      0.039730704 -0.04433663
## freetime   -0.143198407  0.09198747
## goout      -0.063903675  0.12456092
## Dalc       -0.196019263  0.13604693
## Walc       -0.253784731  0.14196203
## health     -0.075615863  0.06582728
## absences   -0.062700175  0.06372583
## G1          0.160611915 -0.35471761
## G2          0.135879999 -0.35589563
## G3          0.097819690 -0.36041494
##                  famrel    freetime
## age         0.053940096  0.01643439
## Medu       -0.003914458  0.03089087
## Fedu       -0.001369727 -0.01284553
## traveltime -0.016807986 -0.01702494
## studytime   0.039730704 -0.14319841
## failures   -0.044336626  0.09198747
## famrel      1.000000000  0.15070144
## freetime    0.150701444  1.00000000
## goout       0.064568411  0.28501871
## Dalc       -0.077594357  0.20900085
## Walc       -0.113397308  0.14782181
## health      0.094055728  0.07573336
## absences   -0.044354095 -0.05807792
## G1          0.022168316  0.01261293
## G2         -0.018281347 -0.01377714
## G3          0.051363429  0.01130724
##                   goout         Dalc
## age         0.126963880  0.131124605
## Medu        0.064094438  0.019834099
## Fedu        0.043104668  0.002386429
## traveltime  0.028539674  0.138325309
## studytime  -0.063903675 -0.196019263
## failures    0.124560922  0.136046931
## famrel      0.064568411 -0.077594357
## freetime    0.285018715  0.209000848
## goout       1.000000000  0.266993848
## Dalc        0.266993848  1.000000000
## Walc        0.420385745  0.647544230
## health     -0.009577254  0.077179582
## absences    0.044302220  0.111908026
## G1         -0.149103967 -0.094158792
## G2         -0.162250034 -0.064120183
## G3         -0.132791474 -0.054660041
##                   Walc       health
## age         0.11727605 -0.062187369
## Medu       -0.04712346 -0.046877829
## Fedu       -0.01263102  0.014741537
## traveltime  0.13411575  0.007500606
## studytime  -0.25378473 -0.075615863
## failures    0.14196203  0.065827282
## famrel     -0.11339731  0.094055728
## freetime    0.14782181  0.075733357
## goout       0.42038575 -0.009577254
## Dalc        0.64754423  0.077179582
## Walc        1.00000000  0.092476317
## health      0.09247632  1.000000000
## absences    0.13629110 -0.029936711
## G1         -0.12617921 -0.073172073
## G2         -0.08492735 -0.097719866
## G3         -0.05193932 -0.061334605
##               absences          G1
## age         0.17523008 -0.06408150
## Medu        0.10028482  0.20534100
## Fedu        0.02447289  0.19026994
## traveltime -0.01294378 -0.09303999
## studytime  -0.06270018  0.16061192
## failures    0.06372583 -0.35471761
## famrel     -0.04435409  0.02216832
## freetime   -0.05807792  0.01261293
## goout       0.04430222 -0.14910397
## Dalc        0.11190803 -0.09415879
## Walc        0.13629110 -0.12617921
## health     -0.02993671 -0.07317207
## absences    1.00000000 -0.03100290
## G1         -0.03100290  1.00000000
## G2         -0.03177670  0.85211807
## G3          0.03424732  0.80146793
##                     G2          G3
## age        -0.14347405 -0.16157944
## Medu        0.21552717  0.21714750
## Fedu        0.16489339  0.15245694
## traveltime -0.15319796 -0.11714205
## studytime   0.13588000  0.09781969
## failures   -0.35589563 -0.36041494
## famrel     -0.01828135  0.05136343
## freetime   -0.01377714  0.01130724
## goout      -0.16225003 -0.13279147
## Dalc       -0.06412018 -0.05466004
## Walc       -0.08492735 -0.05193932
## health     -0.09771987 -0.06133460
## absences   -0.03177670  0.03424732
## G1          0.85211807  0.80146793
## G2          1.00000000  0.90486799
## G3          0.90486799  1.00000000
```

```r
#using corrgram (you directly pass the df)
print(corrgram(df))
```

![plot of chunk unnamed-chunk-42](figure/unnamed-chunk-42-2.png)

```
##                     age         Medu
## age         1.000000000 -0.163658419
## Medu       -0.163658419  1.000000000
## Fedu       -0.163438069  0.623455112
## traveltime  0.070640721 -0.171639305
## studytime  -0.004140037  0.064944137
## failures    0.243665377 -0.236679963
## famrel      0.053940096 -0.003914458
## freetime    0.016434389  0.030890867
## goout       0.126963880  0.064094438
## Dalc        0.131124605  0.019834099
## Walc        0.117276052 -0.047123460
## health     -0.062187369 -0.046877829
## absences    0.175230079  0.100284818
## G1         -0.064081497  0.205340997
## G2         -0.143474049  0.215527168
## G3         -0.161579438  0.217147496
##                    Fedu   traveltime
## age        -0.163438069  0.070640721
## Medu        0.623455112 -0.171639305
## Fedu        1.000000000 -0.158194054
## traveltime -0.158194054  1.000000000
## studytime  -0.009174639 -0.100909119
## failures   -0.250408444  0.092238746
## famrel     -0.001369727 -0.016807986
## freetime   -0.012845528 -0.017024944
## goout       0.043104668  0.028539674
## Dalc        0.002386429  0.138325309
## Walc       -0.012631018  0.134115752
## health      0.014741537  0.007500606
## absences    0.024472887 -0.012943775
## G1          0.190269936 -0.093039992
## G2          0.164893393 -0.153197963
## G3          0.152456939 -0.117142053
##               studytime    failures
## age        -0.004140037  0.24366538
## Medu        0.064944137 -0.23667996
## Fedu       -0.009174639 -0.25040844
## traveltime -0.100909119  0.09223875
## studytime   1.000000000 -0.17356303
## failures   -0.173563031  1.00000000
## famrel      0.039730704 -0.04433663
## freetime   -0.143198407  0.09198747
## goout      -0.063903675  0.12456092
## Dalc       -0.196019263  0.13604693
## Walc       -0.253784731  0.14196203
## health     -0.075615863  0.06582728
## absences   -0.062700175  0.06372583
## G1          0.160611915 -0.35471761
## G2          0.135879999 -0.35589563
## G3          0.097819690 -0.36041494
##                  famrel    freetime
## age         0.053940096  0.01643439
## Medu       -0.003914458  0.03089087
## Fedu       -0.001369727 -0.01284553
## traveltime -0.016807986 -0.01702494
## studytime   0.039730704 -0.14319841
## failures   -0.044336626  0.09198747
## famrel      1.000000000  0.15070144
## freetime    0.150701444  1.00000000
## goout       0.064568411  0.28501871
## Dalc       -0.077594357  0.20900085
## Walc       -0.113397308  0.14782181
## health      0.094055728  0.07573336
## absences   -0.044354095 -0.05807792
## G1          0.022168316  0.01261293
## G2         -0.018281347 -0.01377714
## G3          0.051363429  0.01130724
##                   goout         Dalc
## age         0.126963880  0.131124605
## Medu        0.064094438  0.019834099
## Fedu        0.043104668  0.002386429
## traveltime  0.028539674  0.138325309
## studytime  -0.063903675 -0.196019263
## failures    0.124560922  0.136046931
## famrel      0.064568411 -0.077594357
## freetime    0.285018715  0.209000848
## goout       1.000000000  0.266993848
## Dalc        0.266993848  1.000000000
## Walc        0.420385745  0.647544230
## health     -0.009577254  0.077179582
## absences    0.044302220  0.111908026
## G1         -0.149103967 -0.094158792
## G2         -0.162250034 -0.064120183
## G3         -0.132791474 -0.054660041
##                   Walc       health
## age         0.11727605 -0.062187369
## Medu       -0.04712346 -0.046877829
## Fedu       -0.01263102  0.014741537
## traveltime  0.13411575  0.007500606
## studytime  -0.25378473 -0.075615863
## failures    0.14196203  0.065827282
## famrel     -0.11339731  0.094055728
## freetime    0.14782181  0.075733357
## goout       0.42038575 -0.009577254
## Dalc        0.64754423  0.077179582
## Walc        1.00000000  0.092476317
## health      0.09247632  1.000000000
## absences    0.13629110 -0.029936711
## G1         -0.12617921 -0.073172073
## G2         -0.08492735 -0.097719866
## G3         -0.05193932 -0.061334605
##               absences          G1
## age         0.17523008 -0.06408150
## Medu        0.10028482  0.20534100
## Fedu        0.02447289  0.19026994
## traveltime -0.01294378 -0.09303999
## studytime  -0.06270018  0.16061192
## failures    0.06372583 -0.35471761
## famrel     -0.04435409  0.02216832
## freetime   -0.05807792  0.01261293
## goout       0.04430222 -0.14910397
## Dalc        0.11190803 -0.09415879
## Walc        0.13629110 -0.12617921
## health     -0.02993671 -0.07317207
## absences    1.00000000 -0.03100290
## G1         -0.03100290  1.00000000
## G2         -0.03177670  0.85211807
## G3          0.03424732  0.80146793
##                     G2          G3
## age        -0.14347405 -0.16157944
## Medu        0.21552717  0.21714750
## Fedu        0.16489339  0.15245694
## traveltime -0.15319796 -0.11714205
## studytime   0.13588000  0.09781969
## failures   -0.35589563 -0.36041494
## famrel     -0.01828135  0.05136343
## freetime   -0.01377714  0.01130724
## goout      -0.16225003 -0.13279147
## Dalc       -0.06412018 -0.05466004
## Walc       -0.08492735 -0.05193932
## health     -0.09771987 -0.06133460
## absences   -0.03177670  0.03424732
## G1          0.85211807  0.80146793
## G2          1.00000000  0.90486799
## G3          0.90486799  1.00000000
```

```r
corrgram(df,order=TRUE,lower.panel = panel.shade,upper.panel = panel.pie,text.panel = panel.txt)
```

![plot of chunk unnamed-chunk-42](figure/unnamed-chunk-42-3.png)
Red = negative correlation
Blue = positive correlation

5. Let's plot

```r
ggplot(df,aes(x=G3)) + geom_histogram(bins=20,alpha=0.5,fill="blue")
```

![plot of chunk unnamed-chunk-43](figure/unnamed-chunk-43-1.png)

# Part 2 - Linear Regression
6. We randomly split the data into training set and testing set

```r
library(caTools)
# set a seed
set.seed(101) #we do it specifically to have the same random splits as the instructor

# Split up the sample
sample <- sample.split(df$G3, SplitRatio = 0.7) #Split ratio is the % of data that we'll use as TRAINING data

# 70% of my data in sample column has the value of TRUE
train <- subset(df, sample == TRUE)
# 30% of my data has the value of FALSE
test <- subset(df, sample == FALSE)
```
7. Train our model

```r
# the general model of building a linear regression model in R looks like this:

#model <- lm(y ~ x1 + x2, data) # to use only the features x1 and x2 of your df

#model <- lm(y ~ ., data) #it uses all the features in our df
```

```r
# Training OUR model
model <- lm(G3 ~ ., data = train)

#Running our model

#Interpreting our model
print(summary(model))
```

```
## 
## Call:
## lm(formula = G3 ~ ., data = train)
## 
## Residuals:
##     Min      1Q  Median      3Q 
## -7.4250 -0.6478  0.2844  1.0442 
##     Max 
##  4.9840 
## 
## Coefficients:
##                  Estimate Std. Error
## (Intercept)       3.70763    2.69488
## schoolMS          0.66981    0.47436
## sexM              0.25730    0.29257
## age              -0.36163    0.12949
## addressU          0.08123    0.35652
## famsizeLE3        0.12222    0.28709
## PstatusT          0.06807    0.43032
## Medu              0.11100    0.18757
## Fedu             -0.16373    0.15928
## Mjobhealth       -0.63993    0.65314
## Mjobother        -0.15730    0.42323
## Mjobservices     -0.15872    0.46682
## Mjobteacher      -0.04930    0.62335
## Fjobhealth        0.17565    0.83034
## Fjobother        -0.29559    0.56012
## Fjobservices     -0.76964    0.59476
## Fjobteacher      -0.27009    0.73824
## reasonhome       -0.41126    0.31857
## reasonother       0.06767    0.45323
## reasonreputation  0.13478    0.34735
## guardianmother   -0.05442    0.31663
## guardianother     0.01588    0.58375
## traveltime       -0.02353    0.19540
## studytime        -0.04294    0.16910
## failures         -0.17219    0.19668
## schoolsupyes      0.20742    0.42358
## famsupyes        -0.05329    0.27753
## paidyes           0.31311    0.28284
## activitiesyes    -0.26104    0.26687
## nurseryyes       -0.05345    0.31236
## higheryes        -0.94298    0.74005
## internetyes      -0.15834    0.37029
## romanticyes      -0.30048    0.28115
## famrel            0.36601    0.14609
## freetime          0.08386    0.14247
## goout            -0.12457    0.13306
## Dalc             -0.16995    0.20659
## Walc              0.21053    0.14963
## health            0.07805    0.09341
## absences          0.09547    0.02382
## G1                0.14259    0.07892
## G2                0.98859    0.06929
##                  t value Pr(>|t|)    
## (Intercept)        1.376  0.17019    
## schoolMS           1.412  0.15926    
## sexM               0.879  0.38006    
## age               -2.793  0.00566 ** 
## addressU           0.228  0.81996    
## famsizeLE3         0.426  0.67070    
## PstatusT           0.158  0.87444    
## Medu               0.592  0.55455    
## Fedu              -1.028  0.30503    
## Mjobhealth        -0.980  0.32820    
## Mjobother         -0.372  0.71048    
## Mjobservices      -0.340  0.73415    
## Mjobteacher       -0.079  0.93702    
## Fjobhealth         0.212  0.83265    
## Fjobother         -0.528  0.59818    
## Fjobservices      -1.294  0.19692    
## Fjobteacher       -0.366  0.71480    
## reasonhome        -1.291  0.19799    
## reasonother        0.149  0.88144    
## reasonreputation   0.388  0.69834    
## guardianmother    -0.172  0.86369    
## guardianother      0.027  0.97832    
## traveltime        -0.120  0.90427    
## studytime         -0.254  0.79979    
## failures          -0.875  0.38220    
## schoolsupyes       0.490  0.62481    
## famsupyes         -0.192  0.84789    
## paidyes            1.107  0.26941    
## activitiesyes     -0.978  0.32901    
## nurseryyes        -0.171  0.86428    
## higheryes         -1.274  0.20385    
## internetyes       -0.428  0.66932    
## romanticyes       -1.069  0.28627    
## famrel             2.505  0.01291 *  
## freetime           0.589  0.55668    
## goout             -0.936  0.35015    
## Dalc              -0.823  0.41153    
## Walc               1.407  0.16074    
## health             0.836  0.40426    
## absences           4.008 8.24e-05 ***
## G1                 1.807  0.07206 .  
## G2                14.267  < 2e-16 ***
## ---
## Signif. codes:  
##   0 '***' 0.001 '**' 0.01 '*' 0.05
##   '.' 0.1 ' ' 1
## 
## Residual standard error: 1.962 on 235 degrees of freedom
## Multiple R-squared:  0.8456,	Adjusted R-squared:  0.8187 
## F-statistic: 31.39 on 41 and 235 DF,  p-value: < 2.2e-16
```

- Call: tells you which model you used  
- Residuals: the difference of the actual values in the column you're predicting and the values of your linear regression prediction  
- Coefficients:
-   Estimate: the value of slope calculated by the regression  
-   Std. Error: Lower is better, preferably lower than the value of the Estimate  
-  t value: scores that measures if the variable is significant to the model (used to calculate *P value* and *Significance level*). The more stars (***) = more significance level.
-  Pr(>|t|): probability that the variable is NOT RELEVANT (we want it to be as small as possible)  
- R squared value: the higher the better, it corresponds to the variability of the model and the fit of your model, 1 is the ideal value  

8. Plotting the residuals

```r
res <- residuals(model)
class(res)
```

```
## [1] "numeric"
```

```r
res <- as.data.frame(res)
head(res)
```

```
##           res
## 1   1.4684389
## 2   1.8826707
## 3   1.1866990
## 6  -2.2440152
## 9   0.5974865
## 11  0.8583062
```

```r
ggplot(res, aes(res)) + geom_histogram(fill="blue")
```

```
## `stat_bin()` using `bins = 30`. Pick
## better value with `binwidth`.
```

![plot of chunk unnamed-chunk-47](figure/unnamed-chunk-47-1.png)

```r
#We want a NORMAL DISTRIBUTION with a median in 0, that means that the difference between the real mean value and our model's mean value is 0
```

# Part 3: Linear Regression with R

```r
plot(model) #we get 4 plots out of the data of our model
```

![plot of chunk unnamed-chunk-48](figure/unnamed-chunk-48-1.png)![plot of chunk unnamed-chunk-48](figure/unnamed-chunk-48-2.png)![plot of chunk unnamed-chunk-48](figure/unnamed-chunk-48-3.png)![plot of chunk unnamed-chunk-48](figure/unnamed-chunk-48-4.png)
 9. Predicting values with our model previously trained

```r
G3.predictions <- predict(model, test) #we input the testing data to make predictions with the same format

#we create a dataframe with 2 columns, the predictions and the actual values
results <- cbind(G3.predictions,test$G3)
colnames(results) <- c("predicted","actual")

print(head(results))
```

```
##    predicted actual
## 4  12.682507     15
## 5   9.433677     10
## 7  11.312310     11
## 8   3.101530      6
## 10 15.564674     15
## 13 14.190360     14
```

```r
results <- as.data.frame(results)            
```
 
10. Let's take care of the negative values predicted, as we don't want negative values

```r
to_zero <- function(x){
  if (x<0){
    return(0)
  }else{
    return(x)
  }
}

# Apply zero function to the predicted values of our model
results$predicted <- sapply(results$predicted, to_zero)

#to make sure how off we are with the predictions we find the:
#Mean squared error
mse <- mean((results$actual - results$predicted)^2)
#Root mean squared error
rmse <- mse^0.5

print(c("MSE: ",mse))
```

```
## [1] "MSE: "           
## [2] "3.99167460059075"
```

```r
print(c("RMSE: ",rmse))
```

```
## [1] "RMSE: "          
## [2] "1.99791756601486"
```

```r
# R squared value to find the fit of our model values
SSE <- sum((results$predicted - results$actual)^2) #sum of squared errors
SST <- sum((mean(df$G3)-results$actual)^2) #sum of squared total

R2 <- 1 - SSE/SST #R squared value (the ideal is 1)

print(c("R squared value: ",R2))
```

```
## [1] "R squared value: "
## [2] "0.804447675832027"
```

