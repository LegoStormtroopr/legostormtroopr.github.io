---
id: 468
title: 'Managing Questions in DDI3.1 &#8211; &#8220;Other, please specify&#8221;'
date: 2012-01-22T11:56:16+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=468
permalink: /2012/01/managing-questions-in-ddi3-1-other-please-specify/
aktt_notify_twitter:
  - no
categories:
  - Education
  - Metadata
tags:
  - DDI
  - 'Other - please specify'
  - Ramona
---
A still difficult problem in managing complex questions in DDI is those questions that ask a respondent to pick from a list of options, and if no suitable ones exist, that they write in their own. Below are examples of this kind of question from the US, UK and Australian Censuses (censii/census/censes?):

![UK Census Extract](http://i.imgur.com/9xpvP.png "UK Census Extract")
  
![USA Census Extract](http://i.imgur.com/loDbJ.png "USA Census Extract")

![ABS Census Extract](http://i.imgur.com/W7UCA.png "ABS Census Extract")

In all three questions, respondents are asked about their origins, and are given the option to select from a list of common responses or provide a write in response. The easiest way to manage this is through the use of a DDI [<MultipleQuestionItem>](http://www.ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/FieldLevelDocumentation/datacollection_xsd/elements/MultipleQuestionItem.html "DDI Field Level Documentation; MutlipleQuestionItem"). A <MultipleQuestionItem> is a way to capture a complex question that asks two or more separate questions that are highly linked.

In the above examples we can split the questions into two, as illustrated in the generic answer below:

<pre>&lt;MultipleQuestionItem&gt;
    &lt;SubQuestions&gt;
        &lt;QuestionItem&gt;
            &lt;QuestionText&gt;
                &lt;LiteralText&gt;
                    What is your ancestral origin?
                &lt;/LiteralText&gt;
            &lt;/QuestionText&gt;
            &lt;CodeDomain&gt;
                &lt;!-- This CodeDomain would include a reference to the list of countries or races --&gt;
            &lt;/CodeDomain&gt;
        &lt;/QuestionItem&gt;
        &lt;QuestionItem&gt;
            &lt;QuestionText&gt;
                &lt;LiteralText&gt;
                    Please Specify:
                &lt;/LiteralText&gt;
            &lt;/QuestionText&gt;
            &lt;TextDomain/&gt;
        &lt;/QuestionItem&gt;
    &lt;SubQuestions&gt;
&lt;/MultipleQuestionItem&gt;</pre>

Here we have been able to split the question, while still managing it in a single item. This is needed as without each other, each subquestion is incomplete. This is not a new concept, and is quite an obvious solution to many people who have tried to solve this issue.

However, there is still the problem that this metadata doesn&#8217;t contain the restriction that a respondent should only be able to enter a free text option if the &#8220;other&#8221; option is selected. While there have been a number of published and attempted solutions, none have been satisfactory. Spliting the question outside of a MultipleQuestionItem and using IfThenElse clauses complicates the structure, and leaving this out makes designing self-interviewed computer systems difficult to manage directly from the metadata.

A possible solution, that resolves both of these issues is through the use of the [<SubQuestionSequence>](http://www.ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/FieldLevelDocumentation/datacollection_xsd/elements/SubQuestionSequence.html "DDI Field Level Documentation; SubQuestionSequence"). This is illustrated in the DDI Fragment below:

<pre>&lt;MultipleQuestionItem&gt;
    &lt;SubQuestions&gt;
        &lt;QuestionItem&gt;
            &lt;!-- Ancestral origin QuestionItem --&gt;
        &lt;/QuestionItem&gt;
        &lt;QuestionItem&gt;
            &lt;!-- Please Specify QuestionItem --&gt;
        &lt;/QuestionItem&gt;
    &lt;SubQuestions&gt;
    &lt;SubQuestionSequence&gt;
        &lt;ItemSequenceType&gt;Other&lt;/ItemSequenceType&gt;
        &lt;AlternateSequenceType formalLanguage="Name Of Language Here" &gt;
            &lt;!-- Proprietary command to control logic --&gt;
        &lt;/AlternateSequenceType&gt;
    &lt;/SubQuestionSequence&gt;
&lt;/MultipleQuestionItem&gt;</pre>

In this we have used the SubQuestionSequence to hold the logic used to indicate when the &#8220;Other&#8221; field should be allowable. This field is used to control the specific sequence that the SubQuestions are shown, and in this sense we are controling this ordering, just to specify when a member is not shown &#8211; an excusable use of the field. This choice can be further rationalised, as an unfamiliar agent, for example when moving to a new piece of software, can still interpret the bulk of the metadata, however when presenting the above question would allow a respondent to fill in both sections. But this is no different to how a respondent of a paper-based survey may answer, so it is no great loss of granularity.

How any given agency may choose to populate the commands contained in the AlternateSequenceType will be an individual choice, and a standard way of expressing this may be needed, but this should help other groups more easy solve this problem by indicating where the solution can go and reducing the problem size.

In the next day or two I will be putting a more solid example up into the [DDI Examples Repository](http://www.kidstrythisathome.com/2012/01/ddi-examples-repository-now-available/ "DDI Examples repository now available") for people to work with. As always critiques of these ideas and examples are welcome.