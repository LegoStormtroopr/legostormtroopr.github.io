---
id: 603
title: 'The DDI Identity Crisis and how to solve it &#8211; Part 1 : Versions and Identifiers'
date: 2012-10-13T23:32:29+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=603
permalink: /2012/10/the-ddi-identity-crisis-part-1/
categories:
  - Metadata
tags:
  - DDI
  - DDI4
  - future-proof
  - "I'll make my own specification with blackjack..."
---
This is a 2 part post that examines the the different classes of identifiable object in DDI, and offers critiques for their current design and possible improvements to the standard with the aim to simplify the model and (hopefully) improve the uptake of people using the standard. But first we need to have a quick look at what the 3 different classes of identifiable object in DDI are and where they are used, in an increasing order of complexity:

<ol start="0">
  <li>
    Non-identifiable &#8211; We&#8217;ll include this as the &#8216;base&#8217; case of any DDI object that isn&#8217;t capture by those above. These objects are mostly used to capture basic metadata concepts, such as labels or descriptions for more complex objects.
  </li>
  <li>
    Identifiable &#8211; Objects that only require an ID attribute. These are mostly basic metadata, and below I&#8217;ll show the shady distinction between identifiables and non-identifiables being blurry and why these objects probably don&#8217;t need identifiers at all.
  </li>
  <li>
    Versionable &#8211; A level above identifiables, these require a version and an ID. This is probably the most commonly encountered type of core attribute, as they comprise the bulk of the survey objects people are used to dealing with &#8211; such as questions, variables and codelists. Further down I talk about how these objects don&#8217;t need a version, along with the administrative burden it adds &#8211; without a clear benefit.
  </li>
  <li>
    Maintainable &#8211; The most complex identifier &#8211; with an ID, a version and a reference to a maintainance agency. Maintainable objects are mostly used as either container objects, such as schemes, resource packages or groups; or high-level and survey wide objects such as Study Units or Archival objects. In the following post I&#8217;ll show how they are currently managed, and how they can be better managed as XML objects to simplify RESTful interfaces for DDI.
  </li>
</ol>

## **Identifiable objects don&#8217;t need identifiers**

[Identifiable objects](http://www.ddialliance.org/sites/default/files/documentation/ddi3.1/schemas/reusable_xsd/complexTypes/AbstractIdentifiableType.html) are the subset of all objects within DDI that have only an ID, but no version or agency. In DDI, since ID attributes are only required to be local to the parent maintainable, this means that the reference an identifiable, its ID isn&#8217;t enough, you also needs the ID of the parent object as well! So while an identifiable can be referenced, to access it, it is necessary to first identify and gather the parent resource.

This becomes  interesting when we examine the list of objects which are only identifiable (not versionable or maintainable), shown below:
  


<noscript>
  <pre><code class="language- ">Abstract
Abstract
Access
ActionToMinimizeLosses
Attribute
Coding
CollectionEvent
CollectionSituation
CoordinateGroup
CreationSoftware
DataCollectionMethodology
DataFileIdentification
DefaultAccess
DeviationFromSampleDesign
Embargo
ExternalAid
ExternalInformation
ExternalInterviewerInstructionReference
Geography
GrossFileStructure
GrossRecordStructure
LifecycleEvent
Location
LogicalRecord
Measure
ModeOfCollection
Note
OtherMaterial
PhysicalRecordSegment
ProcessingEvent
Purpose
Purpose
RecordRelationship
Role
SamplingProcedure
Software
SpatialCoverage
TemporalCoverage
TimeMethod
TopicalCoverage
VariableSet
Weighting
</code></pre>
</noscript>

All of these objects constitute (at least to my mind) very basic, textual and contextal dependent metadata. Concepts like an &#8216;abstract&#8217; or &#8216;purpose&#8217; only really make sense given the context of what you are summarizing. This is reinforced by the fact that this information can only be gathered by finding the object you are summarising first, before getting this information.

Which leads us to ask &#8211; what make identifiables different to non-identifiables? In my opinion, nothing &#8211; its a distinction made on convenience. Again, in my opinion, identifiables exist because Notes exist. Because the [methods for extending and improving DDI](http://www.kidstrythisathome.com/2012/09/when-ddi-isnt-enough-part-3-picking-the-right-approach-to-improving-the-standard/ "When DDI isn’t enough Part 3 – Picking the right approach to improving the standard") were not made more obvious to early adopters, DDI Notes have become the most common way to annotate objects, and given the referential nature of Notes, this requires objects to have identities.

**The solution: Remove IDs from identifiables** &#8211; If Notes are deprecated as a solution, IDs on identifiers are no longer needed and there is no other reason to identify them and they can be scaled back to the &#8216;non-identifiable&#8217; class of object.

##  **Versionable objects** shouldn&#8217;t **have versions**

[Versionable objects](http://www.ddialliance.org/sites/default/files/documentation/ddi3.1/schemas/reusable_xsd/complexTypes/AbstractVersionableType.html) are the set of objects that have both an ID and a version, and (as the DDI User Guide states) &#8220;are elements for which changes in content are important to note.&#8221; However, both versions and maintainables have a version, that supports the tracking of changes to an object. This causes a very interesting problem to occur when dealing with objects in practice &#8211; the identifiers of objects can change, without them having changed at all!

Lets look at an example, with a _maintainable_ QuestionScheme called QS1 with version 1, and two _versionable_ Questions, Q1 and Q2, both on version 1 as well. Since the full identifier for a versionable is also comprised of its parent, the full ID for the most recent version of Q1 takes a form similar to <span style="text-decoration: underline;">QS1:V1|Q1:V1</span>, simple enough. A problem arises when Q2 is changed to be version 2. Technically, since Q2 is a child of the QuestionScheme QS1, it has also changed.

Now, the complexity is that QS1 has changed, so the full ID for the most recent version of Q1 has now changed to, QS1:V2|Q1:V1. Which leads to the academic question &#8211; if Question Q1&#8217;s parent has changed, has Q1 itself also changed, meaning that to be apart of the updated parent it also needs a new version?

The discussion to resolve this problem with DDI versionables has actually been kicking around for quite a while, but again the solution for this is pretty clear as the section header states. The first thing to recognise is that all versionable objects are already versioned by their parent object, so strictly speaking, given only the full ID for the parent, and the ID of a current versionable, it is possible to identify a single object for the simple fact that all IDs on objects must be unique within their parent maintainable.

So by removing the version from versionables, and relegating them to instead be identifiables we simplify the model for abstract types in DDI is reduced to two classes, with very clear intentions. In the new model identifiables are objects which are reused through references within other objects to construct rich, linked metadata constructs, while Maintainables are the versioning objects that are used by agencies to administer cross-survey and cross-cycle metadata holdings.

However, as we&#8217;ll see in the next post, this change actually helps us take advantage of a number useful XML technologies to simplify the learning process for DDI, for implementers and developers alike.

## **Next up: How Maintainables aren&#8217;t** properly **maintained**

In the next post, I&#8217;ll cover how to simplify the DDI XSD Schemas to take advantage of XML identities by removing inline schemes and restricting base elements to simplify identification and URI design, so DDI can utilise URLs and XML fragments to precisely define objects for RESTful interfaces.

<div>
</div>