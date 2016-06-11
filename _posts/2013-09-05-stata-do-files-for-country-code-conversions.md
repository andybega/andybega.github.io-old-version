---
layout: single
title: Stata do files for country code conversions
date: 2013-09-05 21:29:04.000000000 +03:00
categories:
- post
tags:
- country codes
- Stata
meta:
  _edit_last: '19821693'
  _wpas_skip_4719251: '1'
  _wpas_skip_4719248: '1'
  _wpas_skip_4719261: '1'
  _oembed_35bd7fbfa7ce135f91f7cab42cf6dc14: '{{unknown}}'
  _oembed_2784df21ff125fbb5ecf534826140617: '{{unknown}}'
  _oembed_37ba49eafff4646d12655ffb8914b683: '{{unknown}}'
---

Blast from the past, in which I used Stata for things: here are some do files that will convert ISO or string country names/codes to COW country codes.

[Country names to COW [.do]]({{ site.url }}/content/2013/Name_to_COW.do) Do-file that creates COW country codes for a dataset that only has country names in it. The file does not take the current year of an observation into account, and does not adjust for state membership (e.g. there was no unified Germany between 1946 and 1989). It should work fine for any cross-section between 1946 and 2004, or for cross-section time-series datasets if you are not concerned about adjusting for state membership.

[ISO country code to COW [.do]]({{ site.url }}/content/2013/ISO_to_COW.do) Do-file that creates COW country codes for a dataset that only has ISO country codes in it. The file does not take the current year of an observation into account, and does not adjust for state membership (e.g. there was no unified Germany between 1946 and 1989). It should work fine for any cross-section between 1946 and 2004, or for cross-section time-series datasets if you are not concerned about adjusting for state membership.

[Time series ISO to COW [.do]]({{ site.url }}/content/2013/time_series_ISO_to_COW.do) Do-file that creates COW country codes fora dataset that only has ISO country codes in it. The file accurately assigns country codes for the time period 1946 to 2004 according to the COW state membership list, but does not drop any country-years that do not conform to COW. If you want a dataset that conforms to COW, this will allow you to merge your dataset to a blank COW state membership list.