# Resources Report

## Get Report

* `GET /v1/:subdomain/reports/resources` returns a **Resources Report**.

### Required Query String Parameters

Parameter | Description
--- | --- | ---
start_date | Start date in ISO 8601 (`YYYY-MM-DD`).
end_date | End date in ISO 8601 (`YYYY-MM-DD`).

**Example:**

```
https://api.resourceguruapp.com/v1/example-corp/reports/resources?start_date=2013-01-01&end_date=2013-01-07
```

### Resources Report Response

```json
{
  "booked": 32640,
  "unbooked": 3360,
  "availability": 36000,
  "waiting_list": 0,
  "utilization": 0.9,
  "resources": [
    {
      "id": "1",
      "name": "John Doe",
      "image": "https://resourceguru.s3.amazonaws.com/images/card_69cb-7f96ae8b2e17.png",
      "booked": 0,
      "unbooked": 2400,
      "availability": 2400,
      "waiting_list": 0,
      "utilization": 0,
      "url": "https://api.resourceguruapp.com/v1/example-corp/resources/1",
      "resource_type": "Person",
      "earliest_available_period": "25 Aug 2014 - 31 Aug 2014",
      "job_title": "Developer",
      "custom_fields": [] 
    },
    {
      "id": "2",
      "name": "Joe Soap",
      "image": "https://resourceguru.s3.amazonaws.com/images/card_12cb-7f968wehjfi2e17.png",
      "booked": 2400,
      "unbooked": 0,
      "availability": 2400,
      "waiting_list": 0,
      "utilization": 1,
      "url": "https://api.resourceguruapp.com/v1/example-corp/resources/2",
      "resource_type": "Person",
      "earliest_available_period": "25 Aug 2014 - 31 Aug 2014",
      "job_title": null,
      "custom_fields": {
        "22": [
          "33"
        ]
      }
    }
  ]
}
```

Key | Type | Description
--- | --- | ---
booked | integer | Total time booked in minutes.
unbooked | integer | Total time unbooked in minutes.
availability | integer | Total availability in minutes: `booked + unbooked`.
waiting_list | integer | Total time on waiting list in minutes.
utilization | integer | Total utilization ratio between `0` and `1`.
resources | array | Report breakdown per Resource. [(Details)](#resources-key)

#### Resources Key

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier of Resource.
name | string | Name of this Resource.
image | string | Image of this Resource.
booked | integer | Time booked in minutes for this Resource.
unbooked | integer | Time unbooked in minutes for this Resource.
availability | integer | Availability in minutes for this Resource: `booked + unbooked`.
waiting_list | integer | Time on waiting list in minutes for this Resource.
utilization | integer | Utilization ratio between `0` and `1` for this Resource.
url | string | URL shortcut to view this Resource.
resource_type | string | Resource type string.
earliest_available_period | string | Resource earliest available period.
job_title | string | Job title of the Resource.
custom_fields | array | All custom field ids for resource. [(Details)](#custom-fields-key)

#### Custom Fields Key

#### The custom fields array contains the id of the custom field and nested within is the selected custom field option for this resource

**Example:**

```json
"custom_fields": {
  "108": [
    "232"
  ]
}
```

# Resource Report

## Get Report

* `GET /v1/:subdomain/reports/resource/:resource_id` returns a **Resource Report**.

### Required Query String Parameters

Parameter | Description
--- | --- | ---
start_date | Start date in ISO 8601 (`YYYY-MM-DD`).
end_date | End date in ISO 8601 (`YYYY-MM-DD`).

**Example:**

```
https://api.resourceguruapp.com/v1/example-corp/reports/resource/1685?start_date=2013-01-01&end_date=2013-01-07
```

### Resource Report Response

```json
{
  "id": 1364,
  "name": "Jane Doe",
  "image": "/images/fallback/resources/person/thumb_default.png",
  "booked": 240,
  "unbooked": 2760,
  "availability": 3000,
  "waiting_list": 0,
  "utilization": 0.08,
  "url": "https://api.resourceguruapp.com/v1/example-corp/resources/1364",
  "resource_type": "Person",
  "earliest_available_period": "",
  "job_title": "",
  "projects": [
    {
      "name": "No project assigned",
      "client_name": "",
      "color": "#bfbfbf",
      "booked": 240,
      "waiting_list": 0,
      "max_usage": 240
    }
  ],
  "clients": [
    {
      "name": "No client assigned",
      "color": "#bfbfbf",
      "booked": 240,
      "waiting_list": 0,
      "max_usage": 240
    }
  ]
  }
}
```
#### Resource Keys

Key | Type | Description
--- | --- | ---
id  | string | Unique identifier of Resource.
name | string | Name of Resource.
image | string | Resource avatar.
booked | integer | Total time booked in minutes.
unbooked | integer | Total time unbooked in minutes.
availability | integer | Total availability in minutes: `booked + unbooked`.
waiting_list | integer | Total time on waiting list in minutes.
utilization | integer | Total utilization ratio between `0` and `1`.
url | string | URL shortcut to view this Resource.
resource_type | string | Resource type string.
earliest_available_period | string | Resource earliest available period.
job_title | string | Job title of the Resource.
projects | array | Report breakdown per Project. [(Details)](#projects-key)
clients | array | Report breakdown per Clients. [(Details)](#client-key)

#### Projects Keys
Key | Type | Description
--- | --- | ---
name | string | Name of project.
client_name | string | Name of client if there is one.
color  | string | Color of project.
booked | integer | Total time booked in minutes.
waiting_list | integer | Total time on waiting list in minutes.
max_usage | integer | Max usage for utilization bar.

#### Clients Keys
Key | Type | Description
--- | --- | ---
name | string | Name of client.
color  | string | Color of client.
booked | integer | Total time booked in minutes.
waiting_list | integer | Total time on waiting list in minutes.
max_usage | integer | Max usage for utilization bar.
