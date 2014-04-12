# Users

## Get Users

* `GET /v1/:subdomain/users` returns an `Array` of **Users**.

### Response

```json
[
  {
    "id": 1,
    "first_name": "Shaun",
    "last_name": "Prestor",
    "email": "shaun@example.com",
    "image": "https://resourceguru.s3.amazonaws.com/images/card_69cb-7f96ae8b2e17.png",
    "color": "#ef247f"
  },
  {
    "id": 2,
    "first_name": "Neil",
    "last_name": "Jones",
    "email": "neil@example.com",
    "image": "https://resourceguru.s3.amazonaws.com/images/card_69cb-7f96ae8b2e17.png",
    "color": "#2654ea"
  }
]
```

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier for a User.
first_name | string | First name of a User.
last_name | string | Last name of a User.
email | string | Email address of a User.
image | string | URL to User's image.
color | string | Hex color code of a User.

## Get User

* `GET /v1/:subdomain/users/:id` returns the specified user. If the special value `me` is given for the id, it will return the user that authenticated the request.

### Response
``` json
{
  "id": 1,
  "first_name": "Shaun",
  "last_name": "Prestor",
  "email": "shaun@example.com",
  "image": "/uploads/development/images/user/1/image/thumb_66343c29-2353-4965-a254-af28ccc53a83.png",
  "color": "#ffcc00"
}
```
Key | Type | Description
--- | --- | ---
id | integer | Unique identifier of the User
first_name | string | First name of the User.
last_name | string | Last name of the User.
email | string | Email address of the User.
image | string | URL to the User's image.
color | string | Hex color code of the User.
