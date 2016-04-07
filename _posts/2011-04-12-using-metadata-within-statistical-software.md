---
id: 210
title: Using metadata within statistical software
date: 2011-04-12T12:17:08+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=210
permalink: /2011/04/using-metadata-within-statistical-software/
aktt_notify_twitter:
  - no
categories:
  - Data
  - Metadata
  - Statistics
tags:
  - Data
  - DSPL
  - Metadata
  - R
  - Statistics
---
Today is the release of a beta of a package I am writing for the [R statistical package](http://www.r-project.org "R Project") to make it easier for researchers to utilise metadata within R and to make it more worthwhile for statisticians to provide metadata.

Most of the methods for R to import data rely solely on the importing of undocumented data, in fact one of the most common ways to import data is through raw CSVs. However, with the release of [DSPL.R](http://code.google.com/p/dspl-r/ "DSPL.R on Google Code") it is now possible to browse the metadata of a dataset within a statistical package.

For example, the following output is example output from the [US Retail Sales dataset provided by Google](http://code.google.com/apis/publicdata/docs/examples.html "DSPL Examples"):

<pre>&gt; print (prep.dspl("~/example/census-retail-sales.zip"))
DSPL Dataset - For more info see: [www.kidstrythisathome.com/dspl.r]
------------                  or: [code.google.com/apis/publicdata/]

Name : Retail Sales in the U.S.
Description : Monthly Retail Trade and Food Services report
            for the United States. This dataset was prepared by Google based
            on data downloaded from the U.S. Census Bureau.
Concepts : 3  -  Type of business, Seasonality, Retail Sales Volume
Slices   : 1  -  retail_sales_business
Tables   : 3  -  businesses, seasonalities, retail_sales_business_tbl
Topics   : 3  -  Industry, Business, Gender</pre>

As this example shows, a user is able to load in a new dataset, and get an immediate sense for what the dataset contains. By being able to allow a user to be able to understand the meaning behind a dataset, without having to leave the statistical environment, users are able to seamlessly work with their data and metadata within the same interface.

While DSPL is seen as a newcomer to the statistical world, and the R is perceived(albeit wrongly) to be inferior to more established commercial statistical tools, the agility of R and the brevity of the DSPL standard act as a strong indicator of how, given time statistical metadata could become an integral part of the all statistical processes.