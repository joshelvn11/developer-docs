# Create Custom Templates

Modifying Django AllAuth templates allows you to customize the look and feel of the authentication pages to match your application's design. Django AllAuth provides default templates for actions like signup, login, logout, and password change, but often, you'll want to tailor these to provide a seamless user experience. Here's a step-by-step guide on how to modify AllAuth templates in a beginner-friendly manner.

### Step 1: Understand AllAuth Template Structure

Django AllAuth uses a set of predefined templates for various authentication processes. These templates are located within the AllAuth package, under `allauth/templates`. The templates are organized by function, such as:

- `account/login.html` for the login page
- `account/signup.html` for the signup page
- `account/logout.html` for the logout confirmation page
- `account/password_change.html` for changing passwords

And many more for email management, social account connections, etc.

### Step 2: Set Up Template Override Directory

To customize these templates, you'll create override templates in your project's `templates` directory. Django looks for templates in the directories listed in `DIRS` of the `TEMPLATES` setting in `settings.py`. Ensure this is correctly set up to include your project's template directory.

```python
TEMPLATES = [
    {
        # Other settings...
        'DIRS': [BASE_DIR / 'templates'],
        # Ensure 'APP_DIRS': True is set as well
    },
]
```

### Step 3: Create Custom Templates

Create a structure within your project's `templates` directory that mirrors the AllAuth template structure. For example, to override the signup and login templates, your directory structure should look like this:

```
myproject/
    templates/
        account/
            login.html
            signup.html
```

You can also copy all AllAuth's default templates to your project's `templates` directory and modify them there. This can be useful if you want to make changes to multiple templates at once.

First find the location of the default templates by running the following command in your terminal:

```bash
pip3 show django-allauth
```

And the using the location provided copy them to your custom templates project directory:

```bash
cp -r <Location>/allauth/templates/* ./templates/
```

### Step 4: Customize the Templates

Now, you can create or edit the `login.html` and `signup.html` files to customize the login and signup pages. You can start from scratch or copy the content from the default AllAuth templates as a starting point. The default templates can be found in the AllAuth GitHub repository or within your site-packages directory where AllAuth is installed.

#### Example: Custom `login.html`

```html
{% extends "base.html" %} {% block content %}
<h2>Login</h2>
<form method="post">
  {% csrf_token %} {{ form.as_p }}
  <button type="submit">Login</button>
  <a href="{% url 'account_reset_password' %}">Forgot Password?</a>
</form>
{% endblock %}
```

- This example assumes you have a base template (`base.html`) that provides the overall HTML structure for your site.
- `{{ form.as_p }}` renders the form fields.
- The template extends the base layout and fills in the content block with the login form.

#### Example: Custom `signup.html`

```html
{% extends "base.html" %} {% block content %}
<h2>Sign Up</h2>
<form method="post">
  {% csrf_token %} {{ form.as_p }}
  <button type="submit">Sign Up</button>
</form>
{% endblock %}
```

### Step 5: Include Additional Context or Custom Logic (Optional)

If you need to include additional context or logic in your templates, you can do so by extending or customizing the views provided by AllAuth. You'll override the AllAuth view, add your custom context or logic, and then point the URL configuration to your customized view.

### Conclusion

Customizing AllAuth templates lets you integrate the authentication flow seamlessly into your site's design, enhancing the user experience. By following the steps to override default templates, you can maintain the functionality provided by Django AllAuth while presenting it in a way that aligns with your application's aesthetics and branding. Remember to follow best practices for template customization, ensuring your modifications are maintainable and seamlessly integrate with AllAuth's robust authentication system.
