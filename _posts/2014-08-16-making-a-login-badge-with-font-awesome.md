---
id: 5961
title: Making a login badge with font-awesome
date: 2014-08-16T00:45:47+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=5961
permalink: /2014/08/making-a-login-badge-with-font-awesome/
categories:
  - Drivel
  - Programming
  - Web Development
tags:
  - bootstrap
  - font awesome
  - web development
---
On a new site I&#8217;m building I was looking for a way to include a nice login badge, similar to those on Google login pages. In fact I found some nice looking bootstrap login templates that actually included the Google login image below directly.

<img class="aligncenter" src="http://i.imgur.com/8YXfo16.png" alt="Google login guy" width="112" height="104" />

Turns out the image is actually a square, with a css border-radius applied, so given that the page already loads the whole set of font-awesome icons, I wondered if it was possible to replicate this without loading an image&#8230; and it is.

<img class="aligncenter" src="http://i.imgur.com/rHnxu6K.png" alt="Font-awesome login guy" />

There were issues getting the user silhouette to sit nicely over a standard font awesome circle, so I went down the route of using the border radius. The colours don&#8217;t match exactly, but the advantage of this approach is the colours can be customised to match any theme very quickly. [The complete code is pretty straight forward](https://gist.github.com/LegoStormtroopr/4dab9ec0868ebae6a9b4) and the gist is below:

<noscript>
  <pre><code class="language-html html">&lt;span class="face"&gt;
  &lt;i class="fg fa fa-user"&gt;&lt;/i&gt;
&lt;/span&gt;</code></pre>
  
  <pre><code class="language-css css">.face {
    display:block;
    -moz-border-radius: 50%;
    -webkit-border-radius: 50%;
    border-radius: 50%;
    margin: auto;
    width: 96px;
    height: 96px;
    background-color:powderblue;
    overflow:hidden;
    text-align:center;
}
.face .fg {
    font-size:650%;
    position:relative;
    top:15px;
    color:royalblue;
}</code></pre>
</noscript>

&nbsp;