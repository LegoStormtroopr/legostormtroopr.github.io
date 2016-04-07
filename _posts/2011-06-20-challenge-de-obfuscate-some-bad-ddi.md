---
id: 339
title: 'Monday Funday &#8211; Challenge: De-obfuscate some bad DDI'
date: 2011-06-20T11:03:44+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=339
permalink: /2011/06/challenge-de-obfuscate-some-bad-ddi/
aktt_notify_twitter:
  - no
categories:
  - Data
  - Drivel
  - Metadata
tags:
  - DDI
  - MondayFunday
  - Obfuscated
---
**The solution is now available below**

DDI can be a harsh mistress sometimes, and mistakes can sometimes be made when trying to use it. As a data format it is flexible enough to handle most situations, but this flexibility can sometimes be a shortcoming.

Below is a poorly written chunk of DDI I&#8217;ve written, that forms part of a survey instrument. The good news it can be written in a much better way. The challenge is how to rewrite it:

<pre>&lt;d:Sequence id="MainSequence"&gt;
    &lt;d:ComputationItem id="CompItem1"&gt;
        &lt;d:Code&gt;
            &lt;r:Code programmingLanguage="pseudoCode"&gt;SET X = X + 1&lt;/r:Code&gt;
        &lt;d:Code&gt;
    &lt;/d:ComputationItem&gt;
    &lt;d:IfThenElse id="ifblock1"&gt;
        &lt;d:IfCondition&gt;
            &lt;d:Code&gt;
                &lt;r:Code programmingLanguage="pseudoCode"&gt;X == Y&lt;/r:Code&gt;
            &lt;d:Code&gt;
        &lt;d:IfCondition&gt;
        &lt;d:ThenConstructReference&gt;
            &lt;r:ID&gt;A_different_sequence&lt;/r:ID&gt;
            &lt;r:ID&gt;MainSequence&lt;/r:ID&gt;
        &lt;/d:ThenConstructReference&gt;
    &lt;/d:IfThenElse&gt;
&lt;/d:Sequence&gt;</pre>

If you think you can correct this code, email a solution to theodore.therone at gmail.com. At the end of the week (When I wake up this Saturday AEST) I&#8217;ll select a solution at random and give away a [$15 voucher for 5senses coffee](http://www.5senses.com.au).

If you need clarification on anything in the example code, post it in the comments and I&#8217;ll clear it up.

&nbsp;

* * *

Unfortunately, there were no correct responses, so the voucher will go to the next challenge, but the answer is still available below.

Solution &#8211; this was a simple computer science riddle wrapped in a layer of DDI. It was a loop rewritten as a recursive if-branch. Rewritten as a loop it comes out as this:

<pre>&lt;d:Loop id="MainLoop"&gt;
    &lt;d:LoopWhile &gt;
            &lt;d:Code&gt;
                &lt;r:Code programmingLanguage="pseudoCode"&gt;X == Y&lt;/r:Code&gt;
            &lt;d:Code&gt;
    &lt;d:LoopWhile&gt;
    &lt;d:StepValue&gt;
        &lt;d:Code&gt;
            &lt;r:Code programmingLanguage="pseudoCode"&gt;SET X = X + 1&lt;/r:Code&gt;
        &lt;d:Code&gt;
    &lt;/d:StepValue&gt;
    &lt;d:ControlConstructReference&gt;
        &lt;r:ID&gt;A_different_sequence&lt;/r:ID&gt;
    &lt;/d:ControlConstructReference&gt;
&lt;/d:Sequence&gt;</pre>

A much cleaner solution!