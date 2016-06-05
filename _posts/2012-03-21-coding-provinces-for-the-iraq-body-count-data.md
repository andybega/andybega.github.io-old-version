---
layout: single
title: Coding provinces for the Iraq Body Count data
date: 2012-03-21 01:34:29.000000000 +02:00
categories:
- post
tags:
- iraq body count
- R
---

The [Iraq Body Count project](http://www.iraqbodycount.org/) collects reports of civilian deaths, and makes their event data publicly available. Each event gives the date, location, description and civilian deaths associated with an incident. Looking at a few examples [[1](http://www.iraqbodycount.org/database/incidents/k18564), [2](http://www.iraqbodycount.org/database/incidents/k18560), [3](http://www.iraqbodycount.org/database/incidents/k18554)], you can see that while the data values for the date and deaths are straightforward, the place values get a little bit complicated. I'm looking for the province in which incidents occurred, so the challenge is to associate each place value with a province.

Using the incident data from 2003 to February 2012, about 27,500 records, I've written an [R script that assign provinces](https://github.com/andybega/Code_IBC_Province/blob/master/code_province.R) to ~95 percent of the records, 26,000.

Here's a basic overview of how it works:

The process basically consists of four steps:

1.  Split the location string into separate words
2.  Identify a candidate word
3.  Strip if of unnecessary parts ("al-", "'s",...)
4.  Check against known city-province list
5.  Repeat until a match is found

Two functions cover steps 3 and 4\. The first strips out the "al-" prefix, which just is an article ("the"), the possessive suffix "'s", and a couple of other characters that are in a words sometimes.

```r  
DelChar <- function(x) {  
word <- sub("al-", "", x, ignore.case = TRUE)  
word <- gsub("'[s]", "", word)  
word <- gsub("[?,']", "", word)  
return(word)  
}  
```

The other function takes a word and checks it against a list of known city and province pairs ("city.prov") to see whether it matches either, and if so returns that province name:

```r  
ProvLook <- function(x) {  
province <- NULL  
repeat {  
if (x %in% city.prov[, 2]) {  
province <- x  
break  
} else if (x %in% city.prov[, 1]) {  
province <- city.prov[(x==city.prov[, 1]), 2]  
break  
} else {  
province <- "no match"  
break  
}  
}  
return(province)  
}  
```

The rest is a loop over the words in location to evaluate each one. It's not very efficient and takes 7 seconds to run over the 27,500 records I'm using, but it's effective enough. Any ideas on how to improve efficiency? I don't know enough to have any clue on this.

I'm pretty happy for now with getting 95 percent of the records, but it would be nice to get all in the future. Here are some ideas for how to do that:

1.  Figure out how to accommodate common misspellings. There are certain patterns in how place names get misspelled. For example, "h" at the end of words that end in a vowel (Basra, Basrah), and repeated or substituted vowels (Qadisiya, Qadisiyya; Baiji, Baaji)
2.  Accomodate place names that consist of more than one word, like "Salman Pak".
3.  Extent the list of known city-province pairs. Ultimately this could become a brute force solution, although unpleasant considering there are ~1,500 uncoded places.