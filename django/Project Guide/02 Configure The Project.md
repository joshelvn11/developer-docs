# Configure The Project

Configuring your Django project involves setting up various components to ensure your application runs smoothly, handles data correctly, and serves static content properly. This step is crucial for tailoring the Django framework to the needs of your specific project. Let's delve into how to configure your project, focusing on the `settings.py` file, database setup, and handling static files.

## Adjusting Settings in `settings.py`

The `settings.py` file in your Django project directory contains configuration for your project. Here are some of the key settings you'll likely need to adjust:

### Databases

By default, Django uses SQLite. To configure a different database (e.g., PostgreSQL), you'll need to change the `DATABASES` setting.

- **Example for PostgreSQL**:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'mydatabase',
        'USER': 'mydatabaseuser',
        'PASSWORD': 'mypassword',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
```

You'll need to install the appropriate database adapter (e.g., `psycopg2` for PostgreSQL) in your virtual environment:

```bash
pip install psycopg2
```

### Installed Apps

Here you can add or remove applications from your Django project. To add an app you've created or a third-party app, add its name to the `INSTALLED_APPS` list.

- **Example**:

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'myapp',  # Your custom app
    'rest_framework',  # An example third-party app
]
```

### Middleware

Middleware is a framework of hooks into Django's request/response processing. It's a lightweight, low-level plugin system for globally altering Django's input or output. If you need to add custom middleware or use middleware from third-party apps, you'll add them here.

- **Example**:

```python
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'mycustommiddleware.SomeMiddleware',  # Your custom middleware
]
```

### Templates

This setting configures how Django loads and renders templates. You might want to specify directories where Django looks for template files.

In `settings.py` create a `TEMPLATES_DIR` constant to build a path for our subdirectory 'templates':

```python
# Build paths inside the project like this: BASE_DIR / 'subdir'.
TEMPLATES_DIR = os.path.join(BASE_DIR, 'templates')
```

Add the `TEMPLATES_DIR` to `DIRS` list:

```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [TEMPLATES_DIR],  # Custom template directory
        'APP_DIRS': True,
    },
]
```

Finally create the top-level demplates directory in your project folder:

```bash
$ mkdir templates
```

### Static Files

Static files (CSS, JavaScript, images) are served from the `STATIC_URL` path. You might need to add directories where Django looks for these files using `STATICFILES_DIRS`, and specify where to collect static files for deployment with `STATIC_ROOT`.

**Example**:

```python
STATIC_URL = '/static/'
STATICFILES_DIRS = [BASE_DIR / 'static',]  # Custom static file directories
STATIC_ROOT = BASE_DIR / 'staticfiles'  # Directory for `collectstatic` to collect static files to
```

## Database Setup

After configuring your database in `settings.py`, you need to set up the database tables that Django uses internally, along with any models you've defined in your apps.

1. **Run Migrations**: Migrations apply changes to your database schema.

   ```bash
   python manage.py migrate
   ```

   This command looks at the `INSTALLED_APPS` setting and creates any necessary database tables according to the database settings in `settings.py` and the migrations defined in each application.

2. **Create a Superuser** (optional but recommended for accessing the Django admin site):

   ```bash
   python manage.py createsuperuser
   ```

   Follow the prompts to create a user account.

## Conclusion

Configuring your Django project properly is crucial for laying a solid foundation for your application. Adjusting the settings in `settings.py` allows you to tailor the project to your specific requirements, including how it handles data with the database, how it finds and serves static files, and how it processes requests and responses. By understanding and correctly setting these configurations, you're well on your way to developing a robust Django web application.
