---
title: Verifying documentation during continuous integration
author: Samuel Spencer
layout: post
categories:
  - Python
  - Continuous Integration
---

After altering some documentation, I made a small tweak to the continuous integration
suite for [Aristotle Metadata Registry](http://www.aristotlemetadata.com) to include a
sphinx build to ensure that the documentation was correct - or as correct as can be automatically checked.

This was as simple as adding two lines during the correct phases (for [Travis-CI](travis-ci.org) at least):

```
install:
  - "pip install Sphinx sphinx-rtd-theme"
before_script:
  - cd docs ; sphinx-build -nW -b html -d _build/doctrees . _build/html ; cd ..
```

Obviously these will need to be intertwined with your own suite and processes, but the principle is the same - 
as code is checked in, changes to documentation are checked before tests. This is especially important when
documentation is generated from code.

The key part in this run specifically is ``sphinx-build -n`` which forces "nit-picky mode" where warnings are raised 
as errors, which are enough to kill the test suite and raise a build error. Be aware though, nit-picky mode
is fairly strict and can be overly sensitive to some problems around objects not having documentation - but a solution 
to this was [posted on StackOverflow which I used to solve the problem](http://stackoverflow.com/a/30624034/764357).

Doing this alone was enough to highlight a few small syntax errors which didn't prevent the documentation from building,
but did cause incorrect or dead links.
