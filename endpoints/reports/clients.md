# Clients Report

## Get Report

* `GET /v1/:subdomain/reports/clients` returns a **Clients Report**.

### Required Query String Parameters

Parameter | Description
--- | --- | ---
start_date | Start date in ISO 8601 (`YYYY-MM-DD`).
end_date | End date in ISO 8601 (`YYYY-MM-DD`).

**Example:**

```
https://api.resourceguruapp.com/v1/example-corp/reports/clients?start_date=2013-01-01&end_date=2013-01-07
```

### Clients Report Response

```json
{
  "booked": 32640,
  "waiting_list": 0,
  "max_usage": 3180,
  "clients": [
    {
      "id": 1,
      "name": "Client A",
      "notes": "This is a note",
      "color": "#FFCC00",
      "booked": 0,
      "waiting_list": 0,
      "url": "https://api.resourceguruapp.com/v1/example-corp/clients/1"
    },
    {
      "id": 2,
      "name": "Client B",
      "notes": "",
      "color": "#0264B0",
      "booked": 4800,
      "waiting_list": 0,
      "url": "https://api.resourceguruapp.com/v1/example-corp/clients/2"
    }
  ]
}
```

Key | Type | Description
--- | --- | ---
booked | integer | Total time booked in minutes.
waiting_list | integer | Total time on waiting list in minutes.
max_usage | integer | Max usage for utilization bar. 
clients | array | Report breakdown per Client. [(Details)](#clients-key)

#### Clients Key

Key | Type | Description
--- | --- | ---
id  | integer | Unique identifier of Client.
name | string | Name of this Client.
notes | string | Extra details about this Client.
color | string | Color used to highlight this Client.
booked | integer | Time booked in minutes for this Client.
waiting_list | integer | Time on waiting list in minutes for this Client.
url | string | URL shortcut to view this Client.

# Client Report

## Get Report

* `GET /v1/:subdomain/reports/clients/:client_id` returns a **Client Report**.

### Required Query String Parameters

Parameter | Description
--- | --- | ---
start_date | Start date in ISO 8601 (`YYYY-MM-DD`).
end_date | End date in ISO 8601 (`YYYY-MM-DD`).

**Example:**

```
https://api.resourceguruapp.com/v1/example-corp/reports/clients/242?start_date=2013-01-01&end_date=2013-01-07
```

### Client Report Response

```json
{
  "id": 242,
  "name": "Client A",
  "notes": "This is a note",
  "color": "#FFCC00",
  "booked": 0,
  "waiting_list": 0,
  "url": "https://api.resourceguruapp.com/v1/example-corp/clients/1",
  "resources": [
    {
      "id": 1685,
      "name": "John Doe",
      "image": "/images/fallback/resources/person/thumb_default.png",
      "booked": 5040,
      "waiting_list": 0,
      "job_title": "Developer",
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
id  | integer | Unique identifier of Client.
name | string | Name of this Client.
notes | string | Extra details about this Client.
color | string | Color used to highlight this Client.
booked | integer | Time booked in minutes for this Client.
waiting_list | integer | Time on waiting list in minutes for this Client.
url | string | URL shortcut to view this Client.
resources | array | Report breakdown per Resource. [(Details)](#resources-key)

#### Resources Key

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier of Resource.
name | string | Name of this Resource.
image | string | Image of this Resource.
booked | integer | Time booked in minutes for this Resource.
waiting_list | integer | Time on waiting list in minutes for this Resource.
job_title | string | Job title of the Resource.
resource_type | string | Resource type string.
earliest_available_period | string | Resource earlist available period.
utilization | integer | Utilization ratio between `0` and `1` for this Resource.
url | string | URL shortcut to view this Resource.


