---
id: 6649
title: Adding advanced user tracking and security to the Aristotle Metadata Registry ecosystem
date: 2016-01-08T04:50:41+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=6649
permalink: /2016/01/adding-advanced-user-tracking-and-security-to-the-aristotle-mdr-ecosystem/
categories:
  - Django
  - Metadata
  - Python
tags:
  - aristotle-mdr
  - pythias
  - security
---
The Aristotle MetaData Registry is already built on the [strong, secure web-framework provided by Django](https://docs.djangoproject.com/en/1.8/topics/security/) and includes a [vast suite of tests that ensure the security of metadata](travis-ci.org/aristotle-mdr/aristotle-metadata-registry/) at all stages of the data lifecycle.

But to enhance this, work has begun on a new [extension to Aristotle, called Pythias,](https://github.com/aristotle-mdr/pythias-user-management) that incorporates additional user tracking and security to provide peace of mind when deploying large scale metadata systems.

Powered by [django-axes](https://github.com/django-pci/django-axes) and [django-user-sessions](https://github.com/Bouke/django-user-sessions) this will give Aristotle site administrators the power to track login successes and failure, block access at an IP level, automatically lock out user accounts and block concurrent logins. It will also give users the ability to view current logins and remote logout from sessions.