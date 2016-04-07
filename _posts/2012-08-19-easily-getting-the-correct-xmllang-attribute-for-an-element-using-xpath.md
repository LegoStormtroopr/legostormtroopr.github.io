---
id: 574
title: Easily getting the correct xml:lang attribute for an element using XPath
date: 2012-08-19T01:46:10+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=574
permalink: /2012/08/easily-getting-the-correct-xmllang-attribute-for-an-element-using-xpath/
aktt_notify_twitter:
  - no
categories:
  - Drivel
  - Programming
tags:
  - i18n
  - XML
  - XPath
---
This is quick interlude before I go back to finishing up the write up about dealing with extensions to DDI.

\___\___\___\___\___\___\___\___\___\___\___\___\___\___\___\___\___\___\___

A problem I&#8217;ve come up against numerous times when dealing with XML processing is the correct handling of (human) languages in XML. The issue come up because the [XML 1.0 Specification for language identification](http://www.w3.org/TR/REC-xml/#sec-lang-tag) is quite clear about how to determine the language of an element in an XML document &#8211; use the elements xml:lang attribute, if that doesn&#8217;t exist use the nearest ancestors xml:lang tag (nearest in this sense means the closest in the document &#8211; eg. parent beats grandparent beats great-grandparent and so on&#8230;)

Unfortunately, this convention doesn&#8217;t always carry over into XML processors. In fact, I don&#8217;t think I&#8217;ve come up against an XML processor that correctly handles this cascading effect. Fortunately, this actually a trivial expression in XPath (but again not one that I&#8217;ve seen before), shown below:

<pre lang="XPath1.0">ancestor-or-self::*[attribute::xml:lang][1]/@xml:lang</pre>

What this does, is quite simple (in fact describing this will mean almost retyping the above part about the XML specification). From the list of this element and all its ancestors, find those that have an xml:lang attribute, grab the first (and thus nearest) one and return the value of its xml:lang attribute.

I&#8217;ve put together an [XSLT that demonstrates this in practice](https://gist.github.com/3390504#file_xml_lang_xpath_resolver.xsl), and adds the correct implied xml:lang attribute to every element in a document. The gist also includes a sample input and output file that shows how it should work, that I&#8217;ve included below:

If we run the XSLT across this file:

<noscript>
  <pre><code class="language-xml xml">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;data&gt;
    &lt;foo xml:lang="en"&gt;
        &lt;bar&gt;
            &lt;tog xml:lang="fr"&gt;
                &lt;wel&gt;
                    &lt;vay xml:lang="sv"/&gt;
                &lt;/wel&gt;
            &lt;/tog&gt;
            &lt;tog&gt;
                &lt;wel&gt;
                    &lt;hut xml:lang="it"/&gt;
                &lt;/wel&gt;
            &lt;/tog&gt;
            &lt;tog xml:lang=""/&gt;
        &lt;/bar&gt;
    &lt;/foo&gt;
&lt;/data&gt;</code></pre>
</noscript>

We should get this output:

<noscript>
  <pre><code class="language-xml xml">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;data xml:lang=""&gt;
    &lt;foo xml:lang="en"&gt;
        &lt;bar xml:lang="en"&gt;
            &lt;tog xml:lang="fr"&gt;
                &lt;wel xml:lang="fr"&gt;
                    &lt;vay xml:lang="sv"/&gt;
                &lt;/wel&gt;
            &lt;/tog&gt;
            &lt;tog xml:lang="en"&gt;
                &lt;wel xml:lang="en"&gt;
                    &lt;hut xml:lang="it"/&gt;
                &lt;/wel&gt;
            &lt;/tog&gt;
            &lt;tog xml:lang=""/&gt;
        &lt;/bar&gt;
    &lt;/foo&gt;
&lt;/data&gt;</code></pre>
</noscript>

While in practice there is a decision to be made as to whether xml:lang tags should be added to an XML file at the start of processing &#8211; for example to make finding every element that is in English easier. But in either way, determining what the language of an element now is much simpler.

The full [Gist of this is up on GitHub](https://gist.github.com/3390504 "Ignore all the changes to it - I don't understand markdown :/"), feel free to fork and improve this if necessary &#8211; or even point out where others have done this before, or why this may not even be necessary).

&nbsp;