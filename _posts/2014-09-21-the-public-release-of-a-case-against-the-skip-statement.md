---
id: 5948
title: 'The public release of &#8220;A Case Against the Skip Statement&#8221;'
date: 2014-09-21T10:38:37+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=5948
permalink: /2014/09/the-public-release-of-a-case-against-the-skip-statement/
categories:
  - Data
  - Education
  - Programming
  - Statistics
tags:
  - computer science
  - programming
  - questionnaires
  - SQBL
  - Structured Questionnaire Design
---
A few years ago I wrote a paper titled &#8220;A Case Against the Skip Statement&#8221; on the logic construction of questionnaires that was [awarded second place in the 2012 Young Statisticians Awards of the International Association of Official Statistics](http://www.statisticsviews.com/details/news/2476771/2012-IAOS-Prize-for-Young-Statisticians.html "Results of the 2012 IAOS Prize for Young Statisticians").

It went through two or three rounds of review over the course of a year, but due to shifting organisational aims, I was never able to get the time to polish it to the point of publication before changing jobs. So for the past few years I have quietly emailed it around and received some positive feedback and have gotten a few requests to have it published so it could be cited. I have even myself referred back to it in conferences and other papers, but never formally cited it myself. I have also used this article as a reason why study of &#8216;classical&#8217; articles in computer science is still important, for the simple fact that while Djikstra&#8217;s &#8220;Gotos Considered Harmful&#8221; is outdated in traditional computer science, its methods and mathematical and logic reasoning can still be useful, as seem in the comparison of programming languages and the logic of questionnaires.

[As a compromise to those requests, I released the full text online](http://bit.ly/CaseAgainstSkip "Case Against the Skip Statement"), with references and a ready to use Bibtex citation for those who are interested. For those interested the abstract follows the Bibtex reference:

<pre>@misc{CaseAgainstSkip,
    title = {A Case Against the Skip Statement},
    author ={Samuel Spencer},
    year = 2012,
    howpublished = {\url{http://bit.ly/CaseAgainstSkip}},
    note = {[Date downloaded]}
}</pre>

or using BibLatex:

<pre>@online{CaseAgainstSkip,
   author ={Samuel Spencer},
   title ={A Case Against the Skip Statement},
   year = 2012,
   url ={http://bit.ly/CaseAgainstSkip},
   urldate ={[Date downloaded]}
}
</pre>

* * *

With statistical agencies facing shrinking budgets and a desire to support evidence-based policy in a rapidly changing world, statistical surveys must become more agile. One possible way to improve productivity and responsiveness is through the automation of questionnaire design, reducing the time necessary to produce complex and valid questionnaires. However, despite computer enhancements to many facets of survey research, questionnaire logic is often managed using templates that are interpreted by specialised staff, reducing efficiency. It must then be asked why, in spite of such benefits, is automation so difficult?

This paper suggests that the stalling point of further automation within questionnaire design is the ‘skip statement’. An artifact of paper questionnaires, skip statements are still used in the specification of computer-aided instruments, complicating the understanding of questionnaires and impeding their transition to computer systems. By examining questionnaire logic in isolation we can analyse the structural similarity to computer programming and examine the applicability of hierarchical patterns described in the structured programming theorum, laying a foundation for more structured patterns in questionnaire logic, which in time will help realise the benefits of automation.