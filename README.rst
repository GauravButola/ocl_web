ocl_web
==============================

Client interface for Open Concept Lab terminology services API.


# Developer Setup

The OCL web server requires a few environment variables to operate. The easiest
way to do this during development is to put the `export` calls in your `virtualenv`
__postactivate__ script, found in the `bin` directory under the specific
ocl_web virtualenv directory.

```
export OCL_API_HOST='<your_api_server_ip>''
export OCL_API_TOKEN='<token for accessing API as admin>''
export OCL_ANON_API_TOKEN='<token for anon access>'

# for deployment
export OCL_WEB_HOST='<web_host_ip>'
export FAB_USER='deploy'
export FAB_PASSWORD=''

export DATABASE_URL=sqlite:////$HOME/webapps/ocl_web/src/ocl.db
```

Settings
------------

cookiecutter-django relies extensively on environment settings which **will not work with Apache/mod_wsgi setups**. It has been deployed successfully with both Gunicorn/Nginx and even uWSGI/Nginx.

For configuration purposes, the following table maps the cookiecutter-django environment variables to their Django setting:

======================================= =========================== ============================================== ===========================================
Environment Variable                    Django Setting              Development Default                            Production Default
======================================= =========================== ============================================== ===========================================
DJANGO_AWS_ACCESS_KEY_ID                AWS_ACCESS_KEY_ID           n/a                                            raises error
DJANGO_AWS_SECRET_ACCESS_KEY            AWS_SECRET_ACCESS_KEY       n/a                                            raises error
DJANGO_AWS_STORAGE_BUCKET_NAME          AWS_STORAGE_BUCKET_NAME     n/a                                            raises error
DJANGO_CACHES                           CACHES                      locmem                                         memcached
DJANGO_DATABASES                        DATABASES                   See code                                       See code
DJANGO_DEBUG                            DEBUG                       True                                           False
DJANGO_EMAIL_BACKEND                    EMAIL_BACKEND               django.core.mail.backends.console.EmailBackend django.core.mail.backends.smtp.EmailBackend
DJANGO_SECRET_KEY                       SECRET_KEY                  CHANGEME!!!                                    raises error
DJANGO_SECURE_BROWSER_XSS_FILTER        SECURE_BROWSER_XSS_FILTER   n/a                                            True
DJANGO_SECURE_SSL_REDIRECT              SECURE_SSL_REDIRECT         n/a                                            True
DJANGO_SECURE_CONTENT_TYPE_NOSNIFF      SECURE_CONTENT_TYPE_NOSNIFF n/a                                            True
DJANGO_SECURE_FRAME_DENY                SECURE_FRAME_DENY           n/a                                            True
DJANGO_SECURE_HSTS_INCLUDE_SUBDOMAINS   HSTS_INCLUDE_SUBDOMAINS     n/a                                            True
DJANGO_SESSION_COOKIE_HTTPONLY          SESSION_COOKIE_HTTPONLY     n/a                                            True
DJANGO_SESSION_COOKIE_SECURE            SESSION_COOKIE_SECURE       n/a                                            False
======================================= =========================== ============================================== ===========================================

* TODO: Add vendor-added settings in another table

Developer Installation
-----------------------

For getting this running on your local machine:

1. Set up a virtualenv.
2. Install all the supporting libraries into your virtualenv::

    pip install -r requirements/local.txt

3. Install Grunt Dependencies.

    npm install

4. Run development server. (For browser auto-reload, use Livereload_ plugins.)

    grunt serve

.. _livereload: https://github.com/gruntjs/grunt-contrib-watch#using-live-reload-with-the-browser-extension



---------------------------------------------------------------------
Copyright (C) 2016 Open Concept Lab. Use of this software is subject
to the terms of the Mozille Public License v2.0. Open Concept Lab is
also distributed under the terms the Healthcare Disclaimer
described at http://www.openconceptlab.com/license/.
---------------------------------------------------------------------
