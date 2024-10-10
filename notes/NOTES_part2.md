# Django Notes

https://docs.djangoproject.com/en/4.1/intro/tutorial02/

## Database Setup

_Set `TIME_ZONE = "America/Chicago"`_

By default, the configuration uses SQLite. If you’re new to databases, or you’re just interested in trying Django, this is the easiest choice. SQLite is included in Python, so you won’t need to install anything else to support your database.
When starting your first real project, however, you may want to use a more scalable database like PostgreSQL, to avoid database-switching headaches down the road.

Also, note the **INSTALLED_APPS** setting at the top of the file. That holds the names of all Django applications that are activated in this Django instance. Apps can be used in multiple projects, and you can package and distribute them for use by others in their projects.

By default, **INSTALLED_APPS** contains the following apps, all of which come with Django:

- `django.contrib.admin` – The admin site. You’ll use it shortly.
- `django.contrib.auth` – An authentication system.
- `django.contrib.contenttypes` – A framework for content types.
- `django.contrib.sessions` – A session framework.
- `django.contrib.messages` – A messaging framework.
- `django.contrib.staticfiles` – A framework for managing static files.

The migrate command looks at the **INSTALLED_APPS** setting and creates any necessary database tables according to the database settings in
your **mysite/settings.py** file and the database migrations shipped with the app (we’ll cover those later).
You’ll see a message for each migration it applies.

## Models

Now we’ll define your models – essentially, your database layout, with additional metadata.

A model is the single, definitive source of information about your data.
It contains the essential fields and behaviors of the data you’re storing.
Django follows the DRY Principle. The goal is to define your data model in one place and automatically derive things from it.

Here, each model is represented by a class that subclasses django.db.models.Model.
Each model has a number of class variables, each of which represents a database field in the model.

Each field is represented by an instance of a Field class – e.g., CharField for character fields and DateTimeField for datetimes.
This tells Django what type of data each field holds.

The name of each Field instance (e.g. question_text or pub_date) is the field’s name, in machine-friendly format.
You’ll use this value in your Python code, and your database will use it as the column name.

### Activating Models

That small bit of model code gives Django a lot of information. With it, Django is able to:

    Create a database schema (CREATE TABLE statements) for this app.
    Create a Python database-access API for accessing Question and Choice objects.

But first we need to tell our project that the polls app is installed.

To include the app in our project, we need to add a reference to its configuration class in the `INSTALLED_APPS` setting.
The PollsConfig class is in the polls/apps.py file, so its dotted path is 'polls.apps.PollsConfig'.
Edit the mysite/settings.py file and add that dotted path to the `INSTALLED_APPS` setting.

There’s a command that will run the migrations for you and manage your database schema automatically - that’s called migrate, and we’ll come to it in a moment - but first,
let’s see what SQL that migration would run. The sqlmigrate command takes migration names and returns their SQL:

```bash
python manage.py sqlmigrate polls 0001
```

If you’re interested, you can also run python manage.py check; this checks for any problems in your project without making migrations or touching the database.

Now, run migrate again to create those model tables in your database:

```bash
python manage.py migrate
```

The migrate command takes all the migrations that haven’t been applied (Django tracks which ones are applied using a special table in your database
called django_migrations) and runs them against your database - essentially, synchronizing the changes you made to your models with the schema in the database.

### Playing with the API

```bash
python manage.py shell
```

It’s important to add **str**() methods to your models, not only for your own convenience when dealing with the interactive prompt,
but also because objects’ representations are used throughout Django’s automatically-generated admin.

## Django Admin

### Creating an admin user

First we’ll need to create a user who can login to the admin site. Run the following command:

```bash
$ python manage.py createsuperuser
```

Enter your desired username and press enter.

```bash
Username: admin
```

You will then be prompted for your desired email address:

```bash
Email address: admin@example.com
```

The final step is to enter your password. You will be asked to enter your password twice, the second time as a confirmation of the first.

```bash
Password: **********
Password (again): *********
Superuser created successfully.
```

### Start the development server

```bash
$ python manage.py runserver
```
