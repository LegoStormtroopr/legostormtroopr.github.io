---
id: 5536
title: Why Linus Torvalds is wrong about XML
date: 2014-03-10T04:00:32+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=5536
permalink: /2014/03/why-linus-torvalds-is-wrong-about-xml/
categories:
  - Data
  - Education
  - Metadata
tags:
  - Data
  - "I'll make my own specification with blackjack..."
  - Metadata
  - XML
---
<span style="font-size: 14px; line-height: 1.5em; font-weight: bold;"><a href="http://en.wikipedia.org/wiki/Linus_Torvalds">Linus Torvalds</a> is one of the most revered figures in modern computer science and has made the kind of contributions to the world that I hope to achieve. However, given his global audience, <a href="https://plus.google.com/+LinusTorvalds/posts/X2XVf9Q7MfV">his recent statements about XML give me pause for reflection.</a></span>

I have worked with XML in a number of jobs, [helped with the specification of international XML formats](http://www.ddialliance.org/), [written tutorials on their use](http://bit.ly/DDI_Tutorials), and [even made my own XML format](http://bit.ly/YAV9l3) ([with reason I might add](http://bit.ly/WOmwtz)). And I must say, in reply to Linus&#8217;s statement that

> XML is the worst format ever designed

XML isn&#8217;t the problem, it is more that the problem is bad programmers. Computer Science is a broad field, not covering just the creation of programs, but also the correct specification of information for computation. The lack of appreciation for that second aspect has seen the recent rise of &#8220;Data Science&#8221; as a field &#8211; a mash of statistics, data management and programming.

While it is undenyable that many programmers write bad XML, this is because of poor understanding and discipline. One could equally say, people write bad code, lets stop them writing code. People will always make mistakes or cut corners, the solution is education, not reinventing the wheel.

Linus and the rest of the Subsurface team are well within their rights to use the data formats they choose, and I am eager to see what new formats he can design. But with that in mind, I will address some of the critiques of Linus and others about XML and point out their issues, followed by some handy tips for programmers looking at using XML.

## XML should be human readable {#xml-should-be-human-readable}

> I did the best that I could with XML, and I suspect the subsurface XML is about as pretty and human-readable as you can make that crap

CSV isn&#8217;t very readable, C, Perl and Python aren&#8217;t very human readable. What is &#8220;human-readable&#8221; is very subjective, as even English isn&#8217;t human-readable to non-English speakers.

Restricting ourselves to just technology, CSV isn&#8217;t very readable as for any non-trivial amount of data as the header will scroll off the top of the screen, and data will overflow onto the next line or outside the horizonal boundaries of the screen. One could argue that its possible in Excel, OpenOffice or using a VIm/Emacs plugin to lock the headers to the top of the screen &#8211; and now we have used a tool to overcome limitations in the format.

Likewise, the same can be said for computer code, code-folding, auto-completion of long function and variable names and syntax highlighting are all _software_ features to overcome failures in the format and make the output more &#8220;human-readable&#8221;. Plain-text supports none of the above, yet no one would recommend using Notepad to write code for the lack of features.

Likewise, I would never, ever recommend writing XML in a non-XML editor. Auto-adding of closing tags, checking schema as you type, easy access to the schema via hotlinks from elements and attributes, and XPath query and replace are all vital functions of a good XML editor. All of these make writing XML much easier and approachable, and compared to code or CSV, a programmer should spend only as much time in an XML editor to understand the format to make writing XML in code easier.

**While it can be said that a poor craftsman blames his tools, a good craftsman knows when to use the right tools as well.**

## XML files should standalone {#xml-files-should-standalone}

This is most visible [in this bug raised in Subsurface](http://trac.hohndel.org/ticket/50) where it is stated that:

> Subsurface only ever stores metric units. But our goal is to create files that make sense and can be read and understood without additional information.

Now, examination of a sample of the [XML from subsurface](http://trac.hohndel.org/browser/subsurface/dives) shows a glaring contradiction. There is nothing in this file that says that units are in metric. The distance &#8216;m&#8217; could equally stand for &#8216;miles&#8217;, and while the order of magnitude would make misinterpretation for a human hard, a dive computer with an incorrect understanding may miscalculate the required oxygen pressure leading to potential death. To accurately understand this file, I need to find the documentation, i.e additional information. The reason for schema is to explicitly describe a data file.

Additionally, because data is stored as &#8220;human-readable&#8221; strings, I could validly put in &#8220;thirty metres&#8221; instead of &#8220;30.0 m&#8221; as a depth. At this point the program might fail, but as someone writing the data elsewhere I&#8217;d have no reason why. Apart from being a description of the data, schema exists as a _contract_. **If you say the data is of this form, then these are the rules you must conform to**. When you are looking at sharing data between programs or organisations this ability to lean on a technical enforcement is invaluable as making &#8220;bad&#8221; data is that much harder.

## XML shouldn&#8217;t need other formats {#xml-should-need-other-formats}

This is a tricky one, as when people think of XML, even if they have made a schema their mid stops there. XML isn&#8217;t just a format, its more a suit of related formats that can make handing and manipulating information easier.

Its worth noting that people have raised databases within that thread as an alternative &#8211; SQL is _only_ a query language, but requires the formal Database Definition Language to describe the data and an engine to query over it. Likewise, HTML without CSS, Javascript or any number of programming and templating languages that power the web would be much less useful to the general public.

Similarly, isolating XML from XML schemas, mean your data has no structure. Isolating XML from XQuery and XPath mean you have no way of querying your data. Without XSLT there is no easy, declarative way to transform XML, and having done this with traditional languages and XSLT, the latter makes using and transforming XML much easier. Ultimately, using XML without taking advantage of many of the technologies that exist in the entire XML landscape is not using technologies to its best.

# Tips for good XML {#tips-for-good-xml}

With all of that aside, XML like all technologies can be used poorly. However, when done well and documented properly, a good XML format with an appropriate schema can reduce errors and give vital metadata that gives data context and longevity. So I present a few handy tips for using XML well.

  1. **Only use XML when appropriate**XML is best suited to complex data, especially hierarchical data. As Linus (and others) points out in the linked thread tabular data is much better suited to CSV or more structured tablular formats, simple key values can be stored in ini files, and markup text can be done in HTML, Markdown or any number of other formats.
  2. **Look for other formats.**If you are thinking of using XML for your tool &#8211; stop and see what others have already done. The world doesn&#8217;t need another format, so if you are thinking of doing so you should have a very, very good reason to do so.
  3. **Use a schema or doctype**If you are chosing to make your own format, this is the most important point. If you chose to use XML, make a schema. How you choose to capture this Doctype, XSD Schema, Schematron, Relax NG is largely _irrelevant_. What is important is that your data format is documented. There are even tools that can automate creating schema stubs from documents, so there is no excuse not to. As stated an XML schema is the formal contract about what your data is and lets others know that if the data doesn&#8217;t conform to this format then it is broken.
  4. **Use XML datatypes**XML already has specifications for text, numeric, datetime and identification data. Use these as a starting point for your data.
  5. **Store one type of data per field.**While the difference between `<dive duration="30:00 mins">` and `<dive duration="30" durationUnit="mins">` is minimal, the former uses a single string for two pieces of data, while the latter uses two fields, a number and an enumerable, each storing one piece of data. An even better solution is using the XML duration data type `<dive duration="PT30M">` based on the existing ISO 8601 standard.