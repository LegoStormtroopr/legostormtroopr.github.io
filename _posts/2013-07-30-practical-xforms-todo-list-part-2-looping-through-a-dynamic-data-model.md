---
id: 3817
title: 'Practical XForms – Todo-list – Part 2: Looping through a dynamic data model'
date: 2013-07-30T11:27:38+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=3817
permalink: /2013/07/practical-xforms-todo-list-part-2-looping-through-a-dynamic-data-model/
categories:
  - Programming
  - Web Development
tags:
  - Tutorial
  - XForms
---
In the [previous tutorial we began building an XForms to-do list](http://bit.ly/14SWrQG "Practical XForms – Todo-list – Part 1: Building and showing the data model"). The last exercise left us with a to-do list that allowed us to view an edit a single task, not terribly useful, but a starting point. In this tutorial we are going to build on the first and allow a user to manage multiple tasks.

<div style="width: 505px" class="wp-caption alignnone">
  <img alt="A screenshot of the complete part 1 of the todo list" src="http://i.imgur.com/afCrp3D.png" width="495" height="245" />
  
  <p class="wp-caption-text">
    Our todo list where we left off.
  </p>
</div>

##  Extending our data model

As with the first tutorial, the first thing we need to do is work with the data model, altering it to allow for the management of multiple tasks. To do this we will change our [XForms data instance](http://www.w3.org/TR/xforms/#concepts-xml-instance-data "XForms data instances") to capture a task list which itself contains a number of tasks.

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
</pre>
      </td>
      
      <td class="code">
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:instance</span> <span style="color: #000066;">xmlns</span>=<span style="color: #ff0000;">""</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;tasklist<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;task</span> <span style="color: #000066;">complete</span>=<span style="color: #ff0000;">"false"</span> <span style="color: #000066;">dueDate</span>=<span style="color: #ff0000;">"2013-07-27"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>Pick up milk<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/task<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;task</span> <span style="color: #000066;">complete</span>=<span style="color: #ff0000;">"true"</span> <span style="color: #000066;">dueDate</span>=<span style="color: #ff0000;">"2013-07-27"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>Make tutorial part 1<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/task<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/tasklist<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:instance<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

Unfortunately, the XForms will continue to look the same as the inputs that were placed in HTML the first tutorial expect a single task.

## Looping through the data model

Having defined our repeating data instance, writing the declarations for a repeating user interface becomes a trivial affair &#8211; we simply need to wrap our current elements in an [In the [previous tutorial we began building an XForms to-do list](http://bit.ly/14SWrQG "Practical XForms – Todo-list – Part 1: Building and showing the data model"). The last exercise left us with a to-do list that allowed us to view an edit a single task, not terribly useful, but a starting point. In this tutorial we are going to build on the first and allow a user to manage multiple tasks.

<div style="width: 505px" class="wp-caption alignnone">
  <img alt="A screenshot of the complete part 1 of the todo list" src="http://i.imgur.com/afCrp3D.png" width="495" height="245" />
  
  <p class="wp-caption-text">
    Our todo list where we left off.
  </p>
</div>

##  Extending our data model

As with the first tutorial, the first thing we need to do is work with the data model, altering it to allow for the management of multiple tasks. To do this we will change our [XForms data instance](http://www.w3.org/TR/xforms/#concepts-xml-instance-data "XForms data instances") to capture a task list which itself contains a number of tasks.

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
</pre>
      </td>
      
      <td class="code">
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:instance</span> <span style="color: #000066;">xmlns</span>=<span style="color: #ff0000;">""</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;tasklist<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;task</span> <span style="color: #000066;">complete</span>=<span style="color: #ff0000;">"false"</span> <span style="color: #000066;">dueDate</span>=<span style="color: #ff0000;">"2013-07-27"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>Pick up milk<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/task<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;task</span> <span style="color: #000066;">complete</span>=<span style="color: #ff0000;">"true"</span> <span style="color: #000066;">dueDate</span>=<span style="color: #ff0000;">"2013-07-27"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>Make tutorial part 1<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/task<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/tasklist<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:instance<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

Unfortunately, the XForms will continue to look the same as the inputs that were placed in HTML the first tutorial expect a single task.

## Looping through the data model

Having defined our repeating data instance, writing the declarations for a repeating user interface becomes a trivial affair &#8211; we simply need to wrap our current elements in an](http://www.w3.org/TR/xforms/#ui-repeat-module "XForms repeat module") (sorry for the repetition (and that pun)). The nodeset or binding in a repeat element allows us to point to a set of elements that will have the child xforms controls under the repeat applied the them.

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
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:repeat</span> <span style="color: #000066;">nodeset</span>=<span style="color: #ff0000;">"/tasklist/task"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
        ...
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:repeat<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

So in the above code we are declaring that we are repeating across the task elements under the tasklist node. In this case we have been very specific, declaring the XPath for the repeated element, but  the important thing to note, is that this would repeat any matching elements. So if we had multiple tasklists, we could target all tasks by using the Xpath &#8220;//task&#8221;.

Now that we have declared what elements to loop over, the next task is to change the inputs to be relative to the repeated element, so inside the body we get:

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
</pre>
      </td>
      
      <td class="code">
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:repeat</span> <span style="color: #000066;">nodeset</span>=<span style="color: #ff0000;">"/tasklist/task"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:input</span> <span style="color: #000066;">ref</span>=<span style="color: #ff0000;">"."</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Task name:<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:input<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:input</span> <span style="color: #000066;">ref</span>=<span style="color: #ff0000;">"@complete"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Complete:<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:input<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:input</span> <span style="color: #000066;">ref</span>=<span style="color: #ff0000;">"@dueDate"</span> <span style="color: #000000; font-weight: bold;">&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Due date:<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:input<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:repeat<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

And our form now looks like this:

<div style="width: 505px" class="wp-caption alignnone">
  <img alt="A repeating form." src="http://i.imgur.com/FarqVaw.png" width="495" height="245" />
  
  <p class="wp-caption-text">
    A repeating form.
  </p>
</div>

Sadly, while we are getting the intended repetitions, it doesn&#8217;t look right.

## Intertwining HTML and XForms

What we have here isn&#8217;t just a set of some unrelated fields, but could be argued to be tabular data. So we should mark it up as such. Fortunately, inside a repeat element everything is repeated, not just the XForms controls. So, by adding a table wrapper with appropriate headings, we can wrap the repeat like so:

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
</pre>
      </td>
      
      <td class="code">
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;table<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;thead<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;tr<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;th<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Task name<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/th<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;th<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Complete<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/th<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;th<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Due date<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/th<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/tr<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/thead<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;tbody<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:repeat</span> <span style="color: #000066;">nodeset</span>=<span style="color: #ff0000;">"/tasklist/task"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;tr<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
               <span style="color: #808080; font-style: italic;">&lt;!-- Each xf:input wrapped in its own td --&gt;</span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/tr<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:repeat<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/tbody<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/table<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

Since we now have labels for each field in the header, we can remove them and we get something that looks like this:

<div style="width: 493px" class="wp-caption alignnone">
  <img alt="A tabular to-do list" src="http://i.imgur.com/g7D9tpW.png" width="483" height="245" />
  
  <p class="wp-caption-text">
    A tabular to-do list
  </p>
</div>

This could have also been done using only CSS (and I&#8217;ll leave the arguments about table layouts for the comments).

## Reviwing our HTML+XForm so far

Now is a good point to show all of the code and look at the changes. So far this tutorial we&#8217;ve extended the data model, wrapped our inputs inside of a repeat, and we&#8217;ve remove the labels in lieu of table headers and remove the CSS as our inputs are now wrapped in table cells:

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
32
33
34
</pre>
      </td>
      
      <td class="code">
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;?xml-stylesheet</span> <span style="color: #000066;">href</span>=<span style="color: #ff0000;">"xsltforms/xsltforms.xsl"</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"text/xsl"</span><span style="color: #000000; font-weight: bold;">?&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;html</span> <span style="color: #000066;">xmlns</span>=<span style="color: #ff0000;">"http://www.w3.org/1999/xhtml"</span> <span style="color: #000066;">xmlns:xf</span>=<span style="color: #ff0000;">"http://www.w3.org/2002/xforms"</span> <span style="color: #000000; font-weight: bold;">&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;head<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;title<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>XForms todo list<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/title<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:model<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:instance</span> <span style="color: #000066;">xmlns</span>=<span style="color: #ff0000;">""</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;tasklist<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;task</span> <span style="color: #000066;">complete</span>=<span style="color: #ff0000;">"false"</span> <span style="color: #000066;">dueDate</span>=<span style="color: #ff0000;">"2013-07-27"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>Pick up milk<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/task<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;task</span> <span style="color: #000066;">complete</span>=<span style="color: #ff0000;">"true"</span> <span style="color: #000066;">dueDate</span>=<span style="color: #ff0000;">"2013-07-27"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>Make tutorial part 1<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/task<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/tasklist<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:instance<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:model<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/head<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;body<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;table<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;thead<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;tr<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;th<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Task name<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/th<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;th<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Complete<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/th<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;th<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Due date<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/th<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/tr<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/thead<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;tbody<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:repeat</span> <span style="color: #000066;">nodeset</span>=<span style="color: #ff0000;">"/tasklist/task"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
                    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;tr<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;td<span style="color: #000000; font-weight: bold;">&gt;</span></span><span style="color: #000000; font-weight: bold;">&lt;xf:input</span> <span style="color: #000066;">ref</span>=<span style="color: #ff0000;">"."</span><span style="color: #000000; font-weight: bold;">/&gt;</span><span style="color: #000000; font-weight: bold;">&lt;/td<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;td<span style="color: #000000; font-weight: bold;">&gt;</span></span><span style="color: #000000; font-weight: bold;">&lt;xf:input</span> <span style="color: #000066;">ref</span>=<span style="color: #ff0000;">"@complete"</span><span style="color: #000000; font-weight: bold;">/&gt;</span><span style="color: #000000; font-weight: bold;">&lt;/td<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;td<span style="color: #000000; font-weight: bold;">&gt;</span></span><span style="color: #000000; font-weight: bold;">&lt;xf:input</span> <span style="color: #000066;">ref</span>=<span style="color: #ff0000;">"@dueDate"</span> <span style="color: #000000; font-weight: bold;">/&gt;</span><span style="color: #000000; font-weight: bold;">&lt;/td<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/tr<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:repeat<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/tbody<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/table<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/body<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/html<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

## Adding and deleting tasks

To now we&#8217;ve only been able to manage tasks that already are in the data model, so the next step is to be able to add tasks of our own and delete old ones. To do this we need to add some buttons to the interface. In XForms the HTML button is replaced by an [XForms trigger](http://www.w3.org/TR/xforms/#ui-trigger "XForms Trigger"). So if we insert this code after the table:

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
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:trigger<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Add Task<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:trigger<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

Gives us this:

<div style="width: 484px" class="wp-caption alignnone">
  <img alt="Todo list with a new button" src="http://i.imgur.com/JLLPDUu.png" width="474" height="306" />
  
  <p class="wp-caption-text">
    Todo list with a new button
  </p>
</div>

However, at this point the button still does nothing, we need to attach an [action or multiple actions](http://www.w3.org/TR/xforms/#action-action "XForms actions") to perform for a specific [XForms event](http://www.w3.org/TR/xforms/#rpm-events "XForms events") for this trigger. Actions can be performed for a number of reasons, such as the XForm being refreshed, when data elements are deleted or, as in this case, when a button is triggered. So we can attach an action to the trigger like so:

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
</pre>
      </td>
      
      <td class="code">
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:trigger<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Add Task<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:action</span> <span style="color: #000066;">ev:event</span>=<span style="color: #ff0000;">"DOMActivate"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:insert</span> <span style="color: #000066;">nodeset</span>=<span style="color: #ff0000;">"/tasklist/task"</span> <span style="color: #000066;">at</span>=<span style="color: #ff0000;">"last()"</span> <span style="color: #000066;">position</span>=<span style="color: #ff0000;">"after"</span> <span style="color: #000000; font-weight: bold;">/&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:action<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:trigger<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

In this example, we have an action that is fired when this button is &#8220;activated&#8221;, and this triggers a task to be inserted at the end of the tasklist after the last element. However, the way this works, it will duplicate the last element, so we can remove the data in the new element like this:

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
</pre>
      </td>
      
      <td class="code">
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:trigger<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Add Task<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:action</span> <span style="color: #000066;">ev:event</span>=<span style="color: #ff0000;">"DOMActivate"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:insert</span> <span style="color: #000066;">nodeset</span>=<span style="color: #ff0000;">"/tasklist/task"</span> <span style="color: #000066;">at</span>=<span style="color: #ff0000;">"last()"</span> <span style="color: #000066;">position</span>=<span style="color: #ff0000;">"after"</span> <span style="color: #000000; font-weight: bold;">/&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:setvalue</span> <span style="color: #000066;">ref</span>=<span style="color: #ff0000;">"/tasklist/task[last()]"</span> <span style="color: #000066;">value</span>=<span style="color: #ff0000;">""</span> <span style="color: #000000; font-weight: bold;">/&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:setvalue</span> <span style="color: #000066;">ref</span>=<span style="color: #ff0000;">"/tasklist/task[last()]/@complete"</span> <span style="color: #000066;">value</span>=<span style="color: #ff0000;">"false()"</span> <span style="color: #000000; font-weight: bold;">/&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:setvalue</span> <span style="color: #000066;">ref</span>=<span style="color: #ff0000;">"/tasklist/task[last()]/@dueDate"</span> <span style="color: #000066;">value</span>=<span style="color: #ff0000;">"'1970-01-01'"</span> <span style="color: #000000; font-weight: bold;">/&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:action<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:trigger<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

Here we have set the value of the texts and clears or resets the form data of the new element using the XPath evaluation in the @value attribute &#8211; hence the double quotes and the false() function. This gives us this:

<div style="width: 484px" class="wp-caption alignnone">
  <img alt="A task list with a new task!" src="http://i.imgur.com/zWlcj8k.png" width="474" height="306" />
  
  <p class="wp-caption-text">
    A task list with a new task!
  </p>
</div>

The last thing to do is add a trigger to delete the currently selected row. This is very much like the last:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="line_numbers">
        <pre>1
2
3
4
5
</pre>
      </td>
      
      <td class="code">
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:trigger<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Delete task <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:output</span> <span style="color: #000066;">value</span>=<span style="color: #ff0000;">"index('tasks')"</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:label<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:delete</span> <span style="color: #000066;">ev:event</span>=<span style="color: #ff0000;">"DOMActivate"</span> <span style="color: #000066;">nodeset</span>=<span style="color: #ff0000;">"/tasklist/task"</span> <span style="color: #000066;">at</span>=<span style="color: #ff0000;">"index('tasks')"</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:trigger<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

The two differences are that we have use the ability to shortcut how events are attached to actions. Rather than use an action element, we can attach the event attribute directly to the specific action itself. Secondly, we&#8217;ve also added an output element so we can see which task we are about to delete based on the index of the repeat element (which we have now given the id &#8220;tasks&#8221; to refer to). We can also style the currently listed row using CSS:

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
        <pre class="css" style="font-family:monospace;"><span style="color: #6666ff;">.xforms-repeat-item-selected</span> <span style="color: #00AA00;">*</span> <span style="color: #00AA00;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">background-color</span><span style="color: #00AA00;">:</span> <span style="color: #cc00cc;">#DDF</span><span style="color: #00AA00;">;</span>
<span style="color: #00AA00;">&#125;</span></pre>
      </td>
    </tr>
  </table>
</div>

All up this gives us:

<div style="width: 484px" class="wp-caption alignnone">
  <img alt="A nearly completed XForm to-do list" src="http://i.imgur.com/VKiEbpP.png" width="474" height="306" />
  
  <p class="wp-caption-text">
    A nearly completed XForm to-do list
  </p>
</div>

A nearly complete To-do list! The code is starting to grow, but you can check out the [code on the XForms To-do List Github](https://github.com/LegoStormtroopr/xforms-todo-list/blob/master/xforms-todo-part2.xml "XForms todo list tutorial 2").

In the next tutorial we will look at how we can provide data validation that will both alter our data and interface, and edit the inputs to provide hints when invalid data is entered.