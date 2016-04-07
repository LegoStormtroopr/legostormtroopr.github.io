---
id: 154
title: 'Reality Doesn&#8217;t Fit RDF'
date: 2011-01-31T10:14:58+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=154
permalink: /2011/01/reality-doesnt-fit-rdf/
aktt_notify_twitter:
  - yes
  - yes
aktt_tweeted:
  - 1
categories:
  - Data
  - Metadata
---
I&#8217;ve been doing recent research into mapping a information models into a useable data format, and one of the first ideas that crossed my mind was using RDF as the serialization format. While I spent a lot of time trying to figure out to best map the model to RDF, and it was possible, it just wasn&#8217;t technically feasible.

One of the main issues I found with RDF, was while there was a lot of theory behind it (and there is a lot of theory) there is very little practice to back it up. You can create an ontology to describe an information model, but I found no way to validate a graph against it, triple-stores while fast each relied on their own slightly different implementation of SPARQL and while RDF graphs support the idea of concise descriptions of objects, these aren&#8217;t quite the same as having a complex object model.

Probably the biggest issue I had was the idea of anonymous nodes, and how they are tolerated to allow complex objects. The basic example of this is a name made of multiple parts, eg:

<pre>me:Sam foaf:name _:name1
_:name1 foaf:first_name "Sam"
_:name1 foaf:last_name "Spencer"
</pre>

In the above example &#8220;_:name1&#8243; is a node all on its own. It can be referred to, and some triple-stores even allow it to be used by multiple identified nodes, except that it doesn&#8217;t really exist. Its a fake, a phoney, a thing that doesn&#8217;t really exist outside of the relationship &#8220;Sam has a name&#8221;. Granted other people will be called &#8220;Sam Spencer&#8221; and you may even want to be able to find all people with the same name, but in a lost of instances a name is just a very abstract concept, a semi-unique identifier.

Wouldn&#8217;t it be simpler to go:

<pre>thisSam = {name: {first: "Sam",
                  last:  "Spencer"}
          }
</pre>

Here we can see that this name belongs to the object &#8220;thisSam&#8221;, and thisSams first name is thisSam.name.first, or more simply &#8220;Sam&#8221;. The ownership of this sub-property is very specific about where it goes.

As the saying goes, this name is mine, there are many like it, but this one is mine.