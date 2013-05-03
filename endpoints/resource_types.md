# Resource Types

## Get Resource Types

* `GET /v1/:subdomain/resource_types` returns an `Array` of **Resource Types**.
* `GET /v1/:subdomain/resource_types/1` returns a specified **Resource Type**.

### Response

```json
[
  {
    "id": 1,
    "name": "Need a good example here?",
    "human": true,
    "custom_fields" = [
      {
        "id": 1,
        "name": "Need a good example here?",
        "custom_field_options": [
          {
            "id": 1,
            "value": "Need a good example here?"
          }
          {
            "id": 2,
            "value": "Need a good example here?"
          }
        ]
      },
      {
        "id": 2,
        "name": "Need a good example here?",
        "custom_field_options": [
          {
            "id": 3,
            "value": "Need a good example here?"
          }
          {
            "id": 4,
            "value": "Need a good example here?"
          }
        ]
      }
    ]
  }
]
```

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier for a Resource Type.
name | string | Name of a Resouce Type.
human | boolean | If `true`, then this Resource Type is a person.
custom_fields | array | -

#### Custom Fields Key

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier for a Custom Field.
name | string | Name of a Custom Field.
custom_field_options | array | -

#### Custom Field Options

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier for a Custom Field Option.
name | string | Name of a Custom Field Option.
