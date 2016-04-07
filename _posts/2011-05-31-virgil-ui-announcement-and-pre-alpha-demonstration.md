---
id: 315
title: 'Virgil UI &#8211; Announcement and Pre-alpha demonstration'
date: 2011-05-31T14:49:50+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=315
permalink: /2011/05/virgil-ui-announcement-and-pre-alpha-demonstration/
aktt_notify_twitter:
  - no
categories:
  - Data
  - Metadata
  - Project
tags:
  - category
  - classification
  - code
  - Data
  - DDI
  - desktop development
  - Virgil
---
When I&#8217;m not writing about writing code, I occasionally get to hop into a terminal and tear out a few lines of code. While Ramona was a bit of a bust that needs to revisit the drawing board before its ready to leave the nest, Virgil has taken off. Virgil is something I&#8217;ve been doing in-between other tasks with the sole purpose of allowing users to edit and manage CodeLists managed in DDI. This is based on [work I did mid-last year](http://code.google.com/p/ddi-codescheme-viewer/ "DCV - DDI CodeScheme Viewer - Google Code") to turn DDI Code and Category Schemes into interactive webpages. To support this I&#8217;ve been working on a tool to allow users to properly edit Codelists in DDI.

A CodeList is a combination of two DDI objects, a [CodeScheme](http://www.ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/FieldLevelDocumentation/logicalproduct_xsd/elements/CodeScheme.html "DDI CodeScheme - Field Level Documentation") and a [CategoryScheme](http://www.ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/FieldLevelDocumentation/logicalproduct_xsd/elements/CategoryScheme.html "DDI CategoryScheme - Field Level Documentation") and enables users to manage complex hierarchies of coded information, as small as codifiying &#8220;Yes/No&#8221; responses to managing large industrial classifications.

To demonstrate how this may be done, I&#8217;ve uploaded a screencast of Virgil-UI in action opening a DDI version of the coded hierarchy from the [Australian and New Zealand Standard Industrial Classification (ANZSIC)](http://www.abs.gov.au/ANZSIC "1292.0 - Australian and New Zealand Standard Industrial Classification (ANZSIC), 2006 (Revision 1.0)   ") editing and saving the file.


  
[The video demonstration is available on youtube &#8211; here](http://youtu.be/KKkOZIiH5eg "Virgil UI - DDI CodeList Editor Pre-alpha demonstration - Youtube").

The video got downscaled when it was uploaded (pressing the expand button helps) but for those having trouble understanding whats in the video, the features demo&#8217;d in the video are:

  * Open the ANZLIC DDI File in the Vim text editor and searching for the term &#8220;LOOK HERE&#8221;. This search term isn&#8217;t in the file&#8230; yet
  * Virgil-UI is run and the same file is loaded
  * Data from the DDI File for a Category is loaded and is displayed in English and German
  * The term &#8220;LOOK HERE&#8221; is added to the description of a category and the file is saved
  * The file is then reloaded in the Vim text editor and the term &#8220;LOOK HERE&#8221; searched for
  * The search term &#8220;LOOK HERE&#8221; is found

When ready (hopefully mid-August for open-beta) Virgil-UI will be released under an free open-source licence and will support the following features &#8211; ** Indicates a feature that is fully or partially implemented already
  
** Complete multilingual support, for both the UI and multilingual DDI files.
  
** DDI3.x file support
  
** Full rich-text editing for DDI Descriptions and Labels
  
** Support for Windows, Mac and Linux
  
* Export support for Virgil-Web an existing tool for generating Web-pages from DDI CodeLists
  
* Import from CSV
  
* Drag-and-drop re-ordering of CodeLists

Planned features after the initial release include:
  
* DDI2.x file support
  
* DDI3.x support from a custom-built repository
  
* DDI3.x support from a Colectica repository