# Static Files and Media

Handling static and media files in Django is crucial for delivering CSS, JavaScript, images, and user-uploaded content in your web application. This guide will walk you through configuring Django to manage these files effectively.

## Static Files

Static files are files that don't change, like CSS, JavaScript, and image files used to style and add functionality to your web pages.

Django collects static files from each of your applications (and any other places you specify) into a single location that can easily be served in production.

### Step 1: Configure Settings

In your `settings.py` file, you need to define a few settings related to static files:

- `STATIC_URL` is the URL to use when referring to static files.
- `STATICFILES_DIRS` is a list of filesystem directories to check when loading static files. It's optional if you're using app-specific `static` directories.
- `STATIC_ROOT` is the directory where `collectstatic` will collect static files for deployment.

```python
# settings.py
STATIC_URL = '/static/'
STATICFILES_DIRS = [
    BASE_DIR / "static",  # Base directory where your global static files are
]
STATIC_ROOT = BASE_DIR / "staticfiles"  # Collect static to here for production
```

### Step 2: Create Static Files Directory

Create the static files directory in the top level directory of your project

```bash
$ mkdir static
```

You can now create further directories inside this for `css` and `js` and create the releveant files too.

### Step 4: Use Static Files in Templates

To use static files in your templates, first load the `{% static %}` template tag at the top of your template. You can then load static files as follows. We'll add the following code the `base.html` as we want it to be used on every page on our site.

```html
{% load static %}
<link rel="stylesheet" type="text/css" href="{% static 'css/style.css' %}" />
```

This tag generates the full URL for static files based on the `STATIC_URL` setting.

## Media Files

Media files are user-uploaded files, like user profile pictures or documents.

### Step 1: Understand Media Files

Unlike static files, media files are dynamic – they're uploaded by users of your application. Django needs a way to serve these files in development and production.

### Step 2: Configure Settings

In your `settings.py` file, define settings for media files:

- `MEDIA_URL` is the URL to use when referring to media files.
- `MEDIA_ROOT` is the filesystem path where uploaded files are stored.

```python
# settings.py
MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / "media"
```

### Step 3: Serve Media Files in Development

Django does not serve media files by default, as it's expected that a production server will handle this. However, for development, you can configure your URLconf to serve media files:

```python
# urls.py of your project
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    # ... your URL patterns
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

This setup tells Django to serve media files through the development server using the `MEDIA_URL` and `MEDIA_ROOT` settings.

## Using Django-Storages for Media Files

For more robust and scalable handling of media files, especially in production, you can use `django-storages` with a cloud storage service like Amazon S3, Google Cloud Storage, or Azure Storage. This approach offloads the serving of media files from your web server and can provide better performance and reliability.

### Step 1: Install Django-Storages

First, you need to install `django-storages` and the necessary library for your chosen storage backend. For example, to use Amazon S3, you would need `boto3`:

```bash
pip install django-storages boto3
```

### Step 2: Configure Your Settings

After installing `django-storages`, you need to configure it in your `settings.py`. The configuration varies depending on the storage service you're using. Below is an example for Amazon S3:

```python
# settings.py

# Add 'storages' to your INSTALLED_APPS
INSTALLED_APPS = [
    ...
    'storages',
    ...
]

# Amazon S3 settings
AWS_ACCESS_KEY_ID = 'your-access-key'
AWS_SECRET_ACCESS_KEY = 'your-secret-key'
AWS_STORAGE_BUCKET_NAME = 'your-bucket-name'
AWS_S3_CUSTOM_DOMAIN = f'{AWS_STORAGE_BUCKET_NAME}.s3.amazonaws.com'
AWS_S3_OBJECT_PARAMETERS = {
    'CacheControl': 'max-age=86400',
}
AWS_LOCATION = 'media'
AWS_DEFAULT_ACL = 'public-read'

# Tell Django to use the S3 media URL for media files
MEDIA_URL = f'https://{AWS_S3_CUSTOM_DOMAIN}/{AWS_LOCATION}/'

# Tell Django to use the S3 storage backend for media files
DEFAULT_FILE_STORAGE = 'storages.backends.s3boto3.S3Boto3Storage'
```

### Step 3: Migrate Media Files to Your Cloud Storage

If you're transitioning an existing project to use cloud storage, you'll need to migrate your media files to the new storage backend. This process will vary depending on your specific setup and the amount of data. Generally, it involves uploading your existing media files to the cloud storage bucket.

### Step 4: Serve Media Files in Production

With `django-storages`, serving media files in production is handled by your cloud storage provider. Ensure your storage bucket is correctly configured to serve files publicly (or with appropriate permissions) and that your Django settings are correctly pointing to the storage service.

### Conclusion

Using `django-storages` with a cloud storage backend is a powerful way to handle media files in a Django project. It simplifies media management, improves performance, and can be more cost-effective at scale. Remember to review the `django-storages` documentation for specific details on configuring different storage backends.

## Inline Explanations

- **`STATICFILES_DIRS` vs. `STATIC_ROOT`**: `STATICFILES_DIRS` is where Django looks for additional static files, besides each app's `static` folder. `STATIC_ROOT` is where Django collects static files from all sources (including `STATICFILES_DIRS` and app `static` folders) to serve them in production.
- **Serving Files in Production**: In production, you should configure your web server (e.g., Nginx, Apache) to serve static and media files. Django's development server is not suitable for production use.
- **Security for Media Files**: Be cautious when serving user-uploaded files, as they can pose security risks. Validate and sanitize inputs where necessary.

## Conclusion

Configuring static and media file handling is essential for a fully functional Django web application. Static files make your site look good and work well, while media files allow users to upload content, making your app interactive and personalized. By following these steps and understanding the underlying concepts, you can effectively manage these files in your Django projects.
