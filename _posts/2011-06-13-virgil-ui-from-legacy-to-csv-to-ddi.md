---
id: 325
title: 'Virgil UI &#8211; Converting from legacy to CSV to DDI'
date: 2011-06-13T05:36:32+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=325
permalink: /2011/06/virgil-ui-from-legacy-to-csv-to-ddi/
aktt_notify_twitter:
  - no
categories:
  - Metadata
  - Project
tags:
  - code
  - desktop development
  - Metadata
  - programming
  - Transformation
  - Virgil
---
While my main machine has been out-of-action, I&#8217;ve devoted a more time to one of the first use cases that prompted the development of Virgil &#8211; transforming legacy CSVs into DDI 3.1.

One of the main features of Virgil is the ability to help users transition from legacy systems, using non-standard formats to using DDI as the main data language for managing codes, categories and classifications. Unfortunately, there is no way for any one system to support every format for classifications, however by targeting a lowest-common denominator we can process the bulk of the work. In this case the lowest common denominator is CSVs.

If a user or developer of a legacy system is able to transform their legacy format into one of several different CSV formats supported by Virgil, then they will be able to import, at the least the basic structure and metadata of their codes and classifications into DDI. With most of the code for the conversion tools done, I&#8217;ve begun putting together the wizard interface for Virgil UI, which will also form part of a standalone conversion tool. Within the next few weeks the standalone conversion tool will be ready for release, and made available as open-source with the supporting code.

Below is a list of questions that users and developers may have around how to prepare CSVs for conversion to DDI listing the convertible metadata, preferred CSV structure and developer support. Although there are restricted possibilities for CSV structuring options for conversion, if there is a need for expanding the formats or metadata available for conversion, make your needs known and this can be incorporated in to future development.

* * *

# What metadata will be supported?

A user will be able to import the code values and the hierarchy of a classification, as well as labels and descriptions of categories. Labels and descriptions can be multilingual, and multiple languages per item are able to be imported.

# Will I have to use Virgil-UI to use this converter

No. This converter will be available as a wizard within Virgil, but the UI for the wizard will be available as a standalone program for users who need to convert from a legacy system to DDI. Lastly, as the code will be entirely open-sourced, the Python module that performs the transformations will be able to be imported into any other Python piece of software. Lastly, since the converter module is written entirely using modules from the Python standard libraries, it will be usable by programs using languages that are compatible or have compatible python compilers &#8211; such as Java using Jython[http://www.jython.org/] or .Net using IronPython[http://ironpython.net/].

In summary there will be at least four ways developers and users will be able to implement the Virgil CSV-DDI converter tools.

# What &#8216;formats&#8217; of CSV will be supported?

CSVs are generally without structure, and are just a basic way of storing tabular data, but by using a simple combination of the following code and category forms within a CSV. When picking a structure, it is important that the &#8216;code&#8217; columns come before any &#8216;category&#8217; columns. However, and combination of a code and category column format if created correctly should convert from CSV to DDI without trouble.

## Column options for importing codes and their hierarchy

Referential CSV Codelist
  
Order: Code , Parent
  
Notes: This can be reversed to go Parent, Code. If a parent is blank it is assumed that this node is a top level code in a CodeScheme

<pre>Example:
A, ,
1,A,
2,A,
B, ,
3,B,
4,B,</pre>

### Semi-structured CSV Codelist

Order: (Empty,)*Code,
  
Notes: If the code is the first entry in a row then it is considered a top code in the CodeScheme. Any children of a code should be indented by **only one** column. The columns for labels and descriptions start in different columns depending on level of the hierarchy.

<pre>Example:
A,
 ,1,
 ,2,
B,
 ,3,
 ,4,</pre>

### Aligned Semi-structured CSV Codelist

Order: (Empty,)\*Code,(Empty,)\*
  
Notes: If the code is the first entry in a row then it is considered a top code in the CodeScheme. Any children of a code should be indented by only one column. All nodes should be padded so that the columns for labels and descriptions start in the same columns.

<pre>Example:
A, ,
 ,1,
 ,2,
B, ,
 ,3,
 ,4,</pre>

## Column options for importing multilingual categories

### Prefix-embedded Language

Order: (Label,Description)+
  
Notes: As many languages as needed can be be repeated within the column as long as they have unique language codes.

<pre>Example: en-au;Chocolate,en-au;Confectionery based on the seed of the cacao plant,fr;Chocolat,fr; Confiseries à base de la graine de la plante de cacao</pre>

### Pre-defined Column

Order: (language,Label,Description)+
  
Notes: As many languages as needed can be be repeated within the column as long as they have unique language codes.

<pre>Example: en-au,Strawberries,Tasty fruit that isn't a true berry,fr,Frasie,Fruits savoureux qui n'est pas une baie vrai</pre>

### Monolingual

Order: (Label,Description)
  
Notes: When only importing a single language that isn&#8217;t expressed in the CSV a default language will need to be given when invoking the converter.

<pre>Example: Vegemite,A yeast extract spread only edible by people from Australia. No other translations exist because no one else can stand it.</pre>

# Can this tool support tab-separated files?

Yes. In the wizard users will be given the opportunity to select from a range of delimiter options or enter their own delimiting character. When using this module in other code, it will also support any delimiter as long it is specified when calling the module.

# How should a developer write CSV for the converter?

With no agreed upon standard for CSVs its hard for developers to try and write &#8216;standard&#8217; CSVs. To simplify development and be as lenient as possible the Virgil CSV-DDI converter using the Python CSV module[http://docs.python.org/library/csv.html]. If you are writing your own CSV writer I&#8217;d suggest testing it against this module to make sure it works.

In a nut shell though &#8211; leading and trailing whitespace is trimmed and any entry that contains a comma (or specified delimiter) should be quoted with double (&#8220;) or single (&#8216;) quote marks.

# What will the wizard and standalone converter look like?

Something like this:

<p style="text-align: center;">
  <a title="Bigger version hosted on imgur.com" href="http://imgur.com/4PnRs"><img class="aligncenter" title="PyQT Mockup of the CSV/DDI Converter" src="http://i.imgur.com/4PnRs.png" alt="PyQT Mockup of the CSV/DDI Converter" width="561" height="383" />Click for bigger&#8230;</a>
</p>