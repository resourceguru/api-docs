# Projects Report

## Get Report

* `GET /v1/:subdomain/reports/projects` returns a **Projects Report**.

### Required Query String Parameters

Parameter | Description
--- | --- | ---
start_date | Start date in ISO 8601 (`YYYY-MM-DD`).
end_date | End date in ISO 8601 (`YYYY-MM-DD`).

**Example:**

```
https://api.resourceguruapp.com/v1/example-corp/reports/projects?start_date=2013-01-01&end_date=2013-01-07
```

### Projects Report Response

```json
{
  "booked": 32640,
  "waiting_list": 0,
  "max_usage": 3180,
  "projects": [
    {
      "id": 148,
      "name": "Project A",
      "client_name": "Client A",
      "client_id": 12,
      "color": "#FFCC00",
      "booked": 0,
      "waiting_list": 0,
      "url": "https://api.resourceguruapp.com/v1/example-corp/projects/1",
    },
    {
      "id": 149,
      "name": "Project B",
      "client_name": "Client A",
      "client_id": 12,
      "color": "#CCFF00",
      "booked": 4800,
      "waiting_list": 0,
      "url": "https://api.resourceguruapp.com/v1/example-corp/projects/2",
    }
  ]
}
```

Key | Type | Description
--- | --- | ---
booked | integer | Total time booked in minutes.
waiting_list | integer | Total time on waiting list in minutes.
max_usage | integer | Max Usage for utilization bar. 
projects | array | Report breakdown per Project. [(Details)](#projects-key)

#### Projects Key

Key | Type | Description
--- | --- | ---
id  | integer | Unique identifier of Project.
name | string | Name of this Project.
client_name | string | Name of Client that this Project belongs to
client_id | string | Unique identifier of Client that this Project belongs to 
color | string | Color used to highlight this Project.
booked | integer | Time booked in minutes for this Project.
waiting_list | integer | Time on waiting list in minutes for this Project.
url | string | URL shortcut to view this Project.
