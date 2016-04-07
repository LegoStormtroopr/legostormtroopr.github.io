---
id: 231
title: 63 years of Australian CPI data
date: 2011-05-02T11:28:41+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=231
permalink: /2011/05/63-years-of-australian-cpi-data/
aktt_notify_twitter:
  - no
categories:
  - Data
  - Metadata
  - Statistics
tags:
  - ABS
  - CPI
  - Data
  - DSPL
---
<p style="text-align: justify;">
  The latest <a title="Australian CPI" href="http://www.abs.gov.au/ausstats/abs@.nsf/mf/6401.0">Australian CPI figures</a> were released last week by the Australian Bureau of Statistics.
</p>

<p style="text-align: justify;">
  Fortunately, each release includes re-weighted indices for each indicator. These cover 11 major topics, including food, clothing, housing and education. Unfortunately, the Excel spreadsheets these are distributed aren&#8217;t the easiest formats to process data from. This is because exporting data from Excel can be time consuming, and the data as it is stored in Excel neglects the hierarchical structure of the CPI indicators.
</p>

<p style="text-align: justify;">
  To help change this, I wrote a few scripts (and lovingly hand-crafted some XML) to help transform the CPI from Excel into a <a title="DSPL Homepage" href="http://code.google.com/apis/publicdata/">DSPL dataset</a>, and have uploaded this into into the <a title="Google Public Data Explorer" href="http://www.google.com/publicdata/directory">Google Public Data Explorer</a>.
</p>

<p style="text-align: justify;">
  The dataset that has been uploaded is based of Table 12 from the <a href="http://www.abs.gov.au/AUSSTATS/abs@.nsf/DetailsPage/6401.0Mar%202011?OpenDocument">Downloads section of the latest CPI page</a>. This dataset includes the indices for each capital city, and Australia, for each level of indicator &#8211; from the broad total CPI to, for example, the more specific &#8220;Food&#8221;, &#8220;Bread and Cereals&#8221; and finally &#8220;Breads&#8221;. There are 12 total broad topic covered, including a miscellaneous group of indices that exclude some of the 11 topics, and there are 144 topics at the finest detail.
</p>

<p style="text-align: justify;">
  The end result is something like this:
</p>

[![](http://i.imgur.com/0535R.png "Hosted by imgur.com")](http://imgur.com/KHV9q "Hosted by imgur.com")

<p style="text-align: justify;">
  If you want to play with the whole dataset, it is available on the <a title="ABS CPI on Google Public Data Explorer" href="http://bit.ly/ABS_CPI" target="_blank">Google Public Data Explorer</a>, or if you would like to download the full DSPL dataset, that is available on the <a href="http://code.google.com/p/dspl-r/downloads/list" target="_blank">DSPL-R downloads page</a>.
</p>

<p style="text-align: justify;">
  Probably one of the more interesting parts was how to create the hierarchical CPI indicators category in DSPL, but I&#8217;ll be following this post up later in the week with a tutorial on how to work with complex datasets.
</p>

<p style="text-align: justify;">
  Update: With the help of a kind statistician from Google the datset is now much better structured. The updated dataset is available here: http://code.google.com/p/dspl-r/downloads/list
</p>