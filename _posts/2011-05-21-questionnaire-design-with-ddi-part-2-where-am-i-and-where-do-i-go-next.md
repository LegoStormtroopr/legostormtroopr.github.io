---
id: 273
title: 'Questionnaire design with DDI – Part 2: Where am I and where do I go next?'
date: 2011-05-21T03:35:13+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=273
permalink: /2011/05/questionnaire-design-with-ddi-part-2-where-am-i-and-where-do-i-go-next/
aktt_notify_twitter:
  - no
categories:
  - Data
  - Metadata
  - Statistics
tags:
  - Best Practice
  - DDI
  - Instrument
  - Sheri
  - Survey
  - Transformation
  - Tutorial
---
<p style="text-align: justify;">
  This is the second in a 5 part series of working with questionnaires and surveys managed using the <a title="DDI Alliance Website" href="http://www.ddialliance.org">Data Documentation Initiative XML standard</a>. With DDI being an emerging technology, it is important that users are provided with best practises to ensure that they use the standard in a way that is logical, coherent and most importantly usable and reusable. This series of tutorials and discussions is aimed toward users who have some knowledge of DDI and would like to know how to effectively design markup existing and future questionnaires in DDI.
</p>

<h1 style="text-align: justify;">
  Part 2 : Where am I and where do I go next?
</h1>

<p style="text-align: justify;">
  In the previous post on questionnaires using DDI we looked at how it is possible in DDI to repeat sequences of questions, potentially leading to endless loops of questions within a survey. In a paper survey this would be quickly picked up, but in an electronic survey this might not always be the case. To help identify these issues  <a title="Sheri" href="http://sandbox.kidstrythisathome.com/dditools/sheri">a tool called Sheri</a> was introduced that consumes a DDI instrument and check for potential issues of repeated questions and endless loops. Sheri also is able to generate a non-standard XML format representing an entire survey marked up in DDI. But this leads to the question “if one were to design a survey in DDI, why introduce another XML format?”
</p>

<p style="text-align: justify;">
  During research into DDI as a data capture standard it became quickly apparent, that for all of its benefits in designing surveys, DDI was very difficult for programs to consume to create instances of these instruments. This is due to how DDI describes an Instrument. In DDI a whole survey instrument is represented by a single tag &#8211; <a title="DDI Instrument - Field Level Documentation" href="http://www.ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/FieldLevelDocumentation/datacollection_xsd/elements/Instrument.html">Instrument</a> -, which in turn references a single <a title="DDI Sequence - Field Level Documentation" href="http://www.ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/FieldLevelDocumentation/datacollection_xsd/elements/Sequence.html">Sequence</a> within a <a title="DDI ControlConstructScheme - Field Level Documentation" href="http://www.ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/FieldLevelDocumentation/datacollection_xsd/elements/ControlConstructScheme.html">ControlStructureScheme</a>. This is simple enough, to understand, but once the first Sequence is found the structure becomes quite interesting. Every Sequence, or other <a title="DDI ControlConstruct - Field Level Documentation" href="http://www.ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/FieldLevelDocumentation/datacollection_xsd/complexTypes/ControlConstructType.html">ControlConstruct</a>, maintains references to its child sequences. For example, a Sequence can reference multiple other Sequences, which reference more Sequences and so on. Likewise, a <a title="DDI Loop - Field Level Documentation" href="http://www.ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/FieldLevelDocumentation/datacollection_xsd/elements/Loop.html">Loop</a> maintains a list of linked ControlStructres to loop over, and conditional <a title="DDI IfThenElse - Field Level Documentation" href="http://www.ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/FieldLevelDocumentation/datacollection_xsd/elements/IfThenElse.html">IfThenElse</a> tags contains references in both Then and Else clause that refer to other ControlStructures. What this means is that although there is an implied hierarchy, it is stored as a flat list of data structures with references between them.
</p>

<p style="text-align: justify;">
  What this leads to is a difficulty in determining where exactly in the hierarchy one is if they are given only the id of the current structure, especially when dealing with the <a title="Stateless Server - Wikipedia" href="http://en.wikipedia.org/wiki/Stateless_server">stateless nature of the web</a>. For example, the test software I was writing, Ramona, would take a sequence id as an argument and render the corresponding DDI sequence as a form on a webpage with web controls for each question. What quickly became an issue was determining the what the next page to display was when a user was done with a sequence.
</p>

<p style="text-align: justify;">
  In a DDI ControlStructure, the ID of a child element is stored as the text of an ID element under a ControlConstructReference. What this means is that to determine the next possible sequence given a sequence id, you need to look for references to the object, not the object itself. Then from the reference, search back for an appropriate ancestor element and then return the next sibling to show the correct form. This quickly becomes complicated and when dealing with large DDI test  files doing plain text searches throughout an unmanaged * hierarchy it became apparent that this method was too slow and complex for real time returns.
</p>

<p style="text-align: justify;">
  A further complication arises if a survey reuses an object using multiple references (as opposed to using Loops). In cases such as this, using the above method it becomes impossible to easily determine which is the correct parent. The reason being that a reverse lookup for referring objects for an object referenced multiple times will only return a list of referring objects with no context about which one we need to follow.
</p>

<p style="text-align: justify;">
  For example in the following sequence:
</p>

<pre>Sequence id="Seq 1"
    sequence reference: Seq 3
Sequence id="Seq 2"
    sequence reference: Seq 3
Sequence id="Seq 3"
    question reference: Q1: Where did I come from?</pre>

<p style="text-align: justify;">
  Resolves to have a structure like:
</p>

<pre>Sequence id="Seq 1"
    Sequence id="Seq 3"
        question reference: Q1: Where did I come from?
Sequence id="Seq 2"
    Sequence id="Seq 3"
        question reference: Q1: Where did I come from?</pre>

<p style="text-align: justify;">
  But, given just the id of Sequence 3 we can’t determine if after answer the question the survey is over (if we arrived at Sequence 3 from Sequence 2), or if we still have to go to Sequence 2.
</p>

<p style="text-align: justify;">
  To solve these issues of both speed, development and determining location, it is therefore necessary for applications using DDI to &#8220;pre-compile&#8221; Instruments into a traditional hierarchy form. In both Ramona and Sheri, the solution is to resolve the references and copy the referenced elements into the parent structure. This allow much of the DDI metadata to be retained and used.
</p>

<p style="text-align: justify;">
  <strong>This is not valid DDI, and it is unlikely that it ever will be.</strong>
</p>

<p style="text-align: justify;">
  This is also not a problem. DDI is useful as an archival and transportation language for statistical metadata, and the flexibility that the current structure provides is quite useful. However, when looking at data collection, it can be safely assumed that the DDI Instrument would be relatively stable. If best practices are followed, once a DDI Instance is published it will never change. Thus it is a perfectly valid action to transform an Instrument in this way, as long as two conditions are met: this is seen as a one-way destructive transformation, and that the resulting pseudo-DDI instrument is never changed. To provide another example of why this is a normal situation, there are tools that are being developed to transform DDI into PDF questionnaires: this is very much the same process, the PDF is seen as a projection of the original DDI to make it easier for people to use, but not the actual &#8216;source-of-truth&#8217;. Transforming DDI Instruments into a dereferenced pseudo-DDI Instrument is exactly the same, a transform of complex metadata into a form that machines can easily work with.
</p>

<p style="text-align: justify;">
  There is one issue that these pseudo-DDI Instruments will have, and that is when a single data structure is referenced multiple times, it will occur multiple times in the resultant tree. In cases like this, it is still difficult to determine which element is the correct one when just given an ID. There are two possible solutions to this issue, the first being that instead of managing state based on a single ID, it is managed as the full XPath of the element, possibly speeding up traversal, but also presenting the possibility the the structure of the form could be shared with users &#8211; which may or may not be a security issue depending on the form. Alternatively, as discussed in the <a title="Questionnaire design with DDI – Part 1: Will this survey ever end?" href="http://www.kidstrythisathome.com/2011/05/questionnaire-design-with-ddi-part-1-will-this-survey-ever-end/">part one of these tutorials</a>, restructuring Instruments so no structure is referenced more than once, making it easier to traverse through the form, as well as limiting user frustration.
</p>

<p style="text-align: justify;">
  It should be noted that restructuring is not a necessity in making DDI Instruments processable by software, just something that makes them easier to use using traditional methods and existing XML libraries, and can provide benefits to execution times if that is an issue. However, when dealing with desktop software, many of the issues of web development with regards to stateless vs. stateful systems or the scalability of systems with concurrent users cease to be an issue. In such situations, it is quite possible to work using the DDI Instrument directly, with manipulating the data strucutre, and in some cases may be preferable.
</p>

<p style="text-align: justify;">
  In conclusion, how strictly we manage the DDI metadata structure depends very strongly on the role the metadata plays in a system. In some cases, such as computer-aided interviewing where the instrument should be extremely stable, the transformation of DDI to a format that is more easily processed by systems, or even users, can be preferable to using plain DDI. what is important is to focus on DDI as a tool for increasing transparency and reusability in statistical processing, but as long as the methods used to transform DDI into intermediate forms are well documented there is no reason why this cannot be done as such the use of well-documented transformations would not violate existing best practice.
</p>

<div>
  <div>
    <p>
      Next up… Questionnaire Design with DDI – Part 3: What am I doing here? &#8211; A look at best practices for what control structures to include in sequences and how to deal with logical structures and questions.
    </p>
  </div>
</div>



<p style="text-align: justify;">
  * Unmanaged in the sense that the hierarchy is stored as references between XML elements, and not as a traditional XML hierarchy, and as such traditional tree traversal methods for XML cannot be used.
</p>