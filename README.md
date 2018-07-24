# DjangoDocker

A template project for creating a Django project with Docker Compose, uWSGI, Nginx, and SQLite.

## Starting a Project and Application

1. Create a virtual environment, `python3 -m venv env`
1. Install the dependencies:
 1. `source env/bin/activate` will enable the new Python environment
 1. `pip install --upgrade pip`
 1. `pip install -r path/to/requirements.txt`
1. A default project is included, _djangoproject_, but a new project can be application can be created in `deployment/app` with the  `django-admin startproject <project_name> `
 - Changing the `deployment` folder will create issues because the Docker Compose file mounts/syncs `deployment` folder
1. Replace the `<project_name>` in the following file:
    - `[base] module=<project_name>.wsgi` in _uswigi.ini
1. `docker-compose up -f docker-compose-dev.yml --build -d` will run the environment and deployment for a "development" environment

By default; the app runs on port `5555`

### Create Applications

1. Creating the applications should be performed via the hosts environment with a virtual environment, otherwise permissions can be fickle
1. In `/deployment/app`, create a new application, `python manage.py startapp <application name>`


## SSH

1. SSH into the docker container, `docker exec -it <mycontainer> bash`


## Volumes

The `app` folder is mounted in the `docker-compose` file, creating Django applications in the `app` folder will reflect in the host codebase and bash shell of the container.
A database called `db.sqlite3` is also mounted to maintain persistence between teardowns


## Django Media

In `nginx-app.conf`, the following media and static servings,
```
    # Django media
    location /media  {
        alias /code/app/data/media;  # your Django project's media files - amend as required
    }

    location /static {
        alias /code/app/data/static; # your Django project's static files - amend as required
    }
```
must be in alignment with the `settings.py` of Django

```
MEDIA_ROOT = os.path.join(BASE_DIR, 'data', 'images')
# 'data' is a mounted dir
STATIC_ROOT = os.path.join(BASE_DIR, 'data', 'static')

# Refers to url construction
STATIC_URL = '/static/'
```