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

## Pagination

Creating pagination in a Django application is an excellent way to manage and navigate large sets of data or content, such as blog posts or product listings. Django's built-in `Paginator` class makes adding pagination straightforward. This guide will walk you through implementing pagination in a simple and beginner-friendly manner.

### Step 1: Update Your View

First, modify the view that renders the page you want to paginate. You'll use Django's `Paginator` class to split your queryset into page-sized chunks.

#### Example: Paginating a List of Objects

Suppose you have a model `MyModel`, and you want to display its objects on a page, paginated.

```python
from django.core.paginator import Paginator
from django.shortcuts import render
from .models import MyModel

def my_model_list(request):
    object_list = MyModel.objects.all()  # Fetch all objects
    paginator = Paginator(object_list, 10)  # Show 10 objects per page

    page_number = request.GET.get('page')  # Get the page number from the URL
    page_obj = paginator.get_page(page_number)

    return render(request, 'myapp/my_model_list.html', {'page_obj': page_obj})
```

- `Paginator(object_list, 10)` creates a paginator object, specifying that each page should contain 10 items.
- `request.GET.get('page')` gets the current page number from the request's query string (e.g., `?page=3`).
- `paginator.get_page(page_number)` fetches the objects for the desired page. It handles invalid page numbers and out-of-range errors gracefully.

### Step 2: Update Your Template

Next, update the template to display the paginated items and navigation links.

#### Example: Displaying the Paginated List and Navigation

```html
{% if page_obj.has_other_pages %}
<ul>
  {% for obj in page_obj %}
  <li>{{ obj.field_name }}</li>
  {% endfor %}
</ul>

<div class="pagination">
  {% if page_obj.has_previous %}
  <a href="?page=1">&laquo; first</a>
  <a href="?page={{ page_obj.previous_page_number }}">previous</a>
  {% endif %}

  <span class="current">
    Page {{ page_obj.number }} of {{ page_obj.paginator.num_pages }}.
  </span>

  {% if page_obj.has_next %}
  <a href="?page={{ page_obj.next_page_number }}">next</a>
  <a href="?page={{ page_obj.paginator.num_pages }}">last &raquo;</a>
  {% endif %}
</div>
{% endif %}
```

- This template snippet iterates over the items in `page_obj` to display them.
- It checks if there are other pages with `page_obj.has_other_pages` to decide whether to show navigation.
- Navigation links are created for the first page, previous page, next page, and last page, where applicable. The `?page=` query string is used to link to specific page numbers.

### Step 3: Style Your Pagination (Optional)

You might want to add some CSS to style your pagination links.

```css
.pagination {
  margin: 20px 0;
  text-align: center;
}

.pagination a,
.pagination span.current {
  margin: 0 5px;
  padding: 5px 10px;
  border: 1px solid #ddd;
  text-decoration: none;
}

.pagination span.current {
  font-weight: bold;
  background-color: #eee;
}

.pagination a:hover {
  background-color: #f9f9f9;
}
```

This CSS adds basic styling to your pagination links, making them more visually distinct and user-friendly.

### Conclusion

By following these steps, you've successfully implemented pagination in your Django application. Pagination is crucial for improving the usability of your app, especially when dealing with large datasets. Django's `Paginator` class simplifies this process, allowing you to create efficient, scalable, and user-friendly paginated views.
