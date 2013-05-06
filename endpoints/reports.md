# Reports

## Get Reports

* `GET /v1/:subdomain/reports` returns List of Report URLs.
* `GET /v1/:subdomain/reports/resources` returns **Resource Reports**.
* `GET /v1/:subdomain/reports/projects` returns **Project Reports**.
* `GET /v1/:subdomain/reports/clients` returns **Client Reports**.

### Query String Parameters

Parameter | Default | Description
--- | --- | ---
start_date | Today | Start date in ISO 8601 (YYYY-MM-DD)
end_date | 6 Days from Today | End date in ISO 8601 (YYYY-MM-DD)

### Resource Reports Response

```json
{
  "booked": 32640,
  "unbooked": 3360,
  "total_availability": 36000
  "waiting_list": 0,
  "utilization": 90,
  "resources": [
    {
      "name": "John Doe",
      "booked": 0,
      "unbooked": 2400,
      "total_availability": 2400,
      "waiting_list": 0,
      "utilization": 0
      "url": "https://api.resourceguruapp.com/v1/example-corp/resources/1"
    },
    {
      "name": "Joe Soap",
      "booked": 2400,
      "unbooked": 0,
      "total_availability": 2400,
      "waiting_list": 0,
      "utilization": 100,
      "url": "https://api.resourceguruapp.com/v1/example-corp/resources/2"
    }
  ]
}
```

Key | Type | Description
--- | --- | ---
booked | integer | Total time booked in minutes.
unbooked | integer | Total time unbooked in minutes.
total_availability | integer | Total availability in minutes: `booked + unbooked`.
waiting_list | integer | Total time in waiting list in minutes.
utilization | integer | Total percentage utilization.
resources | array | Report breakdown per Resource. [(Details)](#resource-key)

#### Resources Key

Key | Type | Description
--- | --- | ---
booked | integer | Total time booked in minutes for this Resource.
unbooked | integer | Total time unbooked in minutes for this Resource.
total_availability | integer | Total availability in minutes for this Resource: `booked + unbooked`.
waiting_list | integer | Total time in waiting list in minutes for this Resource.
utilization | integer | Total percentage utilization for this Resource.
url | string | URL shortcut to view this Resource.
