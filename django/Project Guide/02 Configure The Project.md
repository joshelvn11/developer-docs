# Configure The Project

Configuring your Django project involves setting up various components to ensure your application runs smoothly, handles data correctly, and serves static content properly. This step is crucial for tailoring the Django framework to the needs of your specific project. Let's delve into how to configure your project, focusing on the `settings.py` file, database setup, and handling static files.

## Step 1: Connect A Database

By default, Django uses SQLite. The following steps will show you how to connect to a remote PostgreSQL database.

### Step 1: Create the databse

Create a new database in your PostgreSQL server.

### Step 2: Install packages

Install the `psycopg2` and `dj-database-url` packages in your virtual environment and add them to your requirements file.

```bash
pip3 install psycopg2 dj-database-url
```

```bash
pip3 freeze > requirements.txt
```

### Step 3: Create an environment variable for the database URL

Create an env.py file in your project directory to store the database URL as an environment variable.

```bash
touch env.py
```

In the newly created env.py file, add the following line to store the database URL as an environment variable:

```python
import os

os.environ['DATABASE_URL'] = '<your-database-url>'
```

Remember to add env.py to your .gitignore file to avoid committing sensitive information to your repository.

You can then add `DATABSE_URL` as an environment variable in your deployment platform.

### Step 4: Import `env.py` into `settings.py`

In your `settings.py` file, import the `env.py` file to access the database URL environment variable.

```python
# settings.py

import os
import dj_database_url
if os.path.isfile('env.py'):
    import env
```

Then comment out the default SQLite config in `settings.py`:

```python
# settings.py

# DATABASES = {
#     'default': {
#         'ENGINE': 'django.db.backends.sqlite3',
#         'NAME': BASE_DIR / 'db.sqlite3',
#     }
# }
```

Then connect the database using the `dj_database_url` package and `DATABASE_URL` environment variable.

```python
#settings.py

DATABASES = {
    'default': dj_database_url.parse(os.environ.get("DATABASE_URL"))
}
```

### Step 5: Run migrations

Now that the databse is connected you can run the migrations to create the tables in the database.

```bash
python3 manage.py migrate
```

## Step 2: Create a Superuser

Create a superuser in the database to access the Django admin site.

```bash
python3 manage.py createsuperuser
```

You will then be prompted to enter a username, email, and password for the superuser.

You can then access the Django admin site by running the development server and navigating to `http://127.0.0.1:8000/admin/` in your web browser.

## Conclusion

Configuring your Django project properly is crucial for laying a solid foundation for your application. Adjusting the settings in `settings.py` allows you to tailor the project to your specific requirements, including how it handles data with the database, how it finds and serves static files, and how it processes requests and responses. By understanding and correctly setting these configurations, you're well on your way to developing a robust Django web application.
