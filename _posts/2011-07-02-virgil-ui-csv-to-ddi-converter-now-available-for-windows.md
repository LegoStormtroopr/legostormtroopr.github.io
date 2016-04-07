---
id: 354
title: 'Virgil UI &#8211; CSV to DDI converter now available for Windows'
date: 2011-07-02T04:57:40+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=354
permalink: /2011/07/virgil-ui-csv-to-ddi-converter-now-available-for-windows/
aktt_notify_twitter:
  - no
categories:
  - Data
  - Metadata
  - Project
tags:
  - category
  - code
  - codelist
  - Virgil
---
The day is finally here &#8211; Virgil c2d is available for Windows. You can [download the zip archive from Google Code.](http://code.google.com/p/virgil-ui/downloads/list "Virgil Downloads - Google Code") In future this will be the place that new versions of the tool will be made available, and I am hoping that as people start using it and bug do get noticed that there will be activity, so be sure to check back often to see if changes are available.

For the time being though, [download a copy of the beta](http://code.google.com/p/virgil-ui/downloads/detail?name=virgil-csv-converter_v0.0.1b.zip "Download Virgil c2d v0.0.1b"), checkout [some of the example CSVs](http://code.google.com/p/virgil-ui/source/browse/trunk/test_data/csv/ "Test CSVs for Virgil c2d") and  [learn about how the different CSV types look](http://www.kidstrythisathome.com/2011/06/virgil-ui-from-legacy-to-csv-to-ddi/ "Virgil UI – Converting from legacy to CSV to DDI").

If you have issues getting the application to run, check the _﻿converter_ui.exe.log_ log file for any errors and be sure to raise a bug through the [issue tracker](http://code.google.com/p/virgil-ui/issues/list "Virgil UI Issue Tracker").  If there are issues getting a file to covert check the structure settings are correct, and check the line that the error dialog indicates may be causing the issue. If you are still unable to get the CSV to convert [raise an issue and attach the offending CSV file](http://code.google.com/p/virgil-ui/issues/list "Virgil UI Issue Tracker") and I&#8217;ll see if the problem can be resolved.

When checking out the example CSVs the filenames give some hints to the structure of the data in them:

  * ss: semi-structured
  * mono: monolingual
  * pd: pre-defined language
  * pe: prefix embedded language

For the other files they have type:

  * anzsic 2006 &#8211; codes and titles.csv &#8212; Semi-strucutred, Monoglingual
  * anzsic.csv &#8212; Semi-strucutred, Monoglingual

&nbsp;