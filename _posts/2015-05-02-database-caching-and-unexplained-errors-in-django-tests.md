---
id: 6094
title: Database caching and unexplained errors in Django tests
date: 2015-05-02T02:04:06+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=6094
permalink: /2015/05/database-caching-and-unexplained-errors-in-django-tests/
categories:
  - Django
  - Drivel
  - Python
  - Web Development
tags:
  - aristotle-mdr
  - django
  - its always caching
  - python
---
Unit testing is a grand idea, and Django offers an extraordinary capability to test code to an extraordinary degree. But no-one ever wrote a blog post to talk about how great things are&#8230;

This is a post about the worst kind of test failure. The intermittent ones, that are hard to replicate as they sometimes show up and sometimes don&#8217;t.

Below is a test on an jango item we&#8217;ve just retrieved from the database:

<pre>class TestFoo:
    def test_foo(self):
        foo = models.Foo.objects.create(bar=1) # create an item
        call_some_method_that_sets_bar(foo,bar = 2)
        self.assertTrue(foo.bar == 2)</pre>

<pre>def call_some_method_that_sets_bar(foo_obj,bar):
    f = models.Foo.objects.get(pk=foo_obj.pk)
    f.bar = bar
    f.save()</pre>

Everything here seems ok, and seems like it should work. But it might not, for unclear reasons. On line 3 an item is made and saved in the database, and then instantiated as a python object. On line 4, we change a field in the database that sets the value of bar to 2 and then we check that on line 5.

Again it seems correct, but, despite representing the same row in the database, the python object f in
  
<tt>call_some_method_that_sets_bar</tt> is a different python object to foo in test_foo and since we haven&#8217;t refetched foo from the database, it still has the original value for bar it was instantiated with.

The solution, if you are getting unexplained assertion failures when you are manipulating objects? Re-instantiate them, you might increase your test lengths but it means you are dealing with fresh objects:

<pre>class TestFoo:
    def test_foo(self):
        foo = models.Foo.objects.create(bar=1) # create an item
        call_some_method_that_sets_bar(foo,bar = 2)
        foo = models.Foo.objects.get(pk=foo_obj.pk)
        self.assertTrue(foo.bar == 2)</pre>

Here we use Djangos internal <tt>pk</tt> field, to refetch it, regardless of what other fields exist.