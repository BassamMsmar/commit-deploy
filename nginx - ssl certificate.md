# Deployment Setup for aljeed.shuhnaty.com and admin.aljeed.shuhnaty.com

This README documents the configuration and deployment of the React Frontend and Django Backend (including Admin Panel) with SSL using Nginx and Certbot.

---

## 📂 1. Nginx Configuration

### ▶️ `/etc/nginx/sites-available/aljeed`

**Handles:** `https://aljeed.shuhnaty.com`

```nginx
server {
    listen 80;
    server_name aljeed.shuhnaty.com;
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name aljeed.shuhnaty.com;

    root /var/www/aljeed/dist;
    index index.html;

    ssl_certificate /etc/letsencrypt/live/aljeed.shuhnaty.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/aljeed.shuhnaty.com/privkey.pem;
    include /etc/letsencrypt/options-ssl-nginx.conf;
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;

    location /api/ {
        proxy_pass http://127.0.0.1:8000/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    location /static/ {
        alias /var/www/aljeed/staticfiles/;
    }

    location / {
        try_files $uri /index.html;
    }
}
```

### ▶️ `/etc/nginx/sites-available/admin.aljeed.shuhnaty.com`

**Handles:** `https://admin.aljeed.shuhnaty.com`

```nginx
server {
    listen 80;
    server_name admin.aljeed.shuhnaty.com;
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name admin.aljeed.shuhnaty.com;

    ssl_certificate /etc/letsencrypt/live/aljeed.shuhnaty.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/aljeed.shuhnaty.com/privkey.pem;
    include /etc/letsencrypt/options-ssl-nginx.conf;
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;

    location /static/ {
        alias /var/www/aljeed/staticfiles/;
    }

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

To activate:

```bash
sudo ln -s /etc/nginx/sites-available/admin.aljeed.shuhnaty.com /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/aljeed /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

---

## 🔐 2. SSL Certificates (Certbot)

To issue certificates:

```bash
sudo certbot --nginx -d aljeed.shuhnaty.com -d admin.aljeed.shuhnaty.com
```

---

## ⚙️ 3. Django Settings (`settings.py`)

```python
STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
```

Then run:

```bash
python manage.py collectstatic
```

Static files will be collected into:

```
/var/www/aljeed/staticfiles/
```

---

## 🚀 4. Start Django with Gunicorn

```bash
gunicorn project.wsgi:application --bind 127.0.0.1:8000 --daemon
```

---

## 📄 5. DNS Records

| Type | Hostname                  | Value           |
| ---- | ------------------------- | --------------- |
| A    | aljeed.shuhnaty.com       | 188.166.151.160 |
| A    | admin.aljeed.shuhnaty.com | 188.166.151.160 |

---

## 📅 Final Result

| URL                                                                    | Description          |
| ---------------------------------------------------------------------- | -------------------- |
| [https://aljeed.shuhnaty.com](https://aljeed.shuhnaty.com)             | React Frontend       |
| [https://admin.aljeed.shuhnaty.com](https://admin.aljeed.shuhnaty.com) | Django Admin Panel   |
| [https://aljeed.shuhnaty.com/api/](https://aljeed.shuhnaty.com/api/)   | Backend API (Django) |

---

If you want this as a downloadable file or PDF, let me know.

