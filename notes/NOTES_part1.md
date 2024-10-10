# Django Notes

https://docs.djangoproject.com/en/4.1/intro/tutorial01/

## Creating a Project
To start a project. Go in terminal and do

`django-admin startproject <project name>`


Let’s look at what startproject created:

mysite/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        asgi.py
        wsgi.py

These files are:

* `manage.py`: A command-line utility that let's you interact with Django project. 
* inner `mysite/` directory is the actual Python package for your project. 
* `settings.py`: Settings/configuration for this Django project. 
* `urls.py`: URL declarations for this Django project; a "table of content"
* `asgi.py`: An entry-point for ASGI-compatible web servers 
* `wsgi.py`: An entry-point for WSGI-compatible web servers 

## Development server 

To run the server you can do `python <project name>/manage.py runserver <ip address>:<port number>`

## Application 

Now that we have a project setup, we're ready to build apps. 

Each application you write in Django consists of a Python package that follows a certain convention. Django comes with a utility that automatically generates the basic directory structure of an app, so you can focus on writing code rather than creating directories.


To create your app, make sure you’re in the same directory as manage.py and type this command:

`python manage.py startapp polls`

That’ll create a directory polls, which is laid out like this:

polls/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py


The include() function allows referencing other URLconfs. Whenever Django encounters include(), it chops off whatever part of the URL matched up to that point and sends the remaining string to the included URLconf for further processing.

The idea behind include() is to make it easy to plug-and-play URLs. Since polls are in their own URLconf (polls/urls.py), they can be placed under “/polls/”, or under “/fun_polls/”, or under “/content/polls/”, or any other path root, and the app will still work.

When to use include()

You should always use include() when you include other URL patterns. admin.site.urls is the only exception to this.

You have now wired an **index** view into the URLconf. Verify it's working with following command: 

`python manage.py runserver`

Go to http://localhost:8000/polls/ in your browser, and you should see the text “Hello, world. You’re at the polls index.”, which you defined in the index view.
