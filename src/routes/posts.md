# Posts

Routes related to posts.

> Unlike tags, posts support pagination
> In order to use pagination use following query parameters to set page size and page number:
> `?page=2&page_size=5`

## Author routes

### Create 

```bash
curl --request POST \
  --url https://api.domain.com/v1/admin/post \
  --header 'Authorization: Bearer ACCESS_TOKEN' \
  --header 'Content-Type: application/json' \
  --data '{
	"title": "Title",
	"slug": "Slug",
	"content": "Markdown",
	"tags": [
		"tag_uuid_1"
		"tag_uuid_2"
	],
	"author": "author_uuid"
}'
```

### Get 

```bash
curl --request GET \
  --url https://api.domain.com/v1/admin/post/:uuid \
  --header 'Authorization: Bearer ACCESS_TOKEN'
```

### Get All 

```bash
curl --request GET \
  --url https://api.domain.com/v1/admin/post?page=2&page_size=5 \
  --header 'Authorization: Bearer ACCESS_TOKEN'
```

### Partial Update

```bash
curl --request PUT \
  --url https://api.domain.com/v1/admin/post/:uuid \
  --header 'Authorization: Bearer ACCESS_TOKEN' \
  --header 'Content-Type: application/json' \
  --data '{
	"content": "Updated content",
    "deleted_at": null
}'
```

## Viewer routes 


### Get 

```bash
curl --request GET --url https://api.domain.com/v1/post/:uuid
```

### Get All 

```bash
curl --request GET --url https://api.domain.com/v1/post?page=2&page_size=5
```

### Get All by Tag 

```bash
curl --request GET --url https://api.domain.com/v1/post/tag/:tag_uuid?page=2&page_size=5
```