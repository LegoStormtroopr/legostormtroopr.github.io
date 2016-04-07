---
id: 6044
title: 'Aristotle-Metadata-Registry &#8211; My worst kept secret'
date: 2015-02-25T11:02:06+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=6044
permalink: /2015/02/aristotle-metadata-registry-my-worst-kept-secret/
categories:
  - Data
  - Metadata
  - Python
  - Web Development
---
About 6 months ago I stopped frequently blogging, as I began work on a project that was not quite ready for a wider audience, but today that period comes to a close.

Over the past year, I have been working on a new piece of open-source software &#8211; [an ISO/IEC 11179 metadata registry](http://metadata-standards.org/11179/index.html). This originally began from my experiences working on the [Meteor Metadata Registry](http://meteor.aihw.gov.au), which gave me an in-depth understanding of the systems and governance issues around the management of metadata across large scale organisations. I believe [Aristotle-MDR](http://bit.ly/aristotle_mdr) provides one of the closest open-source implementations of the information model of Part 6 and the registration workflows of Part 3, in an easy to use and install piece of open-source software.

In that time, Aristotle-MDR has grown to several thousand lines of code, most substantially [over 5000 line of rigorously tested Python code](https://coveralls.io/r/LegoStormtroopr/aristotle-metadata-registry), tested [using a suit of over 500 regression tests](https://travis-ci.org/LegoStormtroopr/aristotle-metadata-registry), and [rich documentation covering installation, configuration and extension](http://aristotle-metadata-registry.readthedocs.org/en/latest/). From a front-end perspective, Aristotle-MDR uses the [Bootstrap](http://getbootstrap.com/), [CKEditor](http://ckeditor.com/) and [jQuery](http://jquery.com/) libraries to provide a seemless, responsive experience, the use of the [About 6 months ago I stopped frequently blogging, as I began work on a project that was not quite ready for a wider audience, but today that period comes to a close.

Over the past year, I have been working on a new piece of open-source software &#8211; [an ISO/IEC 11179 metadata registry](http://metadata-standards.org/11179/index.html). This originally began from my experiences working on the [Meteor Metadata Registry](http://meteor.aihw.gov.au), which gave me an in-depth understanding of the systems and governance issues around the management of metadata across large scale organisations. I believe [Aristotle-MDR](http://bit.ly/aristotle_mdr) provides one of the closest open-source implementations of the information model of Part 6 and the registration workflows of Part 3, in an easy to use and install piece of open-source software.

In that time, Aristotle-MDR has grown to several thousand lines of code, most substantially [over 5000 line of rigorously tested Python code](https://coveralls.io/r/LegoStormtroopr/aristotle-metadata-registry), tested [using a suit of over 500 regression tests](https://travis-ci.org/LegoStormtroopr/aristotle-metadata-registry), and [rich documentation covering installation, configuration and extension](http://aristotle-metadata-registry.readthedocs.org/en/latest/). From a front-end perspective, Aristotle-MDR uses the [Bootstrap](http://getbootstrap.com/), [CKEditor](http://ckeditor.com/) and [jQuery](http://jquery.com/) libraries to provide a seemless, responsive experience, the use of the](http://haystacksearch.org/) search engine provides scalable and accurate search capability, while custom wizards encourage the discovery and reuse metadata at the point of content creation.

One of the guiding principles of Aristotle-MDR has been to not only model 11179 straight-forward fashion, but do so in a way that complies with the extension principles of the standard itself. To this end, while the data model of Aristotle-MDR is and will remain quite bare-bones, it provides a robust, tested framework on which [extensions can be built](http://aristotle-metadata-registry.readthedocs.org/en/latest/extensions/index.html). Already a number of such extensions are being built, including those for the [management of datasets](https://github.com/LegoStormtroopr/aristotle-dataset-extensions), [questionnaires](https://github.com/LegoStormtroopr/mallard-questionnaire-registry), and [performance indicators](https://github.com/LegoStormtroopr/comet-indicator-registry) and for the [sharing of information in the Data Documentation Initiative XML Format](https://github.com/LegoStormtroopr/aristotle-ddi-utils).

In the last 12 months, I have learned a lot as a systems developer, had the opportunity to contribute to several Django-based projects and look forward to sharing Aristotle, [especially at IASSIST 2015](http://iassist2015.pop.umn.edu/) where I aim to present Aristotle-MDR as a stable 1.0 release. In the interim, there is a [demonstration server for Aristotle available](http://bit.ly/aristotle-demo), with two guest accounts and a few hundred example items for people to use, test and possibly break.