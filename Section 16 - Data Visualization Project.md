---
title: "Section 16 - Data Visualization Project"
author: "Victoria"
date: "10/1/2021"
output: html_document
---



# **Assignment for ggplot2**
Import the ggplot2 data.table libraries and use fread to load the csv file 'Economist_Assignment_Data.csv' into a dataframe called df (Hint: use drop=1 to skip the first column)

```r
temp <- read.csv("Economist_Assignment_Data.csv")
df <- drop(temp[-1]) #to delete the first col of data
head(df)
```

```
##       Country HDI.Rank   HDI CPI            Region
## 1 Afghanistan      172 0.398 1.5      Asia Pacific
## 2     Albania       70 0.739 3.1 East EU Cemt Asia
## 3     Algeria       96 0.698 2.9              MENA
## 4      Angola      148 0.486 2.0               SSA
## 5   Argentina       45 0.797 3.0          Americas
## 6     Armenia       86 0.716 2.6 East EU Cemt Asia
```
Use ggplot() + geom_point() to create a scatter plot object called pl. You will need to specify x=CPI and y=HDI and color=Region as aesthetics

```r
library(ggplot2)
pl <- ggplot(df,aes(x=CPI,y=HDI)) + geom_point(aes(color=Region))

print(pl)
```

![plot of chunk unnamed-chunk-51](figure/unnamed-chunk-51-1.png)
Change the points to be larger empty circles. (You'll have to go back and add arguments to geom_point() and reassign it to pl.) You'll need to figure out what shape= and size=

```r
library(ggplot2)
pl <- ggplot(df,aes(x=CPI,y=HDI)) + geom_point(aes(color=Region), shape=1 ,size=3)

print(pl)
```

![plot of chunk unnamed-chunk-52](figure/unnamed-chunk-52-1.png)
Add geom_smooth(aes(group=1)) to add a trend line

```r
pl <- ggplot(df,aes(x=CPI,y=HDI)) + geom_point(aes(color=Region), shape=1 ,size=3) + geom_smooth(aes(group=1), method="lm", formula = y ~ log(x), se=FALSE, color = "red")

print(pl)
```

![plot of chunk unnamed-chunk-53](figure/unnamed-chunk-53-1.png)
It's really starting to look similar! But we still need to add labels, we can use geom_text! Add geom_text(aes(label=Country)) to pl2 and see what happens. (Hint: It should be way too many labels)

```r
pl <- ggplot(df,aes(x=CPI,y=HDI)) + geom_point(aes(color=Region), shape=1 ,size=3) + geom_smooth(aes(group=1), method="lm", formula = y ~ log(x), se=FALSE, color = "red") + geom_text(aes(label=Country))

print(pl)
```

![plot of chunk unnamed-chunk-54](figure/unnamed-chunk-54-1.png)
Labeling a subset is actually pretty tricky! So we're just going to give you the answer since it would require manually selecting the subset of countries we want to label!

```r
pointsToLabel <- c("Russia", "Venezuela", "Iraq", "Myanmar", "Sudan",
                   "Afghanistan", "Congo", "Greece", "Argentina", "Brazil",
                   "India", "Italy", "China", "South Africa", "Spane",
                   "Botswana", "Cape Verde", "Bhutan", "Rwanda", "France",
                   "United States", "Germany", "Britain", "Barbados", "Norway", "Japan",
                   "New Zealand", "Singapore")

pl <- ggplot(df,aes(x=CPI,y=HDI)) + geom_point(aes(color=Region), shape=1 ,size=3) + geom_smooth(aes(group=1), method="lm", formula = y ~ log(x), se=FALSE, color = "red")  + geom_text(aes(label = Country), color = "gray20", 
                data = subset(df, Country %in% pointsToLabel),check_overlap = TRUE)

print(pl)
```

![plot of chunk unnamed-chunk-55](figure/unnamed-chunk-55-1.png)
Almost there! Still not perfect, but good enough for this assignment. Later on we'll see why interactive plots are better for labeling. Now let's just add some labels and a theme, set the x and y scales and we're done!

Add theme_bw() to your plot and save this to pl4

```r
library(ggthemes)
pl2 <- pl + theme_economist_white() + xlab("Corruption Perceprions Index. 2011 (10=least corrupt)") + ylab("Human Development Index. 2011 (1=Best)") + ggtitle("Curruption and Human development") + xlim(c(0.1,10.1)) + ylim(c(0.01,1))

print(pl2)
```

![plot of chunk unnamed-chunk-56](figure/unnamed-chunk-56-1.png)

