---
id: 459
title: Always double check the standard before writing code
date: 2011-12-29T22:22:56+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=459
permalink: /2011/12/always-double-check-the-standard-before-writing-code/
aktt_notify_twitter:
  - yes
aktt_tweeted:
  - 1
categories:
  - Drivel
  - Metadata
tags:
  - alwayscheckthestandard
  - DDI
  - eddi
  - Virgil
---
A few weeks ago, I had the privilege of presenting at a collection of DDI Developers in Gothenburg at EDDI. There I presented one of my larger pieces of work, the Virgil-UI DDI Codelist Editor, for critique. While there I received advice, praise and most importantly constructive criticism for which I am grateful. However, this has brought to light a rather large problem.

It was pointed out that I made a small error when dealing with <Code> elements in DDI and accidentally gave them @id attributes, and it was noted that this should be an easy fix. Unfortunately, due to my missing this very early on in the development of Virgil the underlying model relies on Codes having ids to be able to easily make connections between the hierarchical user interface, the <Code>s and the <Category>s that give them meaning.

What this means is that both the DDI coming out of Virgil is invalid, and any valid DDI would not actually be able to be read by Virgil. Essentially, the Virgil model for handling DDI is broken and needs to be almost entirely rewritten and this might take quite a while.

Unfortunately, at this stage rewriting also means re-examining a lot of the initial ideas about what Virgil should be and has highlighted some interesting questions about the DDI model and DDI software, such as:

  1. **Is abstracting the DDI model away from a user a good approach to software design? Yes.**
  
    This was the crux of my talk at EDDI, and I still feel that abstracting the DDI model away from day-to-day users is necessary. The DDI model is complex and covers a wide range of tasks. I believe that designing software that helps users relate the model to specific tasks they are trying to do is a key to getting people to use DDI and think about how they can make their metadata support themselves and those around them.
  2. **Is DDI a standard that is suitable to use for day to day management of information? Probably.**
  
    In practice, the DDI standard needs to be able to be passed between software if it is to move from an archival standard to a practical statistical metadata standard. One of the things I wanted to achieve with Virgil, was a tool that not only produced DDI, but could also consume it from other sources. In the simplest case this to me meant being able to take a DDI file, and edit the contents of part of it, leaving the rest untouched, and in a lot of cases this is possible with DDI. However, since having to rethink how to manage classifications using DDI, I have realised that there are some objects that are not captured well within DDI and unfortunately classifications are one such example.
  3. **Is the DDI model for managing codelists and classifications good enough? Sadly not.**
  
    One of the reasons I relied so heavily on the invalid <Code> @ids was that I needed a hook to tie codes and categories together and without this it becomes very difficult to manage what a &#8216;classification&#8217; is in DDI. Furthermore, classifications don&#8217;t exist in DDI per se, but are a rather loose agreement that if you combine <CodeScheme>s and <CategoryScheme>s you get a good approximation. However, this falls apart when we try to document the classification itself.
  
    For example, where do you store the name of a whole classification? There are three viable places (excuse the XPath) &#8211; as a //CodeScheme/Label (being the label of the hierarchy), as a //CategoryScheme/Label (being the label of the collection of classifying categories) or as a //LogicalProduct/Label (the label of the immediate parent that contains both the hierarchies and the categories).
  
    However, each of these approaches has inherent issues, as neither of these are the documented way to manage this information, and if 3 different agencies approached the problem in different ways, then their metadata becomes incomparable. This needs to be discussed further, as it will become a bigger issue as more tools start to try and manage such an important, and conceptually early in the lifecycle piece of metadata.

It should be noted that these issues don&#8217;t excuse overlooking the actual standard leading to this predicament. However, given the chance to re-examine how to correct the problem in Virgil, also gives me a chance to examine some of the issues I came across while trying to maintain classifications within DDI. Over the coming month or so while I am going to continue writing up some of the issues I identified with classifications within DDI3.1, how to work around these in the short term, and look at ways to correct the problem in future versions of the standard.

Lastly, in the short-term there will be an update to correct the Code/id problem in the CSV to DDI conversion, so the original use case of being able to mine legacy systems to produce valid DDI will still be filled.

Thanks again to everyone at EDDI for their input and company.