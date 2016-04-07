---
id: 557
title: 'When DDI isn&#8217;t enough Part 2 &#8211; XSI Type and DDI'
date: 2012-08-16T10:18:11+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=557
permalink: /2012/08/when-ddi-isnt-enough-part-2-xsi-type-and-ddi/
aktt_notify_twitter:
  - yes
aktt_tweeted:
  - 1
categories:
  - Metadata
  - Programming
tags:
  - DDI
  - DDIX
  - "I'll make my own specification with blackjack..."
  - XML Schema
---
So a colleague left a comment on the [last post of extending DDI](http://www.kidstrythisathome.com/2012/08/when-ddi-isnt-enough-xml-schema-extensions-and-ddi/ "When DDI isn’t enough – XML Schema Extensions and DDI") that brought my attention to the use of XSI:Type extensions to XML elements, that for lack of a better term make my last post look like childs&#8217; play! After having a quick look, this technique can basically be used to make _additions_ to practically every part of an XML-based data model &#8211; such as DDI. The important question is how does it work?

When we add an element is definition is implicitly determined by its namespace and element. This definition tells us  exactly what attributes and elements are required or optional. What we can do, is add an explicit type to the element that allows us to add an extended definition to the element.

For example, in the last post, there is a demonstration of an Extended Conditional Text object that includes default and static text options. The downside of this is that a tool that handles the basic (non-extended) DDI 3.1 schema would not be able to use this content as it is, for all intents and purposes, hidden. An alternative approach is to use the ExtendedConditonalTextType we defined in the previous blog post, and instead of creating a new element, declare our standard DDI ConditionalText to be an extension of this within the XML, like so:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;d:ConditionalText</span> <span style="color: #000066;">xsi:type</span>=<span style="color: #ff0000;">"xd:ConditionalText"</span> <span style="color: #000066;">xmlns:xd</span>=<span style="color: #ff0000;">"ddi:ExtendedDataCollection:3_1"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;d:Expression<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;r:Code</span> <span style="color: #000066;">programmingLanguage</span>=<span style="color: #ff0000;">"Pseudocode"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>if sex == 'Male' {return 'he'} else if sex == 'Female' {return 'she'} else {return 'they'}<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/r:Code<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/d:Expression<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xd:Default<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>...<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xd:Default<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xd:Static<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>he/she<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xd:Static<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/d:ConditionalText<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

What this achieves is the ability to _add_(1) additional elements to the ConditionalText, without having to create a new element. Any software that can process an element of this type can continue to work, without having to accomodate any changes, and any additional elements will be (or should be ignored).

As a second example of an extension thats already being used we will look at [Algenta&#8217;s Colectica tool, which is probably the leading DDI Editor available](http://www.colectica.com/ "Colectica"). This software introduced the ability to document the approximate time taken to complete a question. While this &#8220;time taken&#8221; content is being add to the DDI 3.2 specification, in DDI 3.1, this information is currently stored as a Note, making management and distribution of this information difficult (we will cover why Notes are difficult to manage in the next section of this now 3-part tutorial).

An alternative approach is through the creation of a new XML Schema complex type combined with the use of a similar XSI:Type extension. Below is an example of the XML Schema required to describe the additional element required.

Here we see the declaration of the element type, as well as its extension and lastly the new element <ApproximateTimeToComplete>. Its important to note that rather than having a basic numeric string for seconds or minutes, we are reusing the [XML data type](http://www.w3.org/TR/xmlschema-2/), [So a colleague left a comment on the [last post of extending DDI](http://www.kidstrythisathome.com/2012/08/when-ddi-isnt-enough-xml-schema-extensions-and-ddi/ "When DDI isn’t enough – XML Schema Extensions and DDI") that brought my attention to the use of XSI:Type extensions to XML elements, that for lack of a better term make my last post look like childs&#8217; play! After having a quick look, this technique can basically be used to make _additions_ to practically every part of an XML-based data model &#8211; such as DDI. The important question is how does it work?

When we add an element is definition is implicitly determined by its namespace and element. This definition tells us  exactly what attributes and elements are required or optional. What we can do, is add an explicit type to the element that allows us to add an extended definition to the element.

For example, in the last post, there is a demonstration of an Extended Conditional Text object that includes default and static text options. The downside of this is that a tool that handles the basic (non-extended) DDI 3.1 schema would not be able to use this content as it is, for all intents and purposes, hidden. An alternative approach is to use the ExtendedConditonalTextType we defined in the previous blog post, and instead of creating a new element, declare our standard DDI ConditionalText to be an extension of this within the XML, like so:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;d:ConditionalText</span> <span style="color: #000066;">xsi:type</span>=<span style="color: #ff0000;">"xd:ConditionalText"</span> <span style="color: #000066;">xmlns:xd</span>=<span style="color: #ff0000;">"ddi:ExtendedDataCollection:3_1"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;d:Expression<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;r:Code</span> <span style="color: #000066;">programmingLanguage</span>=<span style="color: #ff0000;">"Pseudocode"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>if sex == 'Male' {return 'he'} else if sex == 'Female' {return 'she'} else {return 'they'}<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/r:Code<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/d:Expression<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xd:Default<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>...<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xd:Default<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xd:Static<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>he/she<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xd:Static<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/d:ConditionalText<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

What this achieves is the ability to _add_(1) additional elements to the ConditionalText, without having to create a new element. Any software that can process an element of this type can continue to work, without having to accomodate any changes, and any additional elements will be (or should be ignored).

As a second example of an extension thats already being used we will look at [Algenta&#8217;s Colectica tool, which is probably the leading DDI Editor available](http://www.colectica.com/ "Colectica"). This software introduced the ability to document the approximate time taken to complete a question. While this &#8220;time taken&#8221; content is being add to the DDI 3.2 specification, in DDI 3.1, this information is currently stored as a Note, making management and distribution of this information difficult (we will cover why Notes are difficult to manage in the next section of this now 3-part tutorial).

An alternative approach is through the creation of a new XML Schema complex type combined with the use of a similar XSI:Type extension. Below is an example of the XML Schema required to describe the additional element required.

Here we see the declaration of the element type, as well as its extension and lastly the new element <ApproximateTimeToComplete>. Its important to note that rather than having a basic numeric string for seconds or minutes, we are reusing the [XML data type](http://www.w3.org/TR/xmlschema-2/),](http://www.w3.org/TR/xmlschema-2/#duration) - an implement of the duration portion of the [ISO 8601 Date Time standard](www.iso.org/iso/catalogue_detail?csnumber=40874 "ISO 8601").

When we combine these we get a [QuestionItem](http://www.ddialliance.org/sites/default/files/documentation/ddi3.1/schemas/datacollection_xsd/elements/QuestionItem.html) that looks similar to that below:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;d:QuestionItem</span> <span style="color: #000066;">id</span>=<span style="color: #ff0000;">"exampleQuestion"</span> <span style="color: #000066;">xsi:type</span>=<span style="color: #ff0000;">"xd:QuestionItemWithTimeTaken"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;d:QuestionText<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;d:LiteralText<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;d:Text<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>You told me your dog likes to play fetch, what does <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/d:Text<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/d:LiteralText<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;d:ConditionalText</span> <span style="color: #000066;">xsi:type</span>=<span style="color: #ff0000;">"xd:ExtendedConditionalTextType"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;d:Expression<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;r:Code</span> <span style="color: #000066;">programmingLanguage</span>=<span style="color: #ff0000;">"Pseudocode"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>if sex == 'Male' {return 'he'} else if sex == 'Female' {return 'she'} else {return 'they'}<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/r:Code<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/d:Expression<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xd:Default<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>...<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xd:Default<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xd:Static<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>he/she<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xd:Static<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/d:ConditionalText<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/d:QuestionText<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;d:TextDomain</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xd:ApproximateTimeToComplete<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>PT2M30S<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xd:ApproximateTimeToComplete<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/d:QuestionItem<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

When this is all put together, we get an XML fragment, that can be widely understood by DDI compliant software, but also contains additional metadata necessary for specific agencies or applications.

Just like last time, the full code for the above examples is available on pastebin &#8211; with the [Extensions schema](http://pastebin.com/KgLTPFdR), and the [example DDI Instance](http://pastebin.com/Y8854kXh) both available for review. In the next post I&#8217;ll go over each of these two approaches and cover their advantages, pitfalls, and when to use each &#8211; as well as covering why with both of these approaches, why Notes are unnecessary and what implications this has for the standard in general.

Footnote:

  1. As of yet I haven&#8217;t figure out how to remove elements (or if it is even possible) &#8230; I wouldn&#8217;t hold your breath for this one.