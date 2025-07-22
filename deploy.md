# update packages

`apt update && apt upgrade -y`

## install python - env 

`apt install python3-pip python3-venv python3-dev build-essential libpq-dev nginx git -y`

## clone project

`git clone https://github.com/your-repo/your-project.git`

## create venv

`cd your-project`
`python3 -m venv venv`
`source venv/bin/activate`

## install requirements

`pip install -r requirements.txt`

## run server

`python manage.py runserver`

## install postgresql
`apt install postgresql postgresql-contrib -y`

## create postgres user and database
`sudo -u postgres psql`

CREATE USER admin WITH PASSWORD 'Aa654321';
CREATE DATABASE aljeed_db OWNER admin;
GRANT ALL PRIVILEGES ON DATABASE aljeed_db TO admin;

## exit postgres
\q


## =====================gunicorn====================
## install gunicorn
`pip install gunicorn`


## run gunicorn
`gunicorn --workers 3 --bind 127.0.0.1:8000 project.wsgi:application`

## run in background && setting servicename
`sudo nano /etc/systemd/system/gunicorn.service`


## context gunicorn
`
[Unit]
Description=gunicorn daemon
After=network.target

[Service]
User=root
Group=www-data
WorkingDirectory=/var/www/shuhnaty360/backend
ExecStart=/var/www/shuhnaty360/venv/bin/gunicorn \
          --workers 3 \
          --bind 127.0.0.1:8000 \
          project.wsgi:application

[Install]
WantedBy=multi-user.target
`

## important commit 
sudo systemctl daemon-reexec &&
sudo systemctl daemon-reload &&
sudo systemctl start gunicorn &&
sudo systemctl enable gunicorn &&
&& sudo systemctl status gunicorn

## status
sudo systemctl status gunicorn




## install nginx
`apt install nginx -y`

## create nginx service
`nano /etc/nginx/sites-available/myproject`


## context nginx

`
server {
    listen 80;
    server_name shuhnaty.com www.shuhnaty.com;

    location = /favicon.ico { access_log off; log_not_found off; }

    location /static/ {
        root /opt/backend;
    }

    location /media/ {
        root /opt/backend;
    }

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
`
## important commit 
ln -s /etc/nginx/sites-available/myproject /etc/nginx/sites-enabled 
nginx -t
systemctl restart nginx
ufw allow 'Nginx Full' 

## status
sudo systemctl status nginx

## nginx logs
sudo journalctl -f -u nginx

## =====================certbot====================
## install certbot
`sudo apt install certbot python3-certbot-nginx -y`

## run certbot
`sudo certbot --nginx -d shuhnaty.com -d www.shuhnaty.com`

## statusgit 
sudo systemctl status certbot

## certbot logs
sudo journalctl -f -u certbot

##
