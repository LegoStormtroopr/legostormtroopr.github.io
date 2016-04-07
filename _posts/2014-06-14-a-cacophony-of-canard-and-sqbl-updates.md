---
id: 5925
title: A cacophony of Canard and SQBL updates.
date: 2014-06-14T06:25:53+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=5925
permalink: /2014/06/a-cacophony-of-canard-and-sqbl-updates/
categories:
  - Uncategorized
---
Late last month [Canard version 0.2.2](https://github.com/LegoStormtroopr/canard/releases/tag/v0.2.2 "Canard v0.2.2") was packaged up and released in time for the 2014 IASSIST conference. This new version changed the Canard Question Module Editor from running on Python 64-bit to 32-bit as was requested by a few people, as well as including import and export plugins for the new [3.2 release of the DDI-Lifecycle XML format](http://www.ddialliance.org/Specification/DDI-Lifecycle/3.2/ "DDI Lifecycle 3.2").

The reason for the timing of this release the was due to me presenting Canard during the DDI tools session as well as the poster session. At both of these session, Canard was was well received, and there was interest in Canard in wide applications from teaching undergraduates about survey design and metadata management, researchers documenting surveys with lots of live feedback, and archivists recapturing questionnaire metadata.

Until recently, Canard (and its underlying data model [SQBL](http://sqbl.org "SQBL homepage")) have been following a very ad hoc release and change process due to its ongoing development. However, given growing interest in the Canard tool, its in everyones interest for this to be made clearer. So first of all a proper [release version of the Simple Questionnaire Building Language Schema is available on Github](https://github.com/LegoStormtroopr/sqbl-schema/releases/tag/v0.1.0 "SQBL release v0.1.0")

New versions of SQBL will be released in a form that remains backwards compatible for minor and patch version numbers &#8211; in essence, this means the addition of no new or removal of old mandatory elements or attributes. Canard release versions will also be based to these version numbers, so starting from Canard v0.2.2, the Canard minor version number will be 1 greater than the SQBL version numbers it supports. Its likely that Canard will have more frequent releases than SQBL, however, given how patch versions may be released, its best to use the latest version of Canard to ensure compatibility with the applicable minor version family of SQBL.

**In short &#8211; this guarantees that in future the latest Canard version 0.2 will open any SQBL v0.1 document made by a prior version of Canard in the 0.2 version family, which makes upgrading a safer option.**

However, this doesn&#8217;t mean that SQBL is &#8216;fixed&#8217; there are already certain issues that will need to be addressed &#8211; especially around describing calculated values in questionnaires &#8211; just that changes will be more predictable. Nor does it mean that the development of Canard will slow, as there are already issues which have been opened (and some closed) since the last release.

Its likely that patch level changes to SQBL will happen every 3 to 4 patch releases of Canard. This will give people time to adjust and find and identify any issues in the software or the schema, as well as give time to migrating import and export plugins.

As always, requests or bugs are more than wanted, so if you are using Canard, please feel free to [raise an issue on Github](https://github.com/LegoStormtroopr/canard/issues "Canard Issues page"), and likewise if there are missing features that require changes to the underlying data model, or deviations from similar standards like DDI, [raise an issue with the SQBL schema](https://github.com/LegoStormtroopr/sqbl-schema/issues "SQBL issues page"), or [join the SQBL mailing list](http://bit.ly/SQBL_ml "SQBL mailing list") and see if there are ways a problem can be captured in the current schema.