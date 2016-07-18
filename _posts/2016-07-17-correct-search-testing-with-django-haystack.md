---
title: Correct search engine testing with Django and Haystack
author: Samuel Spencer
layout: post
categories:
  - Python
  - Continuous Integration
  - Django
  - Gotcha
  - Blogging on the bus
---

[Haystack](http://haystacksearch.org) is an awesome library for [Django](http://djangoproject.com) that
provides a great, hassle-free way of interfacing with search engine. And like any module, when you integrate
and customise it as much has been done for the [Aristotle Metadata Registry](http://www.aristotlemetadata.com)
you want to make sure you test it right.

But there is a big gotcha, sometimes your tests will fail with Haystack when your code looks right and behaves
properly when a test is run in isolation, and its to do with how the search indexing works.

In a Django test, each test is wrapped in a transaction, so after each test the changes are rolled back so
the database is in a "cleaner" state, but the search index *is not*! 

If you are doing tests on the same item thats setup in a `setUp` method, you want to wipe the index during
``tearDown`` to make sure everything is clean again.

```
from django.core.management import call_command
from my_app.models import SomeIndexedModel

class SomeSearchTest(TestCase):
    def setUp(self):
        super(SomeSearchTest, self).setUp()
        self.visible_item = SomeIndexedModel.objects.create(foo='foo')
        self.hidden_item = SomeIndexedModel.objects.create(foo='bar')

    def tearDown(self):
        call_command('clear_index', interactive=False, verbosity=0)

    def test_foo_can_be_found(self):
        pass

    def test_bar_cannot_be_found(self):
        pass
```

Now your code is safe to run, regardless of the order tests are run in.

Forewarning, I did say Django tests leave things "cleaner" because
depending on the database engine ids in auto-incremented may or may not be undone.

On a similar note, Django caches objects so when testing views that manipulate the
database this might fail:

```
my_foo = SomeIndexedModel.objects.create(foo='foo')

self.client.get("/set_foo_to_bar/%s"%my_foo.pk)  # Assume my_foo.foo is set to 'bar' here
self.assertTrue(my_foo.foo == 'bar')             # This will fail because my_foo is still cached
```

To get around this, "decache" the object from the database after the view to test it:



```
my_foo = SomeIndexedModel.objects.create(foo='foo')

self.client.get("/set_foo_to_bar/%s"%my_foo.pk)  # Assume my_foo.foo is set to 'bar' here
my_foo = SomeIndexedModel.objects.get(pk=foo.pk) # De-cache the object
self.assertTrue(my_foo.foo == 'bar')             # Everything is awesome!
```
