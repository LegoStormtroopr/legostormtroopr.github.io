---
id: 6050
title: Aristotle MetaData Registry now has a Github organisation
date: 2015-03-15T06:37:39+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=6050
permalink: /2015/03/aristotle-metadata-registry-now-has-a-github-organisation/
categories:
  - Metadata
  - Programming
  - Python
  - Uncategorized
tags:
  - aristotle-mdr
  - DDI
  - Metadata
---
This weekends task has been upgrading Aristotle from a single user repository to a Github organisation. The new [Aristotle-MDR organisation](https://github.com/aristotle-mdr) holds the [main code for the Aristotle Metadata Registry](https://github.com/aristotle-mdr/aristotle-metadata-registry/), but alongside that it also has the [DDI Utilities codebase](https://github.com/aristotle-mdr/aristotle-ddi-utils) and some additional extensions, along with the new [&#8220;Aristotle Glossary&#8221; extension](https://github.com/aristotle-mdr/aristotle-glossary).

This new extension pulls the Glossary code base out of the code code to improve it status as a &#8220;pure&#8221; ISO/IEC 11179 implementation as stated in the [Aristotle-MDR mission statement](http://aristotle-metadata-registry.readthedocs.org/en/latest/mission_statement.html). It will also provide additional Django post-save hooks to provide easy look-ups from Glossary items, to any item that requires the glossary item in its definition.

If you are curious about [the procedure for migrating an existing project from a personal repository to an organisation, I&#8217;ve written a step-by-step guide on StackExchange](http://stackoverflow.com/questions/29046080/issues-if-migrating-a-repository-to-a-github-organisation-then-forking-the-repo/29057532#29057532) that runs through all of the steps and potential issues.