---
title: "Credits"
excerpt: "References"
permalink: /forecasts/credits
sidebar:
  nav: "forecasts"
---

This project was inspired by and is very similar to Jay Ulfelder's coup forecasts for the years 2012 through 2015 ([2012](https://dartthrowingchimp.wordpress.com/2012/01/30/assessing-coup-risk-in-2012/), [2013](https://dartthrowingchimp.wordpress.com/2012/12/21/coup-forecasts-for-2013/), [2014](https://dartthrowingchimp.wordpress.com/2014/01/25/coup-forecasts-for-2014/), [2015](https://dartthrowingchimp.wordpress.com/2015/01/17/statistical-assessments-of-coup-risk-for-2015/). 

I wouldn't have been able to do this without a range of open source and publicly-available software and data. 

### Software

The data and models were all estimated in [R, a free software environment for statistical computing and graphics](https://www.r-project.org). 

- The `hadleyverse` set of packages (`dplyr`, `tidyr`) for data manipulation.
- The `caret`, `glmnet`, and `randomForest` packages for statistical modeling/machine learning.
- `cshapes` for historically accurate country borders. 

### Data

- Powell & Thyne data on coup attempts and outcomes, available at [Clayton Thyne's website](http://www.uky.edu/~clthyn2/coup_data/home.htm) and [Jonathan Powell's website](http://www.jonathanmpowell.com/coup-detat-dataset.html).
- Archigos data on state leaders, available at [Kristian Skrede Gleditsch' website](http://privatewww.essex.ac.uk/~ksg/archigos.html) and [Hein Goemans' website](http://www.rochester.edu/college/faculty/hgoemans/data.htm). 
- Uppsala Conflict Data Program-Peace Research Institute Oslo Armed Conflict data (UCDP-PRIO ACD for short), available at [http://ucdp.uu.se](http://ucdp.uu.se). 
- [FAO Food Price Index](http://www.fao.org/worldfoodsituation/foodpricesindex/en/), a global index of average food prices. 
- Polity regime data by the Center for Systemic Peace, available at [their website](http://www.systemicpeace.org/polityproject.html).
- World Bank World Development Indicators (WDI), available at the [World Bank's website](http://data.worldbank.org/data-catalog/world-development-indicators) or through the [WDI package in R](https://cran.r-project.org/web/packages/WDI/index.html).  

