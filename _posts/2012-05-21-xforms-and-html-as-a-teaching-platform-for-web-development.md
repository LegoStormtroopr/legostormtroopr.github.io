---
id: 483
title: XForms and HTML as a teaching platform for web development
date: 2012-05-21T11:33:55+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=483
permalink: /2012/05/xforms-and-html-as-a-teaching-platform-for-web-development/
aktt_notify_twitter:
  - yes
aktt_tweeted:
  - 1
categories:
  - Drivel
  - Education
tags:
  - HTML
  - MVC
  - XForms
---
I&#8217;ve found myself getting into discussions on how to teach programming recently. As is often the case various people will talk about how their preferred language is the best language to teach in. However, each programming language has its own pros and cons &#8211; for example, Haskell is ideal for teaching functional programming, but would be terrible for teaching Object-oriented programming. I like to think I take a more moderate approach and suggest languages on their applicability to concepts being taught (but realistically I think python is great for everything!).

Recently I&#8217;ve been doing some research at work with XForms, and I&#8217;ve come to the conclusion that it is an ideal language for teaching model-view-controller (MVC) architecture. While web frameworks like Ruby on Rails have support for generating web applications using MVC, to work with this frameworks often requires an understanding of the frameworks language and the framework itself, some database knowledge and HTML and CSS. While not difficult, for the purposes of teaching a concept, the less time setting up an environment the more time dedicated to theory.

Alternatively, an XForms application is built entirely using MVC principles in a single file on a desktop machine with no setup. Despite the low adoption of client side XForms support, with the single XML directive below and the support of XSLTForms this is of no concern.

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;?xml-stylesheet</span> <span style="color: #000066;">href</span>=<span style="color: #ff0000;">"http://www.agencexml.com/xsltforms/xsltforms/xsltforms.xsl"</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"text/xsl"</span><span style="color: #000000; font-weight: bold;">?&gt;</span></span></pre>
      </td>
    </tr>
  </table>
</div>

Below is a simple &#8220;Hello world&#8221; app in XForms that demonstrates the major principles of MVC in 26 lines. This simple code displays a webpage that requests a name and updates an output field.

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;?xml</span> <span style="color: #000066;">version</span>=<span style="color: #ff0000;">"1.0"</span> <span style="color: #000066;">encoding</span>=<span style="color: #ff0000;">"UTF-8"</span><span style="color: #000000; font-weight: bold;">?&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;?xml-stylesheet</span> <span style="color: #000066;">href</span>=<span style="color: #ff0000;">"http://www.agencexml.com/xsltforms/xsltforms/xsltforms.xsl"</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"text/xsl"</span><span style="color: #000000; font-weight: bold;">?&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;html</span> <span style="color: #000066;">xmlns</span>=<span style="color: #ff0000;">"http://www.w3.org/1999/xhtml"</span> <span style="color: #000066;">xmlns:xforms</span>=<span style="color: #ff0000;">"http://www.w3.org/2002/xforms"</span> <span style="color: #000000; font-weight: bold;">&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;head<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;style</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"text/css"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
        label {
            color: red;
        }
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/style<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xforms:model<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xforms:instance<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;PersonGivenName</span> <span style="color: #000066;">xmlns</span>=<span style="color: #ff0000;">""</span> <span style="color: #000000; font-weight: bold;">/&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xforms:instance<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xforms:bind</span> <span style="color: #000066;">id</span>=<span style="color: #ff0000;">"FirstName"</span> <span style="color: #000066;">nodeset</span>=<span style="color: #ff0000;">"/PersonGivenName"</span> <span style="color: #000000; font-weight: bold;">/&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xforms:model<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/head<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;body<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xforms:input</span> <span style="color: #000066;">bind</span>=<span style="color: #ff0000;">"FirstName"</span> <span style="color: #000066;">incremental</span>=<span style="color: #ff0000;">"true"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xforms:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Input your first name:<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xforms:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xforms:input<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;br</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xforms:output</span> <span style="color: #000066;">bind</span>=<span style="color: #ff0000;">"FirstName"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xforms:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Hello <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xforms:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xforms:output<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>!
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/body<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/html<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

This simple program can demonstrate the importance of separating content and presentation (using CSS and HTML classes), but also shows of the MVC components of XForms.

Here our Model (the xforms:instance element) holds our data model, the xforms:bind element in the xforms:model holds our controller. Using this we can illustrate how we can change our data model and controllers without impacting the view at all. For example, by changing the xforms:model like so:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;?xml</span> <span style="color: #000066;">version</span>=<span style="color: #ff0000;">"1.0"</span> <span style="color: #000066;">encoding</span>=<span style="color: #ff0000;">"UTF-8"</span><span style="color: #000000; font-weight: bold;">?&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;?xml-stylesheet</span> <span style="color: #000066;">href</span>=<span style="color: #ff0000;">"http://www.agencexml.com/xsltforms/xsltforms/xsltforms.xsl"</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"text/xsl"</span><span style="color: #000000; font-weight: bold;">?&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;html</span> <span style="color: #000066;">xmlns</span>=<span style="color: #ff0000;">"http://www.w3.org/1999/xhtml"</span> <span style="color: #000066;">xmlns:xforms</span>=<span style="color: #ff0000;">"http://www.w3.org/2002/xforms"</span> <span style="color: #000000; font-weight: bold;">&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;head<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;style</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"text/css"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
        label {
            color: red;
        }
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/style<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xforms:model<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xforms:instance<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;PersonName</span> <span style="color: #000066;">xmlns</span>=<span style="color: #ff0000;">""</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;First</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;Last</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/PersonName<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xforms:instance<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xforms:bind</span> <span style="color: #000066;">id</span>=<span style="color: #ff0000;">"FirstName"</span> <span style="color: #000066;">nodeset</span>=<span style="color: #ff0000;">"/PersonName/First"</span> <span style="color: #000000; font-weight: bold;">/&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xforms:model<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/head<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;body<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xforms:input</span> <span style="color: #000066;">bind</span>=<span style="color: #ff0000;">"FirstName"</span> <span style="color: #000066;">incremental</span>=<span style="color: #ff0000;">"true"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xforms:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Input your first name:<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xforms:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xforms:input<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;br</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xforms:input</span> <span style="color: #000066;">bind</span>=<span style="color: #ff0000;">"LastName"</span> <span style="color: #000066;">incremental</span>=<span style="color: #ff0000;">"true"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xforms:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Input your last name:<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xforms:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xforms:input<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;br</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xforms:output</span> <span style="color: #000066;">bind</span>=<span style="color: #ff0000;">"FirstName"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xforms:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Hello <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xforms:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xforms:output<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>!
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/body<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/html<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

Here we have updated the model to support full names, without altering the view &#8211; an important principle when teaching MVC. It is left as an exercise for the reader to add controls to store a last name.

While this is a relatively trivial example, as a teaching tool XForms shows extraordinary promise for teaching the model-view-controller approach to design due to its strictly controlled syntax and ease of use to write and deploy in small scale environments.