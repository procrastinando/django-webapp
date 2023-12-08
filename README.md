This code snippet demonstrates the installation of Python, creating a virtual environment, installing libraries, and creating a Django web application.

## 1. Installation Steps for Python (Latest Version) on Windows:
1. Visit the official Python website at https://www.python.org/downloads/ and download the latest version of Python for Windows.
2. Run the downloaded installer and follow the installation wizard.
3. Make sure to check the option "Add Python to PATH" during the installation process.
4. Verify the installation by opening the command prompt and running the command "python --version".

## 2. Installation Steps for Python (Latest Version) on Linux:
1. Open the terminal and run the following command to update the package list: 
    sudo apt update
2. Install Python by running the following command:
    sudo apt install python3
3. Verify the installation by running the command "python3 --version" in the terminal.

## 3. Creating a New project:
1. Open the command prompt or terminal.
2. Navigate to the project directory using the "cd" command.
3. Run the following command to start a new project (webapp):
    django-admin startproject webapp

## 4. Basic settings:
1. Inside the project directory (webapp):
    `python manage.py startapp myapp`
    Append "myapp" to "INSTALLED_APPS" in `./webapp/settings.py`
2. Create an admin user:
    `python ./manage.py createsuperuser`
    The admin page can be acceded from `root/admin`
3. The first time and Everytime modifications are made in the database, migrations have to run:
    `python ./manage.py makemigrations`
    `python ./manage.py migrate`
4. Run `python ./manage.py runserver` and the welcome django page will be shown

## 5. Creating a home page:
1. Create a directory `templates` into `myapp`. The `./myapp/templates/base.html` will be extended to any page that needs it, such as `./myapp/templates/home.html`.
2. Render the page, add this to `./myapp/views.py`:
    python```
    def home(request):
    return render(request, 'home.html')
    ```
3. Define the url in `./myapp/urls.py`:
    python```
    from django.urls import path
    from . import views

    urlpatterns = [
        path('', views.home, name='home'),
    ]
    ```
4. Run `python ./manage.py runserver`

## 6. A To DO List page with database:
### 0. Create a MySQL database
#### 0.1. In `./myapp/webapp.py` insert the db type and credentials:
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'myapp',
        'USER': 'root',
        'PASSWORD': 'example',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
```
#### 0.2. Create the database using workbench, or using python:
```
# Install Mysql on your computer => https://dev.mysql.com/downloads/installer/
import mysql.connector

dataBase = mysql.connector.connect(
	host = 'localhost',
	user = 'root',
	passwd = 'example'
	)

cursorObject = dataBase.cursor()
cursorObject.execute("CREATE DATABASE myapp")
```
### 1. ToDo Database:
#### 1.1. Create a class in `./myapp/models.py`, for example:
```
class TodoItem(models.Model):
    title = models.CharField(max_length=256)
    completed = models.BooleanField(default=False)
```
#### 1.2. Register the site in admin `./myapp/admin.py`, for example:
```
from .models import TodoItem
admin.site.register(TodoItem)
```

### 2. ToDo page:
#### 2.1. Create the html template `./myapp/templates/todos.html`
```
{% extends 'base.html' %}
{% block content %}
<h1>To Do List</h1>
<ul>
    {% for todo in todos %}
    <li>
        {{ todo.title }}: {% if todo.completed %}Completed{% else %}Not Completed{% endif %}
    </li>
    {% endfor %}
</ul>
{% endblock %}
```
#### 2.2. Render the page `./myapp/views.py`, import also data from database:
```
from .models import TodoItem

def todos(request):
    items = TodoItem.objects.all()
    return render(request, 'todos.html', {"todos": items})
```
2.3. Define the URL:
urlpatterns = [
    path("todos/", views.todos, name="todos")
]
### 3. Run `python ./manage.py runserver`
