# Set Up

Django AllAuth is a comprehensive authentication package that supports regular username/password login as well as social authentication, integrating with services like Google, Facebook, Twitter, and more. It provides a complete set of authentication features such as signup, login, logout, password change, password reset, and email verification. Here's a step-by-step guide to integrating AllAuth with Django, making your application's authentication system robust and flexible.

### Step 1: Install Django AllAuth

First, you need to install Django AllAuth. It's available on PyPI, so you can install it using pip:

```bash
pip install django-allauth
```

### Step 2: Configure Installed Apps

After installation, you need to add AllAuth and its dependencies to the `INSTALLED_APPS` in your `settings.py` file:

```python
INSTALLED_APPS = [
    # Django default apps...
    'django.contrib.sites',  # Required by AllAuth

    # AllAuth apps
    'allauth',
    'allauth.account',
    'allauth.socialaccount',
    # Add providers as needed
    # 'allauth.socialaccount.providers.google',
    # 'allauth.socialaccount.providers.facebook',
    # ...
]
```

Add the above lines after `'django.contrib.staticfiles',` in the `INSTALLED_APPS` list.

### Step 3: Configure Site ID

AllAuth uses Django's sites framework. You need to specify your site's ID in `settings.py` directtly after `INSTALLED_APPS`:

```python
SITE_ID = 1
LOGIN_REDIRECT_URL = '/'
LOGOUT_REDIRECT_URL = '/'
```

<details> <summary><strong>Explantion</strong></summary>

In essence, by setting SITE_ID = 1, you're telling Django, "For this project, use the site (website) whose ID is 1 for any functionality that depends on the sites framework." This could include selecting the right templates, applying specific site-based settings, or filtering content to show only what's relevant for the specified site.
<br><br>
This is particularly useful in projects where you might be running multiple websites from a single Django project and need to differentiate between them for things like content management, user authentication, or site-specific settings.</details><br>

Ensure you have the correct site ID as per your database's `django_site` table.

### Step 4: Add AllAuth to Middleware

Append the following line to the `MIDDLEWARRE` list in `settings.py`

```python
'allauth.account.middleware.AccountMiddleware',
```

### Step 5: Update URLs

In your project's `urls.py`, include the URLs for AllAuth:

```python
urlpatterns = [
    # Your URLs...
    path('accounts/', include('allauth.urls')),
]
```

This line adds the necessary URLs for login, logout, password change, and sign-up processes.

### Step 6: Configure AllAuth Settings

AllAuth is highly customizable. Here are some basic settings you might want to configure in your `settings.py`:

```python
# Authentication backends
AUTHENTICATION_BACKENDS = [
    # Needed to login by username in Django admin
    'django.contrib.auth.backends.ModelBackend',

    # `allauth` specific authentication methods
    'allauth.account.auth_backends.AuthenticationBackend',
]

# AllAuth specific settings
ACCOUNT_AUTHENTICATION_METHOD = 'email'  # Can be 'email', 'username', or 'username_email'
ACCOUNT_EMAIL_REQUIRED = True
ACCOUNT_EMAIL_VERIFICATION = 'mandatory'  # Can be 'none', 'optional', or 'mandatory'
ACCOUNT_SIGNUP_EMAIL_ENTER_TWICE = True
ACCOUNT_USERNAME_REQUIRED = False  # Set to False if you use email authentication
```

These lines can be added after the `AUTH_PASSWORD_VALIDATORS` list.

> **Note:** If email verifcation is set to to true it will require additional setup otherwise will return an Internal Server Error

These settings configure AllAuth to use email as the primary form of authentication, make email verification mandatory, and allow users to sign up with an email without requiring a username.

### Step 7: Customize Templates (Optional)

AllAuth uses its own templates for authentication views, but you can override them by creating templates in your project with specific paths. For example, to customize the signup page, create a template at `templates/account/signup.html`.

### Step 8: Run Migrations

Since AllAuth introduces new models, you need to create the necessary database tables:

```bash
python manage.py migrate
```

### Step 9: Update Your Requirements

```bash
pip3 freeze --local > requirements.txt
```

### Step 10: Add Social Authentication (Optional)

If you want to add social authentication (e.g., Google, Facebook), you need to:

1. Add the provider to `INSTALLED_APPS` (see Step 2).
2. Obtain API keys from the social platform and configure them in the Django admin under "Social applications".
3. Optionally, customize the templates to include social login buttons.

### Conclusion

Django AllAuth is a powerful tool that simplifies adding both standard and social authentication to your Django applications. It's flexible, customizable, and comes with a lot of features out of the box. While the setup has several steps, the benefits of using a comprehensive, ready-made solution like AllAuth for handling user authentication are significant, saving you time and effort in developing and maintaining authentication workflows.
