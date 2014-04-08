# Users

## Get Users

* `GET /v1/users` returns an `Array` of **Users**.

### Response

```json
[
  {
    "id": 1,
    "first_name": "Shaun",
    "last_name": "Prestor",
    "image": "https://resourceguru.s3.amazonaws.com/images/card_69cb-7f96ae8b2e17.png",
    "color": "#ef247f"
  },
  {
    "id": 2,
    "first_name": "Neil",
    "last_name": "Jones",
    "image": "https://resourceguru.s3.amazonaws.com/images/card_69cb-7f96ae8b2e17.png",
    "color": "#2654ea"
  }
]
```

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier for a User.
first_name | string | First name of a User.
last_name | string | Last  name of a User.
image | string | URL to User image.
color | string | Hex color code of a User.
