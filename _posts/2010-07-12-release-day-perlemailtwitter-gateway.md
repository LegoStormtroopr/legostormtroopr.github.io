---
id: 113
title: 'Release Day &#8211; Perl/Email/Twitter Gateway'
date: 2010-07-12T15:28:53+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=113
permalink: /2010/07/release-day-perlemailtwitter-gateway/
aktt_notify_twitter:
  - yes
  - yes
aktt_tweeted:
  - 1
categories:
  - PET-Gateway
  - Project
tags:
  - code
  - perl
  - pet-gateway
  - project
  - twitter
---
Today is the alpha release day of [PET-Gateway](http://code.google.com/p/pet-gateway/). A clunky interface to translate between a pair of email addresses and twitter (written in Perl, wouldn&#8217;t you guess). At the moment it has far too little documentation, but this will be corrected after I get back from the slopes.

However, the short version is:

Firstly, download the script from [Google Code](http://code.google.com/p/pet-gateway/ "Perl/Email/Twitter Gateway"), and its numerous dependencies from CPAN.

Then, setup two emails, one as the twitter-server proxy and a second as the twitter-client proxy (you may already have this, like your work email thats hidden behind an oppressive  or an email you can access in an even more oppressive dictator regime).

In the poorly documented config file you at the smtp and pop3 details (IMAP coming later), and the client proxy as the &#8220;to email&#8221; and the add the server proxy username and password under email.

At this stage the pop3 and smtp servers both need to support ssl and use the same details, again this will be updated at a later stage.

Now, copy the .rc file with the same name to your home directory and run the script. It will ask to be [oAuthed](http://dev.twitter.com/pages/oauth_faq "oAuth FAQ") against [Twitter](http://www.twitter.com/legostormtroopr "My Twitter account") using a URL and the returned PIN code. Make sure you are logged into to Twitter when you browse to the given URL.

After that you are all setup, just add a cron job with a command like:

<pre>*/2 * * * * ~/path_to_pet-gateway/pet-gateway.pl &gt;&gt; ~/.pet-gateway.log</pre>

to make the process run as often as you need and you are all set to tweet to your hearts content, even when you can&#8217;t access Twitter!

When you send to the server email address, it only posts the message body upto the first line break, splitting it across tweets if it has too, and also looks for attached images to upload to [imgur.com](http://www.imgur.com). Also, if you want to reply to another tweet, reply to the email the server-proxy sends you, and the it prepends the sending users username automatically, and sends the update properly including the originating tweets ID so the tweets thread correctly.

This was kind of rushed out the door so I could still Tweet on my upcoming holiday, but there should be a fair bit of development when I get back either on this or a python rewrite that should have less dependencies and be easier to distribute and run.

If you find this useful, add a comment here, or on [PET-Gateways main page](http://www.kidstrythisathome.com/projects/perlemailtwitter-gateway/ "PET-Gateway main page") and let me know, and if you find issues with my code feel free to submit a bug, path, diff or complain on the [google code page](http://code.google.com/p/pet-gateway/).