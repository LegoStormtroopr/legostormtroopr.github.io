---
id: 131
title: Twitter Sparkline Generator using Unicode
date: 2010-08-01T14:52:31+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=131
permalink: /2010/08/twitter-sparkline-generator/
aktt_notify_twitter:
  - no
  - no
categories:
  - Data
  - Statistics
tags:
  - code
  - Data
  - Statistics
  - twitter
---
NB: This post uses examples of Unicode that may not show up in some browsers.

One of my main gripes with twitter is the ability to add only text. People often have the desire to share small snippets of data, but to no avail. The ideal idea to share data in such tiny chunks of data Edward Tufte idea of a [Sparklines](http://en.wikipedia.org/wiki/Sparkline).

For those of you disinclined to read the wikipedia page, sparklines are &#8220;data-intense, design-simple, word-sized graphics&#8221;, designed to be entered inline with text, at similar height to help illustrate an idea.

Now I am not the first person to suggest entering [sparklines in to twitter](http://www.datadrivenconsulting.com/2010/06/twitter-sparkline-generator/), in fact the second entry for a google search for sparkline turns up Alex Kerin&#8217;s article. However, there are two slight problems with Kerin&#8217;s implementation. Firstly, the unicode block characters he is using are not designed to be lined up, and examples that are shown on his page demonstrate this. To be fair, this isn&#8217;t his fault at all as unicode compliance isn&#8217;t 100%. The second is that a bar and a line can provide two very different perceptions: bar charts generally being used to display discrete data (or continuous data being shown as discrete) and line charts being used to show continuous data &#8211; for the record there is no good time to use a pie chart.

To this end I have [created a tool for producing two different types of sparkline](http://sandbox.kidstrythisathome.com/louis/) from an input data source &#8211; A crude line graph and a 5-figure box-plot.

Here is an example showing this are using the [June 30th 2010 Perth weather data from the Bureau of Meterology](http://www.bom.gov.au/products/IDW60901/IDW60901.94608.shtml), with bars delimiting 3 hour blocks:

### The weather yesterday in Perth was quite cool (4.1┣▇▇|▇━━┫17.7) with a maximum of 17.7 degrees occuring around 2pm, before quickly cooling down until 3pm. (⣤⣤⣀⎸⣀⣀⣀⎸⣀⣀⡤⎸⠴⠚⠛⎸⠛⠛⠙⎸⠒⠒⠒⎸⠒⠲⠶⎸⠶⠶⠶).

Limiting this example further, restricting ourselves to the 140 characters of twitter:

### Perth 30/06/10: Cool (4.1┣▇▇|▇━━┫17.7), max at 2pm, cooling to around 13°C after 3pm, steady afterwards. (⣤⣤⣀⎸⣀⣀⣀⎸⣀⣀⡤⎸⠴⠚⠛⎸⠛⠛⠙⎸⠒⠒⠒⎸⠒⠲⠶⎸⠶⠶⠶)

This is a 115 character weather report leaving 25 characters for a url to the full data. This may be for temperature only, but it shows the potential and can place 2 dataset in a twitter post with commentary.

I think the boxplots look quite good, however the tool does take a few liberties with the braille layout, relying on people to see a pair of vertical dots as a value in between the two, but it helps convey the message quite well in a limited, text-based format.