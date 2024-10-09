Angular 17 + DRF 3.15 on dev localhost:4200 and localhost:8000 CORS problem
For DRF needs django-cors-headers==4.4.0

```bash
$ pip install django-cors-headers==4.4.0
```

then add to *settings.py*

```
INSTALLED_APPS = [
    ...,
    'corsheaders',
    ...,
]

MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'corsheaders.middleware.CorsMiddleware',
    ...,
]

CORS_ORIGIN_WHITELIST = ['http://localhost:4200']
```
