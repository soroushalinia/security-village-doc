# Enviroment Variables

Template `.env` file with example placeholder values that can be used if you are using docker.

```env
SECRET_KEY=secretkey-insecure@1234
REDIS_URL=redis://redis:6379/1
ALLOWED_HOSTS=https://api.domain.com
DATABASE_DSN=dbname=cms host=postgres port=5432 user=postgres password=12345678
CORS_ALLOWED_ORIGINS=https://api.domain.com
POSTGRES_DB=cms
POSTGRES_USER=postgres
POSTGRES_PASSWORD=12345678
```

> You must change all values before deploying to production.

> You can use `https://djecrety.ir/` to generate secret key for django 

## Security

If `.env` file security is a concern you can use `GPG` to encrypt and decrypt the file whenever needed
and safely store all credentials.