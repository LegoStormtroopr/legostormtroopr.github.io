---
id: 250
title: 'Questionnaire design with DDI &#8211; Part 1: Will this survey ever end?'
date: 2011-05-18T12:37:43+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=250
permalink: /2011/05/questionnaire-design-with-ddi-part-1-will-this-survey-ever-end/
aktt_notify_twitter:
  - no
categories:
  - Metadata
  - Statistics
tags:
  - Best Practice
  - DDI
  - Questionnaire
  - Ramona
  - Sheri
  - Survey
  - Tutorial
---
<p style="text-align: justify;">
  This is the first in a 5 part series of working with questionnaires and surveys managed using the Data Documentation Initiative XML standard. With DDI being an emerging technology, it is important that users are provided with best practises to ensure that they use the standard in a way that is logical, coherent and most importantly usable and reusable. This series of tutorials and discussions is aimed toward users who have some knowledge of DDI and would like to know how to effectively design markup existing and future questionnaires in DDI.
</p>

<h1 style="text-align: justify;">
  Part 1: Will this survey ever end?
</h1>

<p style="text-align: justify;">
  This is a classic question that survey takers often ask, and not usually that politely. When a survey will end is an important question for users and designers alike, as the time users have to spend filling out a form can impact their likelihood of finishing or even starting a survey. So determining if a survey will end is of vital importance for users of DDI.<br /> Unfortunately, the answer, based on simple analysis is that you can never tell. DDI uses a unique methodology of using complex referencing between sequencing objects to build up the structure of a questionnaire in a way that is highly reusable. Take for example the following pseudo-survey:
</p>

<pre>Survey: All about You!
    Part 1: Feelings
        Q1: Are you feeling happy today?
        Q2: How do warm summer days make you feel?
    Part 2: Favourites
        Q3: What is your favourite icde-cream?
        Q4: What is your animal?</pre>

<p style="text-align: justify;">
  Now, restructuring this in a way more analgous with DDI gives:
</p>

<pre>Sequence id="Part 1" title="Feelings"
    question reference: Q1: Are you feeling happy today?
    question reference: Q2: How do warm summer days make you feel?
Sequence id="Part 2" title="Favourites"
    question reference: Q3: What is your favourite ice-cream?
    question reference: Q4: What is your animal?
Instrument id="survey" title="All about You!"
    sequence reference: Part 1
    sequence reference: Part 2</pre>

<p style="text-align: justify;">
  The important thing to notice is that both Part 1 and 2 and the main survey are all the same structure: a <a title="DDI Sequence" href="http://www.ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/FieldLevelDocumentation/datacollection_xsd/elements/Sequence.html">DDI Sequence</a>. In DDI, to increase reusability sequences can be included by reference within each other. However, the issue comes when a designer (either a person or piece of software) fails to account for this sending the survey taker into an endless loop. For example, looking at a different survey strucutre like DDI gives:
</p>

<pre>Sequence id="Verse 1"
    question reference: Q2n-1: Is this the song that never ends?
    sequence reference: Verse 2
Sequence id="Verse 2"
    question reference: Q2n: Does it go on and on my friends?
    sequence reference: Verse 1
# Apologies to Lamb Chop</pre>

<p style="text-align: justify;">
  An even shorter (but much less likely) example would be:
</p>

<pre>Sequence id="infinity"
    question reference: Qn: Do you believe how vastly, hugely, mind- bogglingly big Inifinity is?
    sequence reference: infinity
# Apologies to Douglas Adams</pre>

<p style="text-align: justify;">
  What these two examples show is how it is possible to send a user through the same sequence twice, potentially leading to an endless loop of questioning. With DDI providing appropriate <a title="DDI Loops" href="http://www.ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/FieldLevelDocumentation/datacollection_xsd/elements/Loop.html">mechanisms for Looping over questions</a>, it is quite likely that this kind of structure will always be the result of a mistake. However, what it does highlight is how the flexibility DDI provides to allow users to reuse metadata when used inappropriately can cause issues.<br /> Fortunately, as part of the research in developing a DDI web application for data collection, it was neccessary to create a module that was able determine the implied structure and possible ending of DDI Questionnaire. A web-service for this module (aka. Shari) is <a title="Shari - A DDI Questionnaire Validator" href="http://sandbox.kidstrythisathome.com/dditools/sheri">available online at http://sandbox.kidstrythisathome.com/dditools/sheri</a>.<br /> One of the notable features of Shari, is that is will create a hierarchical non-DDI based XML serialisation of a given questionnaire (the reasons for this will be covered in Part 2 of this series &#8220;Where am I?&#8221;). Along with this it will check that no two sequences have references to the same sequence to confirm that the questionnaire will halt. However, the &#8216;halting&#8217; of the survey is however based on the provision that any DDI Loops within the survey are also able to end, but this is a true <a title="Halting Problem - Wikipedia" href="http://en.wikipedia.org/wiki/Halting_problem">&#8216;halting problem&#8217;</a>.<br /> By throwing an error when ever a sequence is referenced twice, some may believe that this will lead to a perceived issue in which two sequences in different branches could link to a third sequence without causing an endless loop being rejected by the system. However, it is possible to rewrite any instrument that relies on using multiple references to a sequence to ensure convergence of a survey in a way that eliminates duplicated references. For example:
</p>

<pre>Instrument id="Main"
    sequence reference: Seq 1
Sequence id="Seq 1"
    question reference: Q1: Do you like A or B?
    if Q1 = A then goto sequence 2a else goto 3b
Sequence id="Seq 2a"
    question reference: Q2a: Why do you hate B?
    sequence reference: Seq 3
Sequence id="Seq 2b"
    question reference: Q2b: Why do you hate A?
    sequence reference: Seq 3
Sequence id="Seq 3"
    question reference: Q3: Wouldn't it be better if every one got along?</pre>

<p style="text-align: justify;">
  In this minimal example, it is trivial to see that this survey will always end. What is important to note is that this can be rewritten as:
</p>

<pre>Instrument id="Main"
    sequence reference: Seq 1
    sequence reference: Seq 3
Sequence id="Seq 1"
    question reference: Q1: Do you like A or B?
    if Q1 = A then goto sequence 2a else goto 3b
Sequence id="Seq 2a"
    question reference: Q2a: Why do you hate B?
Sequence id="Seq 2b"
    question reference: Q2b: Why do you hate A?
Sequence id="Seq 3"
    question reference: Q3: Wouldn't it be better if every one got along?</pre>

<p style="text-align: justify;">
  As the users steps through the branch, after either of the sequences 2a or b end, the survey steps &#8216;back&#8217; from the inner sequence to Seq 1, not finding a following sibling for the If branch it steps back again to the parent instrument and finds Seq 1 has a following sibling and then steps into Seq 3.What should be taken away from this example, is that is is important before finalising a DDI questionnaire to understand the implied structure of the instrument and refactor it to ensure that it is minimal and logically correct as well as having the structure required by the survey designer.
</p>

<p style="text-align: justify;">
  In conclusion, it should be a little clearer about how to tame the flexibility that DDI allows when creating questionnaires and how to create logically correct survey instruments.
</p>

<p style="text-align: justify;">
  Next up&#8230; Questionnaire Design with DDI &#8211; Part 2: Where am I?- Examining why DDI has issues with non-predictability of movement through an instrument, and how to work around this.
</p>