# Django URLs, Views, and Templates

### **Minimalist vs. Full-featured Frameworks**
___
Django, unlike express is full-featured framework and provides built-in functionality. It also has many conventions/rules. Django has `helper` classes, methods, etc...

### **The Request/Response Cycle in Django**
___
Full-Stack Application:
- Clicking links and submiting forms on the front-end sends HTTP request to the web app running on a web server.
- The web server has routing that matches the HTTP request to code.
- That code typically performs CRUD, then either
    - Renders dynamic templates for Read data operations
    - Redirects to the browser in case of Create, Update, or Delete data operations.
___
# ![Request Flow Chart](https://i.imgur.com/1fFg7lz.png)

### **Start Collector Project**
___
**Create the database**
- Databases are not automatically created by Django

```
$ createdb catcollector
```
**Start the Project**

```
$ django-admin startproject catcollector
```
The above command generates and configures a Django project in a folder named catcollector.

**Create the App**
A Django project contains Django apps that represent and major functionallity in the project.

The `INSTALLED_APPS` list in catcollector/settings.py. These pre-installed apps provide services such as the admin app and the ability to serve static files.

```
$ python3 manage.py startapp main_app
```
You'll now find a main_app folder within the top-level project folder.

```python
INSTALLED_APPS = [
	'main_app',
	'django.contrib.admin',
	'django.contrib.auth',
	'django.contrib.contenttypes',
	'django.contrib.sessions',
	'django.contrib.messages',
	'django.contrib.staticfiles',
]
```
Check to make sure the project starts up:

```
$ python3 manage.py runserver
```
Browse to localhost:8000 and make sure you see the rocket on the page:

![Rocket](https://i.imgur.com/RozMgJ0.png)

**Connecting to the Database**

A Django project's configuration lives in `settings.py`.

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'catcollector',
    }
}
```
> Note: By default, Django uses SQLite

Make the above changes in your Django projects so that PostgreSQL is used instead.

Test the data base:
```
$ python3 manage.py migrate
```

The command `migrate` is used to update the database schema over time.

### **Defining Routes - URLs**
___
Review
- Needs a defined route that matches each HTTP request.
- The purpose of a route is to map to an HTTP request code.
- Django's routing system matches the URL of the request ONLY and ignores the HTTP method/verb.
- For the Home page we'll use the root route [localhost:8000](http://localhost:8000).

**One Time URL Setup**

Routes in Django are defined within URLconf modules named `urls.py`.
There's an existing project catcollector/urls.py that we could add additional routes to, but it's a best practice for each Django app to define its own and include those URLs in the project's URLconf.

1. Setting up main_app's own urls.py

```
$ touch main_app/urls.py
```

2. Include it in the projects catcollectors/urls.py

```python
from django.contrib import admin
# Add the include function to the import
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    # In this case '' represents the root route
    path('', include('main_app.urls')),
]
```
 *Be sure to import the include function near the top. Each item in urlpatterns defines a URL based route, or mounts the routes contained in other URLconf modules. The paths defined in 'main_app.urls' will be appended to the path specified in the include function.*

3. Boilerplate in main_app/urls.py

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'),
]
```
The above code defines a root path using an empty string and maps it to the view.home view function that does not exist yet - making the server unhappy.

### **Defining View Functions**

Main_app/views.py is where all the app's views will be defined.

```python
from django.shortcuts import render

# Add the following import
from django.http import HttpResponse

# Define the home view
def home(request):
  return HttpResponse('<h1>Hello /ᐠ｡‸｡ᐟ\ﾉ</h1>')
```
> Note: In order to use the HttpResponse function, we must import it like the others we've used so far.


Now when browsing to localhost:8000, we should see the welcoming cat instead of seeing the rocket.

### **Using Django Templates**
___
Djando has two templating engines built-in:
- DTL(Django Template Language)
- Jinja2, a Python template engine.

A Django project is pre-configured to use DTL.

**One-time Template Setup**
Django is configured to look for templates inside of a templates folder within each app's folder.

```
$ mkdir main_app/templates
```

**Create an about.html Template**

1. Create the template

```
$ touch main_app/templates/about.html
```
> Note: Django templates have a simple `.html` file extension.

2. Open about.html and add boilerplate `(! + tab )` and update `<title>:`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Cat Collector</title>
</head>
<body>
  
</body>
</html>
```

3. Custom markup within the `<body>` tag.

```html
<h1>About the Cat Collector</h1>
<hr />
<p>Hire the Cat Collector!</p>
<footer>All Rights Reserved, &copy; 2019 Cat Collector</footer>
```
4. Update the about view in views.py to render the about.html template instead of sending a string response.

```python
# main_app/views.py
from django.shortcuts import render

...

def about(request):
  return render(request, 'about.html')
```
> Note: Much like Express' res.render(), except for the positional request arg. Also, the .html extension is required.

Browsing to localhost:8000/about will now render the new about.html template

### **Template Inheritance (Partials)**

Django has a template inheritance feature built-in which is a more flexable version of partials from express.

The reason Django calls it template *inheritance* is because:
- You can declare that a template extends another template

- Extending another template results in defined blocks overriding blocks defined in the template being extended.

![Template Inheritance](https://i.imgur.com/ZajRcLx.jpg)

1. First let's create a base.html template (named by convention):

```
$ touch main_app/templates/base.html
```
This is the template that will hold all of the boilerplate and markup that belongs on every page,such as the <head>, navigation, even a footer if you wish.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Cat Collector</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/css/materialize.min.css">
</head>
<body>
  <header class="navbar-fixed">
    <nav>
      <div class="nav-wrapper">
        <ul>
          <li><a href="/" class="left brand-logo">&nbsp;&nbsp;CatCollector</a></li>
        </ul>
        <ul class="right">
          <li><a href="/about">About</a></li>
        </ul>
      </div>
    </nav>
  </header>
  <main class="container">
    {% block content %}
    {% endblock %}
  </main>
  <footer class="page-footer">
    <div class="right">All Rights Reserved, &copy; 2019 Cat Collector &nbsp;</div>
  </footer>
</body>
</html>
```
The most important part of the boilerplate in regards to template inheritance is:

```html
{% block content %}
{% endblock %}
```
These are DTL template tags, `block` and `endblock`, enclosed within the template tag delimiters {% %}.

Template tags control logic within a template, depending on the tag, they may or may not result in content being emitted in the page.

Whenever another template extends this base.html, that other template's {% block content %} will replace the same block in base.html.

2. Let's update about.html so that it extends base.html:

```html
{% extends 'base.html' %}
{% block content %}

<h1>About the Cat Collector</h1>
<hr />
<p>Hire the Cat Collector!</p>

{% endblock %}
```

### **Including Static Files in a Template**
___


