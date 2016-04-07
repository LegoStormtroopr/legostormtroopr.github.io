---
id: 3798
title: 'Practical XForms &#8211; Todo-list &#8211; Part 1: Building and showing the data model'
date: 2013-07-27T02:07:26+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=3798
permalink: /2013/07/practical-xforms-todo-list-part-1-building-and-showing-the-data-model/
categories:
  - Programming
  - Web Development
tags:
  - Tutorial
  - XForms
---
There was a recent post on [Stack Overflow](http://stackoverflow.com/ "Stack Overflow") that was looking for the simplest way to create  a simple Todo list in HTML. Many of the comments highlighted the fact that HTML really has no dynamicness &#8220;built-in&#8221;&#8221; and began offering different Javascript libraries for building complex UIs and how to manage the connection between the two. Sadly the post was removed as a duplicate before I got a chance to offer an alternative &#8211; [XForms](http://www.w3.org/MarkUp/Forms/ "W3C XForms website"). Despite low browser uptake, I am quite the fan of XForms, and given mature tools like [XSLTForms](http://www.agencexml.com/xsltforms "XSLTForms") that allow you to build an XForm and deploy to any [XSLT](http://www.w3.org/TR/xslt "W3C XSLT Webpage") enabled browser (which is almost all of them now). So with that long introduction done, I present this simple introduction to developing with XForms.

* * *

The to-do list is probably the second most prevalent programming tutorial available after &#8220;hello-world&#8221; especially for GUI development. So I present a simple tutorial to build a to-do list in XForms to offer a gentle introduction into the power of novel language. Before continuing you should probably have a small understanding of how to make forms in HTML, XML and XPath.

## Building our data model

[XForms has a strong adherence to the MVC paradigm](http://www.kidstrythisathome.com/2012/05/xforms-and-html-as-a-teaching-platform-for-web-development/ "XForms and HTML as a teaching platform for web development") and its strong separation of data and presentation so the first thing we can do is describe our data model. Given that we are building a simple to-do list at this stage we need to be able to capture 3 things:

  1. <span style="line-height: 13px;">The task name</span>
  2. The due date and
  3. If the task has been completed

Now given that all data for an XForm is captured within an XML document, we can immediately begin to know that our data model is going to look something like this:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="line_numbers">
        <pre>1
</pre>
      </td>
      
      <td class="code">
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;task</span> <span style="color: #000066;">complete</span>=<span style="color: #ff0000;">"false"</span> <span style="color: #000066;">dueDate</span>=<span style="color: #ff0000;">"2013-07-27"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>Pick up milk<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/task<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

By wrapping this in an [XForms:model](http://www.w3.org/TR/xforms/#structure-model "XForms Model element") element, we are done describing our data model. and convention dictates that this goes in the head of a document so, wrapping this all up in XML we get&#8230;

<div class="wp_syntax">
  <table>
    <tr>
      <td class="line_numbers">
        <pre>1
2
3
4
5
6
7
8
9
10
11
12
</pre>
      </td>
      
      <td class="code">
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;?xml-stylesheet</span> <span style="color: #000066;">href</span>=<span style="color: #ff0000;">"xsltforms/xsltforms.xsl"</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"text/xsl"</span><span style="color: #000000; font-weight: bold;">?&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;html</span> <span style="color: #000066;">xmlns</span>=<span style="color: #ff0000;">"http://www.w3.org/1999/xhtml"</span> <span style="color: #000066;">xmlns:xf</span>=<span style="color: #ff0000;">"http://www.w3.org/2002/xforms"</span> <span style="color: #000000; font-weight: bold;">&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;head<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;title<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>XForms todo list<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/title<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:model<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:instance</span> <span style="color: #000066;">xmlns</span>=<span style="color: #ff0000;">""</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;task</span> <span style="color: #000066;">complete</span>=<span style="color: #ff0000;">"false"</span> <span style="color: #000066;">dueDate</span>=<span style="color: #ff0000;">"2013-07-27"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>Pick up milk<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/task<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:instance<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:model<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/head<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;body</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/html<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

Along with the model there is some boilerplate HTML and an XML directive that calls XSLTForms so we can preview this in a web browser. Sadly, since we only have only defined our data there is nothing to see, yet&#8230;

## Interacting with the data model

So with a piece of data defined, we can start building a way to actually interact with this. This is done through [XForms input](http://www.w3.org/TR/xforms/#ui-input "XForms input element") fields. Inserting an XForms element is very similar to using regular HTML inputs, however rather than giving it a name we need to point to an element or binding (which we will cover later) to store and retrieve data from.

<div class="wp_syntax">
  <table>
    <tr>
      <td class="line_numbers">
        <pre>1
2
3
</pre>
      </td>
      
      <td class="code">
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:input</span> <span style="color: #000066;">ref</span>=<span style="color: #ff0000;">"//task"</span> <span style="color: #000000; font-weight: bold;">/&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:input</span> <span style="color: #000066;">ref</span>=<span style="color: #ff0000;">"//task/@complete"</span> <span style="color: #000000; font-weight: bold;">/&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:input</span> <span style="color: #000066;">ref</span>=<span style="color: #ff0000;">"//task/@dueDate"</span> <span style="color: #000000; font-weight: bold;">/&gt;</span></span></pre>
      </td>
    </tr>
  </table>
</div>

These pointers are either named bindings, or in the case above an XPath to an element in the data model. In the first we are pointing to the **//task** node, which will use the text of that node for the field, however in the others we are pointing to an attribute, eg. **//task/@dueDate** .

However, in the above case it will just a field with no label or indication of what it is, so we will add a label as well (I&#8217;ll just demonstrate the label task name):

<div class="wp_syntax">
  <table>
    <tr>
      <td class="line_numbers">
        <pre>1
2
3
</pre>
      </td>
      
      <td class="code">
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:input</span> <span style="color: #000066;">ref</span>=<span style="color: #ff0000;">"//task"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Task name:<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:input<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

So now our complete document looks something like this:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="line_numbers">
        <pre>1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
</pre>
      </td>
      
      <td class="code">
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;?xml-stylesheet</span> <span style="color: #000066;">href</span>=<span style="color: #ff0000;">"xsltforms/xsltforms.xsl"</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"text/xsl"</span><span style="color: #000000; font-weight: bold;">?&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;html</span> <span style="color: #000066;">xmlns</span>=<span style="color: #ff0000;">"http://www.w3.org/1999/xhtml"</span> <span style="color: #000066;">xmlns:xf</span>=<span style="color: #ff0000;">"http://www.w3.org/2002/xforms"</span> <span style="color: #000000; font-weight: bold;">&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;head<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;title<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>XForms todo list<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/title<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:model<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:instance</span> <span style="color: #000066;">xmlns</span>=<span style="color: #ff0000;">""</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;task</span> <span style="color: #000066;">complete</span>=<span style="color: #ff0000;">"false"</span> <span style="color: #000066;">dueDate</span>=<span style="color: #ff0000;">"2013-07-27"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>Pick up milk<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/task<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:instance<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:model<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/head<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;body<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:input</span> <span style="color: #000066;">ref</span>=<span style="color: #ff0000;">"//task"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Task name:<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:input<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:input</span> <span style="color: #000066;">ref</span>=<span style="color: #ff0000;">"//task/@complete"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Complete:<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:input<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:input</span> <span style="color: #000066;">ref</span>=<span style="color: #ff0000;">"//task/@dueDate"</span> <span style="color: #000000; font-weight: bold;">&gt;</span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Due date:<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:input<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/body<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/html<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

And it looks like this:

<div style="width: 505px" class="wp-caption alignnone">
  <img alt="A screenshot of the partially complete todo list" src="http://i.imgur.com/WZtkLjV.png" width="495" height="245" />
  
  <p class="wp-caption-text">
    Our basic to do list
  </p>
</div>

Now, there are a lot of flaws with this the two big ones being that we can only manage one task, and we have defined what is valid data for any of our fields. But we&#8217;ll take care of these in the next two tutorials. But for now, we&#8217;ll fix one flaw and add a little CSS styling to present the form in a better way to finish off this example. What we want is to have each field on their own line and have the fields all line up. Fortunately this is easy in to achieve in CSS:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="line_numbers">
        <pre>1
2
3
4
5
6
7
</pre>
      </td>
      
      <td class="code">
        <pre class="css" style="font-family:monospace;"><span style="color: #6666ff;">.xforms-input</span>  <span style="color: #00AA00;">&#123;</span>
   <span style="color: #000000; font-weight: bold;">display</span><span style="color: #00AA00;">:</span><span style="color: #993333;">block</span><span style="color: #00AA00;">;</span>
<span style="color: #00AA00;">&#125;</span>
<span style="color: #6666ff;">.xforms-label</span> <span style="color: #00AA00;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">display</span><span style="color: #3333ff;">:inline-</span>block<span style="color: #00AA00;">;</span>
    <span style="color: #000000; font-weight: bold;">width</span><span style="color: #00AA00;">:</span><span style="color: #933;">5em</span><span style="color: #00AA00;">;</span>
<span style="color: #00AA00;">&#125;</span></pre>
      </td>
    </tr>
  </table>
</div>

Because we&#8217;re using an internal CSS stylesheet, we need to use the [CSS classes that target the HTML generated by XSLTForms](http://en.wikibooks.org/wiki/XSLTForms/CSS "XSLTForms and CSS"), but when using an [external stylesheet namespace CSS selectors](http://en.wikibooks.org/wiki/XRX/XSLTForms_and_eXist#Modifying_your_CSS_to_work_with_XSLTForms "Modifying your CSS to work with XSLTForms") can be used. Adding this into the document we get the following code ([which you can very and fork on GitHub](https://github.com/LegoStormtroopr/xforms-todo-list/blob/master/xforms-todo-part1.xml "XForms GitHub Part 1")):

<div class="wp_syntax">
  <table>
    <tr>
      <td class="line_numbers">
        <pre>1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
</pre>
      </td>
      
      <td class="code">
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;?xml-stylesheet</span> <span style="color: #000066;">href</span>=<span style="color: #ff0000;">"xsltforms/xsltforms.xsl"</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"text/xsl"</span><span style="color: #000000; font-weight: bold;">?&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;html</span> <span style="color: #000066;">xmlns</span>=<span style="color: #ff0000;">"http://www.w3.org/1999/xhtml"</span> <span style="color: #000066;">xmlns:xf</span>=<span style="color: #ff0000;">"http://www.w3.org/2002/xforms"</span> <span style="color: #000000; font-weight: bold;">&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;head<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;title<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>XForms todo list<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/title<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:model<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:instance</span> <span style="color: #000066;">xmlns</span>=<span style="color: #ff0000;">""</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;task</span> <span style="color: #000066;">complete</span>=<span style="color: #ff0000;">"false"</span> <span style="color: #000066;">dueDate</span>=<span style="color: #ff0000;">"2013-07-27"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>Pick up milk<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/task<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:instance<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:model<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;style</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"text/css"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
            .xforms-input {
            display:block;
        }
        .xforms-label {
            display:inline-block;
            width:5em;
        }
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/style<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/head<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;body<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:input</span> <span style="color: #000066;">ref</span>=<span style="color: #ff0000;">"//task"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Task name:<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:input<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:input</span> <span style="color: #000066;">ref</span>=<span style="color: #ff0000;">"//task/@complete"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Complete:<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:input<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:input</span> <span style="color: #000066;">ref</span>=<span style="color: #ff0000;">"//task/@dueDate"</span> <span style="color: #000000; font-weight: bold;">&gt;</span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Due date:<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:input<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/body<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/html<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

and it looks like this:

<div style="width: 505px" class="wp-caption alignnone">
  <img alt="A screenshot of the complete part 1 of the todo list" src="http://i.imgur.com/afCrp3D.png" width="495" height="245" />
  
  <p class="wp-caption-text">
    Our final todo list
  </p>
</div>

And there we have it a very simple, XForm built on a pre-defined data model using a declarative language that required very little coding to get done. In the next tutorial we will look at how we can alter our data and interface to display and edit multiple tasks as well as adding and deleting tasks.