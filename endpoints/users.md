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
    "color": "#ef247f",
    "permissions:": "administrator",
    "booking_rights": "manage_all",
    "client_rights:" "manage_all",
    "project_rights:" "manage_all",
    "resource_rights:" "manage_all",
    "report_rights:" "view",
    "owner": "true"
  },
  {
    "id": 2,
    "first_name": "Neil",
    "last_name": "Jones",
    "email": "neil@example.com",
    "image": "https://resourceguru.s3.amazonaws.com/images/card_69cb-7f96ae8b2e17.png",
    "color": "#2654ea"
    "permissions:": "basic_user",
    "booking_rights": "view",
    "client_rights:" "view",
    "project_rights:" "view",
    "resource_rights:" "view",
    "report_rights:" "view",
    "owner:" "false"
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
permissions | string | Permission level of a User(Basic User, Manager, Administrator, Custom).
booking_rights | string | Permissions of a User with regards to Bookings.
client_rights | string | Permissions of a User with regards to Clients.
project_rights | string | Permissions of a User with regards to Projects.
resource_rights | string | Permissions of a User with regards to Resources.
report_rights | string | Permissions of a User with regards to Reports.
owner | boolean | Boolean representing whether a User is the account owner.

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
  "color": "#ffcc00",
  "permissions:": "administrator",
  "booking_rights": "manage_all",
  "client_rights:" "manage_all",
  "project_rights:" "manage_all",
  "resource_rights:" "manage_all",
  "report_rights:" "view",
  "owner": "true"
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
permissions | string | Permission level of a User(Basic User, Manager, Administrator, Custom).
booking_rights | string | Permissions of a User with regards to Bookings.
client_rights | string | Permissions of a User with regards to Clients.
project_rights | string | Permissions of a User with regards to Projects.
resource_rights | string | Permissions of a User with regards to Resources.
report_rights | string | Permissions of a User with regards to Reports.
owner | boolean | Boolean representing whether a User is the account owner.
