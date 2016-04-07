---
id: 3941
title: 'Practical XForms – Todo-list – Part 3: Adding bindings to collect the correct data'
date: 2013-08-17T07:26:28+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=3941
permalink: /2013/08/practical-xforms-todo-list-part-3-adding-bindings-to-collect-the-correct-data/
categories:
  - Uncategorized
---
This is the third in an ongoing series that examines the practical uses of XForms by building a todo list. In this tutorial we are going to build on [part 1 (where we built our data model)](http://www.kidstrythisathome.com/2013/07/practical-xforms-todo-list-part-1-building-and-showing-the-data-model/ "Practical XForms – Todo-list – Part 1: Building and showing the data model") and [part 2 (where we refined the data model to support looping)](http://www.kidstrythisathome.com/2013/07/practical-xforms-todo-list-part-2-looping-through-a-dynamic-data-model/ "Practical XForms – Todo-list – Part 2: Looping through a dynamic data model"). In this tutorial we will cover ways of using binds and inline schemas to correctly type the data model and use correct input types.

We left of from tutorial 2, with a user interface that looked like this:

<div style="width: 484px" class="wp-caption alignnone">
  <img alt="A nearly completed XForm to-do list" src="http://i.imgur.com/VKiEbpP.png" width="474" height="306" />
  
  <p class="wp-caption-text">
    A nearly completed XForm to-do list
  </p>
</div>

The problem with this is that we are required to enter dates and state whether the task is complete manually. What would be preferred is if we could use a checkbox or date picker. A naive approach is to edit the interface directly, and alter the Xforms input into a checkbox. Below, we have code that generates a XForms [select](http://www.w3.org/TR/xforms/#ui-selectMany "W3C XForms Select") option that presents a series of checkboxes, however since we are dealing with binary information, we only need one item to select from:

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
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:select</span> <span style="color: #000066;">ref</span>=<span style="color: #ff0000;">"@complete"</span> <span style="color: #000066;">appearance</span>=<span style="color: #ff0000;">"full"</span> <span style="color: #000000; font-weight: bold;">&gt;</span></span>  
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:item<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
         <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>true<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span> 
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xf:item<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/select<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

<div style="width: 435px" class="wp-caption alignnone">
  <img class=" " alt="A task list with tick boxes" src="http://i.imgur.com/Ogpj2Pd.png" width="425" height="247" />
  
  <p class="wp-caption-text">
    A task list with tick boxes
  </p>
</div>

But the problem with this is that if the true value isn&#8217;t selected, rather than the value be false, it will instead be empty. Additionally there is no &#8220;date input&#8221; input type, so we&#8217;d have to make a custom date picker. We could again hack how we evaluate this value, and make custom handlers for different datatypes, or&#8230; we could type our data correctly.

## Using XForms Binds to provide data-typing

XForms is very data-driven in how it operates, and conforms very strongly to the [Model-View-Controller](http://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller "Wikipedia - Model-View-Controller") design pattern. We have already covered to View &#8211; the HTML/XForms code presented to the user &#8211; and the Model &#8211; the data model that we have designed to describe the information we hope to capture &#8211; now its time to look at the Controller aspect of XForms, the [XForms bind](http://www.w3.org/TR/xforms/#structure-bind-element "W3C - The XForms Bind Element"). Binds have a lot of uses, [dictating the connections between the model and the view](http://en.wikibooks.org/wiki/XForms/Bind "Wikibooks XForms Bind"),  they can be used to compute values, control when certain inputs are available and they can be used to provide explicit data-typing for elements in the model.

To demonstrate this we will revert the insert into our xf:model some bindings for our data:

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
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:bind</span> <span style="color: #000066;">nodeset</span>=<span style="color: #ff0000;">"//task/@complete"</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"xs:boolean"</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:bind</span> <span style="color: #000066;">nodeset</span>=<span style="color: #ff0000;">"//task/@dueDate"</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"xs:date"</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xf:bind</span> <span style="color: #000066;">nodeset</span>=<span style="color: #ff0000;">"//task"</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"xs:string"</span> <span style="color: #000066;">readonly</span>=<span style="color: #ff0000;">"./@complete=true()"</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
<span style="color: #808080; font-style: italic;">&lt;!-- later --&gt;</span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;td<span style="color: #000000; font-weight: bold;">&gt;</span></span><span style="color: #000000; font-weight: bold;">&lt;xf:input</span> <span style="color: #000066;">ref</span>=<span style="color: #ff0000;">"."</span><span style="color: #000000; font-weight: bold;">/&gt;</span><span style="color: #000000; font-weight: bold;">&lt;/td<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;td<span style="color: #000000; font-weight: bold;">&gt;</span></span><span style="color: #000000; font-weight: bold;">&lt;xf:input</span> <span style="color: #000066;">ref</span>=<span style="color: #ff0000;">"@complete"</span><span style="color: #000000; font-weight: bold;">/&gt;</span><span style="color: #000000; font-weight: bold;">&lt;/td<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;td<span style="color: #000000; font-weight: bold;">&gt;</span></span><span style="color: #000000; font-weight: bold;">&lt;xf:input</span> <span style="color: #000066;">ref</span>=<span style="color: #ff0000;">"@dueDate"</span> <span style="color: #000000; font-weight: bold;">/&gt;</span><span style="color: #000000; font-weight: bold;">&lt;/td<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

Here we have reverted our complete entry field to a simple input, but have declare it to be an XML boolean datatype, similarly we have declared the due date to be an XML date and the task name to be a string. We have also demonstrated the ability to disable content based on the binding by saying that a task can only be edited if it has been completed. The end result of this simple and declarative change is shown below:

<div style="width: 455px" class="wp-caption alignnone">
  <img alt="A more completed task list" src="http://i.imgur.com/k27ihsF.png" width="445" height="373" />
  
  <p class="wp-caption-text">
    A more completed task list
  </p>
</div>

The above image shows several changes have taken place:

  * The complete field now has a tick-box (not shown is the fact that this will store a true or false value without further scripting required)
  * The due date field has a button with ellipses (&#8230;) that when pressed shows a date selector.
  * Although subtle, the first task and due date are grayed out indicating it has been disabled. Similarly, the button that would drop down the date selector for the first task is now gone.

So far we now have a fairly complete user interface for managing our tasks. You can see the [full code for the task list on Github](https://github.com/LegoStormtroopr/xforms-todo-list/blob/master/xforms-todo-part3.xml "Github XForms tutorial part 3"), or [view all past code in the same repository](https://github.com/LegoStormtroopr/xforms-todo-list "Github Xforms tutorial"). In the next tutorial we&#8217;ll look at an alternate way of providing datatyping  by linking to or including inline XML schemas, which can be useful when the data structure is known ahead of time. Then we&#8217;ll look at defining submission methods so we can save our data with a web server.