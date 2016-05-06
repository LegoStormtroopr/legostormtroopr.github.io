---
title: Limiting the number of objects for a model in a django database
author: Samuel Spencer
layout: post
categories:
  - Django
  - Python
---

Sometimes you want to set a hard limit on the number of Django objects you let a user
store and unfortunately, this isn't easily possible in a vanilla Django install - 
especially not for objects you don't control, such as the `django.auth.User` model.

However, with some tweaking, this is actually quite easy.

The first step is to setup a [django signal](https://docs.djangoproject.com/en/1.9/topics/signals/) to
catch the particular model *before* it is saved:

```python
    from django.core.exceptions import PermissionDenied
    from django.db.models.signals import pre_save
    
    @receiver(pre_save, User)
    def check_limits(sender, **kwargs):
        if sender.objects.count() > YOUR_LIIMIT:
            raise PermissionDenied
```

This will work, but cause a generic `PermissionDenied` error, when we might want to be clearer.
Instead, if we use a custom exception we know exactly why the save failed:

```python
from django.core.exceptions import PermissionDenied
from django.db.models.signals import pre_save

class LimitExceeed(PermissionDenied):
    pass

@receiver(pre_save, User)
def check_limits(sender, **kwargs):
    if sender.objects.count() > YOUR_LIIMIT:
        raise LimitExceeded
```

But this will propgate up and cause 500 errors instead of the 403 permission denied...

Unless we write a [custom django middleware](https://docs.djangoproject.com/en/1.9/topics/http/middleware/)!

```
class LimitExceededMiddleware(object):
    def process_exception(self, request, exception):
        if isinstance(exception, LimitExceeded):
            return some_view
        return None
```

Here `some_view` is any regular django view necessary to tell the user what happen. And voila, all done.

This code only allows you to restrict but customisation should make other objects easy to trap.
Alternatively, I've started working on [`django-city-limits`](https://github.com/LegoStormtroopr/django-city-limits)
that makes it easier to just define patterns of models and maximum values to make restricting item content easier.
