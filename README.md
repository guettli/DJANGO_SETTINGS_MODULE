# DJANGO_SETTINGS_MODULE
List of options to solve "django.core.exceptions.ImproperlyConfigured: Requested setting INSTALLED_APPS, but settings are not configured. You must either define the environment variable DJANGO_SETTINGS_MODULE or call settings.configure() before accessing settings."

I like sane defaults. 

If there is no sane default, then I am unsure and create a list of options.

Here is a list of options on how to solve this exception, which is well known in the context of the django web framework.


```
Testing started at 09:40 ...
/home/guettli/x/venv/bin/python /snap/pycharm-community/179/plugins/python-ce/helpers/pycharm/_jb_pytest_runner.py 
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
