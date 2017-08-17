# Example Project

![Example Project](https://s17.postimg.org/4jjj8lavj/Screen_Shot_2016_09_07_at_15_58_43.png)

Run your own OIDC provider in a second. This is a Django app with all the necessary things to work with `django-oidc-provider` package.

## Setup & Running

- [Manually](#manually)
- [Using Docker](#using-docker)

### Manually

Setup project environment with [virtualenv](https://virtualenv.pypa.io) and [pip](https://pip.pypa.io).

```bash
# For Python 2.7.
$ virtualenv project_env
# Or Python 3.
$ virtualenv -p /usr/bin/python3.4 project_env

$ source project_env/bin/activate

$ git clone https://github.com/juanifioren/django-oidc-provider.git
$ cd django-oidc-provider/example_project
$ pip install -r requirements.txt
```

Run your provider.

```bash
$ python manage.py migrate
$ python manage.py creatersakey
$ python manage.py createsuperuser
$ python manage.py runserver
```

Open your browser and go to `http://localhost:8000`. Voilà!

### Using Docker

Build and run the container.

```bash
$ docker build -t django-oidc-provider .
$ docker run --name django-oidc-provider -d -p 8000:8000 django-oidc-provider
```

If you're using Docker Toolbox (docker-machine), you'll need to set via environment variable the `SITE_URL` setting so it uses the VM's IP address.

```bash
$ docker run --name django-oidc-provider -d -p 8000:8000 -e "SITE_URL=http://`docker-machine ip`:8000" django-oidc-provider 
```

Create your super user.

```bash
$ docker exec -it django-oidc-provider python manage.py createsuperuser
```

## Install package for development

After you run `pip install -r requirements.txt`.
```bash
# Remove pypi package.
$ pip uninstall django-oidc-provider

# Go back and add the package again.
$ cd ..
$ pip install -e .
```
