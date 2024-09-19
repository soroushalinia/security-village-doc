# Authentication

Routes related to authentication. For more details go to [authentication](../auth/index.md) chapter.

### Login

```bash
curl --request POST \
  --url https://api.domain.com/v1/token \
  --header 'Content-Type: application/json' \
  --data '{
	"username": "superuser",
	"password": "superuserpassword"
}'
```

### Logout

```bash
curl --request POST \
  --url https://api.domain.com/v1/token/logout \
  --header 'Authorization: Bearer ACCESS_TOKEN' \
  --header 'Content-Type: application/json' \
  --data '{
	"refresh": "REFRESH_TOKEN"
}'
```

### Refresh token

```bash
curl --request POST \
  --url https://api.domain.com/v1/token/refresh \
  --header 'Content-Type: application/json' \
  --data '{
	"refresh": "REFRESH_TOKEN"
}'
```