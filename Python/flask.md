# Source

1. Books
    
    Flask Web Development: Developing Web Applications with Python, Miguel Grinberg

# Notes

### Basic Application Structure

    app = Flask(__name__)

Flask uses `__name__`variable to determine the location of the application, which in turn allows it to locate other files that are part of the application.

---
An app.route decorator can have a dynamic component.

    @app.rout('user/<name>')
    def user(name):
        return '<h1>Hello, {}!</h1>'.format(name)

>The dynamic components in routes are strings by default but can also be of different types. For example, the route `/user/<int:id>` would match only URLs that have an integer in the id dynamic segment. Flask supports the types string, int, float, and path for routes.
---

>Flask includes a development web server. This command looks for the name of the Python script that contains the application instance in the `FLASK_APP` environment variable.

    $ set FLASK_APP=hello.py
    $ flask run

`$ $env:FLASK_APP = "hello.py"` in PowerShell.

It is also possible to start the development server programmatically using this snippet at the end:

    if __name__ == "__main__":
        app.run()
---
>Flask applications can optionally be executed in debug mode. In this mode, two very convenient modules of the development server called the reloader and the debugger are enabled by default. When the reloader is enabled, Flask watches all the source code files of your project and automatically restarts the server when any of the files are modified.

To enable the debug mode:

    $ set FLASK_DEBUG=1

`$ $env:FLASK_DEBUG = 1` in PowerShell.
Programatically:

    app.run(debug=True)

---
To get help:

    $ flask run --help

A useful command:


>The --host argument is particularly useful because it tells the web server what network interface to listen to for connections from clients. By default, Flask's development web server listens for connections on *localhost*, so only connections originating from the computer running the server are accepted. The following command makes the web server listen for connections on the public network interface, enabling other computers in the same network to connect as well:

    $ flask run --host 0.0.0.0

> The web server should now be accessible from any computer in the network at *http://a.b.c.d:5000*, where a.b.c.d is the IP address of the computer running the server in your network.

---
>when Flask receives a request from a client, it needs to make a few objects available to the view function that will handle it.

> To avoid cluttering view functions with lots of arguments that may not always be needed, Flask uses contexts to temporarily make certain objects globally accessible.

> In reality `request` cannot be a global variable. Contexts enable Flask to make certain variables globally accessible.

Two contexts in Flask: the *application* context and the *request* context.

|Context| Variable name | Description |
| :-- | :-- | :-- |
| Application | current_app | The application instance for the active session. |
| Application | g | An object that the application can use for temporary storage during the handling of a request. This variable is reset with each request. |
| Request | request | The request object, which encapsulates the contents of an HTTP request sent by the client.|
| Request | session | The user session, a dictionary that the application can use to store values that are "remembered" between requests.|

>Flask activates (or pushes) the application and request contexts before dispatching a request to the application, and removes them after the request is handled.
---
You can see the current URL map using:

    app.url_map

>The */static/&lt;filename>* route is a special route added by Flask to give access to static files.

>The (HEAD, OPTIONS, GET) elements shown in the URL map are the *request methods* that are handled by the routes.
Flask attaches methods to each route so that different request methods sent to the same URL can be handled by different view functions.The HEAD and OPTIONS methods are managed automatically by Flask.
---
Request's object most commonly used attributes and methods:

| Attribute or method | Description |
| :-- | :-- |
| form | A dictionary with all the form fields submitted with the request. |
| args | A dictionary with all the arguments passed in the query string of the URL. |
| values | A dictionary that combines the values in **form** and **args**. |
| cookies | A dictionary with all the cookies included in the request. |
| headers | A dictionary with all the HTTP headers included in the request. |
| files | A dictionary with all the file uploads included with the request. |
| get_data() | Returns the buffered data from the request body. |
| get_json() | Returns a Python dictionary with the parsed JSON included in the body of the request. |
| blueprint | The name of the Flask blueprint that is handling the request. |
| endpoint | The name of the Flask endpoint that is handling the request. Flask uses the name of the view function as the endpoint name for a route. |
| method | The HTTP request method, such as GET or POST. |
| scheme | The URL scheme(http or https) |
| is_secure() | Returns True if the request came through a secure (HTTPS) connection |
| host | The host defined in the request, including the port number if given by the client. |
| path | The path portion of the URL. |
| query_string | The query string portion of the URL, as a raw binary value. |
| full_path | The path and query string portions of the URL. |
| url | The complete URL requested by the client. |
| base_url | Same as url, but without the query string component. |
| remote_addr | The IP address of the client. |
| environ | The raw WSGI environment dictionary of the request. |

---

> Sometimes it is useful to execute code before or after each request is processed. For example, to authenticate a user making the request. There are four request hooks, implemented as decorators, supported by Flask:

| Decorator | Description |
| :-- | :-- |
| before_request | Registers a function to run before each request. |
| before_first_request | Registers a function to run only before the first request is handled. This can be a convenient way to add server initialization tasks. |
| after_request | Registers a function to run after each request, but only if no unhandled exception occurred. |
| teardown_request | Registers a function to run after each request, even if unhandled exceptions occurred. |

> A common pattern to share data between request hook functions and view functions is to use the **g** context global as storage.
---

The view function should return a *status code* as well. Three arguments can be used: html, status code and a dictionary of headers that are added to the HTTP response.

> Instead of returning values, Flask view functions have the option of returning a response object that can be tweaked inside the view function. 

Reponse's object most commonly used attributes and methods:

| Attribute or method | Description |
| :-- | :-- |
| status_code | The numeric HTTP status code. |
| headers | A dictionary-like object with all the headers that will be sent with the response. |
| set_cookie() | Adds a cookie to the response. |
| delete_cookie() | Removes a cookie. |
| content_length | The lenght of the response body. |
| content_type | The media type of the response body. |
| set_data() | Sets the response body as a string or bytes values. |

> There is a special type of response called a *redirect*. This response does not include a page document; it just gives the browser a new URL to navigate to. Can be generated manually with a three-value return or with a response object, but given its frequent use, Flask provides a `redirect()` helper function.

    return redirect("http://www.google.com")

Another special response function is `abort(404)`. Returns status code 404 and raises an exception.

### Templates

>By default Flask looks for templates in a *templates* subdirectory located inside the main application directory.

The view functions need to be modified as follows:

    return render_template("user.html", name=name)

>The function `render_template()` provided by Flask integrates Jinja2 template engine with the application. This function takes the filename of the template as its first argument. Any additional arguments are key-value pairs that represent actual values for variables referenced in the template.
---

>The `{{ name }}` construct references a variable. Jinja2 recognizes variables of any type, even complex types such as lists, dictionaries, and objects:

    {{ mylist[3] }}
    {{ mydict["key"] }}
    {{ myobj.method() }}

...and variables can be modified with *filters*:

    {{name|capitalize}}

Some common filters:

| Filter name | Description |
| :-- | :-- |
| safe | Renders the value without applying escaping. |
| capitalize | Converts the first character of the value to uppercase and the rest to lowercase. |
| lower | Converts the value to lowercase characters. |
| upper | Converts the value to uppercase characters. |
| title | Capitalizes each word in the value. |
| trim | Removes leading and trailing whitespace from the value. |
| striptags | Removes any HTML tags from the value before rendering. |

Conditional statements can also be used in the template:

    {% if user %}
        Hello, {{ user }}!
    {% else %}
        Hello, Stranger!
    {% endif %}

    {% for comment in comments %}
    {% endfor %}

Then there are macros which are similar to functions in Python:

    {% macro render_comment(comment) %}
        <li>{{ comment }}</li>
    {% endmacro %}

Macros can be stored in standalone files:

    {% import 'macros.html' as macros %}

>Portions of template code that need to be repeated in several places can be stored in a separate file and *included* from all the templates:

    {% include 'common.html' %}

Templates can inherit from each other. A *base* template can define blocks to be overridden by derived templates:

    <html>
    <head>
        {% block head %}
        <title> {% block title %}{% endblock %} - My Application</title>
        {% endblock %}
    </head>
    <body>
        {% block body %}
        {% endblock %}
    </body>
    </html>

And then:

    {% extends "base.html" %}
    {% block title %}Index{% endblock %}
    {% block head %}
        {{ super }}
        <style>
        </style>
    {% endblock %}
    {% block body %}
        <h1> Hello, World!</h1>
    {% endblock %}

---

Flask provides Bootstrap integration with Flask-Bootstrap.

    pip install flask-Bootstrap

And then:

    from flask_bootstrap import Bootstrap
    # ...
    bootstrap = Bootstrap(app)

This initializes Flask-Bootstrap.


