---
id: 291
title: 'Questionnaire design with DDI – Part 4: What can I say?'
date: 2011-05-29T05:40:02+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=291
permalink: /2011/05/questionnaire-design-with-ddi-%e2%80%93-part-4-what-can-i-say/
aktt_notify_twitter:
  - no
categories:
  - Data
  - Metadata
  - Web Development
tags:
  - Best Practice
  - DDI
  - HTML5
  - Instrument
  - Survey
  - Transformation
  - Tutorial
  - Validation
---
<p style="text-align: justify;">
  This is the fourth in a 5 part series of working with questionnaires and surveys managed using the <a title="DDI Alliance Website" href="http://www.ddialliance.org">Data Documentation Initiative XML standard</a>. With DDI being an emerging technology, it is important that users are provided with best practises to ensure that they use the standard in a way that is logical, coherent and most importantly usable and reusable. This series of tutorials and discussions is aimed toward users who have some knowledge of DDI and would like to know how to effectively design markup existing and future questionnaires in DDI.
</p>

<h1 style="text-align: justify;">
  Part 4: What can I say?
</h1>

<p style="text-align: justify;">
  One of the more useful aspects of electronic forms is they give us the ability to provide instant feedback to the user regarding their answers. HTML5 web forms especially are able to provide instant feedback to users on invalid data in number of ways. More importantly, electronic forms also allow us to perfom critical validation on data to ensure that we gather the most accurate data possible.
</p>

<p style="text-align: justify;">
  First off, lets look at the simple issue of finding what metadata is available in DDI 3.1 to provide validation. In DDI <a title="DDI QuestionItem - Field Level Documentation" href="http://www.ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/FieldLevelDocumentation/datacollection_xsd/elements/QuestionItem.html">QuestionsItems</a> contain the abstract idea of <a title="DDI ResponseDomain - Field Level Documentation " href="http://www.ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/FieldLevelDocumentation/datacollection_xsd/complexTypes/QuestionItemType.html#r8">ResponseDomains</a>, which in turn can be used to provide hints for systems to encourage certain responses from users, including <a title="DDI CodeDomain - Field Level Documentation " href="http://www.ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/FieldLevelDocumentation/datacollection_xsd/elements/CodeDomain.html">Codes</a> or <a title="DDI CategoryDomain - Field Level Documentation " href="http://www.ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/FieldLevelDocumentation/datacollection_xsd/elements/CategoryDomain.html">Categories</a>, various types of <a title="DDI NumericDomain - Field Level Documentation " href="http://www.ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/FieldLevelDocumentation/datacollection_xsd/elements/NumericDomain.html">Numbers</a>, <a title="DDI TextDomain - Field Level Documentation " href="http://www.ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/FieldLevelDocumentation/datacollection_xsd/elements/TextDomain.html">Strings</a>, <a title="DDI DateTimeDomain - Field Level Documentation " href="http://www.ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/FieldLevelDocumentation/datacollection_xsd/elements/DateTimeDomain.html">Dates and Times</a>, or <a title="DDI GeographicDomain - Field Level Documentation " href="http://www.ddialliance.org/Specification/DDI-Lifecycle/3.1/XMLSchema/FieldLevelDocumentation/datacollection_xsd/elements/GeographicDomain.html">Geographic</a> data. Each of these explicitly imposes a specifc type of expected answer for a question, as well as additional restrictions:<br /> For example, when asking for&#8230;
</p>

<ul style="text-align: justify;">
  <li>
    age we can explicitly request integers over 0
  </li>
  <li>
    percentages we can define responses to be decimal numbers between 0 and 100
  </li>
  <li>
    location data, we can define the geographic coordinate system
  </li>
  <li>
    a unit code for a university course, we can specific a code scheme this must come from
  </li>
  <li>
    a post code as a string, we can specify a pattern the string must match
  </li>
</ul>

<p style="text-align: justify;">
  This is just a short list of possible examples for the use of ResponseDomains, and if there is an issue with restricting responses this is the first place those restrictions could apply. ResponseDomains can even specify top and bottom codes, if for example one wanted to top code ages censor ages above 65. With such a wealth of information available, the only issue becomes using this effectively to assist in response validation.
</p>

<p style="text-align: justify;">
  When looking at validation, web pages can act quite different to desktop applications. On a desktop application the programmer has a lot more control over what the user does and what data gets entered, however on the web, the client can effectively rewrite the webpage before submission making data validation much more important. What both paradigms have in common is that both will unfortunately interact with a user &#8211; the least secure, most buggy and most important part of any system.
</p>

<h2 style="text-align: justify;">
  Client-side / UI validation
</h2>

<p style="text-align: justify;">
  When talking about client-side validation we are discussing ways to ensure that the user is effectively engaging with the system. By quickly and politely notifying the user of their mistakes, or gently preventing them from making mistakes we can try and prevent frustration, hopefully increasing response rates.
</p>

<p style="text-align: justify;">
  The main theme from my talk from the <a title="2nd Annual European DDI Users Group Meeting" href="www.iza.org/eddi10">European DDI User Group in Utrecht last year</a>, was around looking at how DDI can be transformed for use on the the web. With HTML 5 offering so many new features for data collection on the web, using DDI to leverage these new capabilities. Lets look at two examples from <a title="Google Docs - Putting DDI in the driver’s seat EDDI December 2010" href="https://docs.google.com/present/edit?id=0AcB3UT7DvOCOZGhiZ3A3Zm5fMjk1Zjh2cWJkY3Y&hl=en_GB&authkey=CLarqeoL">the slides for that talk</a>.
</p>

<div style="width: 634px" class="wp-caption aligncenter">
  <a href="http://imgur.com/nHQx7"><img class=" " title="Hosted by imgur.com" src="http://i.imgur.com/nHQx7.png" alt="A question with a numeric domain and specific range" width="624" height="442" /></a>
  
  <p class="wp-caption-text">
    A question with a numeric domain and specific range
  </p>
</div>

<div style="width: 646px" class="wp-caption aligncenter">
  <a href="http://imgur.com/P40c1"><img class=" " title="Hosted by imgur.com" src="http://i.imgur.com/P40c1.png" alt="A question with a text domain and specific pattern" width="636" height="424" /></a>
  
  <p class="wp-caption-text">
    A question with a text domain and specific pattern
  </p>
</div>

<p style="text-align: justify;">
   
</p>

<p style="text-align: justify;">
  In these examples the colours indicate how the metadata in DDI can be used to populate a webform. Although there may be debate about the use of some DDI data for certain parts of the HTML Form, this demonstrates how this data can immediately be used. To see this in action there is an example at <a title="Sandbox - DDI HTML5 Example" href="http://sandbox.kidstrythisathome.com/dditools/examples/ddi_html5.html">sandbox.kidstrythisathome.com</a>.
</p>

<p style="text-align: justify;">
  For legacy browsers that don&#8217;t support HTML5, this still isn&#8217;t a huge issue as these can &#8216;fake&#8217; a lot of this functionality with Javascript. This can be accomplished either through the use of <a title="HTML5 Cross Browser Polyfills" href="https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-browser-Polyfills">libraries to add HTML5 functionality to legacy browsers</a> or designing transforms and proprietary Javascript to handle the user interface. The idea however, is to provide users with gentle hints to encourage them to provide the &#8216;right&#8217; answers (ages aren&#8217;t words, and must be over 0) not to provide security about the data&#8230;
</p>

<h2 style="text-align: justify;">
  Server-side / data validation
</h2>

<p style="text-align: justify;">
  That is the role of server or data validation, to ensure that the data that we have recieve is correct. As mentioned, on a webpage hints for the user are provided using javascript or through browser APIs. However, it is trivial for a user to bypass this on a client. Client-side validation should not be relied upon as the client can transmit back almost anything. The issue is that server-side validation is must less well defined: while HTML is a web known standard there is no ubiquitous langauge for server-side systems. However, the trade-off is that the programmer has complete control over the actions of the server.
</p>

<p style="text-align: justify;">
  So what should a programmer do to support good validation of data? The idea I approach in Ramona, was that each question was an object of a question in its own right. Furthermore, by using object inheritence in Python, the question class was sub-classed so that each ResponseDomain in DDI had its own class. This allowed each sub-class to define its own exceptions and errors, as well as inheriting those of the question super class.
</p>

<p style="text-align: justify;">
  For example, the question class defined the &#8216;validate&#8217; method, that each sub-class would futher implement in diferent ways. Numeric questions would check their upper and lower bounds and throw exceptions if the response was outside this range, string questions would check the response against the pattern, etc.. and the server would pass the returned value to each class to validate in order.
</p>

<p style="text-align: justify;">
  In summary, DDI provides excellent support for questionnaire designs looking to control response from users and with this metadata provided in an accessible way providing application support for this an easy way for developers to promote DDI by demonstrating the real-world applications of DDI.
</p>

<p style="text-align: justify;">
  Next up… Questionnaire Design with DDI – Part 5: Can it be done? &#8211; A look back at the previous 3 tutorials and an indepth explanation of the realisation of a Ramona &#8211; A functional DDI Questionnaire tool.
</p>