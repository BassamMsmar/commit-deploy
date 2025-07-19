# Server Check

## Gunicorn Commands

- `gunicorn --bind 0.0.0.0:8000 app.wsgi` : Bind to port 8000.
- `gunicorn --workers 3 app.wsgi` : Run with 3 workers.

## Status

- `sudo systemctl status gunicorn` : View gunicorn status.
- `sudo systemctl stop gunicorn` : Stop gunicorn.
- `sudo systemctl start gunicorn` : Start gunicorn.
- `sudo systemctl restart gunicorn` : Restart gunicorn.

## Logs

- `sudo journalctl -f -u gunicorn` : View gunicorn logs.
- `sudo journalctl -f -u gunicorn -n 10` : View last 10 gunicorn logs.
- `sudo journalctl -f -u gunicorn -n 100` : View last 100 gunicorn logs.
- `sudo journalctl -f -u gunicorn -n 1000` : View last 1000 gunicorn logs.


## nginx

- `sudo systemctl status nginx` : View nginx status.
- `sudo systemctl stop nginx` : Stop nginx.
- `sudo systemctl start nginx` : Start nginx.
- `sudo systemctl restart nginx` : Restart nginx.
- `sudo systemctl enable nginx` : Enable nginx.
- `sudo systemctl disable nginx` : Disable nginx.
- `sudo systemctl reload nginx` : Reload nginx.