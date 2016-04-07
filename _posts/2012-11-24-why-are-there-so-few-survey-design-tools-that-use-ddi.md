---
id: 623
title: Why are there so few survey design tools that use DDI?
date: 2012-11-24T01:37:27+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=623
permalink: /2012/11/why-are-there-so-few-survey-design-tools-that-use-ddi/
categories:
  - Drivel
  - Metadata
tags:
  - DDI
  - "I'll make my own specification with blackjack..."
---
Having been a close part of the DDI community for some time, and having attended a number of DDI focused conferences I have noticed a disturbing trend. There are relatively few content editors that use DDI. I have chosen this term very carefully, as there are a number of DDI Editors but these are tools whose primary function is to produce DDI XML. When I say a DDI-powered content editor I mean a tool with a limited use case that happens to use DDI as the storage format. As an example, we can look at Colectica &#8211; a leading DDI Editor. In this tool to create a survey with some pathing between questions, first I create a QuestionScheme, with some Questions, then I create an Instrument, which create for me a  ControlConstructScheme, then I can start pulling questions into this. If a new question needs to be made, I switch back to my QuestionScheme view, and make a new question, then switch back to the instrument and drag it in. While it is able to make perfectly valid DDI, this is not entirely how people think during this process. This is analogous to opening a Word processor to write a letter, and having to write an alphabetical list of words that I can then drag into the appropriate place in the document, rather than just typing away. But this isn&#8217;t on any part the fault of Colectica itself, but more the only way that an editor that uses DDI could feasibly be written.

To look at why this is, I want to examine two simple use cases that should be able to be done using a simple tool and have the corresponding data managed in DDI. Firstly, how does a survey designer go about reusing an existing question in their survey, and secondly, how does a survey designer create a new question inside of an existing survey instrument? Now to answer these questions I want to look at it from a uer interaction point of view, and pull out what a survey designer would have to do ensure that they have the bare minimum content needed to be &#8216;good&#8217; DDI.

**Use case 1: Reusing a question**

One of the commonly stated advantages of DDI is the reusability of its managed content, so it should be the case that reusing a question is a relatively simple affair. For this use case, we picture a hypothetical user interface, where a survey designer wants to insert a new question into an existing sequence of questions. In DDI terms, they wish to insert a QuestionConstruct into a Sequence, not make a new QuestionItem in a QuestionScheme. So ideally the designer should need to:

  1. Search for a question using some search parameters
  2. If a suitable question is found, drag this question into the sequence.

However, this isn&#8217;t the case. First of all, the user interface needs to differentiate between the QuestionItem and the QuestionConstruct, as the QuestionConstruct is used to insert a question into a sequence by reference. So already we need the survey designer to understand DDI well enough to differentiate these objects. Secondly, if the needed QuestionConstruct doesn&#8217;t exist, this needs to be created by the user, which then necessitates that the user is prompted for the ControlConstructScheme that the new QuestionConstruct lives in. So what actually has to happen is this

  1. Search for a question using some search parameters
  2. If a suitable question is found, look at the list of QuestionConstructs (each with their own different contexts), and drag the appropriate one into the sequence. Nothing further needs to be done.
  3. If an appropriate QuestionConstruct doesn&#8217;t exist, create it with its own label and description.
  4. Prompt the user for where the QuestionConstruct should be maintained
  5. Search for a ControlConstructScheme using some search parameters, selecting the appropriate one.
  6. If none is found, create one with its own label, description, version, etc&#8230;

Here the simple act of reuse has tripled in size, now requiring the survey designer to understand more of the DDI model than necessary, as well as in many cases having to then become administratively responsible for further content than just their original survey content.

**Use case 2: Creating a question**

However this user interaction becomes much more complex when a user wants to add a new question. Again this should be a relatively simple affair, where a survey designer has made the decision that a new question needs to be created. In DDI terms, they wish to insert a QuestionConstruct into a Sequence, and create a new QuestionItem in a QuestionScheme . So ideally the designer should need to:

  1. Click to create a new question in the location needed.
  2. Add the corresponding information, such as question text, a label and description and intent.

Again however, this is far from how it would work using a DDI compatible tool.

  1. Click to create a new question in the location needed.
  2. Add the corresponding information, such as question text, a label and description and intent. 
  3. Prompt the user for the QuestionScheme where the QuestionItem should be maintained. 
  4. Search for a QuestionScheme using some search parameters, selecting the appropriate one. 
  5. If none is found, create a QuestionScheme with its own label, description, version, etc&#8230; 
  6. Create the necessary QuestionConstruct with the corresponding information, such a label and description. 
  7. Prompt the user for where the QuestionConstruct should be maintained 
  8. Search for a ControlConstructScheme using some search parameters, selecting the appropriate one. 
  9. If none is found, create one with its own label, description, version, etc&#8230; 

Here the act of simply adding in a new question is a 9 step process. It can be argued that not all of the steps are necessary, or that content for &#8216;unimportant metadata&#8217; could be filled in at a later stage, but this means that objects remain empty for an indeterminate amount of time or relies on conventions to hide information from users, e.g. A QuestionItem can only link to one QuestionConstruct so they can be treated as &#8216;the same&#8217;. However, while valid DDI, this violates the &#8216;spirit of the standard&#8217;.

**Why is this important?**

Ultimately, users and their tools make or break a standard, if no one can write DDI, or write tools that write DDI, or write tools that people want to use, then the very purpose of the standard is called into question. But the wider implication is this, the reuse of content stored as DDI is contingent on its reuse, but it must initially come from somewhere.  Perhaps in its current state DDI can be made to work for post-hoc research archivists. However, it is still lacking as a living standard where it can be used through the survey lifecycle simply due to the over engineered state.

**How can this be resolved?**

Firstly, by drastically simplifying the content requirements and referential structure in DDI, and this will be achieved by talking with users and determining their needs. Archivists, survey researchers and central bankers will all have very different needs from each other as they all do wildly different things. While its not infeasible that one standard could meet their needs, it comes from identifying their needs first. As a first step I offer this as an opening question: Does anyone actually want to reuse just a single question? I ask this as in my limited experience, I&#8217;ve seen that people really just want to be able to reuse large modules of questions, a limited number of questions with their own internal logic can be reused across a number of areas. It will probably come to mind that the question of &#8216;Sex&#8217; is reused across almost any population research, but the rebuttal is does anyone ever ask Sex, but not Age?