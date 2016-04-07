---
id: 629
title: 'A developers new years resolution: Stop talking about the &#8220;user&#8221;'
date: 2012-12-21T05:17:46+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=629
permalink: /2012/12/a-developers-new-years-resolution-stop-talking-about-the-user/
categories:
  - Drivel
  - Education
  - Programming
tags:
  - no-user
  - UX
---
<p style="text-align: justify;">
  <div class="simplePullQuote">
    <p>
      [The term &#8220;user&#8221;] splits people into two discrete groups &#8211; &#8220;programmers&#8221; and &#8220;users&#8221;, &#8230; the unhelpfully divisive &#8220;us&#8221; and &#8220;them&#8221;
    </p>
  </div>
</p>

User interface, user experience, user story, user error. Application programming is devoted to helping users. But while there have been objections to the term user, and there have been [suggestions to humanise the term](http://www.jnd.org/dn.mss/words_matter_talk_ab.html) by encouraging developers to consider people, as opposed to &#8216;users&#8217;. But even then we are just changing the term, not fixing a problem. There is no generic term for people that is adequate, as all people interact with the world differently, and as such people interact with software in different ways and expecting different interactions.

To see this, lets look at the first [example of a user story on the Wikipedia page](http://en.wikipedia.org/wiki/User_story): _As a user, I want to search for my customers by their first and last names_.

As a developer, if I were to pick this up I have no clue as to what kind of interaction I need to provide. Is this &#8220;user&#8221; a business clerk looking as sales customers, or a MMORPG administrator looking for game players, or veterinarian looking through a list of pets. In each of these cases there are subtle differences, where customers can be people, avatars or pets and as such each set of information may need to be presented differently.

While the term user, may be appropriate when we discuss the broad fields of user experience and user interaction, acting as a catch all for all possible users of software. But when we begin looking at specific classes of people we want to assist with software it ceases to be a helpful term and it splits people into two discrete groups &#8211; &#8220;programmers&#8221; and &#8220;users&#8221;, &#8220;IT-side&#8221; and &#8220;business-side&#8221;, or the unhelpfully divisive &#8220;us&#8221; and &#8220;them&#8221;. Who is &#8220;us&#8221; and who is &#8220;them&#8221; generally depends on which side of the table you are on, but it remains that the term &#8220;user&#8221; draws a clear line in the sand, between our group and the dreaded &#8220;others&#8221;. Worse still, the term for the others is so unhelpfully vague that we can only think in metaphors or stereotypes. By the way, have you ever noticed that programmers type (Ctrl+i)_like this_(Ctrl+i), but users type (clicks Bold)**like this**(clicks Bold again)?.

## The solution: Stop using the word &#8220;user&#8221;

<div class="simplePullQuote">
  <p>
    As soon as you think about a &#8220;user&#8221;, immediately stop and mentally replace the term with an appropriate noun.
  </p>
</div>

As a new years resolution, I want all programmers, developers, business analysts, and so on, to try something. As soon as you think about a &#8220;user&#8221;, immediately stop and mentally replace the term with an appropriate noun that mentions whose needs are being met by the tool you are designing. Regardless of how contrived or long winded that noun needs to be, replace the term user EVERY TIME it enters your thoughts, even before you write it down. Even if you weren&#8217;t going to write something, the second you think &#8220;the user wants&#8230;&#8221; or &#8220;a user will see&#8230;&#8221; immediately go back and replace that term.

So see why this is helpful, I propose another user story: _Clicking the button will allow the user to save their work._

And picture how this interaction may take place and answering some of these questions: What does the button look like? How will the use know to click that button? How will the interface react when the user clicks the button? Given the vagueness of the story, they may be really tough questions to answer.

Now, contrast this with the following by answering the same questions about the following three user stories:

  * Clicking the button will allow the <span style="text-decoration: underline;">author of a novel</span> to save their work.
  * Clicking the button will allow the <span style="text-decoration: underline;">programmer</span> to save their work.
  * Clicking the button will allow the <span style="text-decoration: underline;">child who is drawing</span> to save their work.

When you pictured these interactions, did you visualise them differently? Did you picture different images on the button shown to the author and the child? Is the size of the button different between the child&#8217;s button and the others? More than that did the user story sound unnecessary, for example, does the idea of a programmer clicking a button seem to make sense, or would they be more likely to just use a menu or even keyboard shortcut?

By forcing ourselves to go back and reexamine the &#8220;user&#8221; of any given piece of work, or line of code, it forces programmers to think about what they are trying to achieve. While it might be conceivable that a &#8220;user&#8221; might want to do some given action, it is a helpful mental exercise that forces us to step back and really contemplate if the user really will want or need to do something.

&nbsp;