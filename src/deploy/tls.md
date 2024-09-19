# TLS

You can use Let's encrypt to generate ssl certificates for nginx.

First install certbox using your package manager.

Debian/Ubuntu based distros:

```bash
sudo apt install certbot python3-certbot-nginx nginx
```

In order to generate the certificate for your domain use following command:

```
sudo certbot --nginx -d api.domain.com
```
> Replace `api.domain.com` with your actual domain.

This generates the certificate in path: `/etc/letsencrypt/live/api.domain.com`

There would be two files:

‍- `/etc/letsencrypt/live/api.domain.com/fullchain.pem`
- `/etc/letsencrypt/live/api.domain.com/privkey.pem`

Then generate dhparam using following command:

```
openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048
```

You can use `certbot.timer` for automatic renewal of the certificate:

```
sudo systemctl enable --now certbot.timer
```
