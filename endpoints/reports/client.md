# Client Report

## Get Report

* `GET /v1/:subdomain/reports/clients` returns a **Client Report**.

### Required Query String Parameters

Parameter | Description
--- | --- | ---
start_date | Start date in ISO 8601 (`YYYY-MM-DD`).
end_date | End date in ISO 8601 (`YYYY-MM-DD`).

**Example:**

```
https://api.resourceguruapp.com/v1/example/reports/clients/242?start_date=2013-01-01&end_date=2013-01-07
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
      "name": "Gerhard Koekemoer",
      "image": "/images/fallback/resources/person/thumb_default.png",
      "booked": 5040,
      "unbooked": 52380,
      "availability": 57420,
      "waiting_list": 0
      "utilization": 0.0877742946708464,
      "resource_type": "Person",
      "earliest_available_period": "01 Aug 2014 to 31 Dec 2014 *",
      "url": "https://api.resourceguruapp.com/v1/platform45/resources/1685",
    }
  ]
}
```

Key | Type | Description
--- | --- | ---
id  | integer | Id of client
name | string | Name of this Client.
color | string | Color used to highlight this Client.
booked | integer | Time booked in minutes for this Client.
waiting_list | integer | Time on waiting list in minutes for this Client.
url | string | URL shortcut to view this Client.
resources | array | Report breakdown per Resource. [(Details)](#resources-key)


#### Resources Key

Key | Type | Description
--- | --- | ---
id | integer | Id of Resource
name | string | Name of this Resource.
image | string | Image of this Resource.
booked | integer | Time booked in minutes for this Resource.
unbooked | integer | Time unbooked in minutes for this Resource.
availability | integer | Availability in minutes for this Resource: `booked + unbooked`.
waiting_list | integer | Time on waiting list in minutes for this Resource.
utilization | integer | Utilization ratio between `0` and `1` for this Resource.
url | string | URL shortcut to view this Resource.
resource_type | string | Resource Type String
earliest_available_period | string | Resource Earlist Available Period

