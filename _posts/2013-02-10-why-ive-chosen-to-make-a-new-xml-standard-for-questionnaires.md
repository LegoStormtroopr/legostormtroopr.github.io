---
id: 658
title: 'Why I&#8217;ve chosen to make a new XML standard for questionnaires'
date: 2013-02-10T07:10:11+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=658
permalink: /2013/02/why-ive-chosen-to-make-a-new-xml-standard-for-questionnaires/
categories:
  - Metadata
  - Statistics
tags:
  - "I'll make my own specification with blackjack..."
  - SQBL
---
<div style="width: 510px" class="wp-caption aligncenter">
  <a href="http://xkcd.com/927/"><img alt="XKCD #927" src="http://imgs.xkcd.com/comics/standards.png" width="500" height="283" /></a>
  
  <p class="wp-caption-text">
    Normally I don&#8217;t like XKCD, but this is so true.
  </p>
</div>

I&#8217;ve made no secret of the fact that I&#8217;ve been working on a new format for questionnaires. I recently registered a domain for the [Structured Questionnaire Building Language](http://sqbl.org "Structured Questionnaire Building Language"), and have been [releasing screenshots](http://imgur.com/jnIyb,39BCV "Early Canard Screenshots") and [a video](http://www.youtube.com/watch?v=_FImaXn7EYk "Canard Question Module Editor") of a new tool for questionnaire design that I&#8217;m working on. Considering that I&#8217;ll be covering this work at at least one conference this year, and given my close ties in a few technical communities I felt that it would be good to discuss why this is the case, and answer a few questions that people may have.

### Why is a new format for questionnaire design necessary?

Over the past few years I&#8217;ve done a lot of research analysing how questionnaires are structured in a very generic sense. Given the simplistic nature of the logic traditionally found in paper and electronic questionnaires and their logical similarity to computer programming, I&#8217;ve theorised that it should be possible to use the same methods (and thus the same tools) to supports all questionnaires &#8211; including the oft ignored paper questionnaire. Unfortunately, attempts to improve questionnaires have focus on proprietary or limited use cases, which is why tools and formats such as Blaise, CASES and queXML exist, but generally only support telephone or web surveys. Likewise, all of these attempts have ignore the logical structure in various ways and discouraged questionnaire designers from becoming intimately, and necessarily familiar with the logic of their questionnaires.

SQBL on the other hand is an attempt at designing a specialised format to support the capture of the generic information that describes a questionnaire. Likewise, Canard is a parallel development of a tool to allow a researcher to quickly create this information, as a way to help them create their questionnaire, rather than just document it afterwards.

As a quick aside, if you are interested in this research on _Structured Questionnaire Design,_ I&#8217;m still waiting publication, but if you email me directly, I&#8217;ll be glad to forward you as much as you care to read &#8211; and probably more.

### Why not just use DDI?

Given the superficial overlap between SQBL and DDI, this is not an uncommon question even at this early stage. I&#8217;ve written previously that [writing software for DDI isn&#8217;t easy](http://www.kidstrythisathome.com/2012/11/why-are-there-so-few-survey-design-tools-that-use-ddi/ "Why are there so few survey design tools that use DDI?"), and when trying to write software that is user friendly, and can handle all of the edge cases that DDI does, and operate using the referential structures that make DDI so powerful its hard. Really hard. Given that a format is nothing without the tools to support it, I looked written a [three](http://www.kidstrythisathome.com/2012/08/when-ddi-isnt-enough-xml-schema-extensions-and-ddi/ "When DDI isn’t enough Part 1 – XML Schema Extensions and DDI") [part](http://www.kidstrythisathome.com/2012/08/when-ddi-isnt-enough-part-2-xsi-type-and-ddi/ "When DDI isn’t enough Part 2 – XSI Type and DDI") [essay](http://www.kidstrythisathome.com/2012/09/when-ddi-isnt-enough-part-3-picking-the-right-approach-to-improving-the-standard/ "When DDI isn’t enough Part 3 – Picking the right approach to improving the standard") on how to extend DDI in the necessary ways to support complex questionnaires. However, even this is fraught with trouble as software that writes these extensions would have trouble reading &#8220;un-extended&#8221; DDI. What is needed is a tool that is powerful enough to capture the content required of well structured questionnaires, in a user-friendly way, and it seemed increasingly unlikely that this was possible in DDI.

A counterpoint is to also ask &#8220;why DDI?&#8221; DDI 2 and 3 are exemplary formats when looking at archival and discovery, however this is because both are very flexible, and can capture any and every possible use case &#8211; which is absolutely vital when working in an archive to capture what was done. However, when we turn this around and ask look at formats that can be predictably and reliably written and read what is needed is rigidity and strict structures. While such rigidity could be applied to DDI, it risks fracturing the user base leading to &#8220;archival DDI&#8221;, &#8220;questionnaire DDI&#8221; and who knows what else.

Thus the I deemed the decision to start again, with a strict narrow use case, uncomfortable but necessary.

### What about DDI?

I did some soul searching on this (as much soul searching one can do around picking sides in a &#8216;standards war&#8217;), and realised that there really is no point in &#8220;picking sides&#8221;. SQBL isn&#8217;t perfect and isn&#8217;t yet complete, and more to the point it supports a very narrow use case. If I personally view DDI as an flexible archival format, there is a lot of work necessary to support conversion into and out of it to support discovery and reuse. Likewise, if I view SQBL as a rigid living format for creating questionnaires, the question becomes how to link this relatively limited content with other vital survey information. By definition SQBL has a limit useful timeframe, and once data has been collected (if not earlier) it is no longer necessary so conversion or linkages to other formats become required.

Some where between these overlaps is where DDI and SQBL will handshake, and perhaps in future standards this handshake will be formalised. Which means there is a lot of work on both sides of the fence, that I look forward to playing an active part. But in the interim, and for questionnaire design, I believe SQBL will prove to be a necessary new addition to the wide world of survey research standards.