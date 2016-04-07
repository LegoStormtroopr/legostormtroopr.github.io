---
id: 6287
title: Two new projects for data management with django
date: 2015-08-09T06:15:22+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=6287
permalink: /2015/08/two-new-projects-for-data-management-with-django/
categories:
  - Data
  - Django
  - Metadata
  - Programming
tags:
  - data interrogator
  - django
  - python
  - spaghetti and meatballs
---
I&#8217;ve recently been working on two new projects through work that I&#8217;ve been able to make open source. These are designed to make data and metadata management with Django much easier to do. While I&#8217;m not in a position to talk about the main work yet, I can talk about the libraries that have sprung out of it:

The first is the &#8220;[Django Data Interrogator](https://github.com/LegoStormtroopr/django-data-interrogator)&#8221; which is a Django app for 1.7 and up that allows anyone to create tables of information from a database that stores django models. I can see this being is handy when you are storing lists of people, products or events and want to be able to produce ad-hoc reports similar to &#8220;People with the number of sales made&#8221;, &#8220;Products with the highest sales, grouped by region&#8221;. At this stage this is done by giving a list of relations from a base &#8216;class&#8217;, more information is available on the Git repo. I should give apologies to a more well known project with the same acronym &#8211; I didn&#8217;t pick the name, and will never acronymise this project.

The second is &#8220;[Django Spaghetti and Meatballs](https://github.com/LegoStormtroopr/django-spaghetti-and-meatballs)&#8221; which is a tool to produce ERD-like diagrams from Django projects &#8211; that depending on the colors, and number of models ,looks kind of like a plate of spaghetti. Once given a list of Django apps, this mines the Django content types table and produces an interactive javascript representation, using [the lovely VisJs library](http://visjs.org/). This has been really useful for prototyping the database, as while Django code is very readable, as the number of models and cross-app connections grew, this gave us a good understanding of how the wider picture looked. The other big advantage is that this uses Python docstrings, Django help text and field definitions to produce all the text in the diagrams. The example below shows a few models in three apps: Django&#8217;s build in Auth models, and the Django [notifications](https://github.com/django-notifications/django-notifications) and [revision](https://github.com/etianen/django-reversion) apps:

<div style="width: 509px" class="wp-caption alignnone">
  <a href="https://github.com/LegoStormtroopr/django-spaghetti-and-meatballs"><img class="" src="https://cloud.githubusercontent.com/assets/2173174/9053053/a45e185c-3ab2-11e5-9ea0-89dafb7ac274.png" alt="A graph of django models" width="499" height="641" /></a>
  
  <p class="wp-caption-text">
    A sample plate of spicy meatballs &#8211; Ingredients: Django Auth, Notifications and Revisions
  </p>
</div>