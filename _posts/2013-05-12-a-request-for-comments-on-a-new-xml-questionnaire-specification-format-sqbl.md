---
id: 3206
title: A Request for Comments on a new XML Questionnaire Specification Format (SQBL)
date: 2013-05-12T11:08:51+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=3206
permalink: /2013/05/a-request-for-comments-on-a-new-xml-questionnaire-specification-format-sqbl/
categories:
  - Data
  - Metadata
  - Statistics
tags:
  - "I'll make my own specification with blackjack..."
  - IASSIST
  - questionniare
  - SQBL
---
This is an announcement and Request for Comments on SQBL a new
  
open-source XML format for the cross-platform development of questionnaire
  
specifications. The design decisions behind SQBL and additional details are the
  
subject of a paper to be presented in 2 weeks at the 2013 IASSIST conference in
  
Cologne, Germany:
      
&#8211; Do We Need a Perfect Metadata Standard or is &#8220;Good Enough&#8221; Good Enough?
      
&#8211; <http://www.iassist2013.org/program/sessions/session-c4/#c220>
  
However, to ensure people are well-informed ahead time, I am releasing details
  
ahead to conference.

# The gist {#the-gist}

SQBL &#8211; The Structured (or Simple) Questionnaire Building Language is an
  
emerging XML format designed to allow survey researchers of all fields to
  
easily produce questionnaire specifications with the required structure to
  
enable deployment to any questionnaire platform &#8211; including, but not limited
  
to, Blaise, DDI, LimeSurvey, XForms and paper surveys.

# The problem {#the-problem}

Analysing the current state of questionnaire design and development shows that
  
there are relatively few tools available that are capable of allowing a survey
  
designer to easily create questionnaire specifications in a simple manner,
  
whilst providing the structure necessary to verify respondent routing and
  
provide a reliable input to the automation of questionnaire deployment.

Of the current questionnaire creations tools available, they either:
  
 _Prevent the sharing of content (such as closed tools like SurveyMonkey)
  
_ Require extensive programming experience (such as Blaise or CASES)
  
* or use formats that make transformation difficult (such as those based on DDI)
  
Given the high-cost of questionnaire design, in the creation, testing and
  
deployment of final questionnaires a format that can reduce the cost in any or
  
all of these areas will have positive effects for researchers. 

Furthermore, by providing researchers with the easy tools necessary to create
  
questionnaires they will consequently create structured metadata, thus reducing
  
the well understood documentation burden for archivists.

# Structured questionnaire design {#structured-questionnaire-design}

Last year, I wrote a paper &#8220;The Case Against the Skip Statement&#8221;, that
  
described the computational theory of questionnaire logic &#8211; namely the
  
structures used to describe skips and routing logic in questionnaires. This
  
paper was awarded 3rd place in the International Association of Official
  
Statistics &#8216;2013 Young Statistician Prize&#8217; <http://bit.ly/IAOS2012>. This paper
  
is awaiting publication, but can be made available for private reading on
  
request. It proposed that this routing logic in questionnaires is structurally
  
identical to that of computer programs. Following this assertion, it stated
  
that a higher-order language can be created that acts as a &#8220;high-level
  
questionnaire specification logic&#8221; that can be compiled to any questionnaire
  
platform, in much the same way that computer programming languages can be
  
compiled to machine language. Unfortunately, while some existing formats
  
incorporate some of the principles of Structured Questionnaire Design, they are
  
incomplete or too complex to provide the proposed benefits.

# SQBL &#8211; The Structured (or Simple) Questionnaire Building Language {#sqbl-the-structured-or-simple-questionnaire-building-language}

SQBL <http://sqbl.org> is an XML format that acts as a high-level language for
  
describing questionnaire logic. Small and simple, but powerful it incorporates
  
XML technologies to reduce the barrier to entry and make the description of
  
questionnaire specifications, even in raw XML readable. Underlying this
  
simplicity is a strict schema that enforces single solutions to problems,
  
meaning SQBL can be transformed into a format for any survey tool that has a
  
published specification.

Furthermore, because of its small schema and incorporation of XML and HTTP core
  
technologies, it is easier for developers to work with. In turn, this makes
  
survey design more comprehensible through the creation of easier tools, and
  
will help remove the need for costly, specialised instrument programmers
  
through automation.

# Canard &#8211; the SQBL Question Module Editor {#canard-the-sqbl-question-module-editor}

Announced alongside the Request of Comments of SQBl is an early beta release of
  
the SQBL-based Canard Question Module Editor <http://bit.ly/CANARD>. Canard is
  
designed as a proof-of-concept tool to illustrate how questionnaire
  
specifications can be generated in an easy to use drag-and-drop interface. This
  
is achieved by providing designers with instant feedback on changes to
  
specifications through its 2 panel design that allows researchers to see the
  
logical specification, routing paths and example questionnaires all within the
  
same tool.

# SQBL and other standards {#sqbl-and-other-standards}

SQBL is not a competitor to any existing standard, mainly because a structured
  
approach to questionnaire design based on solid theory has never been attempted
  
before. SQBL fills a niche that other standards don&#8217;t yet do well.

For example, while DDI can _archive_ any questionnaire as is, this is because
  
of the loose structure necessary for being able to archive uncontrolled
  
metadata. However, if we want to be able to make questionnaire specifications
  
that can be used to drive processes, what is needed is the strict structure of
  
SQBL.

Similarly, SQBL has loose couplings to other information through standard HTTP
  
URIs allowing linkages to any networked standard. For example, Date Elements may
  
be described in a DDI registry, which a SQBL question can reference via its
  
DDI-URI. Additionally, to support automation a survey instrument described
  
inside a DDI Data Collection, rather than pointing to a DDI Sequence containing
  
the Instrument details can use existing linkages to external standards to point
  
to a SQBL document via a standard URL. Once data collection is complete,
  
harmonisation can be performed as each SQBL module has questions pointing to
  
variables, so data has comparability downstream.

# SQBL in action {#sqbl-in-action}

The SQBL XML schemas are available on GitHub <http://bit.ly/sqbl-schema> that
  
also contains examples and files from video tutorials.
  
There is a website <http://sqbl.org> with more information on the format that
  
provides more information on some of the principles of Structured Questionnaire
  
Design.

If you don&#8217;t like getting your hands dirty with XML you can download the
  
Windows version of the Canard Question Module Editor from Dropbox
  
<http://bit.ly/canardexe> and start producing questionnaire specifications
  
immediately. All that needs to be done is to unzip the file and run the file
  
named <canard_main.exe>. Due to dependencies flowcharts may not be immediately
  
available, however this can be fixed by installing the free third-party
  
graphing tool Graphviz <http://www.graphviz.org/>

Lastly, there is a growing number of tutorial videos on how to use Canard on Youtube.

Video 1 &#8211; Basic Questions <http://www.youtube.com/watch?v=ijk00SqoBGk> (2:17 min)
  
Video 2 &#8211; Complex Responses <http://www.youtube.com/watch?v=d3Vrn2B4EO4> (2:17 min)
  
Video 3 &#8211; Simple Logic <http://www.youtube.com/watch?v=GrAWbOF-UW8> (4:11 min)

There is also an early beta video that runs through creating an entire
  
questionnaire showing the side-by-side preview.
  
<http://www.youtube.com/watch?v=_FImaXn7EYk> (13:21 mins)

# Joining the SQBL community {#joining-the-sqbl-community}

First of all there is a mailing list for SQBL hosted by Google Groups:
  
<https://groups.google.com/forum/?fromgroups#!forum/sqbl>.

Along with this each of the GitHub repositories <http://bit.ly/sqbl-schema>,
  
<http://bit.ly/CANARD> include issue trackers. Both Canard and SQBL are in
  
early design stages so there is an opportunity for feedback and input to ensure
  
both SQBL and Canard support the needs of all questionnaire designers.

Lastly, while there are initial examples of conversion tools to transform SQBL
  
into DDI-Lifecycle 3.1 and XForms, there is room for growth. Given the
  
proliferation of customised solutions to deploy both paper and web-forms there
  
is a need for developers to support the creation of transformations from SQBL
  
into formats such as Blaise, LimeSurvey, CASES and more.

If you have made it this far thank you for reading all the way through, and I
  
look forward to all the feedback people have to offer.

Cheers and I look forward to feedback now or at IASSIST,

Samuel Spencer.
  
 _SQBL & Canard Lead Developer
  
_ IASSIST Asia/Pacific Regional Secretary

http://about.me/legostormtroopr

http://au.linkedin.com/in/legostormtroopr/