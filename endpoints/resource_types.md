# Resource Types

## Get Resource Types

* `GET /v1/:subdomain/resource_types` returns an `Array` of **Resource Types**.
* `GET /v1/:subdomain/resource_types/1` returns a specified **Resource Type**.

### Response

```json
[
  {
    "id": 1,
    "name": "Meeting Room",
    "human": false,
    "custom_fields": [
      {
        "id": 1,
        "name": "Facilities",
        "custom_field_options": [
          {
            "id": 1,
            "value": "Projector"
          }
          {
            "id": 2,
            "value": "Whiteboard"
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
custom_fields | array | Custom Fields for this Resource Type. [(Details)](#custom-fields-key)

#### Custom Fields Key

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier for a Custom Field.
name | string | Name of a Custom Field.
custom_field_options | array | Custom Field Options for this Custom Field. [(Details)](#custom-field-options-key)

#### Custom Field Options Key

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier for a Custom Field Option.
name | string | Name of a Custom Field Option.
