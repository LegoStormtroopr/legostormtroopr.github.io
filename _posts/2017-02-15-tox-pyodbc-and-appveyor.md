---
title: Running python tests with tox and pyodbc on appveyor
author: Samuel Spencer
layout: post
categories:
  - Django
  - Python
  - Azure
  - Appveyor
---

This is a nice short one, but will be useful for some.

If you are having trouble running [tox scripts](https://tox.readthedocs.io/en/latest/) on Appveyor
when you are using [PyODBC](https://mkleehammer.github.io/pyodbc/) you might see this error:

```
pyodbc.Error: ('IM003', '[IM003] Specified driver could not be loaded due to system error  126:
The specified module could not be found. (SQL Server, %WINDIR%\\system32\\SQLSRV32.dll).
(160) (SQLDriverConnect)')
```

Now, most of the time this is due to running a mismatched version of PyODBC that doesn't conform to the architecture you are running on.
For example, you are running Python x86 with the x64 version of PyODBC to connect to a database.

Worse still, if you Google search for this issue, the top results will *all* describe this as the exact problem,
but changing your ODBC driver won't fix this if you are running tox! Its a different problem entirely.

The problem is (and its subtle) is that PyODBC can't find the correct driver and its because tox is removing the
environment variables PyODBC needs. But, there is an easy fix by
[getting tox to pass the ``WINDIR`` variable in](http://tox.readthedocs.io/en/latest/example/basic.html?highlight=passenv#passing-down-environment-variables)
, like so:

```ini
[testenv]
passenv = 
    WINDIR
```

Or if you are like me and running these tests on appveyor, you might have an environment for that specifically:

```ini
[testenv]
passenv = 
    appveyor: WINDIR
```
