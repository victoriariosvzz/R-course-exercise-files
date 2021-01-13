---
title: "Section 23 - Machine Learning Project - Logistic Regression"
author: "Victoria"
date: "12/1/2021"
output: html_document
---



# **Logistic Regression Project**
In this project we will be working with the UCI adult dataset. We will be attempting to predict if people in the data set belong in a certain class by salary, either making <=50k or >50k per year.

**Typically most of your time is spent cleaning data**, not running the few lines of code that build your model, this project will try to reflect that by showing different issues that may arise when cleaning data.

**Get the Data**
Read in the adult_sal.csv file and set it to a data frame called adult.

```r
adult <- read.csv("adult_sal.csv")

head(adult)
```

```
##   X age    type_employer fnlwgt education
## 1 1  39        State-gov  77516 Bachelors
## 2 2  50 Self-emp-not-inc  83311 Bachelors
## 3 3  38          Private 215646   HS-grad
## 4 4  53          Private 234721      11th
## 5 5  28          Private 338409 Bachelors
## 6 6  37          Private 284582   Masters
##   education_num            marital
## 1            13      Never-married
## 2            13 Married-civ-spouse
## 3             9           Divorced
## 4             7 Married-civ-spouse
## 5            13 Married-civ-spouse
## 6            14 Married-civ-spouse
##          occupation  relationship  race    sex
## 1      Adm-clerical Not-in-family White   Male
## 2   Exec-managerial       Husband White   Male
## 3 Handlers-cleaners Not-in-family White   Male
## 4 Handlers-cleaners       Husband Black   Male
## 5    Prof-specialty          Wife Black Female
## 6   Exec-managerial          Wife White Female
##   capital_gain capital_loss hr_per_week
## 1         2174            0          40
## 2            0            0          13
## 3            0            0          40
## 4            0            0          40
## 5            0            0          40
## 6            0            0          40
##         country income
## 1 United-States  <=50K
## 2 United-States  <=50K
## 3 United-States  <=50K
## 4 United-States  <=50K
## 5          Cuba  <=50K
## 6 United-States  <=50K
```
You should notice the index has been repeated. Drop this column.

```r
library(dplyr)
adult <- select(adult, -X)
```
Check the head,str, and summary of the data now.

```r
head(adult)
```

```
##   age    type_employer fnlwgt education
## 1  39        State-gov  77516 Bachelors
## 2  50 Self-emp-not-inc  83311 Bachelors
## 3  38          Private 215646   HS-grad
## 4  53          Private 234721      11th
## 5  28          Private 338409 Bachelors
## 6  37          Private 284582   Masters
##   education_num            marital
## 1            13      Never-married
## 2            13 Married-civ-spouse
## 3             9           Divorced
## 4             7 Married-civ-spouse
## 5            13 Married-civ-spouse
## 6            14 Married-civ-spouse
##          occupation  relationship  race    sex
## 1      Adm-clerical Not-in-family White   Male
## 2   Exec-managerial       Husband White   Male
## 3 Handlers-cleaners Not-in-family White   Male
## 4 Handlers-cleaners       Husband Black   Male
## 5    Prof-specialty          Wife Black Female
## 6   Exec-managerial          Wife White Female
##   capital_gain capital_loss hr_per_week
## 1         2174            0          40
## 2            0            0          13
## 3            0            0          40
## 4            0            0          40
## 5            0            0          40
## 6            0            0          40
##         country income
## 1 United-States  <=50K
## 2 United-States  <=50K
## 3 United-States  <=50K
## 4 United-States  <=50K
## 5          Cuba  <=50K
## 6 United-States  <=50K
```

```r
str(adult)
```

```
## 'data.frame':	32561 obs. of  15 variables:
##  $ age          : int  39 50 38 53 28 37 49 52 31 42 ...
##  $ type_employer: chr  "State-gov" "Self-emp-not-inc" "Private" "Private" ...
##  $ fnlwgt       : int  77516 83311 215646 234721 338409 284582 160187 209642 45781 159449 ...
##  $ education    : chr  "Bachelors" "Bachelors" "HS-grad" "11th" ...
##  $ education_num: int  13 13 9 7 13 14 5 9 14 13 ...
##  $ marital      : chr  "Never-married" "Married-civ-spouse" "Divorced" "Married-civ-spouse" ...
##  $ occupation   : chr  "Adm-clerical" "Exec-managerial" "Handlers-cleaners" "Handlers-cleaners" ...
##  $ relationship : chr  "Not-in-family" "Husband" "Not-in-family" "Husband" ...
##  $ race         : chr  "White" "White" "White" "Black" ...
##  $ sex          : chr  "Male" "Male" "Male" "Male" ...
##  $ capital_gain : int  2174 0 0 0 0 0 0 0 14084 5178 ...
##  $ capital_loss : int  0 0 0 0 0 0 0 0 0 0 ...
##  $ hr_per_week  : int  40 13 40 40 40 40 16 45 50 40 ...
##  $ country      : chr  "United-States" "United-States" "United-States" "United-States" ...
##  $ income       : chr  "<=50K" "<=50K" "<=50K" "<=50K" ...
```

```r
summary(adult)
```

```
##       age        type_employer     
##  Min.   :17.00   Length:32561      
##  1st Qu.:28.00   Class :character  
##  Median :37.00   Mode  :character  
##  Mean   :38.58                     
##  3rd Qu.:48.00                     
##  Max.   :90.00                     
##      fnlwgt         education        
##  Min.   :  12285   Length:32561      
##  1st Qu.: 117827   Class :character  
##  Median : 178356   Mode  :character  
##  Mean   : 189778                     
##  3rd Qu.: 237051                     
##  Max.   :1484705                     
##  education_num     marital         
##  Min.   : 1.00   Length:32561      
##  1st Qu.: 9.00   Class :character  
##  Median :10.00   Mode  :character  
##  Mean   :10.08                     
##  3rd Qu.:12.00                     
##  Max.   :16.00                     
##   occupation        relationship      
##  Length:32561       Length:32561      
##  Class :character   Class :character  
##  Mode  :character   Mode  :character  
##                                       
##                                       
##                                       
##      race               sex           
##  Length:32561       Length:32561      
##  Class :character   Class :character  
##  Mode  :character   Mode  :character  
##                                       
##                                       
##                                       
##   capital_gain    capital_loss   
##  Min.   :    0   Min.   :   0.0  
##  1st Qu.:    0   1st Qu.:   0.0  
##  Median :    0   Median :   0.0  
##  Mean   : 1078   Mean   :  87.3  
##  3rd Qu.:    0   3rd Qu.:   0.0  
##  Max.   :99999   Max.   :4356.0  
##   hr_per_week      country         
##  Min.   : 1.00   Length:32561      
##  1st Qu.:40.00   Class :character  
##  Median :40.00   Mode  :character  
##  Mean   :40.44                     
##  3rd Qu.:45.00                     
##  Max.   :99.00                     
##     income         
##  Length:32561      
##  Class :character  
##  Mode  :character  
##                    
##                    
## 
```

**Data Cleaning**
Notice that we have a lot of columns that are cateogrical factors, however a lot of these columns have too many factors than may be necessary. In this data cleaning section we'll try to clean these columns up by reducing the number of factors.

*type_employer column*
Use table() to check out the frequency of the type_employer column.

```r
table(adult$type_employer)
```

```
## 
##                ?      Federal-gov 
##             1836              960 
##        Local-gov     Never-worked 
##             2093                7 
##          Private     Self-emp-inc 
##            22696             1116 
## Self-emp-not-inc        State-gov 
##             2541             1298 
##      Without-pay 
##               14
```
How many Null values are there for type_employer? What are the two smallest groups?

```r
null.employed <- subset(adult, type_employer == "?")
count(null.employed) #1836 null values
```

```
##      n
## 1 1836
```

```r
small.groups <- c("Never-worked", "Without-pay")
```

Combine these two smallest groups into a single group called "Unemployed". There are lots of ways to do this, so feel free to get creative. Hint: It may be helpful to convert these objects into character data types (as.character() and then use sapply with a custom function)


```r
class(adult$type_employer)
```

```
## [1] "character"
```

```r
unemp <- function(job){
  job <- as.character(job)
  if (job == "Never-worked" | job=="Without-pay") {
    return("Unemployed")
  }else{
    return(job)
  }
}

adult$type_employer <- sapply(adult$type_employer,unemp) #applying the function

table(adult$type_employer)
```

```
## 
##                ?      Federal-gov 
##             1836              960 
##        Local-gov          Private 
##             2093            22696 
##     Self-emp-inc Self-emp-not-inc 
##             1116             2541 
##        State-gov       Unemployed 
##             1298               21
```
What other columns are suitable for combining? Combine State and Local gov jobs into a category called SL-gov and combine self-employed jobs into a category called self-emp.

```r
fusion <- function(job){
  job <- as.character(job)
  if (job == "State-gov" | job=="Local-gov") {
    return("SL-gov")
  }else if (job == "Self-emp-inc" | job == "Self-emp-not-inc") {
    return("Self-emp")
  }else{
    return(job)
  }
}

adult$type_employer <- sapply(adult$type_employer,fusion) # Applying the function to fuse the categories

table(adult$type_employer)
```

```
## 
##           ? Federal-gov     Private    Self-emp 
##        1836         960       22696        3657 
##      SL-gov  Unemployed 
##        3391          21
```
**Marital Column**
Use table() to look at the marital column

```r
table(adult$marital)
```

```
## 
##              Divorced     Married-AF-spouse 
##                  4443                    23 
##    Married-civ-spouse Married-spouse-absent 
##                 14976                   418 
##         Never-married             Separated 
##                 10683                  1025 
##               Widowed 
##                   993
```

Reduce this to three groups:

Married
Not-Married
Never-Married

```r
marital.st <- function(status){
  status <- as.character(status)
  if (status == "Married-AF-spouse" | status == "Married-civ-spouse" | status == "Married-spouse-absent") {
    return("Married")
  }else if (status == "Never-married") {
    return("Never-Married")
  }else if (status == "Divorced" | status == "Separated" | status == "Widowed") {
    return("Not-Married")
  }
}

adult$marital <- sapply(adult$marital, marital.st)

table(adult$marital)
```

```
## 
##       Married Never-Married   Not-Married 
##         15417         10683          6461
```
**Country Column*
Check the country column using table()

```r
table(adult$country)
```

```
## 
##                          ? 
##                        583 
##                   Cambodia 
##                         19 
##                     Canada 
##                        121 
##                      China 
##                         75 
##                   Columbia 
##                         59 
##                       Cuba 
##                         95 
##         Dominican-Republic 
##                         70 
##                    Ecuador 
##                         28 
##                El-Salvador 
##                        106 
##                    England 
##                         90 
##                     France 
##                         29 
##                    Germany 
##                        137 
##                     Greece 
##                         29 
##                  Guatemala 
##                         64 
##                      Haiti 
##                         44 
##         Holand-Netherlands 
##                          1 
##                   Honduras 
##                         13 
##                       Hong 
##                         20 
##                    Hungary 
##                         13 
##                      India 
##                        100 
##                       Iran 
##                         43 
##                    Ireland 
##                         24 
##                      Italy 
##                         73 
##                    Jamaica 
##                         81 
##                      Japan 
##                         62 
##                       Laos 
##                         18 
##                     Mexico 
##                        643 
##                  Nicaragua 
##                         34 
## Outlying-US(Guam-USVI-etc) 
##                         14 
##                       Peru 
##                         31 
##                Philippines 
##                        198 
##                     Poland 
##                         60 
##                   Portugal 
##                         37 
##                Puerto-Rico 
##                        114 
##                   Scotland 
##                         12 
##                      South 
##                         80 
##                     Taiwan 
##                         51 
##                   Thailand 
##                         18 
##            Trinadad&Tobago 
##                         19 
##              United-States 
##                      29170 
##                    Vietnam 
##                         67 
##                 Yugoslavia 
##                         16
```
We can reduce the countries by grouping them into continents by hand (suggestion)

Check the str() of adult again. Make sure any of the columns we changed have factor levels with factor()

```r
str(adult)
```

```
## 'data.frame':	32561 obs. of  15 variables:
##  $ age          : int  39 50 38 53 28 37 49 52 31 42 ...
##  $ type_employer: chr  "SL-gov" "Self-emp" "Private" "Private" ...
##  $ fnlwgt       : int  77516 83311 215646 234721 338409 284582 160187 209642 45781 159449 ...
##  $ education    : chr  "Bachelors" "Bachelors" "HS-grad" "11th" ...
##  $ education_num: int  13 13 9 7 13 14 5 9 14 13 ...
##  $ marital      : chr  "Never-Married" "Married" "Not-Married" "Married" ...
##  $ occupation   : chr  "Adm-clerical" "Exec-managerial" "Handlers-cleaners" "Handlers-cleaners" ...
##  $ relationship : chr  "Not-in-family" "Husband" "Not-in-family" "Husband" ...
##  $ race         : chr  "White" "White" "White" "Black" ...
##  $ sex          : chr  "Male" "Male" "Male" "Male" ...
##  $ capital_gain : int  2174 0 0 0 0 0 0 0 14084 5178 ...
##  $ capital_loss : int  0 0 0 0 0 0 0 0 0 0 ...
##  $ hr_per_week  : int  40 13 40 40 40 40 16 45 50 40 ...
##  $ country      : chr  "United-States" "United-States" "United-States" "United-States" ...
##  $ income       : chr  "<=50K" "<=50K" "<=50K" "<=50K" ...
```

```r
adult$type_employer <- as.factor(adult$type_employer)

adult$marital <- as.factor(adult$marital)

adult$country <- as.factor(adult$country)

str(adult)
```

```
## 'data.frame':	32561 obs. of  15 variables:
##  $ age          : int  39 50 38 53 28 37 49 52 31 42 ...
##  $ type_employer: Factor w/ 6 levels "?","Federal-gov",..: 5 4 3 3 3 3 3 4 3 3 ...
##  $ fnlwgt       : int  77516 83311 215646 234721 338409 284582 160187 209642 45781 159449 ...
##  $ education    : chr  "Bachelors" "Bachelors" "HS-grad" "11th" ...
##  $ education_num: int  13 13 9 7 13 14 5 9 14 13 ...
##  $ marital      : Factor w/ 3 levels "Married","Never-Married",..: 2 1 3 1 1 1 1 1 2 1 ...
##  $ occupation   : chr  "Adm-clerical" "Exec-managerial" "Handlers-cleaners" "Handlers-cleaners" ...
##  $ relationship : chr  "Not-in-family" "Husband" "Not-in-family" "Husband" ...
##  $ race         : chr  "White" "White" "White" "Black" ...
##  $ sex          : chr  "Male" "Male" "Male" "Male" ...
##  $ capital_gain : int  2174 0 0 0 0 0 0 0 14084 5178 ...
##  $ capital_loss : int  0 0 0 0 0 0 0 0 0 0 ...
##  $ hr_per_week  : int  40 13 40 40 40 40 16 45 50 40 ...
##  $ country      : Factor w/ 42 levels "?","Cambodia",..: 40 40 40 40 6 40 24 40 40 40 ...
##  $ income       : chr  "<=50K" "<=50K" "<=50K" "<=50K" ...
```

**Missing Data**
Notice how we have data that is missing.
Convert any cell with a '?' or a ' ?' value to a NA value. Hint: is.na() may be useful here or you can also use brackets with a conditional statement. Refer to the solutions if you can't figure this step out.

```r
adult[adult=="?"] <- NA

adult$type_employer <- as.factor(adult$type_employer)
adult$marital <- as.factor(adult$marital)
adult$country <- as.factor(adult$country)

table(adult$type_employer)
```

```
## 
##           ? Federal-gov     Private    Self-emp 
##           0         960       22696        3657 
##      SL-gov  Unemployed 
##        3391          21
```

```r
any(is.na(adult))
```

```
## [1] TRUE
```

```r
head(adult)
```

```
##   age type_employer fnlwgt education
## 1  39        SL-gov  77516 Bachelors
## 2  50      Self-emp  83311 Bachelors
## 3  38       Private 215646   HS-grad
## 4  53       Private 234721      11th
## 5  28       Private 338409 Bachelors
## 6  37       Private 284582   Masters
##   education_num       marital        occupation
## 1            13 Never-Married      Adm-clerical
## 2            13       Married   Exec-managerial
## 3             9   Not-Married Handlers-cleaners
## 4             7       Married Handlers-cleaners
## 5            13       Married    Prof-specialty
## 6            14       Married   Exec-managerial
##    relationship  race    sex capital_gain
## 1 Not-in-family White   Male         2174
## 2       Husband White   Male            0
## 3 Not-in-family White   Male            0
## 4       Husband Black   Male            0
## 5          Wife Black Female            0
## 6          Wife White Female            0
##   capital_loss hr_per_week       country income
## 1            0          40 United-States  <=50K
## 2            0          13 United-States  <=50K
## 3            0          40 United-States  <=50K
## 4            0          40 United-States  <=50K
## 5            0          40          Cuba  <=50K
## 6            0          40 United-States  <=50K
```
Using table() on a column with NA values should now not display those NA values, instead you'll just see 0 for ?. Optional: Refactor these columns (may take awhile). 

Play around with the missmap function from the Amelia package. Can you figure out what its doing and how to use it?

```r
library(Amelia)
adult <- as.data.frame(adult)
missmap(adult, col = c("yellow","black"), legend = TRUE)
```

![plot of chunk unnamed-chunk-172](figure/unnamed-chunk-172-1.png)

```r
missmap(adult,y.at=c(1),y.labels = c(''),col=c('yellow','black'))
```

![plot of chunk unnamed-chunk-172](figure/unnamed-chunk-172-2.png)
Use na.omit() to omit NA data from the adult data frame. Note, it really depends on the situation and your data to judge whether or not this is a good decision. You shouldn't always just drop NA values.

```r
adult <- na.omit(adult)
```
Use missmap() to check that all the NA values were in fact dropped.

```r
missmap(adult,y.at=c(1),y.labels = c(''),col=c('yellow','black'))
```

![plot of chunk unnamed-chunk-174](figure/unnamed-chunk-174-1.png)
**EDA**
Although we've cleaned the data, we still have explored it using visualization.

Check the str() of the data.

```r
str(adult)
```

```
## 'data.frame':	30162 obs. of  15 variables:
##  $ age          : int  39 50 38 53 28 37 49 52 31 42 ...
##  $ type_employer: Factor w/ 6 levels "?","Federal-gov",..: 5 4 3 3 3 3 3 4 3 3 ...
##  $ fnlwgt       : int  77516 83311 215646 234721 338409 284582 160187 209642 45781 159449 ...
##  $ education    : chr  "Bachelors" "Bachelors" "HS-grad" "11th" ...
##  $ education_num: int  13 13 9 7 13 14 5 9 14 13 ...
##  $ marital      : Factor w/ 3 levels "Married","Never-Married",..: 2 1 3 1 1 1 1 1 2 1 ...
##  $ occupation   : chr  "Adm-clerical" "Exec-managerial" "Handlers-cleaners" "Handlers-cleaners" ...
##  $ relationship : chr  "Not-in-family" "Husband" "Not-in-family" "Husband" ...
##  $ race         : chr  "White" "White" "White" "Black" ...
##  $ sex          : chr  "Male" "Male" "Male" "Male" ...
##  $ capital_gain : int  2174 0 0 0 0 0 0 0 14084 5178 ...
##  $ capital_loss : int  0 0 0 0 0 0 0 0 0 0 ...
##  $ hr_per_week  : int  40 13 40 40 40 40 16 45 50 40 ...
##  $ country      : Factor w/ 42 levels "?","Cambodia",..: 40 40 40 40 6 40 24 40 40 40 ...
##  $ income       : chr  "<=50K" "<=50K" "<=50K" "<=50K" ...
##  - attr(*, "na.action")= 'omit' Named int [1:2399] 15 28 39 52 62 70 78 94 107 129 ...
##   ..- attr(*, "names")= chr [1:2399] "15" "28" "39" "52" ...
```

```r
adult$education <- as.factor(adult$education)
adult$occupation <- as.factor(adult$occupation)
adult$relationship <- as.factor(adult$relationship)
adult$race <- as.factor(adult$race)
adult$sex <- as.factor(adult$sex)
adult$income <- as.factor(adult$income)
```

Use ggplot2 to create a histogram of ages, colored by income.

```r
library(ggplot2)

ggplot(adult,aes(age)) + geom_histogram(aes(fill = income), color = "black", binwidth = 1) + theme_bw()
```

![plot of chunk unnamed-chunk-176](figure/unnamed-chunk-176-1.png)
Plot a histogram of hours worked per week

```r
ggplot(adult, aes(hr_per_week)) + geom_histogram() + theme_bw()
```

```
## `stat_bin()` using `bins = 30`. Pick better
## value with `binwidth`.
```

![plot of chunk unnamed-chunk-177](figure/unnamed-chunk-177-1.png)
Rename the country column to region column to better reflect the factor levels.

```r
adult <- rename(adult, region = country)
```
Create a barplot of region with the fill color defined by income class. Optional: Figure out how rotate the x axis text for readability

```r
library(plotly)
pl <- ggplot(adult,aes(factor(region))) + geom_bar(aes(fill=income),color="black") + theme_bw()

print(pl)
```

![plot of chunk unnamed-chunk-179](figure/unnamed-chunk-179-1.png)

```r
ggplotly(pl)
```

```
## Error in loadNamespace(name): there is no package called 'webshot'
```
## **Building a Model**
Now it's time to build a model to classify people into two groups: Above or Below 50k in Salary.

**Logistic Regression**
Refer to the Lecture or ISLR if you are fuzzy on any of this.

Logistic Regression is a type of classification model. In classification models, we attempt to predict the outcome of categorical dependent variables, using one or more independent variables. The independent variables can be either categorical or numerical.

Logistic regression is based on the logistic function, which always takes values between 0 and 1. Replacing the dependent variable of the logistic function with a linear combination of dependent variables we intend to use for regression, we arrive at the formula for logistic regression.

Take a quick look at the head() of adult to make sure we have a good overview before going into building the model!

```r
head(adult)
```

```
##   age type_employer fnlwgt education
## 1  39        SL-gov  77516 Bachelors
## 2  50      Self-emp  83311 Bachelors
## 3  38       Private 215646   HS-grad
## 4  53       Private 234721      11th
## 5  28       Private 338409 Bachelors
## 6  37       Private 284582   Masters
##   education_num       marital        occupation
## 1            13 Never-Married      Adm-clerical
## 2            13       Married   Exec-managerial
## 3             9   Not-Married Handlers-cleaners
## 4             7       Married Handlers-cleaners
## 5            13       Married    Prof-specialty
## 6            14       Married   Exec-managerial
##    relationship  race    sex capital_gain
## 1 Not-in-family White   Male         2174
## 2       Husband White   Male            0
## 3 Not-in-family White   Male            0
## 4       Husband Black   Male            0
## 5          Wife Black Female            0
## 6          Wife White Female            0
##   capital_loss hr_per_week        region income
## 1            0          40 United-States  <=50K
## 2            0          13 United-States  <=50K
## 3            0          40 United-States  <=50K
## 4            0          40 United-States  <=50K
## 5            0          40          Cuba  <=50K
## 6            0          40 United-States  <=50K
```
**Train Test Split**
Split the data into a train and test set using the caTools library as done in previous lectures. Reference previous solutions notebooks if you need a refresher.

```r
library(caTools)
set.seed(101)

split <- sample.split(adult$income, SplitRatio = 0.7)

train <- subset(adult, split == TRUE )
test <- subset(adult, split == FALSE)
```
**Training the Model**
Explore the glm() function with help(glm). Read through the documentation.

```r
train.ok <- select(train, -region)
test.ok <- select(test,-region)

model <- glm(income ~ ., family = binomial(link = "logit"), data = train.ok)
```

```
## Warning: glm.fit: fitted probabilities
## numerically 0 or 1 occurred
```

```r
summary(model)
```

```
## 
## Call:
## glm(formula = income ~ ., family = binomial(link = "logit"), 
##     data = train.ok)
## 
## Deviance Residuals: 
##     Min       1Q   Median       3Q      Max  
## -5.0774  -0.5222  -0.1939   0.0000   3.4532  
## 
## Coefficients: (1 not defined because of singularities)
##                               Estimate
## (Intercept)                 -5.083e+00
## age                          2.709e-02
## type_employerPrivate        -5.136e-01
## type_employerSelf-emp       -8.315e-01
## type_employerSL-gov         -7.753e-01
## type_employerUnemployed     -1.402e+01
## fnlwgt                       6.862e-07
## education11th                4.476e-04
## education12th                3.726e-01
## education1st-4th            -7.677e-01
## education5th-6th            -5.761e-01
## education7th-8th            -5.329e-01
## education9th                -4.269e-01
## educationAssoc-acdm          1.180e+00
## educationAssoc-voc           1.205e+00
## educationBachelors           1.868e+00
## educationDoctorate           2.664e+00
## educationHS-grad             6.939e-01
## educationMasters             2.192e+00
## educationPreschool          -1.963e+01
## educationProf-school         2.743e+00
## educationSome-college        1.080e+00
## education_num                       NA
## maritalNever-Married        -1.438e+00
## maritalNot-Married          -8.536e-01
## occupationArmed-Forces      -6.083e-01
## occupationCraft-repair       1.301e-01
## occupationExec-managerial    9.164e-01
## occupationFarming-fishing   -1.027e+00
## occupationHandlers-cleaners -7.180e-01
## occupationMachine-op-inspct -2.225e-01
## occupationOther-service     -6.794e-01
## occupationPriv-house-serv   -1.212e+01
## occupationProf-specialty     6.199e-01
## occupationProtective-serv    7.381e-01
## occupationSales              3.691e-01
## occupationTech-support       6.602e-01
## occupationTransport-moving  -2.964e-02
## relationshipNot-in-family   -8.043e-01
## relationshipOther-relative  -8.786e-01
## relationshipOwn-child       -1.802e+00
## relationshipUnmarried       -1.053e+00
## relationshipWife             1.326e+00
## raceAsian-Pac-Islander       2.956e-01
## raceBlack                    1.725e-01
## raceOther                   -4.860e-02
## raceWhite                    3.665e-01
## sexMale                      8.188e-01
## capital_gain                 3.157e-04
## capital_loss                 6.513e-04
## hr_per_week                  3.014e-02
##                             Std. Error z value
## (Intercept)                  3.795e-01 -13.394
## age                          2.008e-03  13.492
## type_employerPrivate         1.113e-01  -4.613
## type_employerSelf-emp        1.240e-01  -6.707
## type_employerSL-gov          1.261e-01  -6.146
## type_employerUnemployed      3.750e+02  -0.037
## fnlwgt                       2.078e-07   3.303
## education11th                2.517e-01   0.002
## education12th                3.153e-01   1.182
## education1st-4th             5.959e-01  -1.288
## education5th-6th             4.077e-01  -1.413
## education7th-8th             2.882e-01  -1.849
## education9th                 3.391e-01  -1.259
## educationAssoc-acdm          2.132e-01   5.537
## educationAssoc-voc           2.038e-01   5.915
## educationBachelors           1.892e-01   9.875
## educationDoctorate           2.618e-01  10.175
## educationHS-grad             1.839e-01   3.773
## educationMasters             2.026e-01  10.819
## educationPreschool           1.732e+02  -0.113
## educationProf-school         2.465e-01  11.125
## educationSome-college        1.866e-01   5.786
## education_num                       NA      NA
## maritalNever-Married         1.960e-01  -7.336
## maritalNot-Married           1.950e-01  -4.377
## occupationArmed-Forces       1.833e+00  -0.332
## occupationCraft-repair       9.629e-02   1.351
## occupationExec-managerial    9.270e-02   9.886
## occupationFarming-fishing    1.713e-01  -5.996
## occupationHandlers-cleaners  1.742e-01  -4.122
## occupationMachine-op-inspct  1.226e-01  -1.814
## occupationOther-service      1.414e-01  -4.803
## occupationPriv-house-serv    1.343e+02  -0.090
## occupationProf-specialty     9.857e-02   6.289
## occupationProtective-serv    1.484e-01   4.975
## occupationSales              9.889e-02   3.732
## occupationTech-support       1.323e-01   4.992
## occupationTransport-moving   1.192e-01  -0.249
## relationshipNot-in-family    1.922e-01  -4.185
## relationshipOther-relative   2.585e-01  -3.399
## relationshipOwn-child        2.406e-01  -7.491
## relationshipUnmarried        2.177e-01  -4.840
## relationshipWife             1.254e-01  10.569
## raceAsian-Pac-Islander       2.912e-01   1.015
## raceBlack                    2.787e-01   0.619
## raceOther                    4.142e-01  -0.117
## raceWhite                    2.646e-01   1.385
## sexMale                      9.596e-02   8.532
## capital_gain                 1.271e-05  24.842
## capital_loss                 4.630e-05  14.068
## hr_per_week                  2.004e-03  15.045
##                             Pr(>|z|)    
## (Intercept)                  < 2e-16 ***
## age                          < 2e-16 ***
## type_employerPrivate        3.97e-06 ***
## type_employerSelf-emp       1.99e-11 ***
## type_employerSL-gov         7.93e-10 ***
## type_employerUnemployed     0.970179    
## fnlwgt                      0.000957 ***
## education11th               0.998581    
## education12th               0.237308    
## education1st-4th            0.197636    
## education5th-6th            0.157609    
## education7th-8th            0.064446 .  
## education9th                0.207961    
## educationAssoc-acdm         3.08e-08 ***
## educationAssoc-voc          3.32e-09 ***
## educationBachelors           < 2e-16 ***
## educationDoctorate           < 2e-16 ***
## educationHS-grad            0.000161 ***
## educationMasters             < 2e-16 ***
## educationPreschool          0.909727    
## educationProf-school         < 2e-16 ***
## educationSome-college       7.21e-09 ***
## education_num                     NA    
## maritalNever-Married        2.21e-13 ***
## maritalNot-Married          1.20e-05 ***
## occupationArmed-Forces      0.739984    
## occupationCraft-repair      0.176620    
## occupationExec-managerial    < 2e-16 ***
## occupationFarming-fishing   2.03e-09 ***
## occupationHandlers-cleaners 3.75e-05 ***
## occupationMachine-op-inspct 0.069615 .  
## occupationOther-service     1.56e-06 ***
## occupationPriv-house-serv   0.928079    
## occupationProf-specialty    3.20e-10 ***
## occupationProtective-serv   6.54e-07 ***
## occupationSales             0.000190 ***
## occupationTech-support      5.98e-07 ***
## occupationTransport-moving  0.803639    
## relationshipNot-in-family   2.85e-05 ***
## relationshipOther-relative  0.000676 ***
## relationshipOwn-child       6.84e-14 ***
## relationshipUnmarried       1.30e-06 ***
## relationshipWife             < 2e-16 ***
## raceAsian-Pac-Islander      0.309994    
## raceBlack                   0.536079    
## raceOther                   0.906600    
## raceWhite                   0.166075    
## sexMale                      < 2e-16 ***
## capital_gain                 < 2e-16 ***
## capital_loss                 < 2e-16 ***
## hr_per_week                  < 2e-16 ***
## ---
## Signif. codes:  
## 0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 23697  on 21113  degrees of freedom
## Residual deviance: 13773  on 21064  degrees of freedom
## AIC: 13873
## 
## Number of Fisher Scoring iterations: 14
```

```r
#STEP FUNCTION: keeps ONLY the variables that are significant
new.step.model <- step(model)
```

```
## Start:  AIC=13872.68
## income ~ age + type_employer + fnlwgt + education + education_num + 
##     marital + occupation + relationship + race + sex + capital_gain + 
##     capital_loss + hr_per_week
```

```
## Warning: glm.fit: fitted probabilities
## numerically 0 or 1 occurred

## Warning: glm.fit: fitted probabilities
## numerically 0 or 1 occurred

## Warning: glm.fit: fitted probabilities
## numerically 0 or 1 occurred

## Warning: glm.fit: fitted probabilities
## numerically 0 or 1 occurred

## Warning: glm.fit: fitted probabilities
## numerically 0 or 1 occurred

## Warning: glm.fit: fitted probabilities
## numerically 0 or 1 occurred

## Warning: glm.fit: fitted probabilities
## numerically 0 or 1 occurred

## Warning: glm.fit: fitted probabilities
## numerically 0 or 1 occurred

## Warning: glm.fit: fitted probabilities
## numerically 0 or 1 occurred

## Warning: glm.fit: fitted probabilities
## numerically 0 or 1 occurred

## Warning: glm.fit: fitted probabilities
## numerically 0 or 1 occurred

## Warning: glm.fit: fitted probabilities
## numerically 0 or 1 occurred
```

```
## 
## Step:  AIC=13872.68
## income ~ age + type_employer + fnlwgt + education + marital + 
##     occupation + relationship + race + sex + capital_gain + capital_loss + 
##     hr_per_week
```

```
## Warning: glm.fit: fitted probabilities
## numerically 0 or 1 occurred

## Warning: glm.fit: fitted probabilities
## numerically 0 or 1 occurred

## Warning: glm.fit: fitted probabilities
## numerically 0 or 1 occurred

## Warning: glm.fit: fitted probabilities
## numerically 0 or 1 occurred

## Warning: glm.fit: fitted probabilities
## numerically 0 or 1 occurred

## Warning: glm.fit: fitted probabilities
## numerically 0 or 1 occurred

## Warning: glm.fit: fitted probabilities
## numerically 0 or 1 occurred

## Warning: glm.fit: fitted probabilities
## numerically 0 or 1 occurred

## Warning: glm.fit: fitted probabilities
## numerically 0 or 1 occurred
```

```
##                 Df Deviance   AIC
## <none>                13773 13873
## - race           4    13781 13873
## - fnlwgt         1    13784 13882
## - type_employer  4    13838 13930
## - marital        2    13838 13934
## - sex            1    13848 13946
## - age            1    13956 14054
## - capital_loss   1    13976 14074
## - relationship   5    14012 14102
## - hr_per_week    1    14006 14104
## - occupation    13    14221 14295
## - education     15    14482 14552
## - capital_gain   1    14942 15040
```
Let's create a **confussion matrix**

```r
test$predicted.income <- predict(model, test.ok, type = "response")
```

```
## Warning in predict.lm(object, newdata, se.fit,
## scale = 1, type = if (type == : prediction from a
## rank-deficient fit may be misleading
```

```r
table(test$income, test$predicted.income > 0.5)
```

```
##        
##         FALSE TRUE
##   <=50K  6287  509
##   >50K    901 1351
```

```r
##Checking the accuracy
acc <- (6289 + 1355)/(6289 + 1355 + 507 + 897)
acc
```

```
## [1] 0.8448276
```

```r
recall <- 6289/(6289+507)
recall
```

```
## [1] 0.9253973
```

```r
precision <- 6289/(6289+897)
precision
```

```
## [1] 0.8751739
```

