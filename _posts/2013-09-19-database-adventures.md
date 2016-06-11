---
layout: single
title: Database adventures
date: 2013-09-19 03:12:50.000000000 +03:00
categories:
- post
tags:
- Afghanistan
- database
- PostGIS
- R
- SQL
---

Recently I've set up both a PostgreSQL and MySQL server to host databases related to some of our projects in the [Ward Lab](http://mdwardlab.com/). I should note that I have no idea what I'm doing, and this is the first time I've dealt with databases and how to get them working. It's been a very humbling experience, although in the end, we now have two different databases that can be accessed remotely from a laptop through R or other tools like [Quantum GIS](http://www.qgis.org/):

```r  
# setup connection to database  
library(rgdal)  
dsn <- "PG: dbname='db' host='someIP' port='5432' user='me' password='guest'"

# Load Afghanistan boundary (source: GADM)  
state <- readOGR(dsn, layer="afg_adm0")  
plot(state)  
```

[![Afghanistan]({{ site.url }}/content/2013/afg.png)]({{ site.url }}/content/2013/afg.png)

It all started in the beginning of this summer, when we needed a spatial database to support several GB worth of data related to a forecasting project with, surprise, a heavy spatial component. [PostgreSQL](http://www.postgresql.org/), an open source database system, in conjunction with the [PostGIS](http://postgis.net/) extension, provides a database that can store that amount of data, supports spatial data types like polygon and raster data, and provides a useful number of related functions. With it you can do things like finding intersections between roads (lines), subsetting a gigantic raster dataset covering the entire Earth to just one country, and more.

Long story short, without any background knowledge, getting everything working was a really long and frustrating process that lasted several weeks. With the benefit of hindsight, I've written up some documentation on our [Lab wiki](http://mdwardlab.com/wiki/index.php?title=Main_Page) on how to [setup a PostGIS server on a Mac](http://mdwardlab.com/wiki/index.php?title=C-IED_server_install_and_admin) and configure it for remote access, as well as how to [get started guide for users](http://mdwardlab.com/wiki/index.php?title=C-IED_how_to_get_started). Obviously that is all written with our projects in mind, and pretty rough still, but maybe it's helpful if you're doing this for the first time like I did.

One final comment: yesterday I went through a similar process to set up a MySQL database with remote access through R. It took about 2 hours from start to finish, much of which was spent on adding data. Some of that difference in time is hopefully because I'm a little bit more familiar with databases now, but MySQL does seem to be a bit easier to get going than PostgreSQL.