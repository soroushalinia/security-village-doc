# Nginx

There is a preconfigured `nginx.conf` file in source code repository for using nginx.
You can use it for deployment and nginx config. There is also an template for cms inside
this document.

Before doing anything, make sure you have generated tls certificates using let's encrypt.
Refer to [TLS](./tls.md) if you haven't done so.

Generate a file in nginx `site-enabled` folder with your domain:

```
sudo nano /etc/nginx/sites-enabled/api.domain.com
```

Copy all content of the `nginx.conf` file from soruce into new file and change every instance 
of `api.domain.com` to your actual domain.


This configuration serves a root file at /var/www/html which you can change. Sets ssl certificates generated with let's encrypt from previous step, and sets ssl configuration.

Then it sets security headers exactly as mentioned in Security Headers

Static images uploaded by user are also served from /var/www/images at path https://api.domain.com/images Every request sent to nginx will be forwared to localhost:8000 which is the cms api

You can also customize error pages within this file.

Here is an template configuration for nginx with let's encrypt.
```nginx
server {
    listen 80;
    server_name api.domain.com;
    root /var/www/html;

    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name api.domain.com;
    root /var/www/html;

    ssl_certificate /etc/letsencrypt/live/api.domain.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/api.domain.com/privkey.pem;

    ssl_protocols TLSv1.3 TLSv1.2;
    ssl_ciphers 'TLS_AES_128_GCM_SHA256:TLS_AES_256_GCM_SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384';
    ssl_prefer_server_ciphers on;
    ssl_dhparam /etc/ssl/certs/dhparam.pem;
    ssl_session_cache shared:SSL:10m;
    ssl_session_timeout 10m;
    ssl_stapling on;
    ssl_stapling_verify on;

    add_header X-Frame-Options "DENY";
    add_header X-Content-Type-Options "nosniff";
    add_header X-XSS-Protection "1; mode=block";
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
    add_header Content-Security-Policy "default-src 'self'";

    location /images/ {
        alias /var/www/images/;
        autoindex off;
        access_log off; 
        expires max; 
        add_header Cache-Control "public";
    }

    location / {
        proxy_pass http://localhost:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Forwarded-Port $server_port;
    }

    error_page 404 /404.html;
    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
        root /var/www/html;
    }
}
```