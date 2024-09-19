# Users

API Routes related to user management. Superuser is required for user management.
For more details go to [Superuser](../auth/superuser.md) chapter.

### Register

```bash
curl --request POST \
  --url https://api.domain.com/v1/admin/user \
  --header 'Authorization: ACCESS_TOKEN' \
  --header 'Content-Type: application/json' \
  --data '{
	"username": "document",
	"email": "doc@gmail.com",
	"password": "Doc@1234",
	"first_name": "John",
	"last_name": "Doe"
}'
```

### Get 

```bash
curl --request GET \
  --url https://api.domain.com/v1/admin/user/:uuid \
  --header 'Authorization: Bearer ACCESS_TOKEN'
```

### Get All 

```bash
curl --request GET \
  --url https://api.domain.com/v1/admin/user \
  --header 'Authorization: Bearer ACCESS_TOKEN' 
```

### Partial Update

```bash
curl --request PUT \
  --url https://api.domain.com/v1/admin/user/:uuid \
  --header 'Authorization: Bearer ACCESS_TOKEN' \
  --header 'Content-Type: application/json' \
  --data '{
	"password": "new_password",
    "is_active": false,
}'
```

> Note: There is no delete or change password route. in order to change password or disable account use PUT 
> on `https://api.domain.com/v1/admin/user/:uuid` with `is_active` and `password`. First name, last name,
> email and username also can be changed from here. refer to [Authentication](../auth/index.md) chapter.