# The Django Template Language (DTL)

The Django Template Language (DTL) is a powerful, flexible tool for generating HTML dynamically. It's designed to strike a balance between ease of use and power, providing developers with the ability to insert data into HTML in a readable and maintainable way. Here's a beginner-friendly guide to understanding and using the Django Template Language.

## Basics of Django Template Language

### Variables

Variables are used to output data from your Django views into your HTML. In the template, a variable is represented by `{{ variable_name }}`.

```html
<p>My name is {{ name }}.</p>
```

If `name` is `"John"` in the context passed from a view, the output will be:

```html
<p>My name is John.</p>
```

### Filters

Filters transform the display of a variable in the template. They're used with the `|` character followed by the filter name.

```html
<p>My name is {{ name|lower }}.</p>
```

If `name` is `"JOHN"`, using the `lower` filter will output:

```html
<p>My name is john.</p>
```

Filters can also accept arguments. For example, the `date` filter formats Python datetime objects. The argument is passed using `:"argument"` syntax.

```html
<p>The date is {{ current_date|date:"D d M Y" }}.</p>
```

#### List of Filters

| Filter Name          | Description                                                                                                                                                                                   |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `add`                | Adds the argument to the value.                                                                                                                                                               |
| `addslashes`         | Adds slashes before quotes.                                                                                                                                                                   |
| `capfirst`           | Capitalizes the first character of the value.                                                                                                                                                 |
| `center`             | Centers the value in a field of a given width.                                                                                                                                                |
| `cut`                | Removes all values of the argument from the given string.                                                                                                                                     |
| `date`               | Formats a date according to the given format.                                                                                                                                                 |
| `default`            | If the value is falsy, use the given default.                                                                                                                                                 |
| `default_if_none`    | If the value is `None`, use the given default.                                                                                                                                                |
| `dictsort`           | Takes a list of dictionaries and returns that list sorted by the key given in the argument.                                                                                                   |
| `dictsortreversed`   | Same as `dictsort` but in reverse order.                                                                                                                                                      |
| `divisibleby`        | Returns `True` if the value is divisible by the argument.                                                                                                                                     |
| `escape`             | Escapes HTML in the value, replacing characters like `<` and `>` with their entity references.                                                                                                |
| `escapejs`           | Escapes characters for use in JavaScript strings.                                                                                                                                             |
| `filesizeformat`     | Formats the value like a 'human-readable' file size (e.g., `'13 KB'`).                                                                                                                        |
| `first`              | Returns the first item of a list.                                                                                                                                                             |
| `floatformat`        | Formats a floating-point number to a specified number of decimal places.                                                                                                                      |
| `get_digit`          | Returns the nth digit of a number, from the right.                                                                                                                                            |
| `iriencode`          | Encodes an IRI value to be safe for URLs.                                                                                                                                                     |
| `join`               | Joins a list with a string, similar to Python's `str.join(list)`.                                                                                                                             |
| `json_script`        | Safely outputs a Python object as JSON, wrapped in a `<script>` tag.                                                                                                                          |
| `length`             | Returns the length of the value.                                                                                                                                                              |
| `length_is`          | Returns `True` if the value's length is the argument.                                                                                                                                         |
| `linebreaks`         | Replaces line breaks in plain text with appropriate HTML; a single newline becomes an HTML line break (`<br>`) and a new line followed by a blank line becomes a paragraph break (`<p>`).     |
| `linebreaksbr`       | Converts all newlines in a piece of plain text to HTML line breaks (`<br>`).                                                                                                                  |
| `linenumbers`        | Displays text with line numbers.                                                                                                                                                              |
| `ljust`              | Left-justifies in a field of a given width.                                                                                                                                                   |
| `lower`              | Converts text to lowercase.                                                                                                                                                                   |
| `make_list`          | Returns the value turned into a list.                                                                                                                                                         |
| `phone2numeric`      | Converts a phone number (containing letters) to its numerical equivalent.                                                                                                                     |
| `pluralize`          | Returns a plural suffix if the value is not 1. By default, this suffix is `'s'`.                                                                                                              |
| `pprint`             | Outputs a pretty-printed version of a Python object.                                                                                                                                          |
| `random`             | Returns a random item from the list.                                                                                                                                                          |
| `safe`               | Marks a string as not requiring further HTML escaping.                                                                                                                                        |
| `safeseq`            | Marks each item in a sequence as safe.                                                                                                                                                        |
| `slice`              | Returns a slice of the list.                                                                                                                                                                  |
| `slugify`            | Converts to ASCII, converts spaces to hyphens, removes characters that aren't alphanumerics, underscores, or hyphens, converts to lowercase, and also strips leading and trailing whitespace. |
| `stringformat`       | Formats the variable according to the argument, a string formatting specifier.                                                                                                                |
| `striptags`          | Strips all [X]HTML tags.                                                                                                                                                                      |
| `time`               | Formats a time according to the given format.                                                                                                                                                 |
| `timesince`          | Formats a date as the time since that date (e.g., "4 days, 6 hours").                                                                                                                         |
| `timeuntil`          | Formats a date as the time until that date (e.g., "4 days, 6 hours").                                                                                                                         |
| `title`              | Converts to titlecase.                                                                                                                                                                        |
| `truncatechars`      | Truncates a string if it is longer than the specified number of characters.                                                                                                                   |
| `truncatechars_html` | Truncates HTML to a certain number of chars (ignoring tags and preserving HTML integrity).                                                                                                    |
| `truncatewords`      | Truncates a string after a certain number of words.                                                                                                                                           |
| `truncatewords_html` | Truncates                                                                                                                                                                                     |

HTML to a certain number of words (ignoring tags and preserving HTML integrity). |
| `unordered_list` | Takes a list and returns an HTML unordered list - effectively a recursive version of the `|join` filter. |
| `upper` | Converts text to uppercase. |
| `urlencode` | Escapes a value for use in a URL. |
| `urlize` | Converts URLs in plain text into clickable links. |
| `urlizetrunc` | Converts URLs into clickable links, truncating URLs longer than the given character limit. |
| `wordcount` | Returns the number of words. |
| `wordwrap` | Wraps words at specified line length. |
| `yesno` | Maps values to other values, like a switch statement. |

This table offers a snapshot of the available DTL filters as of Django 3.2. For the most current and comprehensive list, always refer to the [official Django documentation](https://docs.djangoproject.com/en/stable/ref/templates/builtins/#built-in-filter-reference).

### Tags

Tags provide more complex logic than variables can handle. They're wrapped in `{% %}`. Tags can do many things, such as looping through lists, loading external templates, or checking conditions.

**For Loop**:

```html
<ul>
  {% for item in item_list %}
  <li>{{ item }}</li>
  {% endfor %}
</ul>
```

**If Statement**:

    ```html
    {% if user.is_authenticated %}
      <p>Welcome, {{ user.username }}!</p>
    {% else %}
      <p>Welcome, guest!</p>
    {% endif %}
    ```

## Inheritance in Django Templates

Template inheritance is a powerful feature of DTL, allowing you to build a base "skeleton" template that contains all the common elements of your site and defines blocks that child templates can override.

**Base Template** (`base.html`):

```html
<html>
  <head>
    <title>{% block title %}My Site{% endblock %}</title>
  </head>
  <body>
    {% block content %} {% endblock %}
  </body>
</html>
```

**Child Template**:

```html
{% extends "base.html" %} {% block title %}Home Page{% endblock %} {% block
content %}
<p>Welcome to my site.</p>
{% endblock %}
```

## Including Templates

The `include` tag allows you to include another template within a template. This is useful for reusing parts of HTML like navigation bars or footers.

```html
<div>{% include "navbar.html" %}</div>
```

## Comments

You can add comments in your templates that won't be rendered to the client. Single-line comments look like `{# #}`, and multi-line comments are wrapped in `{% comment %}` and `{% endcomment %}`.

```html
{# This is a single-line comment #} {% comment %} This is a multi-line comment
{% endcomment %}
```

## Custom Template Tags and Filters

For functionality not covered by the built-in tags and filters, you can create your own custom template tags and filters. This involves creating a `templatetags` directory in your app, defining your tags/filters in a Python file there, and loading them in your template using `{% load %}`.

## Conclusion

The Django Template Language is designed to be easy for front-end developers who may not know Python to work with, while still being powerful and flexible enough for complex applications. By mastering DTL, you can efficiently generate dynamic HTML content for your Django applications, creating a rich, interactive user experience.
