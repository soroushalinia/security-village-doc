# Tags

Routes related to tags.

> Tags do not support pagination.

## Authors routes

### Create

```bash
curl --request POST \
  --url https://api.domain.com/v1/admin/tag \
  --header 'Authorization: ACCESS_TOKEN' \
  --header 'Content-Type: application/json' \
  --data '{
	"name": "New tag",
}'
```

### Get 

```bash
curl --request GET \
  --url https://api.domain.com/v1/admin/tag/:uuid \
  --header 'Authorization: Bearer ACCESS_TOKEN'
```

### Get All 

```bash
curl --request GET \
  --url https://api.domain.com/v1/admin/tag \
  --header 'Authorization: Bearer ACCESS_TOKEN'
```

### Partial Update

```bash
curl --request PUT \
  --url https://api.domain.com/v1/admin/tag/:uuid \
  --header 'Authorization: Bearer ACCESS_TOKEN' \
  --header 'Content-Type: application/json' \
  --data '{
	"name": "Updated name",
}'
```

## Viewer routes 


### Get 

```bash
curl --request GET --url https://api.domain.com/v1/admin/tag/:uuid
```

### Get All 

```bash
curl --request GET --url https://api.domain.com/v1/tag
```