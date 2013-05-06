# Reports

## Get Reports

* `GET /v1/:subdomain/reports/resources` returns **Resource Reports**.
* `GET /v1/:subdomain/reports/projects` returns **Project Reports**.
* `GET /v1/:subdomain/reports/clients` returns **Client Reports**.

### Query String Parameters

Parameter | Description
--- | --- | ---
start_date | Start date in ISO 8601 (YYYY-MM-DD).
end_date | End date in ISO 8601 (YYYY-MM-DD).

**Example:**

```
https://api.resourceguruapp.com/v1/example-corp/reports/resources?start_date=2013-01-01&end_date=2013-01-07
```

### Resource Reports Response

```json
{
  "booked": 32640,
  "unbooked": 3360,
  "availability": 36000,
  "waiting_list": 0,
  "utilization": 0.9,
  "resources": [
    {
      "name": "John Doe",
      "booked": 0,
      "unbooked": 2400,
      "availability": 2400,
      "waiting_list": 0,
      "utilization": 0,
      "url": "https://api.resourceguruapp.com/v1/example-corp/resources/1"
    },
    {
      "name": "Joe Soap",
      "booked": 2400,
      "unbooked": 0,
      "availability": 2400,
      "waiting_list": 0,
      "utilization": 1,
      "url": "https://api.resourceguruapp.com/v1/example-corp/resources/2"
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
utilization | integer | Total Utilization ratio between `0` and `1`.
resources | array | Report breakdown per Resource. [(Details)](#resource-key)

#### Resources Key

Key | Type | Description
--- | --- | ---
booked | integer | Time booked in minutes for this Resource.
unbooked | integer | Time unbooked in minutes for this Resource.
availability | integer | Availability in minutes for this Resource: `booked + unbooked`.
waiting_list | integer | Time on waiting list in minutes for this Resource.
utilization | integer | Utilization ratio between `0` and `1` for this Resource.
url | string | URL shortcut to view this Resource.
