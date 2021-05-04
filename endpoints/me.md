# 🚨 🚨 🚨 Deprecated: please see [Resource Guru API documentation](https://resourceguruapp.com/docs/api) instead

## Get the current User

Use this endpoint to get information about the currently authenticated user.

* `GET /v1/me`

### Response
``` json
{
  "id": 1,
  "first_name": "Shaun",
  "last_name": "Prestor",
  "email": "shaun@example.com",
  "image": "/uploads/development/images/user/1/image/thumb_66343c29-2353-4965-a254-af28ccc53a83.png",
  "timezone": "Pacific Time (US & Canada)",
  "last_login_at": "2014-08-17T21:38:09.000Z",
  "last_logout_at": "2014-08-15T10:56:32.000Z",
  "last_activity_at": "2013-06-26T17:30:11.000Z",
  "activation_state": "active",
  "created_at": "2012-06-05T21:17:19.000Z",
  "updated_at": "2014-08-19T09:27:52.000Z",  
  "last_product_update_read_at": "2018-05-18T10:40:34.000Z"
}
```
Key | Type | Description
--- | --- | ---
id | integer | Unique identifier of the User
first_name | string | First name of the User.
last_name | string | Last name of the User.
email | string | Email address of the User.
image | string | URL to the User's image.
timezone | string | Timezone of a User.
last_login_at | string | Last login timestamp for a User.
last_logout_at | string | Last log out timestamp for a User.
last_activity_at | string | Last activity timestamp for a User.
activation_state | string | Activation state of a User.
created_at | string | Timestamp when a User was created.
updated_at | string | Timestamp when a User was updated.
last_product_update_read_at | timestamp | When user last read a product update
