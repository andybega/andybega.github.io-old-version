---
layout: single
title: Associating points with polygons in R
date: 2014-03-29 02:29:03.000000000 +02:00
categories:
- programming
tags:
- R
- sp
---

Some time ago I posted on how to [find geographic coordinates given a list of village or city names in R](2013-08-06-finding-coordinates-for-cities-etc-with-r/). Somebody emailed me about how to do the reverse: the person had a list of villages in France along with the population in 2010, and wanted to find which administrative unit each village was located in. The problem boils down to associating points, the village coordinates, with polygons, the administrative division which they are a part of.

The village data look like this:

```r
library(foreign)  
library(gdata)  
library(sp)

munic <- read.xls("France-Population.xlsx")  
head(munic)  
```

```r
Name long lat pop_2010  
1 Aast -0.0887339 43.28919 182.5416  
2 Abainville 5.4947440 48.53057 327.2407  
3 Abancourt 1.7649060 49.69672 687.2479  
4 Abancourt 3.2127010 50.23528 448.1252  
5 Abaucourt 6.2579230 48.89637 285.9438  
6 Abaucourt-Hautecourt 5.5405000 49.19700 93.0353  
```

To find the administrative units in which these villages are we can use the `over()` function from the `sp` package. First, we get data on administrative boundaries from [GADM](http://www.gadm.org/):

```r
load("FRA_adm2.RData")  
adm2 <- gadm; rm(gadm)  
head(adm2@data[, c("NAME_1", "NAME_2")])  
```

```  
NAME_1 NAME_2  
1 Picardie Somme  
2 Haute-Normandie Eure  
3 Haute-Normandie Seine-Maritime  
4 Centre Cher  
5 Centre Eure-et-Loir  
6 Centre Indre
```

The data consist of polygons for France's departments, and includes their names as well as the name of the region they are in in the associated data table. To match up the village coordinates with these polygons we need to also convert the village data frame to a spatial object in R:

```r 
coordinates(munic) <- ~ long + lat  
proj4string(munic) <- proj4string(adm2)  
```

The data already include latitude and longitude columns, which we need to identify as such. The second line is about setting the projection the data are in, without which `over()` will throw an error. The GADM data use WGS 84, which seems to be common for global data, and so it's probably safe to assume that the French village data are also. But this isn't necessarily true, especially with data for a smaller geographic area, which might use a projection that works better for that specific region, e.g. a specific [UTM grid zone](http://en.wikipedia.org/wiki/Universal_Transverse_Mercator_coordinate_system).

The last step is to use `over()` to match up points and polygons. Note that `over()` will work with a variety of other spatial data combinations as well.

```r  
munic <- cbind(munic, over(munic, adm2))  
munic[1:5, c("Name", "pop_2010", "NAME_1", "NAME_2")]
```

```
Name pop_2010 NAME_1 NAME_2  
1 Aast 182.5416 Aquitaine Pyrénées-Atlantiques  
2 Abainville 327.2407 Lorraine Meuse  
3 Abancourt 687.2479 Picardie Oise  
4 Abancourt 448.1252 Nord-Pas-de-Calais Nord  
5 Abaucourt 285.9438 Lorraine Meurthe-et-Moselle  
```