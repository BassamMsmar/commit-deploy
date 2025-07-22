# build project from source frontend
```
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -

sudo apt-get install -y nodejs

node -v
npm -v

cd /var/www/shuhnaty/frontend
npm install
npm run build
```

# =================nginx==========================
```
sudo nano /etc/nginx/sites-available/shuhnaty.com
```

```
server {
    listen 80;
    server_name shuhnaty.com www.shuhnaty.com;

    root /var/www/shuhnaty/frontend;
    index index.html;

    location / {
        try_files $uri /index.html;
    }

    location /api/ {
        proxy_pass http://127.0.0.1:8000/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

## test nginx
```
sudo nginx -t
```

## reload nginx
```
sudo systemctl reload nginx
```