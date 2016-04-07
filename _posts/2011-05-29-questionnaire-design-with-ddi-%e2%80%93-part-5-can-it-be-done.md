---
id: 302
title: 'Questionnaire design with DDI – Part 5: Can it be done?'
date: 2011-05-29T05:40:37+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=302
permalink: /2011/05/questionnaire-design-with-ddi-%e2%80%93-part-5-can-it-be-done/
aktt_notify_twitter:
  - no
categories:
  - Data
  - Statistics
  - Web Development
tags:
  - Best Practice
  - caveat
  - DDI
  - Instrument
  - Survey
  - Transformation
  - Tutorial
---
This is the fifth in a 5 part series of working with questionnaires and surveys managed using the [Data Documentation Initiative XML standard](http://www.ddialliance.org "DDI Alliance Website"). With DDI being an emerging technology, it is important that users are provided with best practises to ensure that they use the standard in a way that is logical, coherent and most importantly usable and reusable. This series of tutorials and discussions is aimed toward users who have some knowledge of DDI and would like to know how to effectively design markup existing and future questionnaires in DDI.

# Part 5: Can it be done?

On the eve of [IASSIST 2011](http://www.rdl.sfu.ca/IASSIST/ "IASSIST 2011"), we are going to look back at the last few tutorials and ask the big question: Can DDI 3.1 be used as a viable format for the creation of online survey instruments? The simple answer is yes, but there are a few caveats.

## Caveat 1: Only use a the transformation of a finalised survey

This is a very basic idea, but one that should be reiterated. When working to create a web survey, there will more than likely be an iterative process of design DDI, transform, examine form, refine DDI, repeat until done. This is a necessary part of development, as noone ever gets it right first time. However, once a form has been transformed there should be organisation sign-off to ensure that that form is never changed again. While the DDI will be versioned meaning the original DDI that the form would be based of would still be there, altering and overriding an in production form can only lead to data issues.

## Caveat 2: Transforming DDI into an e-form a destructive transformation

[InstrumentML as presented in Part 2](http://www.kidstrythisathome.com/2011/05/questionnaire-design-with-ddi-part-2-where-am-i-and-where-do-i-go-next/ "Questionnaire design with DDI – Part 2: Where am I and where do I go next?") is not, and will never be, a part of the DDI 3.1 specification. It is a way to transform the logical structure of DDI into a form easily usable in certain situations. InstrumentML is a way of caching the implied instument flow to make machine processing easier. Likewise, the transformation from DDI to e-form is done to present the information in the DDI in a way that is easier for users to understand.

## Caveat 3: Any changes to a HTML instance of a form will not be pushed back to DDI

It is a fact that no transformation that transforms a logical structure into a visual page will be perfect. So it is reasonalbe to assume that web pages created from DDI may need to be altered. Perhaps a list of options for response is better as a list of radio buttons compared to a drop down list, a line break is needed to alter word flow or the dimensions of text box need to be precise. These types of issues will rise and there are 3 cascading ways of resolving this:

  1. Alter the DDI to match the expected output,
  2. Alter the CSS to alter the presentation,
  3. If neither of the above produce the needed results, then and only then edit the generate HTML

With DDI allowing XHTML tags in most labels to allow semantic markup, this is the first and most appropriate way to alter pages. If what needs to be changes is wording this is also the only place to edit.

An example of where editing the HTML is need is where we have a question based on age where we are measuring labour figures. This is a numeric question, but in this case we have decided the populations below 18 and over 65 will be too small, so we are going to code everything outside these ranges to the codes &#8216;<18&#8242; and &#8216;>65&#8242;. So we have maximums and minumums, and their codes, but on advise from a survey methodologist we won&#8217;t be restricting users from entering figures outside these ranges.
  
However our pre-generated HTML ([based on the suggestions in part 4](http://www.kidstrythisathome.com/2011/05/questionnaire-design-with-ddi-%e2%80%93-part-4-what-can-i-say/ "Questionnaire design with DDI – Part 4: What can I say?")) will bring these across, so in this case we can edit this question to move the minimum from 18 to 0, as age still needs to be above 0 and remove the upper restriction.

## Caveat 4: Final transformations should be packagable to be stored with the DDI

If a DDI instrument was transformed into a PDF format for printing, no good archivist would think twice about storing a copy of this as a manifestation of the instrument. Likewise, when transforming from DDI to other formats to ease machine use, keeping a copy of this is paramount. Software will change, and how one version of a tool transforms the DDI way not always be the same as how another transforms it.

In the instance of Ramona, a package consists of the HTML used to semantically mark the questions, the InstrumentML to contain the logical flow and the the CSS of the presentation layer. By storing this information, examining the survey at a layer date becomes easier for researchers who may no longer have access to the software that did the original transformation.

What is also important is making sure any valid alterations to a form, like those described in the previous caveat, are stored as a part of this package.

## What we have is proof that it can be done, but its not done yet

## <span style="font-weight: normal; font-size: 13px;">As a closing point, people may be wondering if they can see the code that a lot of this information is based on. At this stage I&#8217;m not planning on releasing the code for Ramona just yet, mostly because its not very good. These tutorials are based on things I learned as I went about trying to create a DDI Web-form viewer, and as such it is less production code, and more a bloody narrative showing my battles and trials against what can be a very tough and complex standard.</span>

Over the next few weeks I&#8217;ll be stripping the code down, separating the wheat from the chaff and rewriting large sections of it and with luck by the time EDDI2012 rolls around there should be a full functional DDI eforms tool ready to roll out into production.

This brings to a close this series of tutorials dealing with online survey development in DDI. In the coming weeks I&#8217;ll also start putting together a short introduction to DDI for new users, and spending the bulk of my free time actually writing code, rather than writing about writing code.

And lastly, enjoy IASSIST 2011 everyone!