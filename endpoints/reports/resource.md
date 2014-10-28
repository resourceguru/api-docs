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
  "job_title": ""
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
id  | string | Unique identifier of resource.
name | string | Name of resource.
image | string | Resource Avatar.
booked | integer | Total time booked in minutes.
unbooked | integer | Total time unbooked in minutes.
availability | integer | Total availability in minutes: `booked + unbooked`.
waiting_list | integer | Total time on waiting list in minutes.
utilization | integer | Total Utilization ratio between `0` and `1`.
url | string | URL shortcut to view this Resource.
resource_type | string | Resource Type String.
earliest_available_period | string | Resource Earliest Available Period.
job_title | string | Job Title of the Resource.
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
max_usage | integer | Max Usage for utilization bar.

#### Clients Keys
Key | Type | Description
--- | --- | ---
name | string | Name of client.
color  | string | Color of client.
booked | integer | Total time booked in minutes.
waiting_list | integer | Total time on waiting list in minutes.
max_usage | integer | Max Usage for utilization bar.
