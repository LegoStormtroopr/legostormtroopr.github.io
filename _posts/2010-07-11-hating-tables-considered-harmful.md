---
id: 54
title: 'Hating &lt;table&gt;s considered harmful'
date: 2010-07-11T15:31:11+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=54
permalink: /2010/07/hating-tables-considered-harmful/
aktt_notify_twitter:
  - no
  - no
categories:
  - Data
  - Metadata
tags:
  - Data
  - Metadata
  - tablefail
---
Apologies to Dijkstra for butchering that quote _again_ , but the rage against <table>s is getting out of hand. Back in the dark ages, when it was impossible to get consistent HTML rendering across browsers and platforms someone decided to use the <table> element , originally designed to markup tabular data, to layout webpages.

Ever since that moment <table>s have been an unfairly shunned part of the HTML spec. When CSS became a stable and supported spec many people started screaming from the roof tops &#8220;Stop using <table> it ruins webpages&#8221;, and too many people have taken this to heart, so much that any time tabular data needs to be presented bizarre alternatives are used.

This was an example of a [bad table of data](http://communities-dominate.blogs.com/brands/2010/06/full-analysis-of-iphone-economics-its-bad-news-and-then-it-gets-worse.html "Bad table of data") that caught my eye a while ago:

<div style="width: 515px" class="wp-caption alignnone">
  <a href="http://communities-dominate.blogs.com/brands/2010/06/full-analysis-of-iphone-economics-its-bad-news-and-then-it-gets-worse.html"><img title="A screenshot of a table, when you read the next section you'll think I'm such a hypocrite. But its here just incase they change it" src="http://i.imgur.com/n6sas.png" alt="See the &quot;pre&quot; section below" width="505" height="203" /></a>
  
  <p class="wp-caption-text">
    A screenshot for posterity
  </p>
</div>

Its supposed to give an idea of the cumulative revenue of iPhone Apps over time, but its hard to tell that as there is no title. Good data tells a story, good metadata explains that story. There is no metadata here to explain any of these numbers, here is what a search engine sees when they look at the HTML on that page:

<pre>Period ending.....Period downloads.....Cumulative downloads....Period revenues
Jun 2008............no apps...................no apps........................no revenues
Dec 2008.............600 M......................600 M..........................$ 172 M
Jun 2009..............800 M....................1.4 B.............................$  228 M
Dec 2009..........1.6 B.........................3.0 B............................$  458 M
Jun 2010...........2.0 B.........................5.0 B............................$  542 M
Total.................5.0 B.........................5.0 B............................$1.4 B</pre>

Accessibility and search robots aside, here is no context to any of this, the units change between rows, the number of dots changes each time. Its hard to say what this data is without purposefully reading the text around it. I could drone on about the lack of metadata describing the data in this table, but instead I&#8217;ll counter this with a better example.

Here is the same table, rewritten as an actual <table>, using only what&#8217;s defined in the [HTML4 and above W3C specifications](http://www.w3.org/TR/html5/tabular-data.html):



A few things instantly stand out: the columns all match up nicely, both in display and in the [table-model](http://www.w3.org/TR/html5/tabular-data.html#processing-model-0); each of the years is clearly marked; the table is relatively self-explanatory; and lastly it appears as a table to anyone who reads it. Furthermore, all of the formatting is done using CSS; thats right the presentation is left to the CSS and the descriptive markup is done using a <table>, just how it is intended to be done. But even this is only a fraction of the possible metadata to place into a HTML table.

However, this is not the worse example of a &#8216;table&#8217; I have seen, the one that sent me over the edge was this large image that highlights the relative pros and cons of different smart phones:

<div style="width: 485px" class="wp-caption alignnone">
  <a href="http://cache.gawkerassets.com/assets/images/17/2010/06/smartphone_stats.jpg" target="_blank"><img class="    " title="A table comparing different smartphones" src="http://imgur.com/pxwxU.jpg" alt="A very large table comparing different smartphones" width="475" height="760" /></a>
  
  <p class="wp-caption-text">
    This 'table' is too big to show inline, it needed to be reduced to a third of its size to fit
  </p>
</div>

The main issue with this, is this image of a table is mostly text, is quite large and static. You cannot easily copy text out of this, you can’t easily reorder the table and unless you have a large screen it would be quite difficult to compare two products that weren’t both very close to each other. Unlike the table of iPhone revenues, I am not going to go to the effort of transcribing this into a proper HTML table.

Compare this with a [similar table from wikipedia](http://en.wikipedia.org/wiki/Comparison_of_smartphones) also providing a comparison of smartphones and the differences are obvious. First of all, the table is now web-crawlable &#8211; whatever data is in this table is now indexed in Google, instant bonus, and the user can easily search through the page to find what they needed to know. There is also a whole lot of Javascript on the page. For example, clicking the boxes next the each of the column titles reorders the whole table around that column. In the first table this isn’t too noticeable with most entries having either ‘Yes’ or ‘No’, but the [Hardware and OS table](http://en.wikipedia.org/wiki/Comparison_of_smartphones#Hardware_and_OS "Smartphone Hardware and OS comparisons") from further down the same page is full of figures, and now I can easily find the lightest phone (it’s the [HP iPAQ Voice Messenger](https://docs.google.com/w/index.php?title=HP_iPAQ_Voice_Messenger&action=edit&redlink=1), something that would be much harder to find out on the image &#8216;table&#8217;).

<div>
  Furthermore there are plenty of ways that you can easily add functionality to tables, to reoorder, hide, expand or change to add plenty of use to your tables.
</div>

<div>
  The web is supposed to be full of life and allow use to use our data in exciting new ways, so don’t stick with static images, or unstructured text for your tables when there is a much more useful alternative out there.
</div>