---
title: "Section 15 - Data Visualization with R"
author: "Victoria"
date: "7/1/2021"
output: html_document
---



#**Overview of ggplot2**
##ggplot2
Here is the cheat sheet for each kind of plot: {https://rstudio.com/wp-content/uploads/2015/03/ggplot2-cheatsheet.pdf}
Is the most popular data visual package for R
It consists of 3 main layers:
- Geometries  
- Aesthetics  
- Data  
And 3 optional layers:
- Facets  
- Statistics  
- Coordinates

```r
library(ggplot2) #library
pl <- ggplot(data = mtcars,aes(x=mpg, y=hp)) #data and aesthetics
pl + geom_point() #geometry
```

![plot of chunk unnamed-chunk-102](figure/unnamed-chunk-102-1.png)

```r
# DONE!
```
Optional layers
##Facets: allows us to put multiple plots in a single canvas

```r
pl <- ggplot(data = mtcars,aes(x=mpg, y=hp)) + geom_point() #data, aesthetics & geometry
pl + facet_grid(cyl ~ .) #facets, each cyl value has its own plot!
```

![plot of chunk unnamed-chunk-103](figure/unnamed-chunk-103-1.png)

##Statistics: allows us to have a shadow of error (stadistical value)

```r
pl <- ggplot(data = mtcars,aes(x=mpg, y=hp)) + geom_point() #data, aesthetics & geometry
pl + facet_grid(cyl ~ .) + stat_smooth()#facets, each cyl value has its own plot!
```

```
## `geom_smooth()` using method = 'loess' and formula 'y ~ x'
```

![plot of chunk unnamed-chunk-104](figure/unnamed-chunk-104-1.png)
##Coordinates: allows us to set limits of the x and y axis

```r
pl <- ggplot(data = mtcars,aes(x=mpg, y=hp)) + geom_point() #data, aesthetics & geometry
pl2 <- pl + facet_grid(cyl ~ .) + stat_smooth()#facets, each cyl value has its own plot!
pl2 + coord_cartesian(xlim = c(15,25))
```

```
## `geom_smooth()` using method = 'loess' and formula 'y ~ x'
```

![plot of chunk unnamed-chunk-105](figure/unnamed-chunk-105-1.png)
#Theme: to affect the details like fonts, lines, etc.

```r
pl <- ggplot(data = mtcars,aes(x=mpg, y=hp)) + geom_point() #data, aesthetics & geometry
pl2 <- pl + facet_grid(cyl ~ .) + stat_smooth()#facets, each cyl value has its own plot!
pl2 + coord_cartesian(xlim = c(15,25)) + theme_dark()
```

```
## `geom_smooth()` using method = 'loess' and formula 'y ~ x'
```

![plot of chunk unnamed-chunk-106](figure/unnamed-chunk-106-1.png)

#**Histograms**
They are used to plot the **frecuency** of a value in our data frame

```r
library(ggplot2)
library(ggplot2movies)

#Data & Aesthetics layers
pl <- ggplot(movies,aes(x=rating))
#Geometry
pl2 <- pl + geom_histogram(binwidth = 0.1,color="red",fill="pink",alpha=0.4) #the binwidth is the "width" of the values for each block
#alpha controls the transparecy of our blocks
pl3 <- pl2 + xlab("Movie Rating") + ylab("Count")

print(pl3 + ggtitle("Quantity of movie ratings"))
```

![plot of chunk unnamed-chunk-107](figure/unnamed-chunk-107-1.png)

#**Scatterplots**
To show correlations between 2 variables

```r
df <- mtcars
df
```

```
##                      mpg cyl  disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4           21.0   6 160.0 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag       21.0   6 160.0 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710          22.8   4 108.0  93 3.85 2.320 18.61  1  1    4    1
## Hornet 4 Drive      21.4   6 258.0 110 3.08 3.215 19.44  1  0    3    1
## Hornet Sportabout   18.7   8 360.0 175 3.15 3.440 17.02  0  0    3    2
## Valiant             18.1   6 225.0 105 2.76 3.460 20.22  1  0    3    1
## Duster 360          14.3   8 360.0 245 3.21 3.570 15.84  0  0    3    4
## Merc 240D           24.4   4 146.7  62 3.69 3.190 20.00  1  0    4    2
## Merc 230            22.8   4 140.8  95 3.92 3.150 22.90  1  0    4    2
## Merc 280            19.2   6 167.6 123 3.92 3.440 18.30  1  0    4    4
## Merc 280C           17.8   6 167.6 123 3.92 3.440 18.90  1  0    4    4
## Merc 450SE          16.4   8 275.8 180 3.07 4.070 17.40  0  0    3    3
## Merc 450SL          17.3   8 275.8 180 3.07 3.730 17.60  0  0    3    3
## Merc 450SLC         15.2   8 275.8 180 3.07 3.780 18.00  0  0    3    3
## Cadillac Fleetwood  10.4   8 472.0 205 2.93 5.250 17.98  0  0    3    4
## Lincoln Continental 10.4   8 460.0 215 3.00 5.424 17.82  0  0    3    4
## Chrysler Imperial   14.7   8 440.0 230 3.23 5.345 17.42  0  0    3    4
## Fiat 128            32.4   4  78.7  66 4.08 2.200 19.47  1  1    4    1
## Honda Civic         30.4   4  75.7  52 4.93 1.615 18.52  1  1    4    2
## Toyota Corolla      33.9   4  71.1  65 4.22 1.835 19.90  1  1    4    1
## Toyota Corona       21.5   4 120.1  97 3.70 2.465 20.01  1  0    3    1
## Dodge Challenger    15.5   8 318.0 150 2.76 3.520 16.87  0  0    3    2
## AMC Javelin         15.2   8 304.0 150 3.15 3.435 17.30  0  0    3    2
## Camaro Z28          13.3   8 350.0 245 3.73 3.840 15.41  0  0    3    4
## Pontiac Firebird    19.2   8 400.0 175 3.08 3.845 17.05  0  0    3    2
## Fiat X1-9           27.3   4  79.0  66 4.08 1.935 18.90  1  1    4    1
## Porsche 914-2       26.0   4 120.3  91 4.43 2.140 16.70  0  1    5    2
## Lotus Europa        30.4   4  95.1 113 3.77 1.513 16.90  1  1    5    2
## Ford Pantera L      15.8   8 351.0 264 4.22 3.170 14.50  0  1    5    4
## Ferrari Dino        19.7   6 145.0 175 3.62 2.770 15.50  0  1    5    6
## Maserati Bora       15.0   8 301.0 335 3.54 3.570 14.60  0  1    5    8
## Volvo 142E          21.4   4 121.0 109 4.11 2.780 18.60  1  1    4    2
```

```r
# Data & Aesthetics layer
pl <- ggplot(df,aes(x=wt,y=mpg))
# Geometry layer
pl.op1 <- pl + geom_point(size=2,alpha=0.5)
pl.op2<- pl + geom_point(aes(shape=factor(cyl),color=factor(cyl)),size=5) #the size of the points change according to cyl values (this dependency of format and values only works by using aes())

print(pl.op2)
```

![plot of chunk unnamed-chunk-108](figure/unnamed-chunk-108-1.png)
##Color
We can use HEX color arguments too! You can google the HEX code of your favorite color and just paste it as color (#code of the color)

```r
df <- mtcars
# Data & Aesthetics layer
pl <- ggplot(df,aes(x=wt,y=mpg))
# Geometry layer
pl.op2<- pl + geom_point(aes(shape=factor(cyl)),size=5,color="#56ea29") #the size of the points change according to cyl values (this dependency of format and values only works by using aes())

print(pl.op2)
```

![plot of chunk unnamed-chunk-109](figure/unnamed-chunk-109-1.png)

##Scale color gradient
We can set the gradient of colors we want for the scatterplot

```r
df <- mtcars
# Data & Aesthetics layer
pl <- ggplot(df,aes(x=wt,y=mpg))
# Geometry layer
pl1<- pl + geom_point(aes(color=hp),size=5)

pl2 <- pl1 + scale_color_gradient(low = "blue",high = "red")

print(pl2)
```

![plot of chunk unnamed-chunk-110](figure/unnamed-chunk-110-1.png)

#**Barplots**
It's similar to a histogram, but we deal with **categorical data** on the x axis, not with data, the y axis is a count too.

```r
df <- mpg

pl <- ggplot(df,aes(x=class)) #the x axis will be the class of the car
pl + geom_bar(aes(fill=drv))
```

![plot of chunk unnamed-chunk-111](figure/unnamed-chunk-111-1.png)

```r
pl + geom_bar(aes(fill=drv),position = "dodge") 
```

![plot of chunk unnamed-chunk-111](figure/unnamed-chunk-111-2.png)

```r
pl + geom_bar(aes(fill=drv),position = "fill")#we make the color dependent of the drive type to make a stacked bar plot, cool!
```

![plot of chunk unnamed-chunk-111](figure/unnamed-chunk-111-3.png)

```r
#Dodge and fill are types of stacking of the bars
```

#**Boxplots**
TO graph the **quartiles as boxes**, on the x axis should be a categorical or discrete value (we need to use values)
- Bottom and top of the box are: 1st and 3rd quartiles  
- The band in the middle: 2nd quartile (median of the data)  
- The ends of the lines: 1.5x the interquartile range (upper and lower)


```r
df <-  mtcars
head(mtcars)
```

```
##                    mpg cyl disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
## Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
## Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2
## Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1
```

```r
pl <- ggplot(df,aes(x=factor(cyl),y=mpg))

pl + geom_boxplot(aes(fill=factor(cyl))) + coord_flip()
```

![plot of chunk unnamed-chunk-112](figure/unnamed-chunk-112-1.png)

#**2 Variables plotting**

```r
library(ggplot2)
library(ggplot2movies)

pl <- ggplot(movies,aes(x=year,y=rating))
pl2 <- pl + geom_bin2d(binwidth=c(3,1))
pl2 + scale_fill_gradient(low = "blue",high = "red")
```

![plot of chunk unnamed-chunk-113](figure/unnamed-chunk-113-1.png)

```r
#we can also use hexagons, if you wish
pl <- ggplot(movies,aes(x=year,y=rating))
pl2 <- pl + geom_hex()
pl2 + scale_fill_gradient(low = "blue",high = "red")
```

![plot of chunk unnamed-chunk-113](figure/unnamed-chunk-113-2.png)

```r
#Geom to density plot
pl <- ggplot(movies,aes(x=year,y=rating))
pl2 <- pl + geom_density2d_filled()
pl2
```

![plot of chunk unnamed-chunk-113](figure/unnamed-chunk-113-3.png)

```r
#can also be unfilled
pl <- ggplot(movies,aes(x=year,y=rating))
pl2 <- pl + geom_density2d()
pl2
```

![plot of chunk unnamed-chunk-113](figure/unnamed-chunk-113-4.png)

#**Coordinates and faceting**
Coordinates help us to size correctly our plot
Faceting allows us to put more than one plot in the window

```r
library(ggplot2)

#Using coordinates
pl <- ggplot(mpg,aes(x=displ,y=hwy)) + geom_point()
pl + coord_cartesian(xlim = c(1,4),ylim = c(15,30))
```

![plot of chunk unnamed-chunk-114](figure/unnamed-chunk-114-1.png)

```r
print(pl)
```

![plot of chunk unnamed-chunk-114](figure/unnamed-chunk-114-2.png)

```r
#Using facets
pl <- ggplot(mpg,aes(x=displ,y=hwy)) + geom_point()
pl + facet_grid(. ~ cyl) #facet_grid(yaxis ~ xaxis)
```

![plot of chunk unnamed-chunk-114](figure/unnamed-chunk-114-3.png)

```r
pl + facet_grid(drv ~ .)
```

![plot of chunk unnamed-chunk-114](figure/unnamed-chunk-114-4.png)

```r
pl + facet_grid(drv ~ cyl)
```

![plot of chunk unnamed-chunk-114](figure/unnamed-chunk-114-5.png)

#**Themes**
It gives beauty to our plots

```r
library(ggplot2)
library(ggthemes) #it has lots of options of themes

#theme_set(theme_minimal()) #the theme_set sets the theme for ALL the plots in the script otherwise do the below

pl <- ggplot(mtcars,aes(x=wt,y=mpg)) + geom_point() + theme_excel()

print(pl)
```

![plot of chunk unnamed-chunk-115](figure/unnamed-chunk-115-1.png)

#**..ggplot2 Exercises..**
For the first few plots, use the mpg dataset

Histogram of hwy mpg values:

```r
df <- mpg
ggplot(df,aes(x=hwy)) + geom_histogram(fill = "red",alpha = 0.5, bins = 20) + theme_gray()
```

![plot of chunk unnamed-chunk-116](figure/unnamed-chunk-116-1.png)
Barplot of car counts per manufacturer with color fill defined by cyl count

```r
df <- mpg
ggplot(df,aes(x=manufacturer)) + geom_bar(aes(fill=factor(cyl)))
```

![plot of chunk unnamed-chunk-117](figure/unnamed-chunk-117-1.png)
Switch now to use the txhousing dataset that comes with ggplot2

```r
df <- txhousing
ggplot(df,aes(x=sales,y=volume)) + geom_point(aes(color=volume),alpha=0.5)
```

```
## Warning: Removed 568 rows containing missing values (geom_point).
```

![plot of chunk unnamed-chunk-118](figure/unnamed-chunk-118-1.png)

Add a smooth fit line to the scatterplot from above. Hint: You may need to look up geom_smooth()

```r
df <- txhousing
ggplot(df,aes(x=sales,y=volume)) + geom_point(aes(color=volume),alpha=0.5,size=5) + geom_smooth(color = "green")
```

```
## `geom_smooth()` using method = 'gam' and formula 'y ~ s(x, bs = "cs")'
```

```
## Warning: Removed 568 rows containing non-finite values (stat_smooth).
```

```
## Warning: Removed 568 rows containing missing values (geom_point).
```

![plot of chunk unnamed-chunk-119](figure/unnamed-chunk-119-1.png)

