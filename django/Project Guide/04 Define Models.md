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
