---
id: 189
title: DSPL, SDMX and the future of Data
date: 2011-02-22T10:58:48+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=189
permalink: /2011/02/dspl-sdmx-and-the-future-of-data/
aktt_notify_twitter:
  - yes
aktt_tweeted:
  - 1
categories:
  - Data
  - Metadata
tags:
  - Data
  - DSPL
  - Google
  - SDMX
---
It was [It was](http://www.pcmag.com/article2/0,2817,2380458,00.asp) that Google has made their [Public Data Explorer](http://www.google.com/publicdata/directory) open to the public, so now anyone can upload data. While the data that they have made available is interesting, what is more interesting is the much subtler announcement of their [DataSet Publication Language](http://code.google.com/apis/publicdata/) (DSPL).

DSPL is a data/metadata language specification that basically allows people to describe multi-dimensional, aggregate datasets, along with their appropriate metadata in a structured way. For those of you playing along at home, this is almost identical to the ideas behind [SDMX.](http://www.sdmx.org) Both languages support datasets by essentially defining compound keys of dimensions and their associated measures &#8211; dimensions and metrics in DSPL and key families and measures in SDMX. However, there are three significant differences between the two standards which will impact which one will see the wider adoption.

**1: SDMX was a collaborative effort to meet the needs of a wide banking and statistical community, DSPL was made solely by Google to accommodate the Public Data Explorer.**
  
For good or bad, when making DSPL, Google only had to meet their own needs: design a standard that will help people write data for the Public Data Explorer, it would be good if it was easy. SDMX on the other hand, has had a lot of hands pulling it, which means the standard, as well written as it is, is overly complex and meets more needs than any one agency could every likely encounter. The important thing about the size of the spec, is that it has a near linear relationship to the size of the documentation, which means&#8230;

**2: DSPLs documentation is vastly shorter than SDMX.**
  
When I first began looking at SDMX, the documentation was enormous. To be able to go through the simple task of making a dataset, and adding its metadata required reading through reams of documentation. In the end it was possible, but not without a significant investment of time, and for many people if the time to produce something productive is too long they will start to look elsewhere. However, the documentation for DSPL is light, and easy to understand, such that it took me much less time to start working with the standard productively *****. However, one of the main reasons the documentation is so small is because&#8230;

**3: SDMX manages all data and metadata in XML, DSPL uses XML and CSV
  
** This leads to a huge difference in understanding how to start working with data. DSPL works for the same idea as SDMX that data should be defined according to its dimensions, and that these dimensions should be described as XML to allow people and machines to understand them. However, DSPL manages all its data, ie the actual numbers, as tabular in Comma Separated Value (CSV) files, while SDMX serialises the data in XML constructs &#8211; this is a massive difference.

Any programmer worth their salt can process CSVs: readline, split by commas, do things with values, repeat. There are standard libraries for managing CSVs, it can be imported into most RDBMS and is almost a defacto standard for data &#8211; even Excel supports it. This means that to write a tool to work with DSPL, one only needs to learn one new thing, rather than two. It also acts as an improvement to an existing technology, rather than a completely new idea.

 ****

**4: DSPL is backed by Google, SDMX isn&#8217;t**
  
This is probably the biggest difference of all. Despite the fact that SDMX may be managed by some pretty heavy weight players, weighing in against Google they look like small fry. Google also has the advantage that it has visibility with developers and that will make the big difference between the two. A standard could be the best designed, easiest to learn, and most useful, but if no-one is writing tools for it, if no-one is promoting it, if there aren&#8217;t the resources to work with it, then it is doomed to fail. Google has the ability, experience and resources to drive this ground swell.

So where does this leave our two standards?

Well, hopefully, it leaves them in a position to work with each other. DSPL acts as a great entry point into the more complex SDMX metadata requirements &#8211; an SDMX-Lite almost. This is especially of note, considering that with such a large overlap, it would take little effort to write a tool to convert data between the two standards &#8211; albeit with a lossy conversion between SDMX and DSPL.

However, for either to ignore that the other exists is a dangerous proposition. With each format having the potential to tap into slightly different markets, a division between them would present a split between people who ultimately have similar goals,.

***** One could argue that I was able to understand DSPL so quickly because I had already learned how SDMX worked. One wouldn&#8217;t be wrong, but the point about the difference in documentation holds.