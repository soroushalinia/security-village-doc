# Images

Routes related to images. Images do not have routes for viewers and images will be part of post response
with name of `images`. Also they do not have `deleted_at` field since the files are persisted on filesystem.

> Images also support pagination much like posts
> In order to use pagination use following query parameters to set page size and page number:
> `?page=2&page_size=5`

### Create

```bash
curl --request POST \
  --url https://api.domain.com/v1/admin/images \
  --header 'Authorization: Bearer ACCESS_TOKEN' \
  --header 'Content-Type: multipart/form-data' \
  --form 'file=@~/image.jpg' \
  --form slug=image-slug \
  --form post=post_uuid
```

### Get 

```bash
curl --request GET \
  --url https://api.domain.com/v1/admin/images/:uuid \
  --header 'Authorization: Bearer ACCESS_TOKEN'
```

### Get All 

```bash
curl --request GET \
  --url https://api.domain.com/v1/admin/image \
  --header 'Authorization: Bearer ACCESS_TOKEN'
```

### Partial Update

```bash
curl --request PUT \
  --url https://api.domain.com/v1/admin/tag/:uuid \
  --header 'Authorization: Bearer ACCESS_TOKEN' \
   --header 'Content-Type: multipart/form-data' \
  --form 'file=@~/new_image.jpg' \
  --form slug=new-image-slug \
  --form post=new_post_uuid
```
