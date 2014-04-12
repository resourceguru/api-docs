## Get the current User

* `GET /v1/me`

### Response
``` json
{
  "id": 1,
  "first_name": "Shaun",
  "last_name": "Prestor",
  "email": "shaun@example.com",
  "image": "/uploads/development/images/user/1/image/thumb_66343c29-2353-4965-a254-af28ccc53a83.png"
}
```
Key | Type | Description
--- | --- | ---
id | integer | Unique identifier of the User
first_name | string | First name of the User.
last_name | string | Last name of the User.
email | string | Email address of the User.
image | string | URL to the User's image.
