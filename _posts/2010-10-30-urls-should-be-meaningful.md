---
id: 157
title: URLs should be meaningful
date: 2010-10-30T16:08:21+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=157
permalink: /2010/10/urls-should-be-meaningful/
aktt_notify_twitter:
  - yes
  - yes
aktt_tweeted:
  - 1
categories:
  - Data
  - Web Development
tags:
  - internet
  - url
  - web development
---
> In [computing](http://en.wikipedia.org/wiki/Information_technology "Information technology"), a **Uniform Resource Locator** (**URL**) is a [Uniform Resource Identifier](http://en.wikipedia.org/wiki/Uniform_Resource_Identifier "Uniform Resource Identifier") (URI) that specifies where an identified resource is available and the mechanism for retrieving it.
> 
> &#8211; wikipedia.com &#8211; [Uniform Resource Locator](http://en.wikipedia.org/wiki/Uniform_Resource_Locator)

A URL by rights is the first piece of information a user interacts with on your site, because without it they cannot get there, and while most users will follow a link to find your site, URLs still take center space in every browser UI.

So why is it that so many web-developers neglect their usefulness completely?

Take for example the URL of this blog post

<pre>http://www.kidstrythisathome.com/2010/10/urls-should-be-meaningful/</pre>

There is quite a bit of information here, this is a blog post and it was made in October of 2010. If you remove the last section so the URL looks like this:

<pre>http://www.kidstrythisathome.com/2010/10/</pre>

you have a related, but brand new URL, and you now have a link to a page of all blog posts from October 2010. Remove the &#8220;10/&#8221; and you have a page of all posts from 2010, and remove &#8220;2010/&#8221; and you are at the main site again.

_This should be expected behaviour, and users should be encouraged or at least allowed to have this basic interaction with your site._

Now, lets look at an example of a &#8220;bad&#8221; URL: [](http://www.canberra.edu.au/courses-units/m-coursework/information-studies/online/mis)

<pre><a href="http://www.canberra.edu.au/courses-units/m-coursework/information-studies/online/mis">http://www.canberra.edu.au/courses-units/m-coursework/information-studies/online/mis</a></pre>

To look at this URL is very descriptive, you found this I was look at courses at Canberra University examining the units available in Masters by coursework (/m-coursework) in the field of information studies, and looking at the online Masters in Information Studies (/online/mis).

By rights, I should be able to work backwards through this URL, deleting the last section and finding valid information all the way back up the directory structure. For example [](http://www.canberra.edu.au/courses-units/m-coursework/information-studies/online/mis)

<pre><a href="http://www.canberra.edu.au/courses-units/m-coursework/information-studies/online/mis">http://www.canberra.edu.au/courses-units/m-coursework/</a></pre>

should take us to the Canberra University webpage outlining all coursework Masters, likewise with other possible permutations of the above URL. However, it does not, there is no valid URL that can be made by deleting sections from the end of the given URL, and in this sense valid is a URL that resolves to a page with useful and relevant information.

By using meaningful URLs on your site you add another feature for users, and help provide a stronger semantic structure to your pages. That said, if your URL looks like this:

<pre><pre>http://example.com/Directory/exm@.nsf/ProductsbyTopic/D8CBDEC90255GBF7CA2575E70119DFAA?OpenDocument</pre>


<p>
  then you have bigger problems than URL structure and need to start reexamining your entire design.
</p>