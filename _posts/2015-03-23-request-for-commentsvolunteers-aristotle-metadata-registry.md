---
id: 6061
title: Request for comments/volunteers for the Aristotle Metadata Registry
date: 2015-03-23T20:40:51+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=6061
permalink: /2015/03/request-for-commentsvolunteers-aristotle-metadata-registry/
categories:
  - Metadata
  - Project
  - Python
tags:
  - aristotle-mdr
  - django
  - haystack
  - Metadata
  - metadata registry
  - programming
  - python
---
This is a request for comments and volunteers for an open source ISO 11179 metadata registry I have been working on called the Aristotle Metadata Registry (Aristotle-MDR). Aristotle-MDR is a Django/Python application that provides an authoring environment for a wide variety of 11179 compliant metadata objects with a focus to being multilingual. As such, I&#8217;m hoping to raise interest around bug checkers, translators, experienced HTML and Python programmers and data modelers for mapping of ISO 11179 to DDI3.2 (and potentially other formats).

**For the eager:**

  * The github &#8211; <https://github.com/aristotle-mdr/aristotle-metadata-registry/>
  * The demo/dev instance &#8211; <http://aristotle.pythonanywhere.com/>
  * Screenshots &#8211; <https://github.com/aristotle-mdr/aristotle-metadata-registry/wiki/Screenshots>

### Background

Aristotle-MDR is based on the [Australian Institute of Health and Welfare&#8217;s METeOR Registry](http://en.wikipedia.org/wiki/METeOR), an ISO 11179 compliant authoring tool that manages several thousand metadata items for tracking health, community services, hospital and primary care statistics. I have undertaken the Aristotle-MDR project to build upon the ideas behind Meteor, and extend it to improve compliance with 11179, but to also allow for access and discovery using other standards, including DDI and GSIM.

Aristotle-MDR is build on a number of existing open source frameworks, including Django, Haystack, Bootstrap and jQuery which allows it to easily scale from mobile to desktop on the client side, and scale from small shared hosting to full-scale enterprise environments on the server side. Along with the in-built authoring suite is the Haystack search platform which allows for a range of searching solutions from enterprise search such as Solr or Elastisearch, to smaller scale search engines.

The goal of the Aristotle-MDR is to conform to the ISO/IEC 11179 standard as closely as possible, so while it has a limited range of metadata objects, much like the 11179 standard it allows for the easy extension and inclusion of additional items. Among those already available, are extensions for:

  * health indicators: <https://github.com/aristotle-mdr/comet-indicator-registry>
  * datasets: <https://github.com/aristotle-mdr/aristotle-dataset-extensions>
  * glossaries: <https://github.com/aristotle-mdr/aristotle-glossary>

Information on how to create custom objects can be found in the documentation: <http://aristotle-metadata-registry.readthedocs.org/en/latest/extensions/index.html>

Due to the wide variety of needs for users to access information, there is a download extension API that allows for the creation of a wide variety of download formats. Included is the ability to generate PDF versions of content from simple HTML templates, but an additional module allows for the creation of DDI3.2 (at the moment this supports a small number of objects only): <https://github.com/aristotle-mdr/aristotle-ddi-utils>

As mentioned, this is a call for comments and volunteers. First and foremost I&#8217;d appreciate as much help as possible with my mapping of 11179 objects in DDI3.2 (or earlier versions), but also with the translations for the user interface &#8211; which is currently available in English and Swedish (thanks to Olof Olsson). Partial translations into other languages are available thanks to translations in the Django source code, but additional translations around technical terms would be appreciated. More information on how to contribute to translating is available on the wiki: <https://github.com/aristotle-mdr/aristotle-metadata-registry/wiki/Providing-translations>.

To aid with this I&#8217;ve added a few blank translation files in common languages. Once the repository is forked, it should be relatively straightforward to edit these in Github and send a pull request back without having to pull down the entire codebase. These are listed by ISO 639-1 code, and if you don&#8217;t see your own listed let me know and I can quickly pop a boilerplate translation file in.

<https://github.com/aristotle-mdr/aristotle-metadata-registry/tree/master/aristotle_mdr/locale>

If you find bugs or identify areas of work, feel free to raise them either by emailing me or by raising a bug on Github: <https://github.com/aristotle-mdr/aristotle-metadata-registry/issues>