# Django and Next Js Boilerplate

---

# [CodeWithRafiq](https://www.youtube.com/c/CodeWithRafiq/)

---

## Run NextJs Dev Server

```nede
npx create-next-app <name> .
npm run dev
http://localhost:3000/
```

## Add NextJs dependencies

```
npm install axios
npm install js-cookie
```

## Django

```python
python -m venv venv
source venv/Scripts/activate
```
> python -m pip install --upgrade pip

```python
- pip install django
- pip install djangorestframework
- pip install django-cors-headers
- pip install beautifulsoup4
```

```
django-admin startproject <name> .
```

## Run Django Dev Server

```python
python manage.py runserver
http://127.0.0.1:8000/
```

### Create components/env.js file on BASE_DIR

```javascript
import Cookies from "js-cookie";

export const domain = "http://127.0.0.1:8000";
// export const domain = "";

/*
    window.localStorage.setItem('myCat', 'Tom');
    window.localStorage.removeItem('myCat');
    window.localStorage.clear();
    window.localStorage.getItem("token");
    */
const token = "";
const csrftoken = Cookies.get("csrftoken");
export const getheader = {
  Authorization: `token ${token}`,
};

export const postheader = {
  "X-CSRFToken": csrftoken,
};

export const posttokenheader = {
  Authorization: `token ${token}`,
  "X-CSRFToken": csrftoken,
};
```

# Edit package.json file

```
"build": "next build && next export",
npm run build
```

## Edit Django Setting.py file

```python
# Import
from pathlib import Path
import os

# INSTALLED_APPS
'rest_framework',
'rest_framework.authtoken',
'corsheaders',


# MIDDLEWARE
'corsheaders.middleware.CorsMiddleware',

 # TEMPLATES
'DIRS': [os.path.join(BASE_DIR, 'out/')],


# Static files (CSS, JavaScript, Images)

STATIC_URL = '/static/'
MEDIA_URL = '/media/'
STATICFILES_DIRS = [os.path.join(BASE_DIR, 'out')]
STATIC_ROOT = os.path.join(BASE_DIR, 'out/', 'staticroot/')
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')

CORS_ORIGIN_WHITELIST = (
    'http://localhost:3000',
)
CORS_ALLOWED_ORIGINS = [
    'http://localhost:3000',
]
CORS_URLS_REGEX = r'^/api.*'
```

### Edit Django urls.py file

```python
from django.contrib import admin
from django.urls import path, include, re_path
from django.views.generic import TemplateView
from rest_framework.authtoken.views import obtain_auth_token
from django.conf import settings
from django.conf.urls.static import static


urlpatterns = [
    path('admin/', admin.site.urls),
]

if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL,
                          document_root=settings.MEDIA_ROOT)
    urlpatterns += static(settings.STATIC_URL,
                          document_root=settings.STATIC_ROOT)
    urlpatterns += [
        re_path(r'^.*', TemplateView.as_view(template_name='index.html')),
    ]

if not settings.DEBUG:
    urlpatterns += [
        re_path(r'^.*', TemplateView.as_view(template_name='index.html')),
    ]
```

### Create app.py on BASE_DIR

```python
import argparse
import glob
import os
from bs4 import BeautifulSoup


def parse_args():
    parser = argparse.ArgumentParser()
    parser.add_argument(
        '-d',
        '--dir',
        type=str,
        required=True)
    args = parser.parse_args()
    return args


def inspect_parser(soup, tag):
    for x in soup.find_all(tag):
        if x.get('src') and x['src'].startswith('/_next/'):
            x['src'] = "{% static \"" + x['src'] + "\" %}"
        if x.get('href') and x['href'].startswith('/_next/'):
            x['href'] = "{% static \"" + x['href'] + "\" %}"


def render_html_static():
    args = parse_args()
    for html_file in glob.glob(os.path.join(args.dir, '*html')):
        soup = BeautifulSoup(open(html_file), 'html.parser')
        soup.insert(0, '{% load static %}')
        inspect_parser(soup, 'link')
        inspect_parser(soup, 'script')
        fout = open(html_file, 'wb')
        fout.write(soup.prettify('utf-8'))
        fout.close()


render_html_static()

```

```python
python app.py --dir out
python manage.py runserver
http://127.0.0.1:8000/
```
