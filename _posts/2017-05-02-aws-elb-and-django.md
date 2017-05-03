---
title: Handling AWS-ELB terminating a healthy django instance when accessed from an invalid hostname
author: Samuel Spencer
layout: post
categories:
  - django
  - aws
---

When spinning up a new service, Amazon Elastic LoadBalancer needs to check if the service is live and running. This check is done from an IP (from any IP in a private IP range) to the service, this is done by the ELB just doing a simple GET request to a specified path, with no host information - for example GET /heatbeat.

If this instance is a Django service, regardless of the page accessed, this call will fail as in a properly setup Django it is very unlikely that the IP will be in Django's settings.ALLOWED_HOSTS settings.

There are two ways around this, either:

a. Add every IP from every private IP range into your Django project's ALLOWED_HOSTS settings b. Add a simple middleware that returns a simple 200 response, given the specific URL.

The second option is shown below.
Raw

{% gist LegoStormtroopr/7a80e170bd3943b6a37a3bd45a918a0b healthchecker_middleware.py %}

{% gist LegoStormtroopr/7a80e170bd3943b6a37a3bd45a918a0b settings.py %}

[Full gist is here](https://gist.github.com/LegoStormtroopr/7a80e170bd3943b6a37a3bd45a918a0b)
