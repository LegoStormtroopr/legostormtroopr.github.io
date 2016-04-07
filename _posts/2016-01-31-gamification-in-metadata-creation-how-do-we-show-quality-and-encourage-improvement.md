---
id: 6749
title: 'Gamification in metadata creation &#8211; how do we show “quality” and encourage improvement?'
date: 2016-01-31T11:24:42+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=6749
permalink: /2016/01/gamification-in-metadata-creation-how-do-we-show-quality-and-encourage-improvement/
categories:
  - Drivel
  - Metadata
tags:
  - aristotle-mdr
  - Metadata
  - metadata registry
  - quality management
  - quality metadata
---
Encouraging the creation of good metadata can be a challenging exercise. Systems for metadata creation need to allow for blank fields to allow incremental or in progress content to be saved, however some fields may be semantically recommended or mandatory for standardisation. So, while a metadata editing tool needs to be flexible to allow evolving content, it also needs to provide feedback to drive improvement.

This leads to three questions:

  1. Can we automatically measure metadata quality?
  2. Can we use this data to encourage metadata editors to more actively participate and improve content?
  3. How can we best show the “quality” of metadata to an editor to achieve better content?

Gamification is a recognised term for encouraging changes in user behaviour through small incentives. The question I&#8217;d like to pose for Aristotle is, how can these principles be used to encourage the creation of good metadata. Obviously, &#8216;good&#8217; is very subjective, but for metadata objects such as a Data Elements, at the bare minimum having an attached &#8220;Data Element Concept&#8221; and &#8220;Value Domain&#8221; is a prerequisite for a quality item. Likewise, a piece of metadata with a description is good, but a piece of metadata with a longer description is probably better (but not always which leads to further challenges).

For the moment, let’s assume that basic metrics for &#8220;good&#8221; metadata can be constructed and applied to a piece of metadata, and that these can be summed together to give a raw score based on the possible sum. This assumption means we can grade metadata completion and get a raw score like &#8220;77 passes out of a possible 82&#8243;. From these we can derive all sorts of graphics or figures that can influence user behaviour, and it’s that which I&#8217;m interested in right now.

First of all, from these figures we can derive a percentage or rank &#8211; 77 out of 82 is about 94%, &#8220;9/10&#8243;, &#8220;4.5/5&#8243; or &#8220;A-&#8220;. This may mean a metadata item has all its relations, all fields are filled out, but one or two are a little shorter than our metrics would like. Perhaps though, the item is described perfectly &#8211; adding more text in this case is worse.

Secondly, there is the issue of how to present this visually once we&#8217;ve determined a score. There are probably many ways to present this, but for now I want to focus on two &#8211; symbols and progress bars. A symbol can be any repeated small graphic, but the best example is a star ranking where metadata is given a rank out of 5 stars.

Once a raw score is computed, we can then normalise this to a score out of 5 and show stars (or other symbols). However, initial discussions suggest that this presents a more abrupt ranking that discourages work-in-progress, rather than displaying further work to do.

An alternative is the use of progress bars to show the completion of an item. Again, this is computed from the raw score and normalised to a percent and then shown to the user. The images show different possible options including a percentage complete, an integer or rounded decimal rankings out of 10. Again, initial discussions suggest that percentages may encourage over work, where users on 94% might strive for 100% by &#8216;gaming the system&#8217;, opposed to users with metadata ranked 9.5/10. For example, if a metadata item has a well written short description but is under a predefined limit resulting in a score of 94%, we need to design a pattern to discourage an editor from ‘adding’ content free text to ‘score’ 100%. The use of colour is also a possible way to gauge progress analogous to stars that many users are familiar with, but raises the questions of how to define ‘cut-offs’ for quality.

## Metadata quality tracking in practice

In this section we look at a number of possible options for presenting the quality metrics of metadata using the [Aristotle Metadata Registry](https://github.com/aristotle-mdr/aristotle-metadata-registry). At the moment these are just mock-ups, but sample work has shown that dynamic analysis of metadata to quantify “quality” is possible, so here we will address the matter of how to show this.

First of all, it is important to note that these quality rankings can be shown at every stage from first edit all the way through to final publication, so a one-size-fits-all approach may not be the best way. In the simple case, we can look at the difference between progress and a star rating. Alongside with all the basic details, metadata can be given a ranking right on the page as well as a status to give users immediate feedback on its fitness for use.

<div style="width: 659px" class="wp-caption aligncenter">
  <img class="" src="http://i.imgur.com/yx6pizs.png" alt="" width="649" height="154" />
  
  <p class="wp-caption-text">
    An example of how stars or bars may look for a user.
  </p>
</div>

Secondly, we can look at simple presentation options. Here it’s important to note only one rating would be shown out of all the possible options. Stars offer fewer levels of granularity, and when coloured are bright and distracting. However, progress bars blend quite well, even when coloured, and give more options for embedding textual representations.

<img class="aligncenter" src="http://i.imgur.com/EEls5JN.png" alt="" width="648" height="293" />

Lastly, we can see how these would look when a number of items are shown together. Using a ‘sparklines’ approach, we can use stars or bars to quickly highlight trouble spots in metadata when looking at a large number of items.

<img class=" aligncenter" src="http://i.imgur.com/wiCVm3h.png" alt="" width="651" height="145" /><img class="aligncenter" src="http://i.imgur.com/S29waet.png" alt="" width="651" height="130" />
  
For the professional context of a registry, based on initial feedback, there are strengths in the progress bar style that make it more suited for use, however more feedback is required to make a conclusive argument.

## Conclusion

This is intended to be be the first in a number of articles that address the issue of best practices in presenting “quality” in the creation of metadata and the implementation of these practices in the Aristotle Metadata Registry. As such, I welcome and encourage comments and feedback into this design process, both from Aristotle users and the broader community.

### Key questions for feedback

1. Question 1: How can we textually show a metadata quality rank to encourage more participation? Possible options: raw values (77/82), percent (94%), normalised (9/10), graded (A-) or something else?
2. Question 2: How can we visually show metadata rank to encourage participation? Possible options: stars (or others symbols), progress bar, colours, text only or something else?
3. Question 3: How do we positively encourage completion without adversely encouraging “gaming the system”?
4. Future questions:
  * How do we programmatically measure metadata quality?
  * Based on a set of sub-components of quality how and when can we show a user how to improve metadata quality?