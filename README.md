# DjangoDocker
A template project for creating a Django project with Docker Compose, uWSGI, Nginx, and SQLite

1. Create a new project in `deployment/app` - `django-admin <project_name> startproject deployment/app`
1. Replace the `<project_name>` in the following file:
    - `[base] module=<project_name>.wsgi` in _uswigi.ini
1. `docker build -t <your_container_name> .`
1. `docker-compose up`
1. SSH into the docker container, `docker exec -it <mycontainer> bash`
1. `python3 manage.py startapp thoughts`

By default; the app runs on port `5555`
The `app` folder is mounted in the `docker-compose` file, creating Django applications in the `app` folder with the docker container's bash shell will reflect in your host codebase.
A database called `db.sqlite3` is also mounted to maintain persistence between teardowns
