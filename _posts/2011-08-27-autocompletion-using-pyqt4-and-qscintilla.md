---
id: 408
title: Autocompletion using PyQt4 and QScintilla
date: 2011-08-27T05:31:44+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=408
permalink: /2011/08/autocompletion-using-pyqt4-and-qscintilla/
aktt_notify_twitter:
  - yes
aktt_tweeted:
  - 1
categories:
  - Drivel
  - Project
tags:
  - autocompletion
  - code
  - fun
  - pyqt4
  - qscintilla
  - spqr
---
I&#8217;m currently toying with the idea of creating a specialised code editor for questionnaires in [Python](http://www.python.org "Python Homepage") using [PyQt4](http://www.riverbankcomputing.co.uk/software/pyqt/intro "PyQt4 Homepage"). One of the best plugins for Qt for this job is QScintilla, a wrapper around [Scintilla](http://www.scintilla.org/ "Scintilla Homepage") &#8211; an open source editing component. Scintilla to its credit has a huge amount of great features, including code-folding, syntax highlighting and auto-completion of words. But the documentation can be a little lacking at times, and there aren&#8217;t a whole lot of examples on how to use some of the features.

The one feature, that I was trying to implement was auto-completion, but I had no luck finding python examples that demonstrated everything you needed to get it working. So, after some searching, some hacking, some crying and then finally some reading for the documentation, I came up with the following minimal example with auto-completion in a basic editor:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="python" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">#!/usr/bin/env python</span>
<span style="color: #808080; font-style: italic;"># -*- coding: latin1 -*-</span>
&nbsp;
<span style="color: #483d8b;">"""
Basic use of the QScintilla2 widget
&nbsp;
Note : name this file "qt4_sci_ac_test.py"
Base code originally from: http://kib2.free.fr/tutos/PyQt4/QScintilla2.html
"""</span>
&nbsp;
<span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">sys</span>
<span style="color: #ff7700;font-weight:bold;">from</span> PyQt4.<span style="color: black;">QtGui</span> <span style="color: #ff7700;font-weight:bold;">import</span> QApplication
<span style="color: #ff7700;font-weight:bold;">from</span> PyQt4 <span style="color: #ff7700;font-weight:bold;">import</span> QtCore<span style="color: #66cc66;">,</span> QtGui<span style="color: #66cc66;">,</span> Qsci
<span style="color: #ff7700;font-weight:bold;">from</span> PyQt4.<span style="color: black;">Qsci</span> <span style="color: #ff7700;font-weight:bold;">import</span> QsciScintilla<span style="color: #66cc66;">,</span> QsciScintillaBase<span style="color: #66cc66;">,</span> QsciLexerPython
&nbsp;
<span style="color: #ff7700;font-weight:bold;">if</span> __name__ <span style="color: #66cc66;">==</span> <span style="color: #483d8b;">"__main__"</span>:
    app <span style="color: #66cc66;">=</span> QApplication<span style="color: black;">&#40;</span><span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#41;</span>
    editor <span style="color: #66cc66;">=</span> QsciScintilla<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
&nbsp;
    <span style="color: #808080; font-style: italic;">## Choose a lexer</span>
    <span style="color: #808080; font-style: italic;">## This can be any Scintilla lexer, but the original example used Python</span>
    lexer <span style="color: #66cc66;">=</span> QsciLexerPython<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
&nbsp;
    <span style="color: #808080; font-style: italic;">## Create an API for us to populate with our autocomplete terms</span>
    api <span style="color: #66cc66;">=</span> Qsci.<span style="color: black;">QsciAPIs</span><span style="color: black;">&#40;</span>lexer<span style="color: black;">&#41;</span>
    <span style="color: #808080; font-style: italic;">## Add autocompletion strings</span>
    api.<span style="color: black;">add</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">"aLongString"</span><span style="color: black;">&#41;</span>
    api.<span style="color: black;">add</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">"aLongerString"</span><span style="color: black;">&#41;</span>
    api.<span style="color: black;">add</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">"aDifferentString"</span><span style="color: black;">&#41;</span>
    api.<span style="color: black;">add</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">"sOmethingElse"</span><span style="color: black;">&#41;</span>
    <span style="color: #808080; font-style: italic;">## Compile the api for use in the lexer</span>
    api.<span style="color: black;">prepare</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
&nbsp;
    editor.<span style="color: black;">setLexer</span><span style="color: black;">&#40;</span>lexer<span style="color: black;">&#41;</span>
&nbsp;
    <span style="color: #808080; font-style: italic;">## Set the length of the string before the editor tries to autocomplete</span>
    <span style="color: #808080; font-style: italic;">## In practise this would be higher than 1</span>
    <span style="color: #808080; font-style: italic;">## But its set lower here to make the autocompletion more obvious</span>
    editor.<span style="color: black;">setAutoCompletionThreshold</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>
    <span style="color: #808080; font-style: italic;">## Tell the editor we are using a QsciAPI for the autocompletion</span>
    editor.<span style="color: black;">setAutoCompletionSource</span><span style="color: black;">&#40;</span>QsciScintilla.<span style="color: black;">AcsAPIs</span><span style="color: black;">&#41;</span>
&nbsp;
    <span style="color: #808080; font-style: italic;">## Render on screen</span>
    editor.<span style="color: black;">show</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
&nbsp;
    <span style="color: #808080; font-style: italic;">## Show this file in the editor</span>
    editor.<span style="color: black;">setText</span><span style="color: black;">&#40;</span><span style="color: #008000;">open</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">"qt4_sci_ac_test.py"</span><span style="color: black;">&#41;</span>.<span style="color: black;">read</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    <span style="color: #dc143c;">sys</span>.<span style="color: black;">exit</span><span style="color: black;">&#40;</span>app.<span style="color: black;">exec_</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span></pre>
      </td>
    </tr>
  </table>
</div>

Thanks to Kib2 and his [example on code for QScintilla2](http://kib2.free.fr/tutos/PyQt4/QScintilla2.html "PyQt4 Snippets") that this example is based on.