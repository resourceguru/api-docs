# Project Report

## Get Report

* `GET /v1/:subdomain/reports/projects/:project_id` returns a **Project Report**.

### Required Query String Parameters

Parameter | Description
--- | --- | ---
start_date | Start date in ISO 8601 (`YYYY-MM-DD`).
end_date | End date in ISO 8601 (`YYYY-MM-DD`).

**Example:**

```
https://api.resourceguruapp.com/v1/example-corp/reports/projects/148?start_date=2013-01-01&end_date=2013-01-07
```

### Project Report Response

```json
{
  "id": 148,
  "name": "Project A",
  "client_name": "",
  "color": "#FFCC00",
  "booked": 0,
  "waiting_list": 0,
  "url": "https://api.resourceguruapp.com/v1/example-corp/projects/1",
  "resources": [
    {
      "id": 1685,
      "name": "John Doe",
      "image": "/images/fallback/resources/person/thumb_default.png",
      "booked": 5040,
      "waiting_list": 0,
      "job_title": "Developer"
      "resource_type": "Person",
      "earliest_available_period": "01 Aug 2014 to 31 Dec 2014 *",
      "utilization": 1,
      "url": "https://api.resourceguruapp.com/v1/example-corp/resources/1685"
    }
  ]
}
```

Key | Type | Description
--- | --- | ---
id  | integer | Unique identifier of Project.
name | string | Name of this Project.
client_name | string | Name of Client that this Project belongs to
color | string | Color used to highlight this Project.
booked | integer | Time booked in minutes for this Project.
waiting_list | integer | Time on waiting list in minutes for this Project.
url | string | URL shortcut to view this Project.
resources | array | Report breakdown per Resource. [(Details)](#resources-key)

#### Resources Key

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier of Resource.
name | string | Name of this Resource.
image | string | Image of this Resource.
booked | integer | Time booked in minutes for this Resource.
waiting_list | integer | Time on waiting list in minutes for this Resource.
job_title | string | Job Title of the Resource
resource_type | string | Resource Type String.
earliest_available_period | string | Resource Earlist Available Period.
utilization | integer | Utilization ratio between `0` and `1` for this Resource.
url | string | URL shortcut to view this Resource.
