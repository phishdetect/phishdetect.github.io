# Configure Nginx

While PhishDetect Node exposes an HTTP service of its own by default on `127.0.0.1:7856`, you should configure your webserver of choice to proxy requests on your production server. This section provides details on how to configure an [Nginx](https://nginx.org) webserver, but you can adapt this configuration to any other webserver such as [Apache](https://httpd.apache.org/).

## Obtain a TLS Certificate

Before configuring the web server, you need to have a TLS certificate ready for use. In most cases using [Let's Encrypt](https://letsencrypt.org) would be sufficient and, after having appropriately configured your DNS records to point to your server, you can use [certbot](https://certbot.eff.org) to generate a certificate. If you wish to do so, you can also acquire a TLS certificate from a trusted authority.

## Nginx Configuration

You can now create an Nginx configuration for your virtual host. You are going to configure it to proxy incoming requests to PhishDetect Node HTTP server by adding the line `proxy_pass http://127.0.0.1:7856;`. If you changed the host or the port number through [command-line parameters](run.md) make sure you change the value of `proxy_pass` accordingly.

You can use the following template and modify accordingly.

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
    ssl_protocols TLSv1.2 TLSv1.3;
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
