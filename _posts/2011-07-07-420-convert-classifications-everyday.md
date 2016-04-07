---
id: 360
title: 420 convert classifications everyday
date: 2011-07-07T12:37:50+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=360
permalink: /2011/07/420-convert-classifications-everyday/
aktt_notify_twitter:
  - no
categories:
  - Data
  - Metadata
  - Statistics
tags:
  - alcohol
  - classification
  - codelist
  - converter
  - DDI
  - drugs
  - Virgil
---
With the recent release of the new [Australian Standard Classification of Drugs of Concern](http://abs.gov.au/AUSSTATS/abs@.nsf/Lookup/1248.0Main+Features12011?OpenDocument "Australian Standard Classification of Drugs of Concern, 2011") from the ABS, there was the opportunity to field test the Virgil CSV to DDI converter with real data to see how it held up. Fortunately, the classification was released as an [Excel data cube](http://abs.gov.au/AUSSTATS/abs@.nsf/DetailsPage/1248.02011?OpenDocument "1248.0 - Australian Standard Classification of Drugs of Concern, 2011 - Downloads") that conformed almost entirely with the structures that Virgil supports. After a little cleaning of the CSV, it was able to run through the converter without few issues at all. Incidentally the most major error highlighted the massive oversight that the converter fails to add values for the codes! However this has been corrected and changes have been pushed in the svn, and a new version of the Windows tool will be pushed out this weekend.

<div style="width: 688px" class="wp-caption alignnone">
  <a href="http://imgur.com/rp4sz"><img class=" " title="A screen shot of Virgil with the converted classification" src="http://imgur.com/rp4sz.png" alt="A screen shot of Virgil with the converted classification" width="678" height="518" /></a>
  
  <p class="wp-caption-text">
    A screen shot of Virgil with the converted classification
  </p>
</div>

Opening the newly created DDI file in the [Virgil DDI CodeList Editor](http://www.kidstrythisathome.com/2011/05/virgil-ui-announcement-and-pre-alpha-demonstration/ "Virgil UI – Announcement and Pre-alpha demonstration") was another story and pointed out a few flaws with how it handles empty data. With the structure from the Excel file not containing descriptions for any category or any labels for the CodeScheme, there were a few small corrections made to accommodate freshly created DDI, but many of these problems will be ironed out by the time the CodeList editor is available for download.

While the converter hasn&#8217;t been fully integrated into the CodeList Editor, it will shortly be possible to create a single DDI file and import numerous CSV files to create a series of classificatory codelists in a single package. A practical and soon to be realised example would be the [Australian Standard Classification of Drugs of Concern](http://abs.gov.au/AUSSTATS/abs@.nsf/Lookup/1248.0Main+Features12011?OpenDocument "Australian Standard Classification of Drugs of Concern, 2011") with the lists of drugs of concern, forms of drug and methods of consumption codelists all contained in a single machine processable DDI package.

For those who haven&#8217;t been able to download or run the converter, the [output from this example is available for testing](http://www.mediafire.com/?xlgqgfg93i0mhbx "Drugs of Concern DDI file on Mediafire").