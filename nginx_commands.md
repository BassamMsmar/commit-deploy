# Nginx Commands

- `sudo systemctl restart nginx` : Restart Nginx.
- `sudo nginx -t` : Test config.
- `sudo nano /etc/nginx/sites-available/default` : Edit config file.

## SSL
- `sudo certbot --nginx` : Get SSL.
- `sudo certbot renew` : Renew SSL.
- `sudo certbot certonly --webroot` : Get SSL.
- `sudo certbot renew --webroot` : Renew SSL.
- `sudo certbot renew --dry-run` : Test renewal.    