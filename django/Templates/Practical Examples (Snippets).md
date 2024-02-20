# Practical Examples (Snippets)

## Navigation Bar

Creating a reusable navigation bar in Django with an "active" class for the currently active link involves using Django's template inheritance and template tags. This guide will walk you through creating a base template that includes a reusable navigation bar, highlighting the active link based on the current page.

### Step 1: Define Your Base Template

First, you'll need a base template from which other templates will inherit. This base template will contain your navigation bar.

#### `base.html`

```html
<!DOCTYPE html>
<html>
  <head>
    <title>{% block title %}My Django Site{% endblock %}</title>
    <link rel="stylesheet" href="{% static 'css/style.css' %}" />
  </head>
  <body>
    <header>
      <nav>
        <ul>
          <li
            class="{% if request.resolver_match.url_name == 'home' %}active{% endif %}"
          >
            <a href="{% url 'home' %}">Home</a>
          </li>
          <li
            class="{% if request.resolver_match.url_name == 'about' %}active{% endif %}"
          >
            <a href="{% url 'about' %}">About</a>
          </li>
          <li
            class="{% if request.resolver_match.url_name == 'contact' %}active{% endif %}"
          >
            <a href="{% url 'contact' %}">Contact</a>
          </li>
        </ul>
      </nav>
    </header>

    {% block content %}
    <!-- Page specific content will go here -->
    {% endblock content %}

    <footer>
      <!-- Footer content here -->
    </footer>
  </body>
</html>
```

- The `{% static 'css/style.css' %}` tag is used to include a CSS file located in your static files directory.
- The `{% if request.resolver_match.url_name == '...' %}active{% endif %}` condition dynamically adds the `active` class if the current URL name matches the specified name.
- The `{% url '...' %}` tag dynamically resolves the URL for a given view name, ensuring that your links remain accurate even if you change URLs later.

### Step 2: Create Your CSS File

Next, create a CSS file to style your navigation bar and highlight the active link.

#### `style.css` (in your `static/css/` directory)

```css
nav ul {
  list-style-type: none;
  padding: 0;
}

nav ul li {
  display: inline;
  margin-right: 10px;
}

nav ul li a {
  text-decoration: none;
}

.active a {
  color: red; /* Highlight color for the active link */
}
```

This CSS file defines basic styles for the navigation bar and applies a different color to the active link.

### Step 3: Use the Base Template in Your Views

When creating templates for specific pages (e.g., Home, About, Contact), extend the base template and define content within the `{% block content %}` block.

#### Example: `home.html`

```html
{% extends "base.html" %} {% block title %}Home{% endblock %} {% block content
%}
<h1>Welcome to the Home Page</h1>
<p>This is the content of the home page.</p>
{% endblock %}
```

### Step 4: Configure Your URLs

Make sure your `urls.py` file is correctly configured to use named URL patterns, which correspond to the names checked in the base template.

#### `urls.py` (in your project or app directory)

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home_view, name='home'),
    path('about/', views.about_view, name='about'),
    path('contact/', views.contact_view, name='contact'),
]
```

### Conclusion

By following these steps, you've created a reusable navigation bar in Django that highlights the active link based on the current page. This technique leverages Django's powerful template inheritance and template tags to produce a dynamic and maintainable navigation solution suitable for a wide range of projects.
