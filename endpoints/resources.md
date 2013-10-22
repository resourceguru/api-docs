# Resources

## Get Resources

* `GET /v1/:subdomain/resources` returns an `Array` of **Active Resources**.
* `GET /v1/:subdomain/resources/archived` returns an `Array` of **Archived Resources**.

### Query String Parameters

Parameter | Default | Description
--- | --- | --- | ---
limit | 50 | Limit the number of results returned for pagination. To retrieve all the results use `0`.
offset | 0 | Offset the results for pagination, starting from the given record number.

**Example:**

```
https://api.resourceguruapp.com/v1/example-corp/resources?limit=30&offset=30
```

The above example will return the next 30 Resources.

### Response

```json
[
  {
    "id": 1,
    "color": "#CCFF00",
    "name": "Joe Soap",
    "updated_at": "2013-04-30T12:00:00+00:00",
    "url": "https://api.resourceguruapp.com/v1/example-corp/resources/1",
    "resource_type": {
      "id": 1,
      "name": "Name",
      "url": "https://api.resourceguruapp.com/v1/example-corp/resource_types/1"
    },
    "timezone": {
      "name": "London",
      "offset": 0
    }
  },
  {
    "id": 2,
    "color": "#FFCC00",
    "name": "Audi S5",
    "updated_at": "2013-04-30T12:00:00+00:00",
    "url": "https://api.resourceguruapp.com/v1/example-corp/resources/2",
    "resource_type": {
      "id": 1,
      "name": "Name",
      "url": "https://api.resourceguruapp.com/v1/example-corp/resource_types/1"
    },
    "timezone": {
      "name": "London",
      "offset": 0
    }
  }
]
```

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier for a Resource.
color | string | Color used to highlight a Resource.
name | string | Name of a Resouce.
updated_at | timestamp | Last updated date and time in ISO 8601.
url | string | URL to view a Resource.
resource_type | hash | Resource Type information. [(Details)](#resource-type-key)
timezone | hash | Timezone this Resource uses. [(Details)](#timezone-key)

#### Resource Type Key

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier for this Resource Type.
name | string | Name of this Resource Type.
url | string | URL shortcut to view this Resource Type.

#### Timezone Key

Key | Type | Description
--- | --- | ---
name | string | Name of this Timezone
offset | integer | Offset in minutes from UTC

## Get Resource

* `GET /v1/:subdomain/resource/1` returns the specified Resource.

```json
{
  "id": 2,
  "archived": false,
  "bookable": true,
  "available_periods": [
    {
      "week_day": 0,
      "start_time": 540,
      "end_time": 600,
      "valid_from": 2013-01-01,
      "valid_until": null
    }
  ],
  "color": "#CCFF00",
  "email": "joesoap@example.com",
  "image": "https://resourceguru.s3.amazonaws.com/images/card_69cb-7f96ae8b2e17.png",
  "job_title": "Developer",
  "name": "Joe Soap",
  "notes": "Some notes",
  "updated_at": "2013-04-30T12:00:00+00:00",
  "account": {
    "id": 1,
    "name": "Example Corp",
    "url": "https://api.resourceguruapp.com/v1/accounts/1"
  },
  "resource_type": {
    "id": 1,
    "name": "Name",
    "url": "https://api.resourceguruapp.com/v1/example-corp/resource_types/1"
  },
  "selected_custom_field_options": [
    {
      "id": 1,
      "value": "Projector"
    },
    {
      "id": 2,
      "value": "Whiteboard"
    }
  ],
  "timezone": {
    "name": "London",
    "offset": 0
  }
}
```

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier for this Resource.
archived | boolean | If `true`, then this Resource is archived.
bookable | boolean | If `true`, then this Resource is bookable.
color | string | Color used to highlight this Resource.
email | string | Email address for this Resource. Only applicable to Resources linked to User Accounts.
image | string | Image of this Resource.
job_title | string | Job title on this Resource. Only applicable to Resources linked to User Accounts.
name | string | Name of this Resource.
notes | string | Notes about this Resource.
updated_at | timestamp | Last updated date and time in ISO 8601.
account | hash | -
resource_type | hash | -
selected_custom_field_options | array | -
timezone | hash | -

## Get Resource Availability

Use the [Resource Report endpoint](https://github.com/resourceguru/api-docs/blob/fs-v1-docs/endpoints/reports/resources.md "Resource Report endpoint") to get the following for resources - total availability, time booked, time unbooked, time on waiting list and utilization rate.
