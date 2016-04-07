---
id: 335
title: 'Virgil UI &#8211; Site is live and converter code is now available'
date: 2011-06-19T10:35:01+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=335
permalink: /2011/06/virgil-ui-site-is-live-and-converter-code-is-now-available/
aktt_notify_twitter:
  - no
categories:
  - Data
  - Metadata
  - Project
tags:
  - classification
  - DDI
  - Google Code
  - Release
  - Virgil
---
Virgil UI is now starting to get ready for release to the public, with the first step being that it now has a [Google Code project site](http://code.google.com/p/virgil-ui/ "Virgil UI"), which is starting to include.

The first code to go up in the public repository is the utility code for the CSV to DDI conversion described in the last post. This includes the specialised CSV parser, library to create DDI 3.1 Codes and Categories and a sample command line interface to pull it all together.

For those who can&#8217;t wait for either a GUI tool or an executable command-line app, or just want to play with the code, [feel free to grab the source](http://code.google.com/p/virgil-ui/source/checkout "Virgil UI - Source code"). Keep in mind that this is very much pre-beta and is under active development, but if (or more likely when?) you come across a bug, be sure to report it through the issue tracker on the site. To help folks along a few sample CSVs are included to give developers an idea of the required format for the converter to consumer, but that isn&#8217;t a conclusive list of all the possible combinations of code and category list types.

In lieu of actual usage documentation (which will be added during the week) below is a sample execution:

<pre>python2.7 ./converter_cli.py -i ./test_files/anzsic.ss-pd.csv -c SemiStructured -C PreDefinedColumn -o outfile.xml -d DDIInstance_ID --codeSchemeID=Test_codeSchemeID --categorySchemeID=Test_categorySchemeID
python2.7 ./converter_cli.py                - Needed to execute the script
-i ./test_files/anzsic.ss-pd.csv            - The CSV file to transform
-c SemiStructured                           - The CSV CodeList type (see previous blogpost for more info)
-C PreDefinedColumn                         - The CSV Category type (see previous blogpost for more info)
-o outfile.xml                              - File to save the DDI to, if blank output to console
-d DDIInstance_ID                           - The ID for the new parent DDIInstance of the resultant file
--codeSchemeID=Test_codeSchemeID            - ID for the CodeScheme that will hold the codes - is also part of the prefix for all DDI code IDs
--categorySchemeID=Test_categorySchemeID    - ID for the CategoryScheme that will hold the codes - is also part of the prefix for all DDI category IDs
</pre>

note. This does need Python 2.7 to use some of the more advanced XPath options in ElementTree that the DDI module uses.