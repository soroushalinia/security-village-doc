# Admin

CMS allows for two types of author user: normal and superuser.
Only superuser has the ability to create and manage other users and deactivate them.
Before registering any other user the superuser has to be manually created through django `createsuperuser` command itself:

```shell
python3 manage.py createsuperuser
```

The difference between superuser and normal user is the `is_superuser` field which cannot be changed once the user is created.

There is no way to delete any users through api however it can be deactivated to prevent login and showing the posts from that user.
In order to achieve this only change the `is_active` field through user api as a superuser. 

Refer to [User API](../routes/users.md) for more information.