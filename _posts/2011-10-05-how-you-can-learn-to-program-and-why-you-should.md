---
id: 425
title: How you can and why you should learn to program.
date: 2011-10-05T08:45:06+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=425
permalink: /2011/10/how-you-can-learn-to-program-and-why-you-should/
aktt_notify_twitter:
  - yes
aktt_tweeted:
  - 1
categories:
  - Education
  - Programming
tags:
  - beginner
  - Hello World
  - programming
  - python
---
Often people ask me how I learned to program and why I did. The answer is simple, lots of practice because its a useful skill &#8211; and it also helps that I enjoy it.

Not everyone will find programming fun or interesting, however at more than one time people will come up against a problem that computers were made to do. Contrary to popular believe computers are dumb &#8211; at least in the sense that they can only do what they are told. What they can do, is they can do these dumb things very, very quickly. So much so, that they can fool you into believing they are smart &#8211; more than smart, magic even. In fact, if you are even a mediocre programmer people can become convinced you are a magician.

## So why should you learn to program?

Mostly, because your time is valuable. Not to me, but to you. Unlike a computer your time is finite, and if you can make a machine that can give you more time to do something, isn&#8217;t that in your interest? Even if it isn&#8217;t in work, if its just sorting your taxes, or writing a script to check your email for you, there are plenty of small, repetative tasks that you probably do that a machine can do quicker. If you enjoy doing repetitive tasks, then there isn&#8217;t much I can do for you. But if you want to spend more time understanding why you do these things, then read on&#8230;

## Where do you begin?

Well, I think, there are 3 programs every one must be able to write. Because if you can write these 3 programs and adapt them to your needs, you can do most big, boring tasks that will come your way.

There are 3 programs you need to learn to start to become a programmer and as I explain them, I&#8217;ll show you a brief example to edit and play with and ultimately understand what is going on. These examples are written in [Python, a free programming language with a very user friendly syntax](http://www.python.org "Python Homepage").

### Hello, World!

&#8220;Hello world&#8221; is traditionally the first program many new programmers will write. It is simple, when the program is run the computer prints &#8220;Hello, World!&#8221;. In essence, this simple program introduces programming syntax and demonstrates how to display text to a user.

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">"Hello, World!"</span></pre>
      </td>
    </tr>
  </table>
</div>

There isn&#8217;t much to this, but its a starting point. It teaches you some basic syntax and with a lot of languages understanding syntax is important &#8211; computers don&#8217;t speak English and to make them useful you need to learn to talk to them, more than the other way around.

### Simple user interaction

The second is a simple string manipulator. This goal is to create a simple, persistent user interface, with some error checking that fulfills a task. Here we see an example that does actions on a given string based on a command given to it.

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: #008000;">True</span>:
        <span style="color: #008000;">input</span> <span style="color: #66cc66;">=</span> <span style="color: #008000;">raw_input</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">"&gt; "</span><span style="color: black;">&#41;</span>
        <span style="color: #ff7700;font-weight:bold;">try</span>:
                <span style="color: #dc143c;">cmd</span><span style="color: #66cc66;">,</span>text <span style="color: #66cc66;">=</span> <span style="color: #008000;">input</span>.<span style="color: black;">split</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">":"</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>
                <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #dc143c;">cmd</span> <span style="color: #66cc66;">==</span> <span style="color: #483d8b;">"uc"</span>:
                        <span style="color: #ff7700;font-weight:bold;">print</span> text.<span style="color: black;">upper</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
                <span style="color: #ff7700;font-weight:bold;">elif</span> <span style="color: #dc143c;">cmd</span> <span style="color: #66cc66;">==</span> <span style="color: #483d8b;">"lc"</span>:
                        <span style="color: #ff7700;font-weight:bold;">print</span> text.<span style="color: black;">lower</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
                <span style="color: #ff7700;font-weight:bold;">elif</span> <span style="color: #dc143c;">cmd</span> <span style="color: #66cc66;">==</span> <span style="color: #483d8b;">"rev"</span>:
                        text.<span style="color: black;">reverse</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
                        <span style="color: #ff7700;font-weight:bold;">print</span> text
                <span style="color: #ff7700;font-weight:bold;">elif</span> <span style="color: #dc143c;">cmd</span> <span style="color: #66cc66;">==</span> <span style="color: #483d8b;">"quit"</span>:
                        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">"Bye"</span>
                        <span style="color: #ff7700;font-weight:bold;">break</span>
                <span style="color: #ff7700;font-weight:bold;">else</span>:
                        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">"Command not recognised"</span>
        <span style="color: #ff7700;font-weight:bold;">except</span>:
                <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">"Syntax error: enter a command, a colon (:), then a string"</span></pre>
      </td>
    </tr>
  </table>
</div>

Firstly, we start the loop and set it to never stop looping. As long as the user wants to play with strings this program will keep going. Next we ask for some input from the user.
  
Now things get a little more complex, first we try and split the string around a colon, into a command and the text. If the user doesn&#8217;t enter a colon, we throw an error, and give them some help text (after the line that says &#8220;except:&#8221;.
  
If they do enter a command and text, we set the text to upper case, lower case or reverse it. If they tell us to &#8220;quit:&#8221; we quit by breaking out of the loop (the break command) or we tell them we didn&#8217;t recognise the command.

Its not perfect, but it gives us an understanding of errors, handling user input and basic user interaction &#8211; not bad for 18 lines of code.

### File manipulation

The last and most important program is a simple file manipulation tool. Again, what the tool does to the file is irrelevant- it might merge files, look for spelling errors, count lines, anything. Perhaps, we are looking for entries in a diary that start with numbers (like dates) in a large file, and only want to view these.

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="python" style="font-family:monospace;"><span style="color: #008000;">file</span> <span style="color: #66cc66;">=</span> <span style="color: #008000;">open</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">'test'</span><span style="color: black;">&#41;</span>
<span style="color: #ff7700;font-weight:bold;">for</span> line <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">file</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> line<span style="color: black;">&#91;</span><span style="color: #ff4500;"></span><span style="color: black;">&#93;</span>.<span style="color: black;">isdigit</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">print</span> line
<span style="color: #008000;">file</span>.<span style="color: black;">close</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span></pre>
      </td>
    </tr>
  </table>
</div>

Here we open the file, and then line by line we search through it. When we find a line whose first character is a digit we print the line (line[0] essentially means the 0th character from the start &#8211; [its complicated but its how almost everyone deals with subscripting in lists](http://en.wikipedia.org/wiki/Zero-based_numbering "Wikipedia Zero-Based Numbering")). Lastly, we clean everything up by closing the file.

Again, by no means the best implementation, but easy enough to read and alter. This time in 5 lines we have a simple script that could help use find our tax information, search our diary, lookup phone numbers, or anything like this.

## I&#8217;ve done this, what now?

Do whatever task it is that needs doing. Odds are having read these short code snippets you can get an idea of what can be done. Its just a matter of getting out and doing it. You may not be the next Bill Gates/Mark Zuckerburg/whoever, but if you learn to paint a wall you won&#8217;t be the next Da Vinci either. Learn how to do what you need to do, and keep plugging away. Programming is about pulling together pieces of logic, to help us do simple tasks easily and reproducibly. So think lazy, and find all the tasks that you can automate and get something else to do them for you.