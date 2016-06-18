---
layout: single
title: 3d surface plots of GDP vs. event data
slug: 3d-surface-plots
date: 2016-03-03 12:00:00
category: research
tags: [plotly, 3d surface plot]
---

A while ago I <a href="http://andybeger.com/2014/10/06/the-right-kind-of-variance/">wrote a post</a> about how the patterns by which data for cross-national datasets observed over multiple periods, e.g. with country-year or country-month observations, vary is important for modeling and prediction. Here is another way to visualize why this is the case using 3-d surface plots made with <a href="https://plot.ly">Plotly</a>.

[![3d surface plot of logged GDP per capita]({{ site.url }}/content/2016/gdp-logged.png)]({{ site.url }}/content/2016/gdp-logged.png)

The plot shows logged GDP per capita for &gt;150 countries from 1995 to 2013. This is about the time period we cover in our data for <a href="http://rap.sagepub.com/content/1/3/2053168014557511">forecasting irregular leadership changes</a>. Countries are sorted by GDP for the last year with data, which is why the near edge of the plot is smoother than the far end. It's obvious that there are some changes within countries and at rates that differ from other countries, but still most of the variation is between countries.

<!--more-->

The differences are much larger at the high end when we look at the raw, unlogged GDP data:

[![3d surface plot of raw GDP per capita]({{ site.url }}/content/2016/gdp-raw.png)]({{ site.url }}/content/2016/gdp-raw.png)

Yes, there are differences within countries and this is clearer to see with the unlogged data, but overall the surface is pretty flat over the time dimension and sloping or curving over the list of countries on the <em>y</em> dimension.

The reason why variation on one (spatial) or the other (temporal) dimension is important, as I argued in the other post, is that to predict dynamic outcomes like civil war onset, or irregular leadership changes in our case, temporally varying variables are absolutely necessary. Not sufficient by default, but neccessary. Data like GDP, similar structural indicators, and more generally time-invariant or largely invariant variables cannot possibly predict the timing of events.

Now compare the two plots above to what anti-government protests look like:

[![3d surface plot of protest counts]({{ site.url }}/content/2016/protest-count.png)]({{ site.url }}/content/2016/protest-count.png)

That's essentially the same set of countries, and over the same time period, but using monthly rather than annual observations. I also flipped the <em>x</em> and <em>y</em> axes, but that hardly matters, it's spiky either way. The data come from the <a href="https://github.com/andybega/rap-ensemble-forecasting">replication data for the Research &amp; Politics article I linked above</a>, and consist of counts of anti-government protests events in the ICEWS event data. There is more variation over time, and although there are countries with higher mean levels of protests, it's not as pronounced a pattern as it was with GDP. This is the kind of thing that might help pin the timing of events down.

No discussion of event data should probably fail to mention that media-based event data are subject to important biases and irregularities, and that these are crucial for attempts at causal inference. They are not fundamentally a threat to use in prediction sans explanation though.

Creating the plots was pretty easy. There is a <code>plotly</code> R library that allows you to send <code>ggplot2</code> objects to their website, where a bit of clicking and rotating will turn them into interactive 3-d surface plots. Although it seems to not handle missing and ragged--think countries entering at various points in the 60's or 90's--data very well, it's a bit more intuitive than looking at summary means and variances, which in any case might obscure differences like these in the kind of structured data commonly used in IR (country/province/grid cell--year/month)

<a href="https://github.com/andybega/mireg-blogs/tree/master/3d-var-viz">Replication code (3d-var-viz)</a>.

Interactive plots:
<ul>
	<li><a href="https://plot.ly/~andybega/14/gdp-per-capita-ppp-in-constant-2005-international-logged/">GDP per capita, logged</a></li>
	<li><a href="https://plot.ly/~andybega/21/gdp-per-capita-ppp-constant-2005-international/">GDP per capita, raw</a></li>
	<li><a href="https://plot.ly/~andybega/33/anti-government-protests-icews/">Anti-government protests</a></li>
</ul>