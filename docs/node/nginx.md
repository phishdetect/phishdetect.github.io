Before configuring the web server, you need to have a TLS certificate ready for use. In most cases using [Let's Encrypt](https://letsencrypt.org) would be sufficient and, after having appropriately configured your DNS records to point to your server, you can use [certbot](https://certbot.eff.org) to generate a certificate.

You can now create an Nginx configuration for your virtual host. You can use the following template and modify accordingly (particularly the domain name and the paths):

```nginx
server {
    listen 80;
    server_tokens off;

    server_name yourdomain.com;
    rewrite ^(.*) https://yourdomain.com$request_uri? permanent;

    access_log /var/www/yourdomain.com/logs/access.log;
    error_log /var/www/yourdomain.com/logs/error.log;
}

server {
    listen 443;
    server_name yourdomain.com;
    server_tokens off;

    root /var/www/yourdomain.com/public/;
    index index.html index.htm;

    location / {
        proxy_pass http://127.0.0.1:7856;
        proxy_redirect off;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }

    location ~ /\.  { return 403; }

    client_max_body_size 512M;
    add_header Referrer-Policy "no-referrer";

    ssl on;
    ssl_certificate /etc/letsencrypt/live/yourdomain.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/yourdomain.com/privkey.pem;
    ssl_session_cache shared:SSL:10m;
    ssl_session_timeout 10m;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers "EECDH+AESGCM:AES256+EECDH";
    ssl_prefer_server_ciphers on;
    add_header Strict-Transport-Security "max-age=63072000; includeSubdomains; preload";
    add_header X-Frame-Options SAMEORIGIN;
    add_header X-Content-Type-Options nosniff;
    ssl_stapling on;
    ssl_stapling_verify on;
    resolver_timeout 5s;

    access_log /var/www/yourdomain.com/logs/access.log;
    error_log /var/www/yourdomain.com/logs/error.log;
}
```
