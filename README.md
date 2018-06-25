# DjangoDocker
A template project for creating a Django project with Docker Compose, uWSGI, Nginx, and SQLite

1. Create a new project in `deployment/app` - `django-admin <project_name> startproject deployment/app`
1. Replace the `<project_name>` in the following file:
    - `[base] module=<project_name>.wsgi` in _uswigi.ini
1. `docker build -t <your_container_name> .`
1. `docker-compose up`

By default; the app runs on port `5555`
