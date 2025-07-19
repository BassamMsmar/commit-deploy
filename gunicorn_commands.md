# Gunicorn Commands

- `gunicorn app.wsgi:application` : Run app with Gunicorn.
- `gunicorn --bind 0.0.0.0:8000 app.wsgi` : Bind to port 8000.
- `gunicorn --workers 3 app.wsgi` : Run with 3 workers.
