---
id: 286
title: 'Questionnaire design with DDI – Part 3: What am I doing here?'
date: 2011-05-25T10:58:56+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=286
permalink: /2011/05/questionnaire-design-with-ddi-part-3-what-am-i-doing-here/
aktt_notify_twitter:
  - no
categories:
  - Data
  - Metadata
tags:
  - Best Practice
  - DDI
  - Instrument
  - Survey
  - Transformation
  - Tutorial
---
<p style="text-align: justify;">
  This is the third in a 5 part series of working with questionnaires and surveys managed using the <a title="DDI Alliance Website" href="http://www.ddialliance.org">Data Documentation Initiative XML standard</a>. With DDI being an emerging technology, it is important that users are provided with best practises to ensure that they use the standard in a way that is logical, coherent and most importantly usable and reusable. This series of tutorials and discussions is aimed toward users who have some knowledge of DDI and would like to know how to effectively design markup existing and future questionnaires in DDI.
</p>

<h1 style="text-align: justify;">
  Part 3 : What am I doing here?
</h1>

<p style="text-align: justify;">
  So far in the last two parts of this series we have been looking at how to logically structure questionnaires in DDI. In this post we now switch to looking at how to effectively present DDI sequences in an application and how to structure DDI sequences so they are unambiguous and will display in predictable ways in all viewers.
</p>

<p style="text-align: justify;">
  One of the first difficulties in displayign a DDI Intrument in a webpage is, how many questions to show on a page at anyone time. The easiest, and most appropriate method is to display each sequence as a page and perform logic around those sequences on the server when the users submits data. However, Sequences can contain more than questions, and when we deal with mixed types the it can be difficult to predict how an agent may display the form.
</p>

<p style="text-align: justify;">
  For background. a <a title="DDI Sequence - Field Level Documentation" href="http://www.ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/FieldLevelDocumentation/datacollection_xsd/elements/Sequence.html">DDI Sequence</a> is able to reference any <a title="DDI ControlConstruct - Field Level Documentation" href="http://www.ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/FieldLevelDocumentation/datacollection_xsd/elements/ControlConstruct.html">ControlConstruct</a> as a child. We are able to separate ControlConstructs into two different types &#8211; branches and leaves. In tree data structures branches are able to have as children either other branches or leaves, where as leaves are the &#8216;end&#8217; of the structure as they cannot have children. In DDI objects &#8220;tree-branch ControlConstructs&#8221; are objects which cannot reference other ControlConstructs, these are only <a title="DDI StatementItem - Field Level Documentation" href="http://www.ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/FieldLevelDocumentation/datacollection_xsd/elements/StatementItem.html">StatementItem&#8217;s</a> and <a title="DDI QuestionConstruct - Field Level Documentation " href="http://www.ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/FieldLevelDocumentation/datacollection_xsd/elements/QuestionConstruct.html">QuestionConstruct&#8217;s</a>, and every other ControlConstruct is therefore a &#8216;tree-branch&#8217;.
</p>

<p style="text-align: justify;">
  A Statement item is a way of including headers or textual information in an instrument and QuestionConstruct is a way of including a <a title="DDI QuestionItem - Field Level Documentation" href="http://www.ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/FieldLevelDocumentation/datacollection_xsd/elements/QuestionItem.html">QuestionItem</a> by reference into an Instrument. Therefore, it is these that are the most vital elements in questionnaire design, with loops and branches adding &#8216;syntactic sugar&#8217; that improved the form, but don&#8217;t gather data directly. Presenting these on a web page is trivially easy, simply just copying the textual nodes of these into a webpage will suffice. In fact, in Ramona these are almost completely hidden from users, with the server using these to determine the next sequence to present for a user, but forever remaining in the background.
</p>

<p style="text-align: justify;">
  The question is though, how should an agent handle a sequence that contains a mix of leaves and branches? Let us work through this example, where we have a mix of leaves and branches, whose types are unimportant:
</p>

<pre>Sequence id="Seq 1"
    leaf   reference: L1
    branch reference: B2
    leaf   reference: L3</pre>

<p style="text-align: justify;">
  Here we have two object we know need to be displayed to a user separated by branch that may link to any number of other constructs. In a state-less web context, like Ramona, its going to be hard to come back to this page and make sure the right information is still displayed for the user. So we may decide to show all the leaves we can, and then to the branch and continue on like that, safe in the knowledge that even if the connection to the user fails, we&#8217;ll have got all the information in this sequence. However, this effectively reorders the questions in the instrument.
</p>

<p style="text-align: justify;">
  Alternatively, if we are using a desktop application where we have more control over state, it may be possible to present the two leaves and the objects in the branch in the same view. Here we come across an immediate problem: depending on the viewer the user is shown two vastly different forms. The solution is simple: leaves and branches should never be the children of the same parent, and that leaves should always be the child of a DDI Sequence.
</p>

<p style="text-align: justify;">
  This immediate resolves this issue by making the display of objects predictable, when displaying a sequence of leaves the agent only has to display the appropriate text of the statements and questions. When dealing with the logic of loops and branches the agent then can cache this using a format similar to that suggested in <a title="Questionnaire design with DDI – Part 2: Where am I and where do I go next?" href="http://www.kidstrythisathome.com/2011/05/questionnaire-design-with-ddi-part-2-where-am-i-and-where-do-i-go-next/">Part 2 of this tutorial series Where am I and where do I go next?</a>. This allows the logic and presentation of a survey to be separated completely, making the display of a survey a much more predictable action.
</p>

<p style="text-align: justify;">
  There is an issue with this solution, and that is that it deviates from the structure imposed by DDI making survey design more strict about how elements can be combined. Furthermore, this solution requires designers of surveys understand these restrictions and voluntarily comply with them.
</p>

<p style="text-align: justify;">
  If the standard can&#8217;t enforce this restriction, and user can choose not to follow it, is it a good solution? Good, probably not &#8211; but it may be the best.
</p>

<p style="text-align: justify;">
  Admittedly, I hold a biased view in this respect. When designing Ramona, I made a decision not to suppose mixed sequences for this two reasons. Firstly, as above it makes the display of sequences more predictable, but secondly it is just plain easier to work with when you can apply these restrictions. When pre-compiling an instrument Ramona will error if it finds a sequence containing mixed types, and for the foreseeable future, when Ramona gets released, even as a research idea, it will continue to hold these restrictions because it prevents users from making ambiguous surveys.
</p>

<p style="text-align: justify;">
  Next up… Questionnaire Design with DDI – Part 4: Can it be done? &#8211; A look back at the previous 3 tutorials and an indepth explanation of the realisation of a Ramona &#8211; A functional DDI Questionnaire tool.
</p>