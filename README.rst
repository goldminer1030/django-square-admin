Responsive Django Admin
=======================


Features
--------

* Responsive
* Sidebar Menu
* Easy install / setup
* Python 3


INSTALL
-------

from pypi (recommended) ::

    $ pip install bootstrap-admin

And don't forget to add **square\_admin** in ``INSTALLED_APPS`` before
the ``django.contrib.admin``.

Example:

.. code-block:: python

    INSTALLED_APPS = (
        # ...
        'square_admin', # always before django.contrib.admin
        'django.contrib.admin',
        # ...
    )  

CUSTOMIZE
---------

Branding - Overriding logo
^^^^^^^^^^^^^^^^^^^^^^^^^^

If you want to use your own logo, you can achieve this by overriding the **login.html** and **base_site.html**, just like in Django Admin.

First, make sure the ``TEMPLATES`` setting in your settings.py is properly configured:

.. code-block:: python

    TEMPLATES = [
        {
            'BACKEND': 'django.template.backends.django.DjangoTemplates',
            'DIRS': [os.path.join(BASE_DIR, 'my_django_project/templates')],
            'APP_DIRS': True,
            # other stuff
        },
    ]

`DIRS`: You must set the location of your templates, an absolute path.

I'm assuming ``BASE_DIR`` is:

.. code-block:: python

    BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))

This pattern of creating a global templates folder could be useful for you to use for your **base.html** and other global templates.

More info: https://docs.djangoproject.com/en/2.1/ref/templates/api/#configuring-an-engine

Let me show you a project structure as an example:

.. code-block:: 

    ├── my_django_project
    │   ├── core
    │   │   ├── admin.py
    │   │   ├── apps.py
    │   │   ├── models.py
    │   │   ├── tests.py
    │   │   └── views.py
    │   ├── settings.py
    │   ├── templates
    │   │   └── admin
    │   │       ├── base_site.html
    │   │       └── login.html
    │   ├── urls.py
    │   └── wsgi.py
    ├── manage.py

You can see I created a global **templates/** folder, 
with another directory inside **admin/** containing **login.html** and **base_site.html**.

Their respective contents are:

**base_site.html**

.. code-block:: html

    {% extends 'admin/base_site.html' %}
    {% load static %}

    {% block branding %}
        <a href="{% url 'admin:index' %}" class="django-admin-logo">
            <!-- Django Administration -->
            <img height="60" src="{% static "square_admin/img/logo-140x60.png" %}" alt="{{ site_header|default:_('Django administration') }}">
        </a>
    {% endblock branding %}


**login.html**

.. code-block:: html

    {% extends 'admin/login.html' %}
    {% load i18n static %}

    {% block branding %}
        <a href="{% url 'admin:index' %}" class="django-admin-logo">
            <!-- Django Administration -->
            <img height="60" src="{% static "square_admin/img/logo-140x60.png" %}" alt="{{ site_header|default:_('Django administration') }}">
        </a>
    {% endblock branding %}

More info: https://docs.djangoproject.com/en/2.1/ref/contrib/admin/#admin-overriding-templates


