# Headers

Security headers are applied both using middleware in the api itself and using nginx config.

```
X-Frame-Options: "DENY";
X-Content-Type-Options: "nosniff";
X-XSS-Protection: "1; mode=block";
Strict-Transport-Security: "max-age=31536000; includeSubDomains" always;
Content-Security-Policy: "default-src 'self'";
```