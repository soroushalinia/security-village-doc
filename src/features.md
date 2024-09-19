# Feautres

### User Types

1. **Superuser Author**:
   - Can manage other users (activate/deactivate accounts).
   - Has full control over posts, tags, and images.
   - Has access to all data, including soft-deleted posts and tags.
   
2. **Normal Author**:
   - Can create and manage their own posts and tags.
   - Can upload images, reference them in posts, and delete them.
   - Can only view soft-deleted posts and tags created by themselves.


### Entities and Fields

#### Tag
- **ID**: `uuid` (Primary Key)
- **Name**: `string`
- **Soft Delete**: A `deleted_at` timestamp field indicates soft deletion. If set, the tag is hidden from viewers but still accessible by the author who deleted it.

> Soft deletion is indicated by setting the deleted_at field to a timestamp.

#### Post
- **ID**: `uuid` (Primary Key)
- **Title**: `string`
- **Slug**: `string` (Used for frontend routing and identification)
- **Content**: `markdown/string` (Sanitized and escaped before being exposed via the API)
- **Images**: Post responses contain an `images` field with image slugs that are later replaced by actual URLs on the frontend.
- **Soft Delete**: Posts have a `deleted_at` timestamp field. When set, the post is hidden from viewers but can be accessed by its author.

#### User (AuthorUser)
- **ID**: `uuid` (Primary Key)
- **Email**: `string`
- **First Name**: `string`
- **Last Name**: `string`
- **Username**: `string`
- **Password**: `string` (Must meet security criteria: at least 8 characters, include uppercase, lowercase letters, digits and symbols)
- **Is Active**: A field that determines whether the author user is active. Superusers can toggle this field.
- **Is Superuser**: A field that determines whether the author user is superuser. This field is immutable after user creation.

#### Image
- **ID**: `uuid` (Primary Key)
- **Slug**: `string` (Unique slug for the image)
- **URL**: `string` (The file name is stored, and the image is statically served via Nginx)
- **File**: Only authors can upload images. Uploaded images are referenced in post content using their slug. Viewers only see image references in post responses, which are later resolved to actual URLs by the frontend.

### Soft Deletion

Both **Posts** and **Tags** support soft deletion using a `deleted_at` field:
- If a tag or post is soft deleted, it is hidden from viewers but remains accessible to the authors who created it or superusers.
- Superusers have access to all data, including soft-deleted content.

**Users**, however, are deactivated using the `is_active` field:
- A deactivated user cannot log in or create/manage content but its posts are viewable.
- Superusers can toggle the `is_active` flag to reactivate or deactivate users.

### Image Handling

Images are only uploaded and managed by authors:
- The **image slug** is used as a placeholder in the post content.
- In post responses, only the slug and a reference URL (the file name) are included.
- Viewers do not see the image files directly; they only receive image URLs when fetching posts which should be replaced in frontend.

### Content Formatting

- All post content is written in **markdown** and is sanitized and escaped before being exposed through the API to prevent security vulnerabilities like XSS.
- Images in markdown content are referenced using their slug, and the frontend will replace the slug with the actual URL for rendering.

### Security Features

- **Sanitization**: All values including markdown content is sanitized on the backend before being returned to clients.
- **Static Image Serving**: Images are statically served using Nginx to optimize performance and security whilist not relying on third party services.
- **Password Requirements**: At least 8 characters long, including at least one uppercase letter, one lowercase letter, and one digit.
- **Security Headers**: All required security headers are applied through middleware and nginx to prevent common attacks like XSS and more.
- **Obfuscation**: Code is properly obfuscated using PyArmor.
- **Rate Limit**: Rate limit is applied to prevent attacks (like brute-force login attempts, DDOS attacks, etc.) and abuse.
- **TLS**: Backend is served with latest ssl (`TLSv1.3`).
- **Authentication**: JWT Bearer authentication with access and refresh token pair with report about last successful/failed login attempt.
