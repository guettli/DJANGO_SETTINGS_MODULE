# DJANGO_SETTINGS_MODULE
List of options to solve "django.core.exceptions.ImproperlyConfigured: Requested setting INSTALLED_APPS, but settings are not configured. You must either define the environment variable DJANGO_SETTINGS_MODULE or call settings.configure() before accessing settings."


# The stacktrace

I successfully installed django, created a project, and app called `xyz`, created my first models, runserver runs on localhost and the admin interface is working.

Now I wrote some tests and want to execute them directly from my IDE (PyCharm).

But this fails wit this stacktrace:

```
Testing started at 09:40 ...
/home/guettli/x/venv/bin/python 
   /snap/pycharm-community/179/plugins/python-ce/helpers/pycharm/_jb_pytest_runner.py 
   --path /home/guettli/x/xyz/tests.py
Launching pytest with arguments /home/guettli/x/xyz/tests.py in /home/guettli/x

============================= test session starts ==============================
platform linux -- Python 3.6.9, pytest-5.4.1, py-1.8.1, pluggy-0.13.1 --
cachedir: .pytest_cache
rootdir: /home/guettli/x
collecting ... 
xyz/tests.py:None (xyz/tests.py)
xyz/tests.py:6: in <module>
    from . import views
xyz/views.py:5: in <module>
    from xyz.models import Term, SearchLog, GlobalConfig
xyz/models.py:1: in <module>
    from django.contrib.auth.models import User
venv/lib/python3.6/site-packages/django/contrib/auth/models.py:2: in <module>
    from django.contrib.auth.base_user import AbstractBaseUser, BaseUserManager
venv/lib/python3.6/site-packages/django/contrib/auth/base_user.py:47: in <module>
    class AbstractBaseUser(models.Model):
venv/lib/python3.6/site-packages/django/db/models/base.py:107: in __new__
    app_config = apps.get_containing_app_config(module)
venv/lib/python3.6/site-packages/django/apps/registry.py:252: in get_containing_app_config
    self.check_apps_ready()
venv/lib/python3.6/site-packages/django/apps/registry.py:134: in check_apps_ready
    settings.INSTALLED_APPS
venv/lib/python3.6/site-packages/django/conf/__init__.py:76: in __getattr__
    self._setup(name)
venv/lib/python3.6/site-packages/django/conf/__init__.py:61: in _setup
    % (desc, ENVIRONMENT_VARIABLE))
E   django.core.exceptions.ImproperlyConfigured: Requested setting INSTALLED_APPS, 
    but settings are not configured. You must either define the environment variable 
    DJANGO_SETTINGS_MODULE or call settings.configure() before accessing settings.

Assertion failed
collected 0 items / 1 error

```

The error starts in my python file `xyz/tests.py`. This file is part of my app called `xyz`.

In the context of Django an [app](https://docs.djangoproject.com/en/3.0/ref/applications/) is like a library. 
It should be reusable. With other words, it should be independant from your particular environment. 

Why does `manage.py ...` work, but above fails?

Let's look at the directory structure:

```
manage.py
mysite/settings.py
xyz/test.py
```
"mysite" is the project. It contains the configuration in the file settings.py

But "xyz" is the app (aka library) which does not contain any settings. It is the job of the 
project to have settings.

# Solution 1: set environment variable in test.py

I could modify the file `xyz/test.py` and add this at the top:

```python
import os
os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'mysite.settings')
import django
django.setup()
```

Now it works.

Problem solved?

Not really. As soon, as I want to have several files for testing my app, I would need to copy+paste
these lines again and again. I would like to avoid this.

# Guideline: Sane defaults

I like sane defaults. 

If there is no sane default, then I am unsure what to do. To solve the unsureness I usualy create a list of options to 
get an overview.

Here is a list of options on how to solve this exception, which is well known in the context of the django web framework.

Solution2: .pth file
Solution3: set environment variable in PyCharm
Solution4: set environment variable in activate.sh (does not work, if you want to call the test from PyCharm)
Solution5: make test.py to a module and add above lines to `test/__init__.py`

## Related:

[Django: settings for tests of a reusable app?](https://stackoverflow.com/questions/60693395/django-settings-for-tests-of-a-reusable-app)
