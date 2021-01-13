---
title: "Section 27 - Machine Learning Project - Decision Trees and Random Forests"
author: "Victoria"
date: "13/1/2021"
output: html_document
---



#**Tree Methods Project**
For this project we will be exploring the use of tree methods to classify schools as Private or Public based off their features.

Let's start by getting the data which is included in the ISLR library, the College data frame.

```r
library(ISLR)

head(College)
```

```
##                              Private
## Abilene Christian University     Yes
## Adelphi University               Yes
## Adrian College                   Yes
## Agnes Scott College              Yes
## Alaska Pacific University        Yes
## Albertson College                Yes
##                              Apps
## Abilene Christian University 1660
## Adelphi University           2186
## Adrian College               1428
## Agnes Scott College           417
## Alaska Pacific University     193
## Albertson College             587
##                              Accept
## Abilene Christian University   1232
## Adelphi University             1924
## Adrian College                 1097
## Agnes Scott College             349
## Alaska Pacific University       146
## Albertson College               479
##                              Enroll
## Abilene Christian University    721
## Adelphi University              512
## Adrian College                  336
## Agnes Scott College             137
## Alaska Pacific University        55
## Albertson College               158
##                              Top10perc
## Abilene Christian University        23
## Adelphi University                  16
## Adrian College                      22
## Agnes Scott College                 60
## Alaska Pacific University           16
## Albertson College                   38
##                              Top25perc
## Abilene Christian University        52
## Adelphi University                  29
## Adrian College                      50
## Agnes Scott College                 89
## Alaska Pacific University           44
## Albertson College                   62
##                              F.Undergrad
## Abilene Christian University        2885
## Adelphi University                  2683
## Adrian College                      1036
## Agnes Scott College                  510
## Alaska Pacific University            249
## Albertson College                    678
##                              P.Undergrad
## Abilene Christian University         537
## Adelphi University                  1227
## Adrian College                        99
## Agnes Scott College                   63
## Alaska Pacific University            869
## Albertson College                     41
##                              Outstate
## Abilene Christian University     7440
## Adelphi University              12280
## Adrian College                  11250
## Agnes Scott College             12960
## Alaska Pacific University        7560
## Albertson College               13500
##                              Room.Board
## Abilene Christian University       3300
## Adelphi University                 6450
## Adrian College                     3750
## Agnes Scott College                5450
## Alaska Pacific University          4120
## Albertson College                  3335
##                              Books
## Abilene Christian University   450
## Adelphi University             750
## Adrian College                 400
## Agnes Scott College            450
## Alaska Pacific University      800
## Albertson College              500
##                              Personal
## Abilene Christian University     2200
## Adelphi University               1500
## Adrian College                   1165
## Agnes Scott College               875
## Alaska Pacific University        1500
## Albertson College                 675
##                              PhD
## Abilene Christian University  70
## Adelphi University            29
## Adrian College                53
## Agnes Scott College           92
## Alaska Pacific University     76
## Albertson College             67
##                              Terminal
## Abilene Christian University       78
## Adelphi University                 30
## Adrian College                     66
## Agnes Scott College                97
## Alaska Pacific University          72
## Albertson College                  73
##                              S.F.Ratio
## Abilene Christian University      18.1
## Adelphi University                12.2
## Adrian College                    12.9
## Agnes Scott College                7.7
## Alaska Pacific University         11.9
## Albertson College                  9.4
##                              perc.alumni
## Abilene Christian University          12
## Adelphi University                    16
## Adrian College                        30
## Agnes Scott College                   37
## Alaska Pacific University              2
## Albertson College                     11
##                              Expend
## Abilene Christian University   7041
## Adelphi University            10527
## Adrian College                 8735
## Agnes Scott College           19016
## Alaska Pacific University     10922
## Albertson College              9727
##                              Grad.Rate
## Abilene Christian University        60
## Adelphi University                  56
## Adrian College                      54
## Agnes Scott College                 59
## Alaska Pacific University           15
## Albertson College                   55
```

```r
df <- College
colnames(df)
```

```
##  [1] "Private"     "Apps"       
##  [3] "Accept"      "Enroll"     
##  [5] "Top10perc"   "Top25perc"  
##  [7] "F.Undergrad" "P.Undergrad"
##  [9] "Outstate"    "Room.Board" 
## [11] "Books"       "Personal"   
## [13] "PhD"         "Terminal"   
## [15] "S.F.Ratio"   "perc.alumni"
## [17] "Expend"      "Grad.Rate"
```

**EDA**
Let's explore the data!

Create a scatterplot of Grad.Rate versus Room.Board, colored by the Private column.

```r
library(ggplot2)

ggplot(df, aes(x = Room.Board, y = Grad.Rate)) + geom_point(aes(color = Private)) + theme_bw()
```

![plot of chunk unnamed-chunk-37](figure/unnamed-chunk-37-1.png)

Create a histogram of full time undergrad students, color by Private.

```r
ggplot(df, aes(x = F.Undergrad)) + geom_histogram(aes(fill = Private), color = "black") + theme_bw()
```

```
## `stat_bin()` using `bins = 30`. Pick
## better value with `binwidth`.
```

![plot of chunk unnamed-chunk-38](figure/unnamed-chunk-38-1.png)

Create a histogram of Grad.Rate colored by Private. You should see something odd here.

```r
ggplot(df, aes(x = Grad.Rate)) + geom_histogram(aes(fill = Private), color = "black") + theme_bw()
```

```
## `stat_bin()` using `bins = 30`. Pick
## better value with `binwidth`.
```

![plot of chunk unnamed-chunk-39](figure/unnamed-chunk-39-1.png)
What college had a Graduation Rate of above 100% ?

```r
grad.above100 <- subset(df, Grad.Rate > 100)

print(grad.above100)
```

```
##                   Private Apps Accept
## Cazenovia College     Yes 3847   3433
##                   Enroll Top10perc
## Cazenovia College    527         9
##                   Top25perc
## Cazenovia College        35
##                   F.Undergrad
## Cazenovia College        1010
##                   P.Undergrad Outstate
## Cazenovia College          12     9384
##                   Room.Board Books
## Cazenovia College       4840   600
##                   Personal PhD
## Cazenovia College      500  22
##                   Terminal S.F.Ratio
## Cazenovia College       47      14.3
##                   perc.alumni Expend
## Cazenovia College          20   7697
##                   Grad.Rate
## Cazenovia College       118
```


Change that college's grad rate to 100%

```r
df["Cazenovia College","Grad.Rate"] <- 100

df["Cazenovia College","Grad.Rate"]
```

```
## [1] 100
```
**Train Test Split**
Split your data into training and testing sets 70/30. Use the caTools library to do this.


```r
library(caTools)

split <- sample.split(df, SplitRatio = 0.7)

train <- subset(df, split == TRUE)
test <- subset(df, split == FALSE)
```

**Decision Tree**
Use the rpart library to build a decision tree to predict whether or not a school is Private. Remember to only build your tree off the training data.

```r
library(rpart)

tree <- rpart(Private ~ ., method = "class", data = train)
```

Use predict() to predict the Private label on the test data.

```r
predicted.Private <- predict(tree, test)
```

Check the Head of the predicted values. You should notice that you actually have two columns with the probabilities.

```r
head(predicted.Private)
```

```
##                                   No
## Adelphi University        0.01846154
## Alaska Pacific University 0.20454545
## Albertson College         0.01846154
## Alma College              0.01846154
## Amherst College           0.01846154
## Anderson University       0.01846154
##                                 Yes
## Adelphi University        0.9815385
## Alaska Pacific University 0.7954545
## Albertson College         0.9815385
## Alma College              0.9815385
## Amherst College           0.9815385
## Anderson University       0.9815385
```

Turn these two columns into one column to match the original Yes/No Label for a Private column.

```r
predicted.Private <- as.data.frame(predicted.Private)

joiner <- function(x){
  if (x >= 0.5) {
    return("Yes")
  }else{
    return("No")
  }
}

predicted.Private$Private <- sapply(predicted.Private$Yes,joiner)

head(predicted.Private)
```

```
##                                   No
## Adelphi University        0.01846154
## Alaska Pacific University 0.20454545
## Albertson College         0.01846154
## Alma College              0.01846154
## Amherst College           0.01846154
## Anderson University       0.01846154
##                                 Yes
## Adelphi University        0.9815385
## Alaska Pacific University 0.7954545
## Albertson College         0.9815385
## Alma College              0.9815385
## Amherst College           0.9815385
## Anderson University       0.9815385
##                           Private
## Adelphi University            Yes
## Alaska Pacific University     Yes
## Albertson College             Yes
## Alma College                  Yes
## Amherst College               Yes
## Anderson University           Yes
```

Now use table() to create a confusion matrix of your tree model.

```r
table(predicted.Private$Private, test$Private)
```

```
##      
##        No Yes
##   No   53   7
##   Yes  13 186
```
Use the rpart.plot library and the prp() function to plot out your tree model.

```r
library(rpart.plot)

prp(tree)
```

![plot of chunk unnamed-chunk-48](figure/unnamed-chunk-48-1.png)
**Random Forest**
Now let's build out a random forest model!

Call the randomForest package library

```r
library(randomForest)
```

Now use randomForest() to build out a model to predict Private class. Add importance=TRUE as a parameter in the model. (Use help(randomForest) to find out what this does.

```r
rf.model <- randomForest(Private ~ ., data = train, importance = TRUE)

print(rf.model)
```

```
## 
## Call:
##  randomForest(formula = Private ~ ., data = train, importance = TRUE) 
##                Type of random forest: classification
##                      Number of trees: 500
## No. of variables tried at each split: 4
## 
##         OOB estimate of  error rate: 6.76%
## Confusion matrix:
##      No Yes class.error
## No  127  19  0.13013699
## Yes  16 356  0.04301075
```

What was your model's confusion matrix on its own training set? Use model$confusion.

```r
rf.model$confusion
```

```
##      No Yes class.error
## No  127  19  0.13013699
## Yes  16 356  0.04301075
```

```r
rf.model$importance
```

```
##                       No           Yes
## Apps        0.0280218616  0.0099706588
## Accept      0.0277104405  0.0110390206
## Enroll      0.0529508828  0.0277964605
## Top10perc   0.0097682155  0.0048517387
## Top25perc   0.0074876758  0.0034961238
## F.Undergrad 0.1647090600  0.0617411616
## P.Undergrad 0.0407689787  0.0051417084
## Outstate    0.1571676885  0.0719824583
## Room.Board  0.0231722473  0.0163400107
## Books       0.0008083974 -0.0007885343
## Personal    0.0018034754  0.0004231744
## PhD         0.0112025604  0.0067903413
## Terminal    0.0053220459  0.0061830429
## S.F.Ratio   0.0232858385  0.0060709488
## perc.alumni 0.0440169362  0.0027743051
## Expend      0.0185265773  0.0165073018
## Grad.Rate   0.0206248564  0.0044782802
##             MeanDecreaseAccuracy
## Apps                0.0149529926
## Accept              0.0157631832
## Enroll              0.0347181003
## Top10perc           0.0061974095
## Top25perc           0.0046320734
## F.Undergrad         0.0909135271
## P.Undergrad         0.0150746942
## Outstate            0.0957624821
## Room.Board          0.0181422212
## Books              -0.0003575402
## Personal            0.0008280707
## PhD                 0.0079993266
## Terminal            0.0059350657
## S.F.Ratio           0.0108526349
## perc.alumni         0.0142597103
## Expend              0.0171009288
## Grad.Rate           0.0089835382
##             MeanDecreaseGini
## Apps                8.057710
## Accept             11.184418
## Enroll             21.686685
## Top10perc           4.404714
## Top25perc           4.136279
## F.Undergrad        36.514184
## P.Undergrad        13.597617
## Outstate           47.661878
## Room.Board         10.469634
## Books               2.117435
## Personal            3.386998
## PhD                 4.812396
## Terminal            4.833436
## S.F.Ratio          12.425649
## perc.alumni         7.662452
## Expend              9.740632
## Grad.Rate           6.447582
```

```r
rf.model$predicted
```

```
##                  Abilene Christian University 
##                                            No 
##                                Adrian College 
##                                           Yes 
##                           Agnes Scott College 
##                                           Yes 
##                       Albertus Magnus College 
##                                           Yes 
##                                Albion College 
##                                           Yes 
##                              Albright College 
##                                           Yes 
##                     Alderson-Broaddus College 
##                                           Yes 
##                             Alfred University 
##                                           Yes 
##                             Allegheny College 
##                                           Yes 
##       Allentown Coll. of St. Francis de Sales 
##                                           Yes 
##                               Alverno College 
##                                           Yes 
##                American International College 
##                                           Yes 
##                            Andrews University 
##                                           Yes 
##                            Antioch University 
##                                           Yes 
##                  Appalachian State University 
##                                            No 
##               Arkansas College (Lyon College) 
##                                           Yes 
##                      Arkansas Tech University 
##                                            No 
##                            Assumption College 
##                                           Yes 
##                 Auburn University-Main Campus 
##                                            No 
##                              Augsburg College 
##                                           Yes 
##                          Augustana College IL 
##                                           Yes 
##                             Augustana College 
##                                           Yes 
##                               Averett College 
##                                           Yes 
##                              Baker University 
##                                           Yes 
##                                  Bard College 
##                                           Yes 
##                              Barry University 
##                                           Yes 
##                             Baylor University 
##                                            No 
##                         Belmont Abbey College 
##                                           Yes 
##                            Belmont University 
##                                           Yes 
##                                Beloit College 
##                                           Yes 
##                      Bemidji State University 
##                                            No 
##                           Benedictine College 
##                                           Yes 
##                            Bennington College 
##                                           Yes 
##                               Bentley College 
##                                           Yes 
##                               Bethany College 
##                                           Yes 
##                             Bethel College KS 
##                                           Yes 
##                   Birmingham-Southern College 
##                                           Yes 
##              Bloomsburg Univ. of Pennsylvania 
##                                            No 
##                             Bluefield College 
##                                           Yes 
##                               Bowdoin College 
##                                           Yes 
##                Bowling Green State University 
##                                            No 
##                              Bradford College 
##                                           Yes 
##                            Bradley University 
##                                           Yes 
##                           Brandeis University 
##                                           Yes 
##                             Brenau University 
##                                           Yes 
##                        Brewton-Parker College 
##                                            No 
##                           Bridgewater College 
##                                           Yes 
##             Brigham Young University at Provo 
##                                            No 
##                           Bucknell University 
##                                           Yes 
##                             Butler University 
##                                           Yes 
##                               Cabrini College 
##                                           Yes 
##               California Polytechnic-San Luis 
##                                            No 
##         California State University at Fresno 
##                                            No 
##                                Calvin College 
##                                           Yes 
##                           Campbell University 
##                                            No 
##                        Campbellsville College 
##                                           Yes 
##                              Canisius College 
##                                           Yes 
##                            Capital University 
##                                           Yes 
##                              Carleton College 
##                                           Yes 
##                    Carnegie Mellon University 
##                                           Yes 
##                              Carthage College 
##                                           Yes 
##                       Castleton State College 
##                                           Yes 
##                               Catawba College 
##                                           Yes 
##                           Cedar Crest College 
##                                           Yes 
##                            Cedarville College 
##                                           Yes 
##                             Centenary College 
##                                           Yes 
##                Centenary College of Louisiana 
##                                           Yes 
##                   Center for Creative Studies 
##                                           Yes 
##                               Central College 
##                                           Yes 
##          Central Connecticut State University 
##                                            No 
##                 Central Washington University 
##                                            No 
##                      Central Wesleyan College 
##                                           Yes 
##                               Chatham College 
##                                           Yes 
##                           Christendom College 
##                                           Yes 
##                 Christian Brothers University 
##                                           Yes 
##                     Claremont McKenna College 
##                                           Yes 
##                              Clark University 
##                                           Yes 
##                                Clarke College 
##                                           Yes 
##                           Clarkson University 
##                                           Yes 
##                            Clemson University 
##                                            No 
## Clinch Valley Coll. of  the Univ. of Virginia 
##                                           Yes 
##                                   Coe College 
##                                           Yes 
##                                 Colby College 
##                                           Yes 
##                            Colgate University 
##                                           Yes 
##                   College of Mount St. Joseph 
##                                           Yes 
##                         College of Notre Dame 
##                                           Yes 
##             College of Notre Dame of Maryland 
##                                           Yes 
##                    College of Saint Elizabeth 
##                                           Yes 
##                         College of Saint Rose 
##                                           Yes 
##                           College of Santa Fe 
##                                           Yes 
##                         College of St. Joseph 
##                                           Yes 
##                    College of St. Scholastica 
##                                           Yes 
##                     College of the Holy Cross 
##                                           Yes 
##                   College of William and Mary 
##                                           Yes 
##                              Colorado College 
##                                           Yes 
##                     Colorado State University 
##                                            No 
##                           Columbia University 
##                                           Yes 
##                    Concordia Lutheran College 
##                                           Yes 
##                       Concordia University CA 
##                                           Yes 
##                              Converse College 
##                                           Yes 
##                               Cornell College 
##                                           Yes 
##                          Creighton University 
##                                           Yes 
##                       Culver-Stockton College 
##                                           Yes 
##                            Cumberland College 
##                                           Yes 
##                            D'Youville College 
##                                           Yes 
##                                  Dana College 
##                                           Yes 
##                             Dartmouth College 
##                                           Yes 
##                              Davidson College 
##                                           Yes 
##                            Denison University 
##                                           Yes 
##                             Dickinson College 
##                                           Yes 
##                    Dickinson State University 
##                                           Yes 
##                 Dominican College of Blauvelt 
##                                           Yes 
##                                 Dordt College 
##                                           Yes 
##                               Dowling College 
##                                           Yes 
##                              Drake University 
##                                           Yes 
##                               Drew University 
##                                           Yes 
##                                 Drury College 
##                                           Yes 
##                               Duke University 
##                                           Yes 
##                      East Carolina University 
##                                            No 
##               East Tennessee State University 
##                                            No 
##          Eastern Connecticut State University 
##                                            No 
##                     Eastern Mennonite College 
##                                           Yes 
##                      Eastern Nazarene College 
##                                           Yes 
##                                Elmira College 
##                                           Yes 
##                                  Elms College 
##                                           Yes 
##                                  Elon College 
##                                           Yes 
##          Embry Riddle Aeronautical University 
##                                            No 
##                         Emory & Henry College 
##                                           Yes 
##                              Emory University 
##                                           Yes 
##                      Emporia State University 
##                                            No 
##                                Eureka College 
##                                           Yes 
##                       Evergreen State College 
##                                            No 
##                                Ferrum College 
##                                           Yes 
##               Florida Institute of Technology 
##                                           Yes 
##              Florida International University 
##                                            No 
##                             Fontbonne College 
##                                           Yes 
##                            Fordham University 
##                                           Yes 
##                            Fort Lewis College 
##                                            No 
##                     Francis Marion University 
##                                            No 
##         Franciscan University of Steubenville 
##                                           Yes 
##                              Franklin College 
##                                           Yes 
##                       Franklin Pierce College 
##                                           Yes 
##                        Fresno Pacific College 
##                                           Yes 
##                             Furman University 
##                                           Yes 
##                                Geneva College 
##                                           Yes 
##                       George Mason University 
##                                            No 
##                  George Washington University 
##                                           Yes 
##               Georgia Institute of Technology 
##                                            No 
##                      Georgia State University 
##                                            No 
##                        Georgian Court College 
##                                           Yes 
##                            Gettysburg College 
##                                           Yes 
##                         Goldey Beacom College 
##                                           Yes 
##                            Gonzaga University 
##                                           Yes 
##                                Gordon College 
##                                           Yes 
##                               Goucher College 
##                                           Yes 
##                    Grace College and Seminary 
##                                           Yes 
##                        Green Mountain College 
##                                           Yes 
##                            Greenville College 
##                                           Yes 
##                              Grinnell College 
##                                           Yes 
##                     Gustavus Adolphus College 
##                                           Yes 
##                         Gwynedd Mercy College 
##                                           Yes 
##                              Hamilton College 
##                                           Yes 
##                            Hamline University 
##                                           Yes 
##                      Hampden - Sydney College 
##                                           Yes 
##                            Hampton University 
##                                            No 
##                               Hanover College 
##                                           Yes 
##                            Harding University 
##                                            No 
##                              Hartwick College 
##                                           Yes 
##                              Hastings College 
##                                           Yes 
##                             Hillsdale College 
##                                           Yes 
##                                 Hiram College 
##                                           Yes 
##                               Hollins College 
##                                           Yes 
##                                  Hood College 
##                                           Yes 
##                                  Hope College 
##                                           Yes 
##                              Houghton College 
##                                           Yes 
##                            Huntingdon College 
##                                           Yes 
##                            Huntington College 
##                                           Yes 
##                              Huron University 
##                                           Yes 
##                  Illinois Benedictine College 
##                                           Yes 
##                              Illinois College 
##                                           Yes 
##                  Illinois Wesleyan University 
##                                           Yes 
##                        Incarnate Word College 
##                                           Yes 
##                      Indiana State University 
##                                            No 
##                                  Iona College 
##                                           Yes 
##                         Iowa State University 
##                                            No 
##                                Ithaca College 
##                                           Yes 
##                      James Madison University 
##                                            No 
##                             Jamestown College 
##                                            No 
##                     Jersey City State College 
##                                            No 
##                         John Brown University 
##                                           Yes 
##                      Johns Hopkins University 
##                                           Yes 
##                         Johnson State College 
##                                           Yes 
##                       Kansas State University 
##                                            No 
##                           Keene State College 
##                                            No 
##                     Kentucky Wesleyan College 
##                                           Yes 
##                                King's College 
##                                           Yes 
##                                  King College 
##                                           Yes 
##                                  Knox College 
##                                           Yes 
##                              La Roche College 
##                                           Yes 
##                           La Salle University 
##                                           Yes 
##                             Lafayette College 
##                                           Yes 
##                              LaGrange College 
##                                           Yes 
##                              Lakeland College 
##                                           Yes 
##                              Lamar University 
##                                            No 
##                           Lawrence University 
##                                           Yes 
##                        Lebanon Valley College 
##                                           Yes 
##                             Lehigh University 
##                                           Yes 
##                         LeTourneau University 
##                                           Yes 
##                       Lewis and Clark College 
##                                           Yes 
##                              Lewis University 
##                                           Yes 
##                   Lincoln Memorial University 
##                                           Yes 
##                            Lincoln University 
##                                           Yes 
##                            Lindenwood College 
##                                           Yes 
##                              Linfield College 
##                                           Yes 
##         Lock Haven University of Pennsylvania 
##                                            No 
##                              Longwood College 
##                                           Yes 
##     Louisiana State University at Baton Rouge 
##                                            No 
##                                Loyola College 
##                                           Yes 
##                   Loyola Marymount University 
##                                           Yes 
##                                Luther College 
##                                           Yes 
##                              Lycoming College 
##                                           Yes 
##                             Lynchburg College 
##                                           Yes 
##                          Lyndon State College 
##                                           Yes 
##                            Macalester College 
##                                           Yes 
##                             MacMurray College 
##                                           Yes 
##                                Malone College 
##                                           Yes 
##                             Manhattan College 
##                                           Yes 
##                        Manhattanville College 
##                                           Yes 
##                              Marietta College 
##                                           Yes 
##                          Marquette University 
##                                           Yes 
##                           Marshall University 
##                                            No 
##                   Marymount College Tarrytown 
##                                           Yes 
##                   Marymount Manhattan College 
##                                           Yes 
##                          Marymount University 
##                                           Yes 
##                             Maryville College 
##                                           Yes 
##                          Maryville University 
##                                           Yes 
##                              Marywood College 
##                                           Yes 
##         Massachusetts Institute of Technology 
##                                           Yes 
##                             McKendree College 
##                                           Yes 
##                            McMurry University 
##                                           Yes 
##                            Mercyhurst College 
##                                           Yes 
##                             Merrimack College 
##                                           Yes 
##                            Mesa State College 
##                                            No 
##                     Michigan State University 
##                                            No 
##             Michigan Technological University 
##                                            No 
##                   MidAmerica Nazarene College 
##                                           Yes 
##              Millersville University of Penn. 
##                                            No 
##                              Milligan College 
##                                           Yes 
##                           Millikin University 
##                                           Yes 
##                              Millsaps College 
##                                           Yes 
##                           Mississippi College 
##                                            No 
##                  Mississippi State University 
##                                            No 
##                       Missouri Valley College 
##                                           Yes 
##                              Monmouth College 
##                                           Yes 
##       Montana College of Mineral Sci. & Tech. 
##                                           Yes 
##                     Montreat-Anderson College 
##                                           Yes 
##                     Moorhead State University 
##                                            No 
##                              Moravian College 
##                                           Yes 
##                             Morehouse College 
##                                           Yes 
##                           Morningside College 
##                                           Yes 
##                                Morris College 
##                                           Yes 
##                         Mount Holyoke College 
##                                           Yes 
##                            Mount Mary College 
##                                           Yes 
##                           Mount Mercy College 
##                                           Yes 
##                      Mount Saint Mary College 
##                                           Yes 
##                           Mount Union College 
##                                           Yes 
##                 Mount Vernon Nazarene College 
##                                           Yes 
##                             Muskingum College 
##                                           Yes 
##                     National-Louis University 
##                                           Yes 
##                 Nazareth College of Rochester 
##                                           Yes 
##            New Jersey Institute of Technology 
##                                           Yes 
##      New Mexico Institute of Mining and Tech. 
##                                           Yes 
##                           New York University 
##                                           Yes 
##                              Newberry College 
##                                           Yes 
##                     North Adams State College 
##                                           Yes 
##       North Carolina A. & T. State University 
##                                            No 
##                         North Central College 
##                                           Yes 
##                            North Park College 
##                                           Yes 
##           Northeast Missouri State University 
##                                            No 
##                  Northern Illinois University 
##                                            No 
##           Northwest Missouri State University 
##                                            No 
##                    Northwest Nazarene College 
##                                           Yes 
##                          Northwestern College 
##                                           Yes 
##                       Northwestern University 
##                                           Yes 
##                            Norwich University 
##                                           Yes 
##                            Notre Dame College 
##                                           Yes 
##                               Oberlin College 
##                                           Yes 
##                            Occidental College 
##                                           Yes 
##                               Ohio University 
##                                            No 
##                   Oklahoma Baptist University 
##                                           Yes 
##                 Oklahoma Christian University 
##                                           Yes 
##                   Ouachita Baptist University 
##                                           Yes 
##               Our Lady of the Lake University 
##                                           Yes 
##                               Pace University 
##                                            No 
##                   Pacific Lutheran University 
##                                           Yes 
##                         Pacific Union College 
##                                           Yes 
##                            Pacific University 
##                                           Yes 
##                     Pembroke State University 
##                                            No 
##                         Pepperdine University 
##                                           Yes 
##                            Peru State College 
##                                            No 
##                           Phillips University 
##                                           Yes 
##                             Pikeville College 
##                                           Yes 
##                                Pitzer College 
##                                           Yes 
##                        Polytechnic University 
##                                           Yes 
##             Prairie View A. and M. University 
##                                            No 
##                          Presbyterian College 
##                                           Yes 
##                          Princeton University 
##                                           Yes 
##                            Providence College 
##                                           Yes 
##           Purdue University at West Lafayette 
##                                            No 
##                                Queens College 
##                                           Yes 
##                            Quinnipiac College 
##                                           Yes 
##                            Radford University 
##                                            No 
##                Randolph-Macon Woman's College 
##                                           Yes 
##                                 Regis College 
##                                           Yes 
##              Rensselaer Polytechnic Institute 
##                                           Yes 
##                                 Ripon College 
##                                           Yes 
##                                Rivier College 
##                                           Yes 
##                               Roanoke College 
##                                           Yes 
##                             Rockhurst College 
##                                           Yes 
##                        Rocky Mountain College 
##                                           Yes 
##                     Roger Williams University 
##                                           Yes 
##                               Rollins College 
##                                           Yes 
##                   Rowan College of New Jersey 
##                                            No 
##                      Rutgers at New Brunswick 
##                                            No 
##                       Sacred Heart University 
##                                           Yes 
##                          Saint Anselm College 
##                                           Yes 
##                  Saint Cloud State University 
##                                            No 
##                       Saint John's University 
##                                           Yes 
##                     Saint Joseph's College IN 
##                                           Yes 
##                        Saint Joseph's College 
##                                           Yes 
##                     Saint Joseph's University 
##                                           Yes 
##                          Saint Joseph College 
##                                           Yes 
##                        Saint Louis University 
##                                           Yes 
##                          Saint Mary's College 
##                                           Yes 
##               Saint Mary-of-the-Woods College 
##                                           Yes 
##                       Saint Michael's College 
##                                           Yes 
##                         Saint Vincent College 
##                                           Yes 
##                       Salem-Teikyo University 
##                                           Yes 
##                                 Salem College 
##                                           Yes 
##                    San Diego State University 
##                                            No 
##                        Santa Clara University 
##                                           Yes 
##                        Sarah Lawrence College 
##                                           Yes 
##              Savannah Coll. of Art and Design 
##                                           Yes 
##                             Schreiner College 
##                                           Yes 
##                               Scripps College 
##                                           Yes 
##                    Seattle Pacific University 
##                                           Yes 
##                         Seton Hall University 
##                                           Yes 
##                            Seton Hill College 
##                                           Yes 
##                                 Siena College 
##                                           Yes 
##                               Simmons College 
##                                           Yes 
##                               Simpson College 
##                                           Yes 
##                                 Smith College 
##                                           Yes 
##                 South Dakota State University 
##                                            No 
##           Southeast Missouri State University 
##                                            No 
##             Southeastern Oklahoma State Univ. 
##                                            No 
##                   Southern California College 
##                                           Yes 
##  Southern Illinois University at Edwardsville 
##                                            No 
##                 Southern Methodist University 
##                                           Yes 
##           Southwest Missouri State University 
##                                            No 
##                    Southwest State University 
##                                            No 
##                       Southwestern University 
##                                           Yes 
##                               Spelman College 
##                                           Yes 
##                          Spring Arbor College 
##                                           Yes 
##                       St. John Fisher College 
##                                           Yes 
##                       St. Lawrence University 
##                                           Yes 
##                          St. Martin's College 
##                                           Yes 
##              St. Mary's College of California 
##                                           Yes 
##                St. Mary's College of Maryland 
##                                           Yes 
##          St. Mary's University of San Antonio 
##                                           Yes 
##                           St. Norbert College 
##                                           Yes 
##                    St. Thomas Aquinas College 
##                                           Yes 
##                              Stephens College 
##                                           Yes 
##                Stockton College of New Jersey 
##                                            No 
##                                SUNY at Albany 
##                                            No 
##                            SUNY at Binghamton 
##                                            No 
##                    SUNY College  at Brockport 
##                                            No 
##                       SUNY College  at Oswego 
##                                            No 
##                       SUNY College at Buffalo 
##                                            No 
##                      SUNY College at Cortland 
##                                            No 
##                      SUNY College at Fredonia 
##                                            No 
##                       SUNY College at Geneseo 
##                                            No 
##                     SUNY College at New Paltz 
##                                            No 
##                       SUNY College at Potsdam 
##                                            No 
##                      SUNY College at Purchase 
##                                            No 
##                           Syracuse University 
##                                           Yes 
##                             Talladega College 
##                                           Yes 
##                             Taylor University 
##                                           Yes 
##             Texas A&M University at Galveston 
##                                           Yes 
##                    Texas Christian University 
##                                            No 
##                        Texas Lutheran College 
##                                           Yes 
##                     Texas Southern University 
##                                            No 
##                     Texas Wesleyan University 
##                                            No 
##                                   The Citadel 
##                                           Yes 
##                                 Thiel College 
##                                           Yes 
##                       Transylvania University 
##                                           Yes 
##                         Trenton State College 
##                                            No 
##                            Trinity College DC 
##                                           Yes 
##                            Trinity University 
##                                           Yes 
##                             Tulane University 
##                                           Yes 
##                              Union College KY 
##                                           Yes 
##                              Union College NY 
##                                           Yes 
##                 Univ. of Wisconsin at OshKosh 
##                                            No 
##           University of Alabama at Birmingham 
##                                            No 
##        University of Arkansas at Fayetteville 
##                                            No 
##          University of California at Berkeley 
##                                            No 
##            University of California at Irvine 
##                                            No 
##                      University of Charleston 
##                                           Yes 
##                         University of Chicago 
##                                           Yes 
##                          University of Dallas 
##                                           Yes 
##                        University of Delaware 
##                                            No 
##                          University of Denver 
##                                           Yes 
##                      University of Evansville 
##                                           Yes 
##                         University of Florida 
##                                            No 
##                         University of Georgia 
##                                            No 
##                        University of Hartford 
##                                           Yes 
##                 University of Hawaii at Manoa 
##                                            No 
##               University of Illinois - Urbana 
##                                            No 
##             University of Illinois at Chicago 
##                                            No 
##                          University of Kansas 
##                                            No 
##                        University of La Verne 
##                                           Yes 
##                University of Maine at Machias 
##                                           Yes 
##    University of Maryland at Baltimore County 
##                                            No 
##        University of Maryland at College Park 
##                                            No 
##                           University of Miami 
##                                           Yes 
##           University of Michigan at Ann Arbor 
##                                            No 
##             University of Minnesota at Duluth 
##                                            No 
##             University of Minnesota at Morris 
##                                           Yes 
##           University of Minnesota Twin Cities 
##                                            No 
##                     University of Mississippi 
##                                            No 
##            University of Missouri at Columbia 
##                                            No 
##         University of Missouri at Saint Louis 
##                                            No 
##                          University of Mobile 
##                                           Yes 
##                     University of New England 
##                                           Yes 
##     University of North Carolina at Asheville 
##                                            No 
##   University of North Carolina at Chapel Hill 
##                                            No 
##    University of North Carolina at Wilmington 
##                                            No 
##                    University of North Dakota 
##                                            No 
##                   University of North Florida 
##                                            No 
##                     University of North Texas 
##                                            No 
##               University of Northern Colorado 
##                                            No 
##                   University of Northern Iowa 
##                                            No 
##                      University of Notre Dame 
##                                           Yes 
##                          University of Oregon 
##                                            No 
##                    University of Pennsylvania 
##                                           Yes 
##                     University of Puget Sound 
##                                           Yes 
##                        University of Richmond 
##                                           Yes 
##                       University of Rochester 
##                                           Yes 
##       University of Sci. and Arts of Oklahoma 
##                                            No 
##                        University of Scranton 
##                                           Yes 
##         University of South Carolina at Aiken 
##                                           Yes 
##      University of South Carolina at Columbia 
##                                            No 
##                   University of South Florida 
##                                            No 
##             University of Southern California 
##                                           Yes 
##               University of Southern Colorado 
##                                            No 
##            University of Southern Mississippi 
##                                            No 
##                   University of St. Thomas MN 
##                                           Yes 
##              University of Texas at Arlington 
##                                            No 
##            University of Texas at San Antonio 
##                                            No 
##                        University of the Arts 
##                                           Yes 
##                           University of Tulsa 
##                                           Yes 
##                            University of Utah 
##                                            No 
##                         University of Vermont 
##                                           Yes 
##                        University of Virginia 
##                                            No 
##                      University of Washington 
##                                            No 
##                    University of West Florida 
##                                            No 
##                 University of Wisconsin-Stout 
##                                            No 
##            University of Wisconsin-Whitewater 
##                                            No 
##          University of Wisconsin at Green Bay 
##                                            No 
##                         University of Wyoming 
##                                            No 
##                               Ursinus College 
##                                           Yes 
##                              Ursuline College 
##                                           Yes 
##                         Vanderbilt University 
##                                           Yes 
##                                Vassar College 
##                                           Yes 
##                          Villanova University 
##                                           Yes 
##              Virginia Commonwealth University 
##                                            No 
##                     Virginia State University 
##                                            No 
##                                 Virginia Tech 
##                                            No 
##                     Virginia Union University 
##                                           Yes 
##                               Viterbo College 
##                                           Yes 
##                              Voorhees College 
##                                           Yes 
##                        Wake Forest University 
##                                           Yes 
##                         Warren Wilson College 
##                                           Yes 
##                              Wartburg College 
##                                           Yes 
##                            Washington College 
##                                           Yes 
##                   Washington State University 
##                                            No 
##                         Washington University 
##                                           Yes 
##                           Wayne State College 
##                                            No 
##                            Waynesburg College 
##                                           Yes 
##                                Webber College 
##                                           Yes 
##                            Webster University 
##                                           Yes 
##                                 Wells College 
##                                           Yes 
##             Wentworth Institute of Technology 
##                                           Yes 
##              West Chester University of Penn. 
##                                            No 
##                West Virginia Wesleyan College 
##                                           Yes 
##                   Western Carolina University 
##                                            No 
##                   Western New England College 
##                                           Yes 
##             Western State College of Colorado 
##                                            No 
##                 Western Washington University 
##                                            No 
##                       Westfield State College 
##                                            No 
##                        Westminster College MO 
##                                           Yes 
##                           Westminster College 
##                                           Yes 
##         Westminster College of Salt Lake City 
##                                           Yes 
##                            Wheaton College IL 
##                                           Yes 
##                        Westminster College PA 
##                                           Yes 
##                              Whittier College 
##                                           Yes 
##                            Widener University 
##                                           Yes 
##                             Wilkes University 
##                                           Yes 
##                      William Woods University 
##                                           Yes 
##                              Williams College 
##                                           Yes 
##                                Wilson College 
##                                           Yes 
##                               Wingate College 
##                                           Yes 
##                       Winona State University 
##                                            No 
##                           Winthrop University 
##                                            No 
##                    Wisconsin Lutheran College 
##                                           Yes 
##                               Wofford College 
##                                           Yes 
##               Worcester Polytechnic Institute 
##                                           Yes 
##                Xavier University of Louisiana 
##                                           Yes 
##                  York College of Pennsylvania 
##                                            No 
## Levels: No Yes
```

**Predictions**
Now use your random forest model to predict on your test set!

```r
rf.preds <- predict(rf.model,test)

table(rf.preds, test$Private)
```

```
##         
## rf.preds  No Yes
##      No   58   1
##      Yes   8 192
```

```r
accuracy <- (53 + 187) / (53 + 9 + 11 + 187)
accuracy
```

```
## [1] 0.9230769
```
It should have performed better than just a single tree, how much better depends on whether you are emasuring recall, precision, or accuracy as the most important measure of the model.
