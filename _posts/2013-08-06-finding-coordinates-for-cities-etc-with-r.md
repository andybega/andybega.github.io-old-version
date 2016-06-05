---
layout: single
title: Finding coordinates for cities, etc. with R
date: 2013-08-06 05:54:41.000000000 +03:00
categories:
- post
tags:
- geonames
- R
- spatial
---

The problem: you have data that includes the name of a village or city in which something happened, but not coordinates for that village or city. This seems to be a pretty common problem, or at least I've come across it a few times.

The (or a) solution is to look up the city names with the [GeoNames](http://www.geonames.org/) database. Their website has a search feature and with that it's pretty easy to figure out the coordinates for a city or village name. Of course, that stops being convenient when you are dealing with more than a few city names for which you want coordinates.

So, can we do this in R? Yes, and it's not that difficult. There is a `geonames` package that provides an interface for R. [The documentation](http://cran.r-project.org/web/packages/geonames/geonames.pdf) is pretty short, but the `GNSearch()` function seems to be what we need (under `Searching`). It's main argument is just a pointer to [GeoNames' search arguments](http://www.geonames.org/export/geonames-search.html).

Let's start with some data, in this case 5 cities in Afghanistan for which we'd like geographic coordinates:

```r
library(geonames)

# list of city names (in Afghanistan)  
cities <- c("Gereshk", "Lahkar Gah", "Lashkar Gah", "Marjah", "Nad-e Ali")  
```

That gives:

```r 
> cities  
[1] "Gereshk" "Lashkar Gah" "Marjah" "Nad-e Ali"  
```

Now we need to run them through `GNsearch`. We can restrict the search to Afghanistan with `country="AF"`. But first, since the arguments passed by `GNsearch` to GeoNames are not named (i.e. `...`), I write a convenience function with which we can use `sapply()`. It just takes a city name, passes it to `GNsearch` with the appropriate option to search in Afghanistan, and returns the first search result (I checked that the first result in this case is always the city we want). The result is a list, which we can format into a data frame containing what we want, city name and latitute/longitude:

```r
# conveninence function to look up and format results  
GNsearchAF <- function(x) {  
  res <- GNsearch(name=x, country="AF")  
  return(res[1, ])  
}

# loop over city names and reformat  
GNresult <- sapply(cities, GNsearchAF)  
GNresult <- do.call("rbind", GNresult)  
GNresult <- cbind(city=row.names(GNresult),  
subset(GNresult, select=c("lng", "lat", "adminName1")))  
```

Final data frame:

```r 
> GNresult  
city    lng lat adminName1  
Gereshk Gereshk 64.57005 31.82089 Helmand  
Lashkar Gah Lashkar Gah 64.37161 31.59382 Helmand  
Marjah Marjah 64.11760 31.52112 Helmand  
Nad-e Ali Nad-e Ali 64.23982 31.64286 Helmand  
```

Here is the [complete code](https://gist.github.com/andybega/6159870).

One comment: Writing that convenience function so that I can use `sapply` might be a horrible thing to do. Maybe it would be easier to just write a `for` loop.