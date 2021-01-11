---
title: "Section 17 - Interactive Visualizations with Plotly"
author: "Victoria"
date: "10/1/2021"
output: html_document
---



#**Interactive visualizations with Plotly**
Open source library for creating interactive visualizations with the ggplot2 instructions

```r
library(ggplot2)
library(plotly)
#with ggplot
pl <- ggplot(mtcars,aes(mpg,wt)) + geom_point()
print(pl)
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5-1.png)

```r
#with plotly
gpl <- ggplotly(pl)
print(gpl)
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5-2.png)

Go to [https://plotly.com/ggplot2/] for examples of all the types of interactive plots using ggplot2 to plotly
