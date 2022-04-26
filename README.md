[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# Intro to Django

So far we've learened how to make the back-end for web applications two different ways: in Express with Node in JavaScript, and then with Flask in Python. Both are relatively lightweight and require other libraries in order to have even basic functionality (such as Mongoose or PeeWee). Django is philosophically different in that it strives to be a full-featured *framework*, so it will include significantly more features and have much stronger "opinions" on how its code should be written. Neither philosophical approach (lightweight vs. full-featured) is intrinsically better than the other as both have advantages and disadvantages. You may find yourself prefering one way over the other.

Let's learn the core features of Django and how to build web apps "the Django
way."

## Objectives

By the end of this, you should be able to:

* Discuss the core features of Django
* Create a Django application
* Use `manage.py` to create, edit, update and seed a Postgres database

## What is Django?

Created in 2003 by Adrian Holovaty and Simon Willison, developers at the Lawrence Journal World Newspaper, Django was born out of frustrations the developers had working with PHP. Working for the publication, applications often had to be created very quickly, sometimes within a few hours, and Holovaty and Willison needed a tool to accomplish just that, while keeping the development process clean and maintainable. They wanted to move from PHP to building with Python, but none of the tools and technologies that were around at the time came with the features they wanted - things like CSS, well designed URLs, the way the request/response cycle would work, and deployment. 

Although the initial intention may not have been to create a new web framework, Django proved itself to be an extremely useful and dynamic tool, and the World Company (who owned the newspaper) agreed to open source it. And the rest is history!

Instagram is the largest Django application out there right now. When it was sold to Facebook, they had a total of 13 employees working on the app. Today, they have hundreds!


## Setting Up a Django Project

We're going to make a Django project called `nyc_subway` that will keep track of subway stations and lines!
We'll start by creating our project folder: `mkdir nyc_subway`. 


### Set Up & Manage Virtual Environment

We'll be using [virtualenvwrapper](https://virtualenvwrapper.readthedocs.io/en/latest/) to manage our virtual environments. 

Create the virutal environment with `mkvirtualenv nyc_subway`.

We'll automatically enter the virtual envirnoment when we create it. Exit the environemnt with the `deactivate` command and re-enter with `workon nyc_subway`. 

Running just the `workon` command will list all of our available environments and `rmvirtualenv environment_name` to delete one.


### Install Django
To install Django we'll run `pip install django`.

In order to manage our dependencies, we can run run `pip freeze > requirements.txt`. The `pip freeze` command on its own will show what dependencies are installed (in this case, for our virtual environment). 

If someone wants to install the project's dependencies on another computer, they would create a virtual environemnt and run `pip install -r requirements.txt`.


### Using `django-admin` to create our Django Project

Django includes a `django-admin` command that we can use to quickly start a project template.

Run the command (including the `.` at the end): `django-admin startproject nyc_subway . `. Your directory should look like this:
```
.
├── nyc_subway
│   ├── asgi.py
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── manage.py
└── requirements.txt
```

It should *not* look like this:
```
.
├── nyc_subway
│   ├── nyc_subway
│   │   ├── asgi.py
│   │   ├── __init__.py
│   │   ├── settings.py
│   │   ├── urls.py
│   │   └── wsgi.py
│   └── manage.py
└── requirements.txt
```

If it looks like the second example, you ran the command wrong. Make sure you ran `django-admin startproject nyc_subway . ` with the `.` at the end. Delete the directory and start over. Also make sure you've run the `pip freeze > requirements.txt` command after!


#### Start the Server

Our Django project has create a file called `manage.py`! The `manage.py` script contains a lot of management commands for Django. You can see a list of the commands `manage.py` offers by typing `python manage.py`.

We can run `python manage.py runserver` to start the server. We can run this right now to check that our project runs without errors. For now it will load a nice homepage and not do much else.


### Setting Up Postgresql

By default Django uses SQLite. We'll be using Postgresql instead. Make sure that our database is up and running with `brew services list`, then run the following SQL script:


```sql
-- Create the database
CREATE DATABASE nyc_subway;

-- Create an admin user for our app to use
CREATE USER nyc_subway_admin WITH PASSWORD 'password';

-- Give that user permissins to manage the database:
GRANT ALL PRIVILEGES ON DATABASE nyc_subway TO nyc_subway_admin;
```

Next, install our Postgres adaptor: `pip install psycopg2-binary`.

Update our project requirements with `pip freeze > requirements.txt`.

Finally, we will edit our `nyc_subway/stettings.py` to include the database configuration:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'nyc_subway',
        'USER': 'nyc_subway_admin',
        'PASSWORD': 'password',
        'HOST': 'localhost'
    }
}
```

Run the `python manage.py runserver` command to make sure it connects to our database without errors. 


### Using `django-admin` to create our Djang App

A Django *project* is composed of many *apps*. Our `nyc_subway` project directory is the base of the Django project where we'll handle our base routes, project-level configurations and include our apps. We'll make a `subway` app where we will write our models.

Create the app with `django-admin startapp subway`. (Note there's no `.` at the end this time). 

Then, update `nyc_subway/settings.py` to include `'subway'` in the list of `INSTALLED_APPS`:
```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'subway'
]
```

Directory:
```
.
├── nyc_subway
│   ├── asgi.py
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── subway
│   ├── migrations
│   │   └── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── __init__.py
│   ├── models.py
│   ├── tests.py
│   └── views.py
├── manage.py
└── requirements.txt
```


### Running a Migration

Django automatically comes with users. But, we need our database to have a `user` table, etc. In order to "update" our database we'll run a *migration*.

Create & run migrations:
```
python manage.py makemigrations
python manage.py migrate
```

See how the `nyc_subway` database has changed with `psql`. What has been added?

Whenever we make changes to our Django application that will require changes to the database (such as new tables or column changes) we will need to create and run a migration.


### Creating Our First Model

First, let's plan our models using an UML diagram.

https://yuml.me/diagram/scruffy/class/draw

We'll have three models:
 - Subway Trains
 - Subway Lines
 - Subway Stations

What are the relationships between the trains, lines and stations?

Our train models will have the following fields:
  - Model
  - Car Count
  - Line

Our line models will have the following:
  - Name
  - Color
  - Stations

Our stations will have the following:
  - Name
  - Lines

```python
# subway/models.py

class Train(models.Model):
  name = models.CharField(max_length=5)
  cbtc_enabled = models.BooleanField()
  line = models.ForeignKey(Line, on_delete=models.CASCADE, related_name='trains')

  def __str__(self):
    return self.name


class Line(models.Model):
  name = models.CharField(max_length=4)
  hex_color = models.CharField(max_length=6)
  stations = models.ManyToManyField(Station)

  def __str__(self):
    return self.name


class Station(models.Model):
  name = models.CharField(max_length=120)

  def __str__(self):
    return self.name
```

## Then..

create super user

python manage.py createsuperuser


Create admin panel
