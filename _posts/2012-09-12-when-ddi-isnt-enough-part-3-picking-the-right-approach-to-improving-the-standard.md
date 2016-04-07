---
id: 561
title: 'When DDI isn&#8217;t enough Part 3 &#8211; Picking the right approach to improving the standard'
date: 2012-09-12T10:41:23+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=561
permalink: /2012/09/when-ddi-isnt-enough-part-3-picking-the-right-approach-to-improving-the-standard/
aktt_notify_twitter:
  - yes
aktt_tweeted:
  - 1
categories:
  - Uncategorized
tags:
  - Best Practice
  - DDI
  - "I'll make my own specification with blackjack..."
  - Metadata
  - Tutorial
---
**Warning:** This post is a wordy and contains some pretty heavy-handed criticisms about DDI and its implementations &#8211; so I&#8217;ll reiterate that this is my _personal opinion_ as an open-source developer working with DDI-Lifecycle.

So in two recent posts, I presented 2 alternative approaches(2) to extending the DDI information model &#8211; [one method using XML Substitution Groups](http://www.kidstrythisathome.com/2012/08/when-ddi-isnt-enough-xml-schema-extensions-and-ddi/ "When DDI isn’t enough Part 1 – XML Schema Extensions and DDI"), [the other using XSI Type Extensions](http://www.kidstrythisathome.com/2012/08/when-ddi-isnt-enough-part-2-xsi-type-and-ddi/ "When DDI isn’t enough Part 2 – XSI Type and DDI") &#8211; which leads us to ask which is better? The unhelpful, fence-sitting answer is both have their advantages &#8211; while being a vast improvements on the [DDI Note Element](http://www.ddialliance.org/sites/default/files/documentation/ddi3.1/schemas/reusable_xsd/elements/Note.html).

<div class="simplePullQuote">
  <p>
    [DDI Notes] limit the ability for implementers to coexist with the future vision of the standard
  </p>
</div>

Ultimately, Notes are the last way one would want to extend the DDI specification becuase they are wholly unstructured (despite the ironic fact that the [Content](http://www.ddialliance.org/sites/default/files/documentation/ddi3.1/schemas/reusable_xsd/elements/Content.html) of the Note is of a [StructuredStringType](http://www.ddialliance.org/sites/default/files/documentation/ddi3.1/schemas/reusable_xsd/complexTypes/StructuredStringType.html)). The content of this note can take any form &#8211; plain text, html, csv, even XML embedded within CDATA &#8211; and a receiving party, be it a person or software, will in most cases be none the wiser about the structure of the content. Given how far removed Notes can be from the extended object, the receiving party may not even be aware of any extension at all.

<div class="simplePullQuote">
  <p>
     The advantage is that users could create XML extensions, generate their documentation, push it upstream, and limit the amount of change in their own systems -<em> its a clear case where self-interest helps everyone</em>.
  </p>
</div>

This lack of structure ultimately, removes any benefit of using a standard &#8211; to that point that **_in my own personal opinion_**, Notes should be deprecated as soon as practical. This is due to people being able to add Notes when a better approach within the standard is either difficult to find, or hard to match to existing legacy software. Furthermore, they limit the ability for implementers to coexist with the future vision of the standard. The two approaches I&#8217;ve illustrated conform to good XML practice and encourage good documentation of changes, but they also provide direct ways to extend the standard in sharable ways, while also providing starting points for future changes. Since both methods require creating XML Schema to properly document the extensions, it is not unfeasible that schema created in this way could almost be directly imported into new versions of the standard. The advantage is that users could create XML extensions, generate their documentation, push it upstream, and limit the amount of change in their own systems &#8211; its a clear case where self-interest helps everyone.

**_But, having gotten down from my high horse&#8230;_**

Substitution Groups give the ability to create entirely new custom objects, they are unable to be easily recognized by existing tools they are limited on where they can go based on the original and unchangeable schema. While on the other hand, XSI Extensions can be used anywhere and on any element, without causing trouble for existing tools, they can only add information to existing to help fill data gaps. Ultimately, it is up to the implement to weight these benefits to determine the correct approach, before sharing these solutions with the community to support maintained ongoing support for the standard.

**Note:** I should point out that in the second post on XSI:types I specifically singled out a Note use in the Colectica implementation of DDI that could have been rewritten as using XSI extensions. Since the above diatribe could be read as an overly harsh criticism of their use of Notes, I feel that it should be stated that notes within DDI exported from Colectica are well-documented and Algenta provided support that helped push the time taken element into DDI 3.2.