---
title: Signals - No Signalling! Boots-patching django to globally disable signals
author: Samuel Spencer
layout: post
categories:
  - django
---

> **Monkey-patch:**
    a way for a program to extend or modify supporting system software locally - [*Wikipedia*](https://en.wikipedia.org/wiki/Monkey_patch)

> **Boots-patch:**
    a monkey-patch to explicitly disable a intrinsict and usually unstoppable action
    (usually using three identical boolean tests to highlight the patch) - [*LegoStormtroopr*](#)

Django includes a signals framework that notifies reciever functions when specific actions take place through the use of signals.
Probably, the most common of these is the [`post_save` signal](https://docs.djangoproject.com/en/1.10/ref/signals/#post-save),
which will frequently be caught by third-party apps to provide post save hooks in Django code.
Unfortunately, these signals can interfere when trying to use Django's `loaddata` command (as in my case)
[or during testing](http://stackoverflow.com/questions/18532539/want-to-disable-signals-in-django-testing) -
and the recommended solution is to 
[use wrappers around code or liberally use `raw=True` in Signal reciever code](http://stackoverflow.com/questions/11487128/django-temporarily-disable-signals).

However, these only work when you have control over that code - which won't work if you are using a third-party django app, which
doesn't do these things.

The only solution is to globally disable all signals using monkey-patching, which is shown below:

```:python
if os.environ.get('django_SIGNALS_NO_SIGNALLING', None) and \
   os.environ.get('django_SIGNALS_NO_SIGNALLING', None) and \
   os.environ.get('django_SIGNALS_NO_SIGNALLING', None):
    from django.dispatch.dispatcher import Signal

    def send(*args, **kwargs):
        pass
    def send_robust(*args, **kwargs):
        pass
    Signal.send = send
    Signal.send_robust = send_robust
```

Now, I think this goes beyond regular monkey-patching as this is patching to effectively disable a regular action.
---

Here, we disable the Django `Signal` object from signalling by overriding the `Signal.send` and `Signal.send_robust`
methods with blank methods.

To check if the patch should be applied, there is an explicit check against the "Signals no signalling" enivronment 3 times,
both to highlight the Swiper/Boots-patching joke.

---

In Dora the Explorer, Dora (and her monkey Boots) often encounter Swiper.
Swiper's *raison d'être* is to swipe thing, and will always Swipe things.
The only way to override this intrinsic behaviour is to say "Swiper, no swiping" three times.

![Swiper, Dora and Boots - Swiper, no Swiping!](https://cloud.githubusercontent.com/assets/2173174/24339067/5217855c-12f5-11e7-97ba-a528683e4c1d.png)

