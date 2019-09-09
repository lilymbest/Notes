### **1. Create the database**
___
```
$ createdb dbname
```
### **2. Start the Project**
___

```
$ django-admin startproject dbname
```
### **3. Create the App**
___
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

### **4. Connecting to the Database**
___
A Django project's configuration lives in `settings.py`.

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'dbname',
    }
}
```
### **5. Test the data base:**
___
```
$ python3 manage.py migrate
```
### **6. One Time URL Setup**
___

**1. Setting up main_app's own urls.py**

```
$ touch main_app/urls.py
```

**2. Include it in the projects dbname/urls.py**

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
**3. Boilerplate in main_app/urls.py**

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'),
]
```

### **7. Defining View Functions**
___

Main_app/views.py is where all the app's views will be defined.

```python
from django.shortcuts import render

# Add the following import
from django.http import HttpResponse

# Define the home view
def home(request):
  return HttpResponse('<h1>Hello /ᐠ｡‸｡ᐟ\ﾉ</h1>')
```
### **8. Using Django Templates**
___
**1. Create a Templates Directory**
```
$ mkdir main_app/templates
```

**2. Create a Template**
```
$ touch main_app/templates/about.html
```
**3. Open about.html and add boilerplate**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Title</title>
</head>
<body>
  
</body>
</html>
```
**4. Update the about view in views.py to render the about.html template instead of sending a string response.**

```python
# main_app/views.py
from django.shortcuts import render

...

def about(request):
  return render(request, 'about.html')
```
### **Template Inheritance (Partials)**
___
![Template Inheritance](https://i.imgur.com/ZajRcLx.jpg)

**1. Create a base.html template (named by convention):**

```
$ touch main_app/templates/base.html
```

```html
  <main class="container">
    {% block content %}
    {% endblock %}
  </main>
```

**2. Update about.html to extend to base.html:**

```html
{% extends 'base.html' %}
{% block content %}

<h1>About the Cat Collector</h1>
<hr />
<p>Hire the Cat Collector!</p>

{% endblock %}
```

