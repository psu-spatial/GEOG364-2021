---
title: "Tutorial 8: Summary Statistics"
subtitle: <h5 style="font-style:normal">GEOG-364 - Spatial Analysis</h4>
output: 
  html_document:
    toc: true
    toc_depth: 4
    toc_float: true
    theme: flatly
---


<style>
p.comment {
background-color: #DBDBDB;
padding: 10px;
border: 1px solid black;
margin-left: 0px;
border-radius: 5px;
font-style: normal;
}

h1.title {
  font-weight: bold;
  font-family: Arial;  
}

h2.title {
  font-family: Arial;  
}

</style>


<style type="text/css">
#TOC {
  font-size: 12px;
  font-family: Arial;
}
</style>

\


## Tutorial 8: Summary Statistics

This tutorial is all about exploratory data analysis

 - [**Tutorial 8A: What is a data.frame?**](#Tut8_whatisit)
  <br>
      a. [Understanding the data itself](#Tut8a1_basics)
      b. [Summary Statistics](#Tut8a2_summary)
<br>

<div style="margin-bottom:25px;">
</div>  
### Data.frame introduction {#Tut8a_whatisit}

Most of the data we will look at is in "data.frame" format.  This is a table, just like an excel spreadsheet, with one row for each observation and one column for each variable. Each column has a column name.

In this tutorial, I will focus on in-built R datasets. 

Let's choose one now. I'm going to work with the pirates dataset from the `yarrr` package. We can choose the data here.




```r
library(yarrr)
library(tidyverse)
?pirates
piratedataset <- pirates
```


### Looking at the data itself {#Tut8a1_basics}


To have a look at the data there are many options. You can:

 - click on its name in the environment tab
 - Type its name into the console or into a code chunk (e.g. for our table, type `piratedataset` into the console or a code chunk)
 - Run the command `View(variable_name)` (View is a command from the tidyverse package).<br> This will open the data in a new tab.
 - Run the command `head(variable_name)` to see the first 6 lines or so (good for quick checks)
 - Run the command `glimpse(variable_name)` to get a nice summary.
 - Run the command `names(variable_name)` to get the column names.
 - 
 
<br>
 
For example
 

```r
# Note, there are more columns to the right, use the arrow to see
head(piratedataset)
```

```
##   id    sex age height weight headband college tattoos tchests parrots
## 1  1   male  28 173.11   70.5      yes   JSSFP       9       0       0
## 2  2   male  31 209.25  105.6      yes   JSSFP       9      11       0
## 3  3   male  26 169.95   77.1      yes    CCCC      10      10       1
## 4  4 female  31 144.29   58.5       no   JSSFP       2       0       2
## 5  5 female  41 157.85   58.4      yes   JSSFP       9       6       4
## 6  6   male  26 190.20   85.4      yes    CCCC       7      19       0
##   favorite.pirate sword.type eyepatch sword.time beard.length
## 1    Jack Sparrow    cutlass        1       0.58           16
## 2    Jack Sparrow    cutlass        0       1.11           21
## 3    Jack Sparrow    cutlass        1       1.44           19
## 4    Jack Sparrow   scimitar        1      36.11            2
## 5            Hook    cutlass        1       0.11            0
## 6    Jack Sparrow    cutlass        1       0.59           17
##             fav.pixar grogg
## 1      Monsters, Inc.    11
## 2              WALL-E     9
## 3          Inside Out     7
## 4          Inside Out     9
## 5          Inside Out    14
## 6 Monsters University     7
```
To see what the column names are, you can use the `names(dataset)` command


```r
names(piratedataset)
```

```
##  [1] "id"              "sex"             "age"             "height"         
##  [5] "weight"          "headband"        "college"         "tattoos"        
##  [9] "tchests"         "parrots"         "favorite.pirate" "sword.type"     
## [13] "eyepatch"        "sword.time"      "beard.length"    "fav.pixar"      
## [17] "grogg"
```

Or the glimpse command:


```r
glimpse(piratedataset)
```

```
## Rows: 1,000
## Columns: 17
## $ id              <int> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16,…
## $ sex             <chr> "male", "male", "male", "female", "female", "male", "f…
## $ age             <dbl> 28, 31, 26, 31, 41, 26, 31, 31, 28, 30, 25, 20, 24, 26…
## $ height          <dbl> 173.11, 209.25, 169.95, 144.29, 157.85, 190.20, 158.05…
## $ weight          <dbl> 70.5, 105.6, 77.1, 58.5, 58.4, 85.4, 59.6, 74.5, 68.7,…
## $ headband        <chr> "yes", "yes", "yes", "no", "yes", "yes", "yes", "yes",…
## $ college         <chr> "JSSFP", "JSSFP", "CCCC", "JSSFP", "JSSFP", "CCCC", "J…
## $ tattoos         <dbl> 9, 9, 10, 2, 9, 7, 9, 5, 12, 12, 10, 14, 8, 9, 14, 8, …
## $ tchests         <dbl> 0, 11, 10, 0, 6, 19, 1, 13, 37, 69, 1, 5, 6, 12, 70, 3…
## $ parrots         <dbl> 0, 0, 1, 2, 4, 0, 7, 7, 2, 4, 3, 3, 0, 3, 0, 1, 0, 3, …
## $ favorite.pirate <chr> "Jack Sparrow", "Jack Sparrow", "Jack Sparrow", "Jack …
## $ sword.type      <chr> "cutlass", "cutlass", "cutlass", "scimitar", "cutlass"…
## $ eyepatch        <dbl> 1, 0, 1, 1, 1, 1, 0, 1, 0, 1, 1, 0, 0, 1, 1, 1, 0, 0, …
## $ sword.time      <dbl> 0.58, 1.11, 1.44, 36.11, 0.11, 0.59, 3.01, 0.06, 0.74,…
## $ beard.length    <dbl> 16, 21, 19, 2, 0, 17, 1, 1, 1, 25, 1, 27, 0, 19, 0, 1,…
## $ fav.pixar       <chr> "Monsters, Inc.", "WALL-E", "Inside Out", "Inside Out"…
## $ grogg           <dbl> 11, 9, 7, 9, 14, 7, 9, 12, 16, 9, 7, 8, 12, 7, 9, 10, …
```
To see how many columns and rows there are, you can use the `nrow()` and `ncol()` commands


```r
nrow(piratedataset)
```

```
## [1] 1000
```

```r
ncol(piratedataset)
```

```
## [1] 17
```

### Summary statistics {#Tut8a2_summary}

To look at the summaries there are a load of options. Choose your favourites:

 - `summary(dataset)`
 - `skim(dataset)` in the skimr package
 - `summarize(dataset)` in the papeR package. This looks pretty powerful, I'm just learning it

Or look at the summary


```r
summary(piratedataset) 
```

```
##        id             sex                 age            height     
##  Min.   :   1.0   Length:1000        Min.   :11.00   Min.   :129.8  
##  1st Qu.: 250.8   Class :character   1st Qu.:24.00   1st Qu.:161.4  
##  Median : 500.5   Mode  :character   Median :27.00   Median :169.9  
##  Mean   : 500.5                      Mean   :27.36   Mean   :170.2  
##  3rd Qu.: 750.2                      3rd Qu.:31.00   3rd Qu.:178.5  
##  Max.   :1000.0                      Max.   :46.00   Max.   :209.2  
##      weight         headband           college             tattoos      
##  Min.   : 33.00   Length:1000        Length:1000        Min.   : 0.000  
##  1st Qu.: 62.08   Class :character   Class :character   1st Qu.: 7.000  
##  Median : 69.55   Mode  :character   Mode  :character   Median :10.000  
##  Mean   : 69.74                                         Mean   : 9.429  
##  3rd Qu.: 76.90                                         3rd Qu.:12.000  
##  Max.   :105.60                                         Max.   :19.000  
##     tchests          parrots       favorite.pirate     sword.type       
##  Min.   :  0.00   Min.   : 0.000   Length:1000        Length:1000       
##  1st Qu.:  6.00   1st Qu.: 1.000   Class :character   Class :character  
##  Median : 15.00   Median : 2.000   Mode  :character   Mode  :character  
##  Mean   : 22.69   Mean   : 2.819                                        
##  3rd Qu.: 30.00   3rd Qu.: 4.000                                        
##  Max.   :147.00   Max.   :27.000                                        
##     eyepatch       sword.time        beard.length    fav.pixar        
##  Min.   :0.000   Min.   :  0.0000   Min.   : 0.00   Length:1000       
##  1st Qu.:0.000   1st Qu.:  0.2175   1st Qu.: 0.00   Class :character  
##  Median :1.000   Median :  0.5850   Median : 9.00   Mode  :character  
##  Mean   :0.658   Mean   :  2.5427   Mean   :10.38                     
##  3rd Qu.:1.000   3rd Qu.:  1.3300   3rd Qu.:20.00                     
##  Max.   :1.000   Max.   :169.8800   Max.   :40.00                     
##      grogg      
##  Min.   : 0.00  
##  1st Qu.: 8.00  
##  Median :10.00  
##  Mean   :10.14  
##  3rd Qu.:12.00  
##  Max.   :21.00
```

In the skimr library there is the skim command


```r
library(skimr)
skim(piratedataset) 
```


<table style='width: auto;'
        class='table table-condensed'>
<caption>Data summary</caption>
 <thead>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:left;">   </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Name </td>
   <td style="text-align:left;"> piratedataset </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Number of rows </td>
   <td style="text-align:left;"> 1000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Number of columns </td>
   <td style="text-align:left;"> 17 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> _______________________ </td>
   <td style="text-align:left;">  </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Column type frequency: </td>
   <td style="text-align:left;">  </td>
  </tr>
  <tr>
   <td style="text-align:left;"> character </td>
   <td style="text-align:left;"> 6 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> numeric </td>
   <td style="text-align:left;"> 11 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> ________________________ </td>
   <td style="text-align:left;">  </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Group variables </td>
   <td style="text-align:left;"> None </td>
  </tr>
</tbody>
</table>


**Variable type: character**

<table>
 <thead>
  <tr>
   <th style="text-align:left;"> skim_variable </th>
   <th style="text-align:right;"> n_missing </th>
   <th style="text-align:right;"> complete_rate </th>
   <th style="text-align:right;"> min </th>
   <th style="text-align:right;"> max </th>
   <th style="text-align:right;"> empty </th>
   <th style="text-align:right;"> n_unique </th>
   <th style="text-align:right;"> whitespace </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> sex </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:right;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> headband </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 2 </td>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 2 </td>
   <td style="text-align:right;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> college </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:right;"> 5 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 2 </td>
   <td style="text-align:right;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> favorite.pirate </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:right;"> 12 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:right;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> sword.type </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 5 </td>
   <td style="text-align:right;"> 8 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:right;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> fav.pixar </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 2 </td>
   <td style="text-align:right;"> 19 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 15 </td>
   <td style="text-align:right;"> 0 </td>
  </tr>
</tbody>
</table>


**Variable type: numeric**

<table>
 <thead>
  <tr>
   <th style="text-align:left;"> skim_variable </th>
   <th style="text-align:right;"> n_missing </th>
   <th style="text-align:right;"> complete_rate </th>
   <th style="text-align:right;"> mean </th>
   <th style="text-align:right;"> sd </th>
   <th style="text-align:right;"> p0 </th>
   <th style="text-align:right;"> p25 </th>
   <th style="text-align:right;"> p50 </th>
   <th style="text-align:right;"> p75 </th>
   <th style="text-align:right;"> p100 </th>
   <th style="text-align:left;"> hist </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> id </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 500.50 </td>
   <td style="text-align:right;"> 288.82 </td>
   <td style="text-align:right;"> 1.00 </td>
   <td style="text-align:right;"> 250.75 </td>
   <td style="text-align:right;"> 500.50 </td>
   <td style="text-align:right;"> 750.25 </td>
   <td style="text-align:right;"> 1000.00 </td>
   <td style="text-align:left;"> ▇▇▇▇▇ </td>
  </tr>
  <tr>
   <td style="text-align:left;"> age </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 27.36 </td>
   <td style="text-align:right;"> 5.79 </td>
   <td style="text-align:right;"> 11.00 </td>
   <td style="text-align:right;"> 24.00 </td>
   <td style="text-align:right;"> 27.00 </td>
   <td style="text-align:right;"> 31.00 </td>
   <td style="text-align:right;"> 46.00 </td>
   <td style="text-align:left;"> ▁▅▇▃▁ </td>
  </tr>
  <tr>
   <td style="text-align:left;"> height </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 170.23 </td>
   <td style="text-align:right;"> 12.39 </td>
   <td style="text-align:right;"> 129.83 </td>
   <td style="text-align:right;"> 161.36 </td>
   <td style="text-align:right;"> 169.86 </td>
   <td style="text-align:right;"> 178.54 </td>
   <td style="text-align:right;"> 209.25 </td>
   <td style="text-align:left;"> ▁▅▇▅▁ </td>
  </tr>
  <tr>
   <td style="text-align:left;"> weight </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 69.74 </td>
   <td style="text-align:right;"> 10.82 </td>
   <td style="text-align:right;"> 33.00 </td>
   <td style="text-align:right;"> 62.08 </td>
   <td style="text-align:right;"> 69.55 </td>
   <td style="text-align:right;"> 76.90 </td>
   <td style="text-align:right;"> 105.60 </td>
   <td style="text-align:left;"> ▁▃▇▅▁ </td>
  </tr>
  <tr>
   <td style="text-align:left;"> tattoos </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 9.43 </td>
   <td style="text-align:right;"> 3.37 </td>
   <td style="text-align:right;"> 0.00 </td>
   <td style="text-align:right;"> 7.00 </td>
   <td style="text-align:right;"> 10.00 </td>
   <td style="text-align:right;"> 12.00 </td>
   <td style="text-align:right;"> 19.00 </td>
   <td style="text-align:left;"> ▁▃▇▃▁ </td>
  </tr>
  <tr>
   <td style="text-align:left;"> tchests </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 22.69 </td>
   <td style="text-align:right;"> 24.46 </td>
   <td style="text-align:right;"> 0.00 </td>
   <td style="text-align:right;"> 6.00 </td>
   <td style="text-align:right;"> 15.00 </td>
   <td style="text-align:right;"> 30.00 </td>
   <td style="text-align:right;"> 147.00 </td>
   <td style="text-align:left;"> ▇▂▁▁▁ </td>
  </tr>
  <tr>
   <td style="text-align:left;"> parrots </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 2.82 </td>
   <td style="text-align:right;"> 3.21 </td>
   <td style="text-align:right;"> 0.00 </td>
   <td style="text-align:right;"> 1.00 </td>
   <td style="text-align:right;"> 2.00 </td>
   <td style="text-align:right;"> 4.00 </td>
   <td style="text-align:right;"> 27.00 </td>
   <td style="text-align:left;"> ▇▁▁▁▁ </td>
  </tr>
  <tr>
   <td style="text-align:left;"> eyepatch </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 0.66 </td>
   <td style="text-align:right;"> 0.47 </td>
   <td style="text-align:right;"> 0.00 </td>
   <td style="text-align:right;"> 0.00 </td>
   <td style="text-align:right;"> 1.00 </td>
   <td style="text-align:right;"> 1.00 </td>
   <td style="text-align:right;"> 1.00 </td>
   <td style="text-align:left;"> ▅▁▁▁▇ </td>
  </tr>
  <tr>
   <td style="text-align:left;"> sword.time </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 2.54 </td>
   <td style="text-align:right;"> 9.33 </td>
   <td style="text-align:right;"> 0.00 </td>
   <td style="text-align:right;"> 0.22 </td>
   <td style="text-align:right;"> 0.58 </td>
   <td style="text-align:right;"> 1.33 </td>
   <td style="text-align:right;"> 169.88 </td>
   <td style="text-align:left;"> ▇▁▁▁▁ </td>
  </tr>
  <tr>
   <td style="text-align:left;"> beard.length </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 10.38 </td>
   <td style="text-align:right;"> 10.31 </td>
   <td style="text-align:right;"> 0.00 </td>
   <td style="text-align:right;"> 0.00 </td>
   <td style="text-align:right;"> 9.00 </td>
   <td style="text-align:right;"> 20.00 </td>
   <td style="text-align:right;"> 40.00 </td>
   <td style="text-align:left;"> ▇▂▅▂▁ </td>
  </tr>
  <tr>
   <td style="text-align:left;"> grogg </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 10.14 </td>
   <td style="text-align:right;"> 3.07 </td>
   <td style="text-align:right;"> 0.00 </td>
   <td style="text-align:right;"> 8.00 </td>
   <td style="text-align:right;"> 10.00 </td>
   <td style="text-align:right;"> 12.00 </td>
   <td style="text-align:right;"> 21.00 </td>
   <td style="text-align:left;"> ▁▅▇▃▁ </td>
  </tr>
</tbody>
</table>





<br>
<br>


***

Website created and maintained by [Helen Greatrex](https://www.geog.psu.edu/directory/helen-greatrex). Website template by [Noli Brazil](https://nbrazil.faculty.ucdavis.edu/)
