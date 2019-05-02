# HottestHouse.com

A better way to get started in real estate investing.

### Basic Usage
1. First run `make build` inside root directory.
2. Then run `make up` to start up the project for first time.

Checkout the [commands](#commands) section for more usage.

1. `make up` to build the project and starting containers.
2. `make build` to build the project.
3. `make start` to start containers if project has been up already.
4. `make stop` to stop containers.
5. `make shell-web` to shell access web container.
6. `make shell-db` to shell access db container.
7. `make shell-nginx` to shell access nginx container.
8. `make logs-web` to log access web container.
9. `make logs-db` to log access db container.
10. `make logs-nginx` to log access nginx container.
11. `make collectstatic` to put static files in static directory.
12. `make log-web` to log access web container.
13. `make log-db` to log access db container.
14. `make log-nginx` to log access nginx container.
14. `make restart` to restart containers.


## The Stack
HottestHouse.com uses a docker container based architecture.

![Benchmark Img](https://github.com/benscanlan/httpssl/blob/master/documentation%20/Hottest-House-Stack.png?raw=true)

* Container Communication Sockets:
  * Port 80 <-> UWSGI <-> SQL

New stack is nginx reverse proxy, django to handle session security, and postgresql with redis cache and celery message queing.

## Socket Architecture

    docker ps #host port maps to -> docker vm port
or    
    
    docker container ls
yields

    CONTAINER ID        IMAGE                      COMMAND                  CREATED             STATUS              PORTS                          NAMES
    e33a758f1483        nginx:latest               "nginx -g 'daemon of…"   About an hour ago   Up About an hour    80/tcp, 0.0.0.0:80->8000/tcp   nz01
    f6222bb6e542        docker-django-master_web   "/bin/sh -c 'python …"   2 hours ago         Up About an hour    8000/tcp                       dz01
    51e737db502b        redis:latest               "docker-entrypoint.s…"   3 hours ago         Up About an hour    0.0.0.0:6379->6379/tcp         rz01
    415be0e1155e        postgres:latest            "docker-entrypoint.s…"   3 hours ago         Up About an hour    5432/tcp                       pz01

## Docker Containers

## Application Features

* Chat about a house
* Customer Q&A Public Submission page (with alert emails when answered)

## File Tree

    Bens-MacBook-Pro:docker-django benscanlan$ tree
    .
    ├── Dockerfile
    ├── Makefile
    ├── config
    │   └── nginx
    │       └── mydjango.conf
    ├── docker-compose.yml
    ├── docs
    ├── readme.md
    └── src
        ├── manage.py
        ├── myapp
        │   ├── __init__.py
        │   ├── __pycache__
        │   │   ├── __init__.cpython-37.pyc
        │   │   ├── admin.cpython-37.pyc
        │   │   ├── apps.cpython-37.pyc
        │   │   ├── models.cpython-37.pyc
        │   │   ├── tasks.cpython-37.pyc
        │   │   └── views.cpython-37.pyc
        │   ├── admin.py
        │   ├── apps.py
        │   ├── migrations
        │   │   ├── __init__.py
        │   │   └── __pycache__
        │   │       └── __init__.cpython-37.pyc
        │   ├── models.py
        │   ├── tasks.py
        │   ├── tests.py
        │   └── views.py
        ├── mydjango
        │   ├── __init__.py
        │   ├── __pycache__
        │   │   ├── __init__.cpython-37.pyc
        │   │   ├── celery.cpython-37.pyc
        │   │   ├── settings.cpython-37.pyc
        │   │   ├── urls.cpython-37.pyc
        │   │   └── wsgi.cpython-37.pyc
        │   ├── celery.py
        │   ├── settings.py
        │   ├── urls.py
        │   └── wsgi.py
        ├── requirements.pip
        ├── static
        │   └── admin
        │       ├── css
        │       │   ├── autocomplete.css
        │       │   ├── base.css
        │       │   ├── changelists.css
        │       │   ├── dashboard.css
        │       │   ├── fonts.css
        │       │   ├── forms.css
        │       │   ├── login.css
        │       │   ├── responsive.css
        │       │   ├── responsive_rtl.css
        │       │   ├── rtl.css
        │       │   ├── vendor
        │       │   │   └── select2
        │       │   │       ├── LICENSE-SELECT2.md
        │       │   │       ├── select2.css
        │       │   │       └── select2.min.css
        │       │   └── widgets.css
        │       ├── fonts
        │       │   ├── LICENSE.txt
        │       │   ├── README.txt
        │       │   ├── Roboto-Bold-webfont.woff
        │       │   ├── Roboto-Light-webfont.woff
        │       │   └── Roboto-Regular-webfont.woff
        │       ├── img
        │       │   ├── LICENSE
        │       │   ├── README.txt
        │       │   ├── calendar-icons.svg
        │       │   ├── gis
        │       │   │   ├── move_vertex_off.svg
        │       │   │   └── move_vertex_on.svg
        │       │   ├── icon-addlink.svg
        │       │   ├── icon-alert.svg
        │       │   ├── icon-calendar.svg
        │       │   ├── icon-changelink.svg
        │       │   ├── icon-clock.svg
        │       │   ├── icon-deletelink.svg
        │       │   ├── icon-no.svg
        │       │   ├── icon-unknown-alt.svg
        │       │   ├── icon-unknown.svg
        │       │   ├── icon-viewlink.svg
        │       │   ├── icon-yes.svg
        │       │   ├── inline-delete.svg
        │       │   ├── search.svg
        │       │   ├── selector-icons.svg
        │       │   ├── sorting-icons.svg
        │       │   ├── tooltag-add.svg
        │       │   └── tooltag-arrowright.svg
        │       └── js
        │           ├── SelectBox.js
        │           ├── SelectFilter2.js
        │           ├── actions.js
        │           ├── actions.min.js
        │           ├── admin
        │           │   ├── DateTimeShortcuts.js
        │           │   └── RelatedObjectLookups.js
        │           ├── autocomplete.js
        │           ├── calendar.js
        │           ├── cancel.js
        │           ├── change_form.js
        │           ├── collapse.js
        │           ├── collapse.min.js
        │           ├── core.js
        │           ├── inlines.js
        │           ├── inlines.min.js
        │           ├── jquery.init.js
        │           ├── popup_response.js
        │           ├── prepopulate.js
        │           ├── prepopulate.min.js
        │           ├── prepopulate_init.js
        │           ├── timeparse.js
        │           ├── urlify.js
        │           └── vendor
        │               ├── jquery
        │               │   ├── LICENSE.txt
        │               │   ├── jquery.js
        │               │   └── jquery.min.js
        │               ├── select2
        │               │   ├── LICENSE.md
        │               │   ├── i18n
        │               │   │   ├── ar.js
        │               │   │   ├── az.js
        │               │   │   ├── bg.js
        │               │   │   ├── ca.js
        │               │   │   ├── cs.js
        │               │   │   ├── da.js
        │               │   │   ├── de.js
        │               │   │   ├── el.js
        │               │   │   ├── en.js
        │               │   │   ├── es.js
        │               │   │   ├── et.js
        │               │   │   ├── eu.js
        │               │   │   ├── fa.js
        │               │   │   ├── fi.js
        │               │   │   ├── fr.js
        │               │   │   ├── gl.js
        │               │   │   ├── he.js
        │               │   │   ├── hi.js
        │               │   │   ├── hr.js
        │               │   │   ├── hu.js
        │               │   │   ├── id.js
        │               │   │   ├── is.js
        │               │   │   ├── it.js
        │               │   │   ├── ja.js
        │               │   │   ├── km.js
        │               │   │   ├── ko.js
        │               │   │   ├── lt.js
        │               │   │   ├── lv.js
        │               │   │   ├── mk.js
        │               │   │   ├── ms.js
        │               │   │   ├── nb.js
        │               │   │   ├── nl.js
        │               │   │   ├── pl.js
        │               │   │   ├── pt-BR.js
        │               │   │   ├── pt.js
        │               │   │   ├── ro.js
        │               │   │   ├── ru.js
        │               │   │   ├── sk.js
        │               │   │   ├── sr-Cyrl.js
        │               │   │   ├── sr.js
        │               │   │   ├── sv.js
        │               │   │   ├── th.js
        │               │   │   ├── tr.js
        │               │   │   ├── uk.js
        │               │   │   ├── vi.js
        │               │   │   ├── zh-CN.js
        │               │   │   └── zh-TW.js
        │               │   ├── select2.full.js
        │               │   └── select2.full.min.js
        │               └── xregexp
        │                   ├── LICENSE.txt
        │                   ├── xregexp.js
        │                   └── xregexp.min.js
        └── templates
            └── hello_world.html

    26 directories, 152 files
