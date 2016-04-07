---
id: 6533
title: Make sure your continuous testing is continuous
date: 2015-10-22T06:31:19+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=6533
permalink: /2015/10/make-sure-your-continuous-testing-is-continuous/
categories:
  - Data
  - Metadata
  - Python
tags:
  - aristotle-mdr
  - Best Practice
  - continuous testing
  - programming
  - python
  - testing
---
One of the key features of the [Aristotle Metadata Registry](https://github.com/aristotle-mdr/aristotle-metadata-registry) is its [extensive test suite](https://travis-ci.org/aristotle-mdr/aristotle-metadata-registry). Every time code is checked-in, the test suites are run and about 20 minutes later I get a notification saying everything is fine&#8230; or so it should be.

I recently made a small change to the test suite, that altered no code, and just changed some of the reporting. This shouldn&#8217;t have changed how the last tests were run, so they should have completed without problems, but this wasn&#8217;t the case.

After a short investigation, I discovered that a library that is used in the Aristotle admin interface had changed in a big way. Unfortunately, I haven&#8217;t been able to work on Aristotle as frequently as I&#8217;d like over the past few months, so this had gone completely unnoticed. Since the test environment is rebuilt every time the test are run, it was using the most recent version, while my code depended on an earlier version.

Since Aristotle is still in beta, the result wasn&#8217;t disastrous, however it still highlights (for me at least) an issue with relying on a green tick in the test suite saying everything is alright &#8211; because while the tests might be alright at that point in time, its prone to change.

So if you have to put down a project for a few weeks, or longer, make sure to nudge your code periodically, just to make sure everything is still running ok.

As for how it was fixed, a short alteration to the requirements file got the tests passing again, and a newer version that incorporates the updated library will be coming shortly.