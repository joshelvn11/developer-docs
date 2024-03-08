# Create The Base Template & Homepage

In Django, the base template serves as the foundation for all other templates within a project. It defines a common structure and set of elements that are shared across multiple pages, such as headers, footers, navigation bars, and CSS or JavaScript references. By using a base template, developers can ensure consistency in the design and layout of their web application, while also reducing redundancy and simplifying the maintenance of the codebase. The base template acts as a parent template from which other templates can inherit, allowing for the easy integration of common elements and the customization of specific sections as needed for individual pages.

## Step 1: Create The Base Template

In the projects root directory create a new `templates` directory.

```bash
mkdir templates
```

In the new created `templates` directory create a new file called `base.html`

```bash
touch base.html
```

The base template will be used to define the structure of all the other templates in the project. It will generally contain elements that will appear across your site such as the header, footer, and navigation bar and global CSS and JS files.

Here's an example of a simple base template:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>{% block title %}My Django Project{% endblock %}</title>
    {% block css %}
    <!-- Add your CSS files here -->
    {% endblock %}
  </head>
  <body>
    <header>
      <h1>Welcome to My Django Project</h1>
      <nav>
        <ul>
          <li><a href="{% url 'home' %}">Home</a></li>
          <li><a href="{% url 'about' %}">About</a></li>
          <li><a href="{% url 'contact' %}">Contact</a></li>
        </ul>
      </nav>
    </header>

    <main>
      {% block content %}
      <!-- Main content goes here -->
      {% endblock %}
    </main>

    <footer>
      <p>&copy; 2023 My Django Project. All rights reserved.</p>
    </footer>

    {% block js %}
    <!-- Add your JavaScript files here -->
    {% endblock %}
  </body>
</html>
```

## Step 2: Create The Homepage

We can now create a homepage that will extend the base template. Essentially we are just creating the content that will appear in the `{% block content %}` tags.

Start by creating a file `index.html` in the `templates` directory of you app i.e `myapp/templates/myapp/index.html`. Inside thise file you can create your homepage content.

Here is a basic example of a homepage that extends the base template:

```html
{% extends 'base.html' %} {% block content %}
<h2>Welcome to My Django Project</h2>
<p>
  This is the homepage of my Django project. You can use this page as a starting
  point to build your own web application.
</p>
{% endblock %}
```

## Step 3: Add the homepage URL to the project's URLconfifg

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='home'),
]
```
