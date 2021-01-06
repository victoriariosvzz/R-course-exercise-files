---
title: "Section 10 - R Lists"
author: "Victoria"
date: "5/1/2021"
output: html_document
---



#**R Lists**
Lists allows **different types of data structure** in the same variable
**NOTE:**lists is more of an organizational tool, dataframes and matrices are to work with data directly

```r
v <- c(1,2,3) #Vector
m <- matrix(1:10,nrow=2) #matrix
df <- mtcars #data frame

class(v)
```

```
## [1] "numeric"
```

```r
class(m)
```

```
## [1] "matrix" "array"
```

```r
class(df)
```

```
## [1] "data.frame"
```
### To create a list

```r
my.list <- list(v,m,df)
my.list
```

```
## [[1]]
## [1] 1 2 3
## 
## [[2]]
##      [,1] [,2] [,3] [,4] [,5]
## [1,]    1    3    5    7    9
## [2,]    2    4    6    8   10
## 
## [[3]]
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
We can also assign names instead of the automatic list order

```r
my.named.list <- list(sample.vec = v, my.matrix = m, sample.df = df)
my.named.list
```

```
## $sample.vec
## [1] 1 2 3
## 
## $my.matrix
##      [,1] [,2] [,3] [,4] [,5]
## [1,]    1    3    5    7    9
## [2,]    2    4    6    8   10
## 
## $sample.df
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
#to call certain elements of the list
my.named.list$my.matrix #to call the matrix with $
```

```
##      [,1] [,2] [,3] [,4] [,5]
## [1,]    1    3    5    7    9
## [2,]    2    4    6    8   10
```

```r
my.named.list[["my.matrix"]]
```

```
##      [,1] [,2] [,3] [,4] [,5]
## [1,]    1    3    5    7    9
## [2,]    2    4    6    8   10
```

```r
my.named.list[[1]]
```

```
## [1] 1 2 3
```

```r
class(my.named.list)
```

```
## [1] "list"
```

```r
#to get the list element in its original format, use the $ method
class(my.named.list$my.matrix)
```

```
## [1] "matrix" "array"
```

```r
double.list <- c(my.named.list,my.named.list) #to combine 2 lists together
```
The best way to get info about the list is with the str function

```r
str(my.named.list)
```

```
## List of 3
##  $ sample.vec: num [1:3] 1 2 3
##  $ my.matrix : int [1:2, 1:5] 1 2 3 4 5 6 7 8 9 10
##  $ sample.df :'data.frame':	32 obs. of  11 variables:
##   ..$ mpg : num [1:32] 21 21 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 ...
##   ..$ cyl : num [1:32] 6 6 4 6 8 6 8 4 4 6 ...
##   ..$ disp: num [1:32] 160 160 108 258 360 ...
##   ..$ hp  : num [1:32] 110 110 93 110 175 105 245 62 95 123 ...
##   ..$ drat: num [1:32] 3.9 3.9 3.85 3.08 3.15 2.76 3.21 3.69 3.92 3.92 ...
##   ..$ wt  : num [1:32] 2.62 2.88 2.32 3.21 3.44 ...
##   ..$ qsec: num [1:32] 16.5 17 18.6 19.4 17 ...
##   ..$ vs  : num [1:32] 0 0 1 1 0 1 0 1 1 1 ...
##   ..$ am  : num [1:32] 1 1 1 0 0 0 0 0 0 0 ...
##   ..$ gear: num [1:32] 4 4 4 3 3 3 3 4 4 4 ...
##   ..$ carb: num [1:32] 4 4 1 1 2 1 4 2 2 4 ...
```

# **Data Input and Output**
###**CSV Input and Output**
CSV are the most common data files to work with data. 
- The first line: indicates the columns names  
- The rest of the rows are data separated by commas

```r
write.csv(mtcars, file = "my_example.csv") #to create a new csv file with an existing data frame
```
To **read a csv file**

```r
ex <- read.csv("another_example.csv") #we create a data frame out of the csv file
```

```
## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
## incomplete final line found by readTableHeader on 'another_example.csv'
```

```r
ex #a data frame!
```

```
##      Name Orders       Date
## 1    John     12 12/05/2016
## 2 Charlie     11 12/06/2016
## 3 Matilda     10 12/07/2016
```

```r
head(ex)
```

```
##      Name Orders       Date
## 1    John     12 12/05/2016
## 2 Charlie     11 12/06/2016
## 3 Matilda     10 12/07/2016
```

```r
tail(ex)
```

```
##      Name Orders       Date
## 1    John     12 12/05/2016
## 2 Charlie     11 12/06/2016
## 3 Matilda     10 12/07/2016
```
To **write to a csv file**

```r
write.csv(ex,file = "my_new_example.csv")
read.csv("my_new_example.csv")
```

```
##   X    Name Orders       Date
## 1 1    John     12 12/05/2016
## 2 2 Charlie     11 12/06/2016
## 3 3 Matilda     10 12/07/2016
```

# **Excel Files with R**

```r
library(readxl) #to call the library
excel_sheets("Sample-Sales-Data.xlsx") #this tells us the name of the sheets that the file has
```

```
## [1] "Sheet1"
```

```r
df <- read_excel("Sample-Sales-Data.xlsx", sheet = "Sheet1")
head(df) #the excel file is read as a data frame
```

```
## # A tibble: 6 x 5
##   Postcode Sales_Rep_ID Sales_Rep_Name  Year  Value
##   <chr>           <dbl> <chr>          <dbl>  <dbl>
## 1 2121              456 Jane            2011 84219.
## 2 2092              789 Ashish          2012 28322.
## 3 2128              456 Jane            2013 81879.
## 4 2073              123 John            2011 44491.
## 5 2134              789 Ashish          2012 71838.
## 6 2162              123 John            2013 64532.
```
Now we can make the regular **data frame operations**

```r
mean(df$Value)
```

```
## [1] 49229.39
```

```r
sum(df$Value)
```

```
## [1] 19199461
```

```r
summary(df)
```

```
##    Postcode          Sales_Rep_ID Sales_Rep_Name          Year     
##  Length:390         Min.   :123   Length:390         Min.   :2011  
##  Class :character   1st Qu.:123   Class :character   1st Qu.:2011  
##  Mode  :character   Median :456   Mode  :character   Median :2012  
##                     Mean   :456                      Mean   :2012  
##                     3rd Qu.:789                      3rd Qu.:2013  
##                     Max.   :789                      Max.   :2013  
##      Value        
##  Min.   :  106.4  
##  1st Qu.:26101.5  
##  Median :47447.4  
##  Mean   :49229.4  
##  3rd Qu.:72277.8  
##  Max.   :99878.5
```

```r
str(df)
```

```
## tibble [390 x 5] (S3: tbl_df/tbl/data.frame)
##  $ Postcode      : chr [1:390] "2121" "2092" "2128" "2073" ...
##  $ Sales_Rep_ID  : num [1:390] 456 789 456 123 789 123 456 789 123 789 ...
##  $ Sales_Rep_Name: chr [1:390] "Jane" "Ashish" "Jane" "John" ...
##  $ Year          : num [1:390] 2011 2012 2013 2011 2012 ...
##  $ Value         : num [1:390] 84219 28322 81879 44491 71838 ...
```
##**Lets use lists to store a whole excel file with different sheets (aka data frames)**
List = whole excel workbook
Data frames = sheets

```r
#To read a simple xlsx file as a dataframe
library(openxlsx)

df.wb <- read.xlsx( "Sample-Sales-Data.xlsx")

#To read a complete workbook of excel as a dataframe
df.complete <- loadWorkbook("Reporte de Actividades (Ago-Dic 2020).xlsx") #to load the workbook
df.sheet1 <- read.xlsx(df.complete,sheet = 1) #to create a dataframe of each sheet
df.sheet2 <- read.xlsx(df.complete,sheet = 2)
df.sheet3 <- read.xlsx(df.complete,sheet = 3)
```
## How to write into an Excel file

```r
df2xl <- mtcars #we create an example data frame to export as an excel file
write.xlsx(df2xl,file = "output_example1")
```
To create a workbook of how many excel sheets we want

```r
## setup a workbook with 3 worksheets
wb <- createWorkbook()
addWorksheet(wb = wb, sheetName = "Sheet 1", gridLines = FALSE)
writeDataTable(wb = wb, sheet = 1, x = iris) #x is the dataframe of info to go on that sheet
addWorksheet(wb = wb, sheetName = "mtcars (Sheet 2)", gridLines = FALSE)
writeData(wb = wb, sheet = 2, x = mtcars)
addWorksheet(wb = wb, sheetName = "Sheet 3", gridLines = FALSE)
writeData(wb = wb, sheet = 3, x = Formaldehyde)
worksheetOrder(wb)
```

```
## [1] 1 2 3
```

```r
names(wb)
```

```
## [1] "Sheet 1"          "mtcars (Sheet 2)" "Sheet 3"
```

```r
worksheetOrder(wb) <- c(1, 3, 2) # switch position of sheets 2 & 3
writeData(wb, 2, 'This is still the "mtcars" worksheet', startCol = 15)
worksheetOrder(wb)
```

```
## [1] 1 3 2
```

```r
names(wb) ## ordering within workbook is not changed
```

```
## [1] "Sheet 1"          "mtcars (Sheet 2)" "Sheet 3"
```

#**SQL with R**
SQL is the most used programming languaged used to interact with databases online
**There are special packages for each database** we have to search in Google: database + R

```r
#install.packages("RODBC")
#RODBC Example of syntax
#library(RODBC)
```
another example

```r
library(RPostgreSQL)
```
And finally google in R-bloggers for examples of the required library

#**Web Scrapping with R**
You need to know HTML, CSS and the %<% R operation to do manual web scrapping (obtaining csv files from websites) **OR** you can enter to [www.import.io] and paste the URL to get the csv file of data
## **Manual method**

```r
#demo(package = "rvest")
#demo(package = "rvest",topic = "tripadvisor") #we'll get a built in tutorial to use it
```

