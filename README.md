# 8 minutes to a production web app
Here is the code after completing the steps in my tutorial video.

## Running Locally

1. Create a virtual environment (>=python 3.8)
2. Activate the virtual environment
2. Install the package requirements `pip install -r requirements.txt
3. Run the server: `python manage.py runserver`
Your Django application is now available at `http://localhost:8000`.
In production, the app uses the Web Server Gateway Interface (WSGI) with Django to enable handling requests on Vercel with Serverless Functions.


## How it Works

Our Django application, `example` is configured as an installed application in `vercel_app/settings.py`:
```python
# vercel_app/settings.py
INSTALLED_APPS = [
    # ...
    'example',
]
```

There is a single view which renders the current time in `example/views.py`. 
This view is exposed a URL through `example/urls.py`:

```python
# example/urls.py
from django.urls import path

from example.views import index


urlpatterns = [
    path('', index),
    ...
]
```

Finally, it's made accessible to the Django server inside `vercel_app/urls.py`:

```python
# vercel_app/urls.py
from django.urls import path, include

urlpatterns = [
    ...
    path('', include('example.urls')),
]
```
