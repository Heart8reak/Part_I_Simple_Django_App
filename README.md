## Part I
## Create a simple Django Newsletter web app:

### 1 Home page
### 2 About page
### 3 Sign up page
### 4 launch it live on Heroku


1.0 Start on the Desktop and create a directory to contain the Django Project

```bash
mkdir 'name of directory/project'
cd 'name of directory/project'
```

1.1 Setup virtual environment

```bash
virtualenv -p python3 .
```

1.1.1 activate virtual environemt

```bash
source bin/activate
```

1.1.2 deactivate virtual environment

```bash
deactivate
```

1.2 create directory to store source code

```bash
mkdir src
```

1.2.1 open up VScode within the directory

```bash
code .
cd src
```

2.0 pip install dependacies to support Heroku

```bash
pip freeze

pip install django

pip install dj-database-url

pip install psycopg2-binary

pip install gunicorn
```

2.1 create a django project

```bash
django-admin startproject 'name of project' .
```

2.2 runserver

```bash
python manage.py runserver
```

2.3 add requirements.txt in the root directory (src)

```bash
pip freeze > requirements.txt
```

2.4 create a django app

```bash
python manage.py startapp 'name of app'
```

2.5 go to settings file and add new app to INSTALLED_APPS = []

2.6 create a templates directory in the root (src)

```bash
mkdir templates
cd templates
```

2.6.1 create html pages

```bash
touch home.html
touch about.html
touch signup.html
touch base.html
```

3.0 need to add templates directory into settings file under TEMPLATES = []

```python
os.path.join(BASE_DIR, "templates")
```
3.1 Open up views.py in the 'app' directory, create a function base view

```python
from django.http import HttpResponse
from django.shortcuts import render

def home_view(request):
        return render(request, "home.html", {})

def about_view(request):
        return render(request, "about.html", {})

def signup_view(request):
        return render(request, "signup.html", {})
```

3.2 go to urls.py and route the function based views

```python
from signup import views

urlpatterns = [
    path('', views.home_view),
    path('about/', views.about_view),
    path('signup/', views.signup_view)
]
```

3.3 Using Django Template Tags

```python
{% block content %}
{% endblock %}

{% extends 'base.html' %}
```

4.0 CDN Bootstrap, add these to base.html

```html
 <!-- bootstrap css -->
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">

<!-- bootstrap js -->
    <script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js" integrity="sha384-UO2eT0CpHqdSJQ6hJty5KVphtPhzWj9WO1clHTMGa3JDZwrnQq4sF86dIHNDz0W1" crossorigin="anonymous"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js" integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM" crossorigin="anonymous"></script>
```

### Launch web app online with Heroku

5.0 create .gitignore file, go to the link below, copy paste this file to the .gitignore file
    https://raw.githubusercontent.com/github/gitignore/master/Python.gitignore

5.1. create a Procfile in the src directory and add these lines

```
release: python manage.py migrate
web: gunicorn meetup_news.wsgi
```

5.2 install heroku cli or update heroku

```bash
heroku update
heroku login
heroku create 'name of web app'
```

5.3 add the new heroku url and local host '127.0.0.1' to settings.py file under ALLOWED_HOSTS and DEBUG = False

5.4 Initialize a git repository

```bash
git int
git status
git add .
git commit -m "Initail commit"
git push heroku master
```

5.5 in case we run into an error, we have to disable collectstatic files

```bash
heroku config:set DISABLE_COLLECTSTATIC=1
git push heroku master
```

## And we are live Hosuton!
