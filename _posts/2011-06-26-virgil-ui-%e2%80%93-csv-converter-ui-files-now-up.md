---
id: 347
title: Virgil UI – CSV Converter UI Files now up
date: 2011-06-26T11:47:13+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=347
permalink: /2011/06/virgil-ui-%e2%80%93-csv-converter-ui-files-now-up/
aktt_notify_twitter:
  - no
categories:
  - Data
  - Metadata
  - Project
tags:
  - category
  - classifications
  - code
  - CSV
  - DDI
  - desktop
  - Virgil
---
Over the week I&#8217;ve been coding away wrapping the CSV to DDI converter module with a nice user interface. Well, after a weekend of work it has _a_ user interface, whether it is nice is in the eye of the beholder. As with the rest of the Virgil project the python code for this tool is available on [Google Code](http://code.google.com/p/virgil-ui/ "Vigril UI on Google Code"). Unfortunately I haven&#8217;t had time to compile this into a Windows executable suitable for novice use, but interested parties are again welcome to download and test the tool from source.

For the curious, I&#8217;ve again recorded a demonstration and put it up on youtube, which is embeded below:



Again there is no audio, but I&#8217;ve included a brief transcription below so people can get a better idea of what the demonstration is trying to illustrate:

  * Open the anzsic.csv file to briefly view the contents of the CSV holding the labels and some descriptions of categories in the 2006 Australia and New Zealand Standard Industrial Classification.
  * Execute the conversion tool,  and load the ansic.csv file
  * Select the correct structure options for the CSV, as per the allowed structures [described in a previous post](http://www.kidstrythisathome.com/2011/06/virgil-ui-from-legacy-to-csv-to-ddi/ "Virgil UI – Converting from legacy to CSV to DDI").
  * Add a default language code and ID prefix for the DDI Instance and all codes and categories.
  * Demoing the preview table, showing how the header row can be ignored.
  * Convert the file, in the background you can see debug text for each code encountered.
  * Open a folder to save, and confirm the folder is empty.
  * Open the newly created file.
  * Add some line breaks to the automatically created XML  and search for a term from the original CSV.

Hopefully by this time next week there will be a fully downloadable Windows executable available for people to try.