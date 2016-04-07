---
id: 6650
title: Hiding ModelForm fields in a Django modelformset_factory
date: 2016-01-04T02:51:53+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=6650
permalink: /2016/01/hiding-modelform-fields-in-a-django-modelformset_factory/
categories:
  - Django
  - Drivel
  - Python
---
A small short and sweet one. I had trouble hiding a field in a Django <tt>modelformset_factory</tt> and none of the usual places were any help.

It turns out the simple answer is using the undocumented <tt>widgets</tt> parameter when creating it:
  
`A small short and sweet one. I had trouble hiding a field in a Django <tt>modelformset_factory</tt> and none of the usual places were any help.

It turns out the simple answer is using the undocumented <tt>widgets</tt> parameter when creating it:
  
` 

This also means in a template it shows up as hidden, and isn&#8217;t included in the <tt>form.fields</tt>, but _is_ included in <tt>form.hidden_fields</tt> &#8211; the more you know!