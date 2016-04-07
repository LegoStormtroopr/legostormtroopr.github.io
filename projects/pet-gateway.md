---
id: 117
title: Perl/Email/Twitter Gateway
date: 2010-07-12T15:27:13+00:00
author: Samuel Spencer
layout: page
guid: http://www.kidstrythisathome.com/
aktt_notify_twitter:
  - no
---
<div>
  <p>
    <a href="http://code.google.com/p/pet-gateway/">PET-Gateway</a> is a clunky interface to translate between a pair of email addresses and twitter (written in Perl, wouldn&#8217;t you guess). At the moment it has far too little documentation, but this will be corrected after I get back from the slopes.
  </p>
  
  <p>
    However, the short version is:
  </p>
  
  <p>
    Firstly, download the script from <a title="Perl/Email/Twitter Gateway" href="http://code.google.com/p/pet-gateway/">Google Code</a>, and its numerous dependencies from CPAN.
  </p>
  
  <p>
    Then, setup two emails, one as the twitter-server proxy and a second as the twitter-client proxy (you may already have this, like your work email thats hidden behind an oppressive  or an email you can access in an even more oppressive dictator regime).
  </p>
  
  <p>
    In the poorly documented config file you at the smtp and pop3 details (IMAP coming later), and the client proxy as the &#8220;to email&#8221; and the add the server proxy username and password under email.
  </p>
  
  <p>
    At this stage the pop3 and smtp servers both need to support ssl and use the same details, again this will be updated at a later stage.
  </p>
  
  <p>
    Now, copy the .rc file with the same name to your home directory and run the script. It will ask to be <a title="oAuth FAQ" href="http://dev.twitter.com/pages/oauth_faq">oAuthed</a> against <a title="My Twitter account" href="http://www.twitter.com/legostormtroopr">Twitter</a> using a URL and the returned PIN code. Make sure you are logged into to Twitter when you browse to the given URL.
  </p>
  
  <p>
    After that you are all setup, just add a cron job with a command like:
  </p>
  
  <pre>*/2 * * * * ~/path_to_pet-gateway/pet-gateway.pl &gt;&gt; ~/.pet-gateway.log</pre>
  
  <p>
    to make the process run as often as you need and you are all set to tweet to your hearts content, even when you can&#8217;t access Twitter!
  </p>
  
  <p>
    When you send to the server email address, it only posts the message body upto the first line break, splitting it across tweets if it has too, and also looks for attached images to upload to <a href="http://www.imgur.com">imgur.com</a>. Also, if you want to reply to another tweet, reply to the email the server-proxy sends you, and the it prepends the sending users username automatically, and sends the update properly including the originating tweets ID so the tweets thread correctly.
  </p>
  
  <p>
    If you find this useful, add a comment here and let me know, and if you find issues with my code feel free to submit a bug, path, diff or complain on the <a href="http://code.google.com/p/pet-gateway/">google code page</a>.
  </p>
</div>