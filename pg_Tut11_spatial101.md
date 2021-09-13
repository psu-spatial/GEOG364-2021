---
title: "Tutorial: Spatial 101"
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


## Tutorial 11: Spatial 101

This tutorial is all about creating and manipulating spatial data

 - [**Tutorial 11A: Spatial basics**](#Tut11a_basics)
  <br>
      a. [Why treat spatial differently](#Tut11aa_whatisit)
       <br>
      b. [Map projections](#Tut11ab_proj)
      
   <br>
   
 - [**Tutorial 11B: Vector Data**](#Tut11b_vector)
  <br>
      a. [Marked data](#Tut11ba_mark)
       <br>
      c. [Converting existing data to "spatial"](#Tut11bb_convert)
       <br>
       
       
      d. [Reading in spatial vector data from file](#Tut11bc_read)
       <br>
      e. [Manipulating vector data](#Tut11bd_manip)
       <br>
      f. [Plotting vector data](#Tut11be_plot)
      
   <br>
   
 - [**Tutorial 11C: Raster data**](#Tut11c_raster)
      a. [To come!](#Tut11ca_basic)


<br>

<div style="margin-bottom:25px;">
</div>  
## Tutorial 11A: Spatial basics {#Tut11a_basics}
 
<br>

### Why treat spatial differently {#Tut11aa_whatisit}

Geographical data needs special treatment. As well as standard data analysis, we need to tell R that our data has a spatial location on the Earth's surface.  R needs to understand what units our spatial location is in (e.g. metres, degrees..) and how we want the data to appear on plots and maps.  R also needs to understand the different types of vector data (e.g. what we mean by a "polygon" or "point"). 

To achieve this there are some specialist "spatial" types of data we need to use and several spatial data packages.

We're going to split this tutorial by vector and raster (field) data


<br>

### Map Projections {#Tut11ab_proj}

See here for a great overview: https://source.opennews.org/articles/choosing-right-map-projection/

At its simplest, think of our map projections as the "units" of the x-y-z coordinates of geographic data. For example, here is the same map, but in two different projections.  

 - On the left, the figure is in latitiude/longitude in units of degrees.  


 - On the right the same map is in UTM.  In the UTM system, the Earth is divided into 60 zones. Northing values are given by the metres north, or south (in the southern hemisphere) of the equator. Easting values are established as the number of metres from the central meridian of a zone. 

<div class="figure" style="text-align: center">
<img src="pg_Tut11_markdown_fig1.png" alt="*Examples of geographic coordinate systems for raster data (WGS 84; left, in Lon/Lat degrees) and projected (NAD83 / UTM zone 12N; right, in metres), figure from https://geocompr.robinlovelace.net/spatial-class.html*" width="80%" />
<p class="caption">*Examples of geographic coordinate systems for raster data (WGS 84; left, in Lon/Lat degrees) and projected (NAD83 / UTM zone 12N; right, in metres), figure from https://geocompr.robinlovelace.net/spatial-class.html*</p>
</div>

You can see the UTM zone here 
 
<div class="figure" style="text-align: center">
<img src="pg_Tut11_markdown_fig2.png" alt="Zone 12N: https://epsg.io/32612" width="45%" />
<p class="caption">Zone 12N: https://epsg.io/32612</p>
</div>

Each map projection has a unique numeric code called an EPSG code.  To find them, I tend to use these resources, but in this course I will try to provide the codes

- google & reading the dataset documentation
- https://epsg.io
- https://mangomap.com/robertyoung/maps/69585/what-utm-zone-am-i-in-

<p class="comment">**R is stupid.  It has no idea what units or projection your coordinates are in** </p>

**We need to tell R what units/projection/EPSG code your data is orginally in**

**THEN we need to convert it to the units/projection/EPSG we need for analysis**

We will go into how to do this in each tutorial.



<br>

<div style="margin-bottom:25px;">
</div>   
## Tutorial 11B: Vector Data {#Tut11b_vector}
 
As you know, vector data are "objects" you can "pick up and move around" on a map.  So points, lines, polygons, volumes etc.  

There are several families of commands available to manipulate vector spatial data.

 - **sp** : The original spatial package.
    + Find a detailed tutorial here: https://rspatial.org/raster/spatial/3-vectordata.html
    <br>
 - **terra** : Another new spatial package that we shall ignore.
     + Detailed tutorial here: https://rspatial.org/terra/spatial/3-vectordata.html
    <br>
 - **sf** : A newer spatial package that fits into the tidyverse family.
    + Detailed tutorial here: https://r-spatial.github.io/sf/articles/sf1.html
    <br>
 - **spatstat**: A specific package for point pattern analysis    

Spatial data packages are like competing mafia families.  Some commands will only work with one spatial data type, so normally I will store my spatial data as each type.  e.g. I will name my variables:

 - mydata    :  My raw data (R doesn't understand this is spatial)
 - mydata.sp :  The sp version of my data
 - mydata.sf :  The sf version of my data

<br>

### a. Marked data {#Tut11ba_mark}

It is very important to understand whether your spatial data is "marked".

**Un-marked** vector data means that we just know about the *location* of the spatial objects (points, polygons..).  For example, the location of crimes, the location of city boundaries etc.  We can assess if these objects are clustered together, spread out etc..

![](pg_Tut11_spatial101_files/figure-html/unnamed-chunk-1-1.svg)<!-- -->


**Marked** vector data has some attribute e.g. we know some *information* about each point/polygon. For example, with our weather station data, we know marks such as the Elevation at each location, the distance to the ocean and the average last frost date:

![](pg_Tut11_spatial101_files/figure-html/unnamed-chunk-2-1.svg)<!-- -->


<br>

<div style="margin-bottom:25px;">
</div>   
### b. Converting a data.frame in R to spatial sf{#Tut11bb_convert}

This is only one route, but it's the one I use


#### **Step 1: Check what columns your x and y coordinates are stored in.**

Look at your data! View your data table and note what the column names your x and y data is stored in. Note, these don't have to be fancy spatial names, they can be "elephanT" and "popcorn".  


```r
head(frost)
```

```
## # A tibble: 6 × 8
##   Station    State Type_Fake Avg_DOY_SpringFrost Latitude Longitude Elevation
##   <chr>      <chr> <chr>                   <dbl>    <dbl>     <dbl>     <dbl>
## 1 Valley     AL    City                    110.      34.6     -85.6      1020
## 2 Union      AL    City                     82.3     32.0     -85.8       440
## 3 Saint      AL    Airport                  99.8     34.2     -86.8       800
## 4 Fernandina FL    City                     46.9     30.7     -81.5        13
## 5 Lake       FL    City                     60.6     30.2     -82.6       195
## 6 West       GA    City                     85.6     32.9     -85.2       575
## # … with 1 more variable: Dist_to_Coast <dbl>
```

Here, we can see that the data coordinates are in columns called "Longitude" and "Latitude".

<br> 

#### **Step 2: Check what map projections your x and y coordinates are stored in.**

Look at the data inside your x and y columns.  Is it longitude/latitude in degrees?  A large number (likely metres in UTM), something else?  Look at the documentation of your data for clues.  If you can find the map projection your data is in then you can google the CRS code.

If your data is in long/lat degrees,  then the CRS code 4326 should work.  (I got that from this pdf: https://www.nceas.ucsb.edu/sites/default/files/2020-04/OverviewCoordinateReferenceSystems.pdf)

<br> 

#### **Step 3 Convert to sf using the st_as_sf command**

`st_as_sf (tablename, coords=c(XColumnName,YColumnName),crs=MapProjection)`

For example for our frost data, here is how I turned it into a sf spatial data format.  From step 2, I know this is in long/lat coordinates and the crs is 4326.


```r
frost.sf <- st_as_sf(frost,coords=c("Longitude","Latitude"),crs=4326)
```

Now I can check I did it correctly.  Here is my attempt at plotting the long/lat data directly.  It doesn't look much like the USA!


```r
plot(frost$Longitude,frost$Latitude)
```

![](pg_Tut11_spatial101_files/figure-html/unnamed-chunk-5-1.svg)<!-- -->

But here you can see the shapes of the USA.  R has also tried to plot the marks.  All the spatial commands will now work. 


```r
plot(frost.sf)
```

![](pg_Tut11_spatial101_files/figure-html/unnamed-chunk-6-1.svg)<!-- -->

<br>

#### **Step 4. Check your map projection **

There are a LOAD of ways to check the map projection of your data.  Perhaps the easiest are the `st_crs` and `crs` commands:


```r
st_crs(frost.sf)
```

```
## Coordinate Reference System:
##   User input: EPSG:4326 
##   wkt:
## GEOGCRS["WGS 84",
##     DATUM["World Geodetic System 1984",
##         ELLIPSOID["WGS 84",6378137,298.257223563,
##             LENGTHUNIT["metre",1]]],
##     PRIMEM["Greenwich",0,
##         ANGLEUNIT["degree",0.0174532925199433]],
##     CS[ellipsoidal,2],
##         AXIS["geodetic latitude (Lat)",north,
##             ORDER[1],
##             ANGLEUNIT["degree",0.0174532925199433]],
##         AXIS["geodetic longitude (Lon)",east,
##             ORDER[2],
##             ANGLEUNIT["degree",0.0174532925199433]],
##     USAGE[
##         SCOPE["Horizontal component of 3D system."],
##         AREA["World."],
##         BBOX[-90,-180,90,180]],
##     ID["EPSG",4326]]
```

```r
crs(frost.sf)
```

```
## CRS arguments: +proj=longlat +datum=WGS84 +no_defs
```

Here we can see that we assigned our data to be in Lat/Long, with a datum (the shape of the world) of WGS 84 and EPSG/CRS code 4326.

You can use this command on any sf data to check.

<br>

#### **Step 5. Assign a new map projection **

When we do our plots and analyses, we will often need many layers of data - for example, our points, state borders, city locations, a raster map of temperatures..

Chances are each of these layers is stored using different map projections and units. This means that they won't plot correctly!  

So it's good practice to make sure all your layers have the same map projection.  We do this using the st_transform command:

`yoursfvariable <- st_transform (yoursfvariable, crs=NEWNUMBER)`

E.g apply the st_transform command to your sf data with the new crs, then assign the output to a variable of the same name to overwrite, or a new name to create a new version with our new projection.

<br>

For example, to transform our data to the UTM (the map projection in meters):

1. Go here: https://mangomap.com/robertyoung/maps/69585/what-utm-zone-am-i-in- and choose the zone you want. 
    + *I chose a generic US East Coast zone:  UTM Zone: 18N.*
    
3. You can also choose a "datum" (the shape of the earth's spheroid).
    + *For us, let's always choose __WGS 84__*
    
4. Search for the CRS code of that zone here: https://epsg.io . E.g search `UTM Zone XX WGS 84`
    + *For example for me:  https://epsg.io/?q=UTM+zone+18N+WGS+84*
    + *This brought up code 32618: https://epsg.io/32618*

5. Apply the command.  Here I made three versions, one with lat/long, one with UTM and one with a  polar stereographic projection.  I often add the projection to the end of the variable name to keep things neat.


```r
frost.sf.lonlat <- st_transform(frost.sf, 4326)
frost.sf.utm <- st_transform(frost.sf, 32618)
frost.sf.polar <- st_transform(frost.sf, 3995)
```

<br>

Let's see what we did


```r
crs(frost.sf.lonlat)
```

```
## CRS arguments: +proj=longlat +datum=WGS84 +no_defs
```


```r
# YOU CAN SEE THE MAP UNITS ARE IN METRES!
crs(frost.sf.utm)
```

```
## CRS arguments:
##  +proj=utm +zone=18 +datum=WGS84 +units=m +no_defs
```


```r
crs(frost.sf.polar)
```

```
## CRS arguments:
##  +proj=stere +lat_0=90 +lat_ts=71 +lon_0=0 +x_0=0 +y_0=0 +datum=WGS84
## +units=m +no_defs
```

![](pg_Tut11_spatial101_files/figure-html/unnamed-chunk-13-1.svg)<!-- -->![](pg_Tut11_spatial101_files/figure-html/unnamed-chunk-13-2.svg)<!-- -->![](pg_Tut11_spatial101_files/figure-html/unnamed-chunk-13-3.svg)<!-- -->

<br>

#### **Step 6. Make a sp version **

Now we have the data in the projection we want, let's store an sp version just in case we need it.

To do this we use the "as" command.  change the sf format to "Spatial" (sp) format.  


```r
# NOTE, I have changed the variable name from sf to sp!
frost.sp.lonlat <- as(frost.sf.lonlat, "Spatial")
frost.sp.utm <- as(frost.sf.utm, "Spatial")
frost.sp.polar <- as(frost.sf.polar, "Spatial")
```

For some commands, you might get an error using the sf version, so now you also have a convenient sp version

#### **Step 7. ALL COMMANDS **

Here are all the commands in one place for future labs.  See how i'm using code comments to keep things neat.


```
## [1] "Station"             "State"               "Type_Fake"          
## [4] "Avg_DOY_SpringFrost" "Latitude"            "Longitude"          
## [7] "Elevation"           "Dist_to_Coast"
```

The advantage of naming them this way is that it's now really easy to find stuff in your environment tab.  For example I can immediately see that if I want the latlon sf version of the frost dataset, I would go to frost.sf.lonlat

<img src="pg_Tut11_markdown_fig3.png" width="80%" style="display: block; margin: auto;" />


<br>

<div style="margin-bottom:25px;">
</div>   
### c. Using RNaturalEarth built-in vector datasets{#Tut11bc_read}

Let's now also include some vector-line data on top of our points, but adding in some regional administrative boundaries. In later labs, we will learn how to read in vector data from a file, but this time we are going to use data that is already built into R.  

This is part of the `rnaturalearth` package, which links automatically with the "Natural Earth" dataset, found here: https://www.naturalearthdata.com/features/

First, if you haven't already, download the high-resolution data in rnaturalearth by running this command in the console:


```r
remotes::install_github("ropenscilabs/rnaturalearthhires")
```

For administrative border data, we can use the `ne_countries` or the `ne_states`commands. 

For example, ne_countries will load the entire world borders and assign it to a variable called worldborder.


```r
# You can choose if you want the output to be sf or sp data
worldborder.sf <- ne_countries(scale = "medium", returnclass = "sf")

# st_geometry just means plot the borders
plot(st_geometry(worldborder.sf))
```

![](pg_Tut11_spatial101_files/figure-html/unnamed-chunk-17-1.svg)<!-- -->

```r
# You can choose if you want the output to be sf or sp data
UK.country.sf <- ne_countries(country="united kingdom",returnclass = "sf",scale = "medium")

plot(st_geometry(UK.country.sf))
```

![](pg_Tut11_spatial101_files/figure-html/unnamed-chunk-18-1.svg)<!-- -->

If you want states/regions for your country, you can use the command `ne_states()`.


```r
# You can choose if you want the output to be sf or sp data
UK.regions.sf <- ne_states(country="united kingdom",returnclass = "sf")

plot(st_geometry(UK.regions.sf))
```

![](pg_Tut11_spatial101_files/figure-html/unnamed-chunk-19-1.svg)<!-- -->

Let's improve our frost plot


```r
US.states.sf <-  ne_states(country="united states of america",returnclass = "sf")
# Transform to UTM
US.states.sf.utm <- st_transform(US.states.sf,crs=32618)

plot(st_geometry(frost.sf.utm),col="red",pch=16)
plot(st_geometry(US.states.sf.utm),add=TRUE)
```

![](pg_Tut11_spatial101_files/figure-html/unnamed-chunk-20-1.svg)<!-- -->


<br>

<div style="margin-bottom:25px;">
</div> 
### d. Manipulating sf data{#Tut11bd_manip}

Manipulating your spatial data is actually exactly the same as manipulating your dataframes.  You can access columns, filter, select etc in exactly the same way. You might simply see some additional messages saying that the data comes from a "spatial" data frame.

For example, to print the first 10 rows:


```r
head(frost.sf.lonlat)
```

```
## Simple feature collection with 6 features and 6 fields
## Geometry type: POINT
## Dimension:     XY
## Bounding box:  xmin: -86.82 ymin: 30.18 xmax: -81.47 ymax: 34.57
## Geodetic CRS:  WGS 84
## # A tibble: 6 × 7
##   Station    State Type_Fake Avg_DOY_SpringFrost Elevation Dist_to_Coast
##   <chr>      <chr> <chr>                   <dbl>     <dbl>         <dbl>
## 1 Valley     AL    City                    110.       1020        295.  
## 2 Union      AL    City                     82.3       440        122.  
## 3 Saint      AL    Airport                  99.8       800        252.  
## 4 Fernandina FL    City                     46.9        13          1.15
## 5 Lake       FL    City                     60.6       195         63.0 
## 6 West       GA    City                     85.6       575        187.  
## # … with 1 more variable: geometry <POINT [°]>
```

To filter for just Florida and Alabama stations below 500feet and save to a new variable


```r
frost.FL.sf.lonlat <- dplyr::filter(frost.sf.lonlat, State %in% c("FL","AL"))
frost.FL.sf.lonlat <- dplyr::filter(frost.sf.lonlat, Elevation < 500)
```

To make a table of stations in each state in our new dataset


```r
table(frost.FL.sf.lonlat$State,frost.FL.sf.lonlat$Type_Fake)
```

```
##     
##      Agricultural_Research_Station Airport City
##   AL                             1       0    1
##   FL                             1       0    5
##   GA                             3       3    5
##   NC                             0       1    7
##   SC                             4       2    3
##   VA                             0       3    0
```

Or check the maximum elevation in our new dataset


```r
max(frost.FL.sf.lonlat$Elevation)
```

```
## [1] 490
```


<br>

<div style="margin-bottom:25px;">
</div> 
### e. Plotting vector data{#Tut11be_plot}

See tutorial 12.

<br>

<div style="margin-bottom:25px;">
</div> 
## Tutorial 11C: Raster Data {#Tut11c_raster}

### Raster basics {#Tut11ca_whatisit}

To come!


<br>
<br>


***

Website created and maintained by [Helen Greatrex](https://www.geog.psu.edu/directory/helen-greatrex). Website template by [Noli Brazil](https://nbrazil.faculty.ucdavis.edu/)
