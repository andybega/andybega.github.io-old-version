---
layout: single
title: Building rgdal from source
date: 2014-10-15 16:45:31.000000000 +03:00
categories:
- programming
tags:
- homebrew
- OS X Mavericks
- PostGIS
- PostgreSQL
- proj
- rgdal
---

My limited knowledge of what happens in Terminal, and thus by extension shell, is mostly driven by PostgreSQL/PostGID/rgdal/RPostgreSQL install errors. In the latest variant of this, `rgdal` throws the following error when attempting to build from source:

<!--more-->

```r
checking PROJ.4: epsg found and readable... no  
Error: proj/epsg not found  
Either install missing proj support files, for example the proj-nad and  proj-epsg RPMs on systems using RPMs, or if installed but not autodetected, set PROJ_LIB to the correct path, and if need be use the --with-proj-share=configure argument.  
```

I have to build from source by the way because the default `rgdal` package for Mac does not include a PostgreSQL driver, meaning I have to build it against another version of GDAL that does. This was another fun thing to discover, but at least is easy to diagnose by checking whether `PostgreSQL` shows up when you run `ogrDrivers()` in R. Anyways, as far as I can tell the problem was that I installed `proj` via [homebrew](http://brew.sh/), a package manager for OS X. As a result although `rgdal` could find the `proj` binary via a symlink, it could not find the `epsg` and related data files that were in a little dark corner by themselves. The solution was to build the package with an option providing the file location manually:

```r
install.packages("rgdal", type = "source", 
  configure.args="--with-proj-share=/usr/local/Cellar/proj/4.8.0/share/proj")  
```

This is I guess exactly what the install error message told me to do.
