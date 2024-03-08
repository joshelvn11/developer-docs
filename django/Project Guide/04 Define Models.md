# 4. Define Models

## Step 1: Define Models

Now that the database is set up and connected to your Django project, you can define the models for your application. Models are Python classes that represent the structure of the data in your database. Django uses models to create tables in the database and to interact with the data in those tables.

Models are defined in the `models.py` file of your app. Each model is used to define a table in the database. Each field in the model represents a column in the table.

Here is an example for a simple model that represents a blog post:

```python
from django.db import models
from django.contrib.auth.models import User

STATUS = ((0, "Draft"), (1, "Published"))

class Post(models.Model):
    title = models.CharField(max_length=100)
    content = models.TextField()
    author = models.ForeignKey(User, on_delete=models.CASCADE)
    slug = models.SlugField(max_length=100, unique=True)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    status = models.IntegerField(choices=STATUS, default=0)
```

In the example above, the `Post` model has five fields:

- `title`: A character field that represents the title of the blog post.
- `content`: A text field that represents the content of the blog post.
- `created_at`: A date and time field that records when the blog post was created.
- `updated_at`: A date and time field that records when the blog post was last updated.
- `status`: An integer field that represents the status of the blog post. The `STATUS` variable is a tuple of tuples that defines the choices for the `status` field. The `status` field has a default value of `0` which represents "Draft".

Here is another example for a model that represents a comment on a blog post:

```python
class Comment(models.Model):
    post = models.ForeignKey(Post, on_delete=models.CASCADE)
    author = models.ForeignKey(User, on_delete=models.CASCADE)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
```

## Step 2: Create Migrations

Now that the models are defined, you can create migrations for the models. Migrations are used to create the tables in the database and to keep the database schema in sync with the models.

Start by running the following command in your terminal to create the migrations for the models:

```bash
python3 manage.py makemigrations
```

Once the migrations have been created, you can apply the migrations to create the tables in the database by running the following command in your terminal:

```bash
python3 manage.py migrate
```

## Step 3: Register Models

Register the models with the admin site by adding the following code to `admin.py` in the `myapp` directory:

```python
from django.contrib import admin
from .models import Post, Comment

# Register your models here
admin.site.register(Post)
admin.site.register(Comment)
```

## Step 4: Add CSRF Trusted Origins

You can add the following code to the `settings.py` file in the `myapp` directory to allow the `localhost` and other domains to make requests to your Django project, you will also need to add your production site URL to the list of trusted origins, the following example uses Heroku as the production platform

```python
CSRF_TRUSTED_ORIGINS = [
    "https://*.herokuapp.com",
    "http://localhost"
]
```

<details>
<summary>CSRF Explanation</summary>
<p>Cross-Site Request Forgery (CSRF) is a type of attack that forces an end user to execute unwanted actions on a web application in which they're currently authenticated. CSRF attacks specifically target state-changing requests, not theft of data, since the attacker has no way to see the response to the forged request. To mitigate this risk, Django has a built-in mechanism to protect against CSRF attacks by using tokens that are checked with each POST request. This ensures that the request is coming from a trusted source, namely your own web application.

The `CSRF_TRUSTED_ORIGINS` setting in Django is a security measure that allows you to explicitly specify which domains are trusted sources of requests to your application. This is particularly useful when your application is interacting with client-side JavaScript that might be hosted on other domains or when your application is deployed across multiple domains.

When you specify domains in the `CSRF_TRUSTED_ORIGINS` list, you're telling Django that it's safe to accept form submissions and AJAX requests from these origins, as they are part of your application's ecosystem. This is crucial for the security of your application, especially when deploying it to production where it might interact with various services and APIs.

For example, if your Django application is hosted on Heroku and you have a frontend application hosted on Netlify, you would need to add both domains to the `CSRF_TRUSTED_ORIGINS` to ensure that requests between these services are not blocked by Django's CSRF protection mechanism.

It's important to be cautious and only add domains that you control or trust, as adding untrusted domains can open your application to CSRF attacks. Always review and update this list in accordance with the domains your application is interacting with.</p>

</details>

## Adding Additional Info to Models

### The `Meta` Class

In Django, the `Meta` class within a model is a special class that holds configuration for the model itself. It's used to define options like ordering of records, database table name, verbose names, and much more.

Here's an example of using the `Meta` class within a model:

```python

class Article(models.Model):
title = models.CharField(max_length=200)
body = models.TextField()
author = models.ForeignKey(Author, on_delete=models.CASCADE)
publish_date = models.DateTimeField(auto_now_add=True)

    class Meta:
        ordering = ['-publish_date']
        verbose_name = 'Article'
        verbose_name_plural = 'Articles'

```

`ordering`: This option is used to specify how lists of objects should be ordered when retrieved from the database. In the given example, `ordering = ['-publish_date']` means that objects will be ordered by `publish_date` in descending order (newest first). The `-` sign indicates descending order. Without the `-`, objects would be ordered in ascending order.

`verbose_name`: This is a human-readable name for the object, singular form. Django uses this in the Django admin interface and other places where it needs to refer to the object. In the example, `verbose_name = 'Article'` specifies that the human-readable name for the object is "Article".

`verbose_name_plural`: Similar to `verbose_name`, but for the plural form of the object's name. This is used in places where Django needs to refer to more than one instance of the object. In the example, `verbose_name_plural = 'Articles'` specifies that the plural name is "Articles".

These options help make the admin interface and other parts of Django more intuitive and easier to work with by providing clear, human-readable names for models and specifying default ordering for model objects.

### The `__str__` Method

The `__str__` method in Django models is a special method that defines how an object is represented as a string. This method is particularly useful when you need a human-readable representation of the model instance, which can be very helpful during debugging and in the Django admin interface.

Here's an example of using the `__str__` method within a model:

```python
class Post(models.Model):
    # …
    def __str__(self):
        return f"The title of this post is {self.title}"
```

## Creating Dry Runs

Dry runs are a useful feature in Django that allows developers to simulate database migrations without actually applying them. This can be particularly helpful when you want to ensure that your migrations will run smoothly before making any changes to the database. Dry runs can help catch potential issues early in the development process, saving time and reducing the risk of data loss or corruption.

To perform a dry run of your migrations, you can use the `--dry-run` option with the `makemigrations` and `migrate` commands. Here's how to use it:

1. **Dry Run for Creating Migrations**

   Before creating new migrations, you can simulate the process to see what changes Django would make. Run the following command in your terminal:

   ```bash
   python3 manage.py makemigrations --dry-run
   ```

````

This command will output the migrations that Django intends to create without actually creating the migration files.

2. **Dry Run for Applying Migrations**

   Similarly, you can simulate applying migrations to your database to check for potential issues. Use the `--dry-run` option with the `migrate` command as shown below:

   ```bash
   python3 manage.py migrate --dry-run
   ```

   This will show you what changes would be applied to your database without actually applying the migrations.

Using dry runs is a best practice, especially in production environments, to ensure that your migrations will not cause any unexpected issues. Always consider performing a dry run before applying new migrations to your database.
````
