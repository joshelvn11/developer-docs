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

## Passing Contextual Data To JavaScript

Passing context from Django to JavaScript can be achieved in several ways, allowing you to dynamically use Django variables within your JavaScript code. Here are three common methods to do this, each suitable for different scenarios:

### Method 1: Inline Script Tag

You can directly include Django template variables within a `<script>` tag in your HTML template. This method is straightforward for passing simple data types like strings, integers, or lists.

#### Example:

```html
<!-- In your Django template -->
<script type="text/javascript">
  var myVar = '{{ django_variable }}';
  var myList = {{ django_list|safe }};
</script>
```

- Use the `{{ django_variable }}` syntax to inject Django template variables directly into your JavaScript code.
- To pass more complex data types like lists or dictionaries, use the `|safe` filter to prevent Django from escaping the JSON string.

### Method 2: Data Attributes

For a cleaner separation of HTML and JavaScript, you can use data attributes in your HTML elements to store Django context variables. Then, access these attributes via JavaScript.

#### Example:

```html
<!-- In your Django template -->
<div
  id="my-div"
  data-my-var="{{ django_variable }}"
  data-my-list="{{ django_list|safe }}"
></div>

<script type="text/javascript">
  var myVar = document.getElementById("my-div").getAttribute("data-my-var");
  var myList = JSON.parse(
    document.getElementById("my-div").getAttribute("data-my-list")
  );
</script>
```

- This method keeps the JavaScript clean of Django template syntax.
- Use `JSON.parse()` to convert JSON strings into JavaScript objects or arrays.

### Method 3: Using the `json_script` Template Tag

Django 2.1 introduced the `json_script` template tag, which securely outputs a Python dictionary as a JSON object within a `<script>` tag. This method is especially useful for passing complex data structures like dictionaries or lists of objects.

#### Example:

```html
<!-- In your Django template -->
{% json_script "django_variables" %} { "myVar": "{{ django_variable }}",
"myList": {{ django_list|safe }} } {% endjson_script %}

<script type="text/javascript">
  var djangoData = JSON.parse(
    document.getElementById("django_variables").textContent
  );
  var myVar = djangoData.myVar;
  var myList = djangoData.myList;
</script>
```

- The `json_script` tag takes a unique identifier as its first argument and outputs a `<script>` tag with type `application/json` containing the JSON data.
- Access the data in JavaScript by parsing the content of the generated `<script>` tag.

### Considerations

- **Security**: Be cautious when injecting data directly into JavaScript to avoid XSS (Cross-Site Scripting) vulnerabilities, especially with user-generated content. Always sanitize and validate the data.
- **Performance**: For large amounts of data, consider fetching the data asynchronously via an API endpoint instead of embedding it directly into the template. This can improve page load times and overall performance.

Each method has its use cases, with inline scripts being quick and straightforward, data attributes offering a clean separation of concerns, and the `json_script` tag providing a secure and robust way to pass complex data. Choose the method that best fits the complexity of your data and your project's architectural guidelines.
