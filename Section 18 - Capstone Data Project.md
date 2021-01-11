---
title: "Section 18 - Capstone Data Project"
author: "Victoria"
date: "10/1/2021"
output: html_document
---



#**MoneyBall Project**
Use R to open the Batting.csv file and assign it to a dataframe called batting using read.csv

```r
batting <- read.csv("Batting.csv")
head(batting)
```

```
##    playerID yearID stint teamID lgID  G G_batting AB R H X2B X3B HR RBI SB CS BB SO
## 1 aardsda01   2004     1    SFN   NL 11        11  0 0 0   0   0  0   0  0  0  0  0
## 2 aardsda01   2006     1    CHN   NL 45        43  2 0 0   0   0  0   0  0  0  0  0
## 3 aardsda01   2007     1    CHA   AL 25         2  0 0 0   0   0  0   0  0  0  0  0
## 4 aardsda01   2008     1    BOS   AL 47         5  1 0 0   0   0  0   0  0  0  0  1
## 5 aardsda01   2009     1    SEA   AL 73         3  0 0 0   0   0  0   0  0  0  0  0
## 6 aardsda01   2010     1    SEA   AL 53         4  0 0 0   0   0  0   0  0  0  0  0
##   IBB HBP SH SF GIDP G_old
## 1   0   0  0  0    0    11
## 2   0   0  1  0    0    45
## 3   0   0  0  0    0     2
## 4   0   0  0  0    0     5
## 5   0   0  0  0    0    NA
## 6   0   0  0  0    0    NA
```

```r
str(batting)
```

```
## 'data.frame':	97889 obs. of  24 variables:
##  $ playerID : chr  "aardsda01" "aardsda01" "aardsda01" "aardsda01" ...
##  $ yearID   : int  2004 2006 2007 2008 2009 2010 2012 1954 1955 1956 ...
##  $ stint    : int  1 1 1 1 1 1 1 1 1 1 ...
##  $ teamID   : chr  "SFN" "CHN" "CHA" "BOS" ...
##  $ lgID     : chr  "NL" "NL" "AL" "AL" ...
##  $ G        : int  11 45 25 47 73 53 1 122 153 153 ...
##  $ G_batting: int  11 43 2 5 3 4 NA 122 153 153 ...
##  $ AB       : int  0 2 0 1 0 0 NA 468 602 609 ...
##  $ R        : int  0 0 0 0 0 0 NA 58 105 106 ...
##  $ H        : int  0 0 0 0 0 0 NA 131 189 200 ...
##  $ X2B      : int  0 0 0 0 0 0 NA 27 37 34 ...
##  $ X3B      : int  0 0 0 0 0 0 NA 6 9 14 ...
##  $ HR       : int  0 0 0 0 0 0 NA 13 27 26 ...
##  $ RBI      : int  0 0 0 0 0 0 NA 69 106 92 ...
##  $ SB       : int  0 0 0 0 0 0 NA 2 3 2 ...
##  $ CS       : int  0 0 0 0 0 0 NA 2 1 4 ...
##  $ BB       : int  0 0 0 0 0 0 NA 28 49 37 ...
##  $ SO       : int  0 0 0 1 0 0 NA 39 61 54 ...
##  $ IBB      : int  0 0 0 0 0 0 NA NA 5 6 ...
##  $ HBP      : int  0 0 0 0 0 0 NA 3 3 2 ...
##  $ SH       : int  0 1 0 0 0 0 NA 6 7 5 ...
##  $ SF       : int  0 0 0 0 0 0 NA 4 4 7 ...
##  $ GIDP     : int  0 0 0 0 0 0 NA 13 20 21 ...
##  $ G_old    : int  11 45 2 5 NA NA NA 122 153 153 ...
```
Call the head() of the first five rows of AB (At Bats) column

```r
head(batting$AB)
```

```
## [1] 0 2 0 1 0 0
```
Call the head of the doubles (X2B) column

```r
head(batting$X2B)
```

```
## [1] 0 0 0 0 0 0
```
Which means that the Batting Average is equal to H (Hits) divided by AB (At Base). So we'll do the following to create a new column called BA and add it to our data frame:

```r
batting$BA <- batting$H / batting$AB #new column of batting average
```
After doing this operation, check the last 5 entries of the BA column of your data frame and it should look like this:

```r
tail(batting$BA)
```

```
## [1] 0.0000000 0.1230769 0.2746479 0.1470588 0.2745098 0.2138728
```
Now do the same for some new columns! On Base Percentage (OBP) and Slugging Percentage (SLG). Hint: For SLG, you need 1B (Singles), this isn't in your data frame. However you can calculate it by subtracting doubles,triples, and home runs from total hits (H): 1B = H-2B-3B-HR

Create an OBP Column

```r
batting$OBP <- (batting$H + batting$BB + batting$HBP)/(batting$AB + batting$BB + batting$HBP + batting$SF)

tail(batting$OBP)
```

```
## [1] 0.0000000 0.1343284 0.3443918 0.1470588 0.3543759 0.2901554
```

For SLG, you need 1B (Singles), this isn't in your data frame. However you can calculate it by subtracting doubles,triples, and home runs from total hits (H): 1B = H-2B-3B-HR

```r
batting$X1B <- batting$H - batting$X2B - batting$X3B - batting$HR

tail(batting$X1B)
```

```
## [1]   0   7 102   5 117  27
```


Create an SLG Column

```r
batting$SLG <- (batting$X1B + (2*batting$X2B) + (3*batting$X3B) + (4*batting$HR)) / batting$AB

tail(batting$AB)
```

```
## [1]   2  65 568  34 612 173
```

Check the structure of your data frame using str()

```r
str(batting)
```

```
## 'data.frame':	97889 obs. of  28 variables:
##  $ playerID : chr  "aardsda01" "aardsda01" "aardsda01" "aardsda01" ...
##  $ yearID   : int  2004 2006 2007 2008 2009 2010 2012 1954 1955 1956 ...
##  $ stint    : int  1 1 1 1 1 1 1 1 1 1 ...
##  $ teamID   : chr  "SFN" "CHN" "CHA" "BOS" ...
##  $ lgID     : chr  "NL" "NL" "AL" "AL" ...
##  $ G        : int  11 45 25 47 73 53 1 122 153 153 ...
##  $ G_batting: int  11 43 2 5 3 4 NA 122 153 153 ...
##  $ AB       : int  0 2 0 1 0 0 NA 468 602 609 ...
##  $ R        : int  0 0 0 0 0 0 NA 58 105 106 ...
##  $ H        : int  0 0 0 0 0 0 NA 131 189 200 ...
##  $ X2B      : int  0 0 0 0 0 0 NA 27 37 34 ...
##  $ X3B      : int  0 0 0 0 0 0 NA 6 9 14 ...
##  $ HR       : int  0 0 0 0 0 0 NA 13 27 26 ...
##  $ RBI      : int  0 0 0 0 0 0 NA 69 106 92 ...
##  $ SB       : int  0 0 0 0 0 0 NA 2 3 2 ...
##  $ CS       : int  0 0 0 0 0 0 NA 2 1 4 ...
##  $ BB       : int  0 0 0 0 0 0 NA 28 49 37 ...
##  $ SO       : int  0 0 0 1 0 0 NA 39 61 54 ...
##  $ IBB      : int  0 0 0 0 0 0 NA NA 5 6 ...
##  $ HBP      : int  0 0 0 0 0 0 NA 3 3 2 ...
##  $ SH       : int  0 1 0 0 0 0 NA 6 7 5 ...
##  $ SF       : int  0 0 0 0 0 0 NA 4 4 7 ...
##  $ GIDP     : int  0 0 0 0 0 0 NA 13 20 21 ...
##  $ G_old    : int  11 45 2 5 NA NA NA 122 153 153 ...
##  $ BA       : num  NaN 0 NaN 0 NaN ...
##  $ OBP      : num  NaN 0 NaN 0 NaN ...
##  $ X1B      : int  0 0 0 0 0 0 NA 85 116 126 ...
##  $ SLG      : num  NaN 0 NaN 0 NaN ...
```

##**Merging Salary Data with Batting Data**
Load the Salaries.csv file into a dataframe called sal using read.csv

```r
sal <- read.csv("Salaries.csv")

combo <- merge(batting,sal,by=c("playerID","yearID"))
str(combo)
```

```
## 'data.frame':	25397 obs. of  31 variables:
##  $ playerID : chr  "aardsda01" "aardsda01" "aardsda01" "aardsda01" ...
##  $ yearID   : int  2004 2007 2008 2009 2010 2012 1986 1987 1988 1989 ...
##  $ stint    : int  1 1 1 1 1 1 1 1 1 1 ...
##  $ teamID.x : chr  "SFN" "CHA" "BOS" "SEA" ...
##  $ lgID.x   : chr  "NL" "AL" "AL" "AL" ...
##  $ G        : int  11 25 47 73 53 1 66 7 35 49 ...
##  $ G_batting: int  11 2 5 3 4 NA 0 0 0 49 ...
##  $ AB       : int  0 0 1 0 0 NA NA NA NA 5 ...
##  $ R        : int  0 0 0 0 0 NA NA NA NA 0 ...
##  $ H        : int  0 0 0 0 0 NA NA NA NA 0 ...
##  $ X2B      : int  0 0 0 0 0 NA NA NA NA 0 ...
##  $ X3B      : int  0 0 0 0 0 NA NA NA NA 0 ...
##  $ HR       : int  0 0 0 0 0 NA NA NA NA 0 ...
##  $ RBI      : int  0 0 0 0 0 NA NA NA NA 0 ...
##  $ SB       : int  0 0 0 0 0 NA NA NA NA 0 ...
##  $ CS       : int  0 0 0 0 0 NA NA NA NA 0 ...
##  $ BB       : int  0 0 0 0 0 NA NA NA NA 0 ...
##  $ SO       : int  0 0 1 0 0 NA NA NA NA 3 ...
##  $ IBB      : int  0 0 0 0 0 NA NA NA NA 0 ...
##  $ HBP      : int  0 0 0 0 0 NA NA NA NA 0 ...
##  $ SH       : int  0 0 0 0 0 NA NA NA NA 0 ...
##  $ SF       : int  0 0 0 0 0 NA NA NA NA 0 ...
##  $ GIDP     : int  0 0 0 0 0 NA NA NA NA 0 ...
##  $ G_old    : int  11 2 5 NA NA NA 66 7 35 49 ...
##  $ BA       : num  NaN NaN 0 NaN NaN NA NA NA NA 0 ...
##  $ OBP      : num  NaN NaN 0 NaN NaN NA NA NA NA 0 ...
##  $ X1B      : int  0 0 0 0 0 NA NA NA NA 0 ...
##  $ SLG      : num  NaN NaN 0 NaN NaN NA NA NA NA 0 ...
##  $ teamID.y : chr  "SFN" "CHA" "BOS" "SEA" ...
##  $ lgID.y   : chr  "NL" "AL" "AL" "AL" ...
##  $ salary   : int  300000 387500 403250 419000 2750000 500000 600000 625000 675000 400000 ...
```

Use summary to get a summary of the batting data frame and notice the minimum year in the yearID column. Our batting data goes back to 1871! Our salary data starts at 1985, meaning we need to remove the batting data that occured before 1985.

Use subset() to reassign batting to only contain data from 1985 and onwards

```r
summary(sal)
```

```
##      yearID        teamID              lgID             playerID        
##  Min.   :1985   Length:23956       Length:23956       Length:23956      
##  1st Qu.:1993   Class :character   Class :character   Class :character  
##  Median :1999   Mode  :character   Mode  :character   Mode  :character  
##  Mean   :1999                                                           
##  3rd Qu.:2006                                                           
##  Max.   :2013                                                           
##      salary        
##  Min.   :       0  
##  1st Qu.:  250000  
##  Median :  507950  
##  Mean   : 1864357  
##  3rd Qu.: 2100000  
##  Max.   :33000000
```

```r
str(sal)
```

```
## 'data.frame':	23956 obs. of  5 variables:
##  $ yearID  : int  1985 1985 1985 1985 1985 1985 1985 1985 1985 1985 ...
##  $ teamID  : chr  "BAL" "BAL" "BAL" "BAL" ...
##  $ lgID    : chr  "AL" "AL" "AL" "AL" ...
##  $ playerID: chr  "murraed02" "lynnfr01" "ripkeca01" "lacyle01" ...
##  $ salary  : int  1472819 1090000 800000 725000 641667 625000 581250 560000 558333 547143 ...
```

```r
sal.filtered <- subset(sal,subset = yearID >= 1985)

summary(sal.filtered)
```

```
##      yearID        teamID              lgID             playerID        
##  Min.   :1985   Length:23956       Length:23956       Length:23956      
##  1st Qu.:1993   Class :character   Class :character   Class :character  
##  Median :1999   Mode  :character   Mode  :character   Mode  :character  
##  Mean   :1999                                                           
##  3rd Qu.:2006                                                           
##  Max.   :2013                                                           
##      salary        
##  Min.   :       0  
##  1st Qu.:  250000  
##  Median :  507950  
##  Mean   : 1864357  
##  3rd Qu.: 2100000  
##  Max.   :33000000
```

```r
str(sal.filtered)
```

```
## 'data.frame':	23956 obs. of  5 variables:
##  $ yearID  : int  1985 1985 1985 1985 1985 1985 1985 1985 1985 1985 ...
##  $ teamID  : chr  "BAL" "BAL" "BAL" "BAL" ...
##  $ lgID    : chr  "AL" "AL" "AL" "AL" ...
##  $ playerID: chr  "murraed02" "lynnfr01" "ripkeca01" "lacyle01" ...
##  $ salary  : int  1472819 1090000 800000 725000 641667 625000 581250 560000 558333 547143 ...
```

#**Analyzing the Lost Players**
As previously mentioned, the Oakland A's lost 3 key players during the off-season. We'll want to get their stats to see what we have to replace. The players lost were: first baseman 2000 AL MVP Jason Giambi (giambja01) to the New York Yankees, outfielder Johnny Damon (damonjo01) to the Boston Red Sox and infielder Rainer Gustavo "Ray" Olmedo ('saenzol01').

Use the subset() function to get a data frame called lost_players from the combo data frame consisting of those 3 players. Hint: Try to figure out how to use %in% to avoid a bunch of or statements!

```r
library(dplyr)
lost_players_vec <- c("giambja01","damonjo01","saenzol01") #these are the playerID values of the lost players

lost_players <- subset(batting, batting$playerID %in% lost_players_vec) #we get a df of only those 3 lost players

print(lost_players)
```

```
##        playerID yearID stint teamID lgID   G G_batting  AB   R   H X2B X3B HR RBI SB
## 19740 damonjo01   1995     1    KCA   AL  47        47 188  32  53  11   5  3  23  7
## 19741 damonjo01   1996     1    KCA   AL 145       145 517  61 140  22   5  6  50 25
## 19742 damonjo01   1997     1    KCA   AL 146       146 472  70 130  12   8  8  48 16
## 19743 damonjo01   1998     1    KCA   AL 161       161 642 104 178  30  10 18  66 26
## 19744 damonjo01   1999     1    KCA   AL 145       145 583 101 179  39   9 14  77 36
## 19745 damonjo01   2000     1    KCA   AL 159       159 655 136 214  42  10 16  88 46
## 19746 damonjo01   2001     1    OAK   AL 155       155 644 108 165  34   4  9  49 27
## 19747 damonjo01   2002     1    BOS   AL 154       154 623 118 178  34  11 14  63 31
## 19748 damonjo01   2003     1    BOS   AL 145       145 608 103 166  32   6 12  67 30
## 19749 damonjo01   2004     1    BOS   AL 150       150 621 123 189  35   6 20  94 19
## 19750 damonjo01   2005     1    BOS   AL 148       148 624 117 197  35   6 10  75 18
## 19751 damonjo01   2006     1    NYA   AL 149       149 593 115 169  35   5 24  80 25
## 19752 damonjo01   2007     1    NYA   AL 141       141 533  93 144  27   2 12  63 27
## 19753 damonjo01   2008     1    NYA   AL 143       143 555  95 168  27   5 17  71 29
## 19754 damonjo01   2009     1    NYA   AL 143       143 550 107 155  36   3 24  82 12
## 19755 damonjo01   2010     1    DET   AL 145       145 539  81 146  36   5  8  51 11
## 19756 damonjo01   2011     1    TBA   AL 150       150 582  79 152  29   7 16  73 19
## 19757 damonjo01   2012     1    CLE   AL  64        NA 207  25  46   6   2  4  19  4
## 30720 giambja01   1995     1    OAK   AL  54        54 176  27  45   7   0  6  25  2
## 30721 giambja01   1996     1    OAK   AL 140       140 536  84 156  40   1 20  79  0
## 30722 giambja01   1997     1    OAK   AL 142       142 519  66 152  41   2 20  81  0
## 30723 giambja01   1998     1    OAK   AL 153       153 562  92 166  28   0 27 110  2
## 30724 giambja01   1999     1    OAK   AL 158       158 575 115 181  36   1 33 123  1
## 30725 giambja01   2000     1    OAK   AL 152       152 510 108 170  29   1 43 137  2
## 30726 giambja01   2001     1    OAK   AL 154       154 520 109 178  47   2 38 120  2
## 30727 giambja01   2002     1    NYA   AL 155       155 560 120 176  34   1 41 122  2
## 30728 giambja01   2003     1    NYA   AL 156       156 535  97 134  25   0 41 107  2
## 30729 giambja01   2004     1    NYA   AL  80        80 264  33  55   9   0 12  40  0
## 30730 giambja01   2005     1    NYA   AL 139       139 417  74 113  14   0 32  87  0
## 30731 giambja01   2006     1    NYA   AL 139       139 446  92 113  25   0 37 113  2
## 30732 giambja01   2007     1    NYA   AL  83        83 254  31  60   8   0 14  39  1
## 30733 giambja01   2008     1    NYA   AL 145       145 458  68 113  19   1 32  96  2
## 30734 giambja01   2009     1    OAK   AL  83        83 269  39  52  13   0 11  40  0
## 30735 giambja01   2009     2    COL   NL  19        19  24   4   7   1   0  2  11  0
## 30736 giambja01   2010     1    COL   NL  87        87 176  17  43   9   0  6  35  2
##       CS  BB  SO IBB HBP SH SF GIDP G_old        BA       OBP X1B       SLG
## 19740  0  12  22   0   1  2  3    2    47 0.2819149 0.3235294  34 0.4414894
## 19741  5  31  64   3   3 10  5    4   145 0.2707930 0.3129496 107 0.3675048
## 19742 10  42  70   2   3  6  1    3   146 0.2754237 0.3378378 102 0.3855932
## 19743 12  58  84   4   4  3  3    4   161 0.2772586 0.3394625 120 0.4392523
## 19744  6  67  50   5   3  3  4   13   145 0.3070326 0.3789954 117 0.4768439
## 19745  9  65  60   4   1  8 12    7   159 0.3267176 0.3819918 146 0.4946565
## 19746 12  61  70   1   5  5  4    7   155 0.2562112 0.3235294 118 0.3633540
## 19747  6  65  70   5   6  3  5    4   154 0.2857143 0.3562232 119 0.4430177
## 19748  6  68  74   4   2  6  6    5   145 0.2730263 0.3450292 116 0.4046053
## 19749  8  76  71   1   2  0  3    8   150 0.3043478 0.3803419 128 0.4766506
## 19750  1  53  69   3   2  0  9    5   148 0.3157051 0.3662791 146 0.4391026
## 19751 10  67  85   1   4  2  5    4   149 0.2849916 0.3587444 105 0.4822934
## 19752  3  66  79   1   2  1  3    4   141 0.2701689 0.3509934 103 0.3958724
## 19753  8  64  82   0   1  2  1    5   143 0.3027027 0.3752013 119 0.4612613
## 19754  0  71  98   1   2  2  1    9    NA 0.2818182 0.3653846  92 0.4890909
## 19755  1  69  90   2   2  2  1    5    NA 0.2708720 0.3551555  97 0.4007421
## 19756  6  51  92   1   7  2  5    4   150 0.2611684 0.3255814 100 0.4175258
## 19757  0  17  27   0   0  0  0    0    NA 0.2222222 0.2812500  34 0.3285024
## 30720  1  28  31   0   3  1  2    4    54 0.2556818 0.3636364  32 0.3977273
## 30721  1  51  95   3   5  1  5   15   140 0.2910448 0.3551089  95 0.4813433
## 30722  1  55  89   3   6  0  8   11   142 0.2928709 0.3622449  89 0.4951830
## 30723  2  81 102   7   5  0  9   16   153 0.2953737 0.3835616 111 0.4893238
## 30724  1 105 106   6   7  0  8   11   158 0.3147826 0.4215827 111 0.5530435
## 30725  0 137  96   6   9  0  8    9   152 0.3333333 0.4759036  97 0.6470588
## 30726  0 129  83  24  13  0  9   17   154 0.3423077 0.4769001  91 0.6596154
## 30727  2 109 112   4  15  0  5   18   155 0.3142857 0.4354136 100 0.5982143
## 30728  1 129 140   9  21  0  5    9   156 0.2504673 0.4115942  68 0.5271028
## 30729  1  47  62   1   8  0  3    5    80 0.2083333 0.3416149  34 0.3787879
## 30730  0 108 109   5  19  0  1    7   139 0.2709832 0.4403670  67 0.5347722
## 30731  0 110 106  12  16  0  7   10   139 0.2533632 0.4127807  51 0.5582960
## 30732  0  40  66   2   8  0  1    1    83 0.2362205 0.3564356  38 0.4330709
## 30733  1  76 111   5  22  0  9    6   145 0.2467249 0.3734513  61 0.5021834
## 30734  0  50  72   1   7  0  2    6    NA 0.1933086 0.3323171  28 0.3643123
## 30735  0   7   8   0   0  0  0    0    NA 0.2916667 0.4516129   4 0.5833333
## 30736  0  35  47   5   6  0  5    5    NA 0.2443182 0.3783784  28 0.3977273
##  [ reached 'max' / getOption("max.print") -- omitted 12 rows ]
```
Since all these players were lost in after 2001 in the offseason, let's only concern ourselves with the data from 2001.

Use subset again to only grab the rows where the yearID was 2001.

```r
lost_players_2001 <- subset(lost_players, lost_players$yearID == 2001)
print(lost_players_2001)
```

```
##        playerID yearID stint teamID lgID   G G_batting  AB   R   H X2B X3B HR RBI SB
## 19746 damonjo01   2001     1    OAK   AL 155       155 644 108 165  34   4  9  49 27
## 30726 giambja01   2001     1    OAK   AL 154       154 520 109 178  47   2 38 120  2
## 76246 saenzol01   2001     1    OAK   AL 106       106 305  33  67  21   1  9  32  0
##       CS  BB SO IBB HBP SH SF GIDP G_old        BA       OBP X1B       SLG
## 19746 12  61 70   1   5  5  4    7   155 0.2562112 0.3235294 118 0.3633540
## 30726  0 129 83  24  13  0  9   17   154 0.3423077 0.4769001  91 0.6596154
## 76246  1  19 64   1  13  1  3    9   106 0.2196721 0.2911765  36 0.3836066
```

Reduce the lost_players data frame to the following columns: playerID,H,X2B,X3B,HR,OBP,SLG,BA,AB

```r
lost_players <- lost_players_2001[,c("playerID","H","X2B","X3B","HR","OBP","SLG","BA","AB")]
print(lost_players)
```

```
##        playerID   H X2B X3B HR       OBP       SLG        BA  AB
## 19746 damonjo01 165  34   4  9 0.3235294 0.3633540 0.2562112 644
## 30726 giambja01 178  47   2 38 0.4769001 0.6596154 0.3423077 520
## 76246 saenzol01  67  21   1  9 0.2911765 0.3836066 0.2196721 305
```

#**Replacement Players**
Now we have all the information we need! Here is your final task - Find Replacement Players for the key three players we lost! However, you have three constraints:

- The total combined salary of the three players can not exceed 15 million dollars.  
- Their combined number of At Bats (AB) needs to be equal to or greater than the lost players.  
- Their mean OBP had to equal to or greater than the mean OBP of the lost players.  

```r
library(ggplot2)
combo <- subset(combo, yearID == 2001)
ggplot(combo, aes(x=OBP,y=salary)) + geom_point(size=2)
```

```
## Warning: Removed 168 rows containing missing values (geom_point).
```

![plot of chunk unnamed-chunk-83](figure/unnamed-chunk-83-1.png)

```r
combo <- subset(combo,salary<8000000 & OBP>0)
ggplot(combo, aes(x=OBP,y=salary)) + geom_point(size=2)
```

![plot of chunk unnamed-chunk-83](figure/unnamed-chunk-83-2.png)

```r
combo <- subset(combo, AB >= 450)
ggplot(combo, aes(x=OBP,y=salary)) + geom_point(size=2)
```

![plot of chunk unnamed-chunk-83](figure/unnamed-chunk-83-3.png)

```r
combo.ord <- head(arrange(combo, desc(OBP)),10)

combo.ord[,c("playerID","AB","salary","OBP")]
```

```
##     playerID  AB  salary       OBP
## 1  giambja01 520 4103333 0.4769001
## 2  heltoto01 587 4950000 0.4316547
## 3  berkmla01 577  305000 0.4302326
## 4  gonzalu01 609 4833333 0.4285714
## 5  martied01 470 5500000 0.4234079
## 6  thomeji01 526 7875000 0.4161491
## 7  alomaro01 575 7750000 0.4146707
## 8  edmonji01 500 6333333 0.4102142
## 9  gilesbr02 576 7333333 0.4035608
## 10 pujolal01 590  200000 0.4029630
```

