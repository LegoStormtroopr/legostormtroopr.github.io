---
id: 421
title: 'Erdos &#8211; A javascript interface to create Graphviz charts'
date: 2011-09-06T09:49:11+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=421
permalink: /2011/09/erdos-a-javascript-interface-to-create-graphviz-charts/
aktt_notify_twitter:
  - yes
aktt_tweeted:
  - 1
categories:
  - Drivel
  - Project
tags:
  - erdos
  - fun
  - graph
  - javascript
---
So I found myself needing to be able to generate large graphs and I&#8217;ve found that [Graphviz](http://graphviz.org/ "Graphviz homepage") and its [DOT language](http://graphviz.org/content/dot-language "DOT specification") is the easiest way to produce large graph diagrams. Unfortunately, its not always easy to get access to the tools you need immediately, so to resolve this, I set about creating an easy online Graphviz compiler.

In looking I did find a few existing tools, but those I found did a lot of the processing themselves, and limited the number of possible nodes. After some searching though, I found the [Google Chart API](http://code.google.com/apis/chart/image/docs/gallery/graphviz.html "Google Chart Graphviz API") which has a Graphviz option that renders up to 200 nodes and 400 edges.

using a little Jquery, a little HTML, and very little CSS I was quickly able to put together a tool for drawing graphs on the go.

To see it in action [check it out in the sandbox](http://sandbox.kidstrythisathome.com/erdos/index.html "Erdos").