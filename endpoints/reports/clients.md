# Client Report

## Get Report

* `GET /v1/:subdomain/reports/clients` returns a **Client Report**.

### Required Query String Parameters

Parameter | Description
--- | --- | ---
start_date | Start date in ISO 8601 (YYYY-MM-DD).
end_date | End date in ISO 8601 (YYYY-MM-DD).

**Example:**

```
https://api.resourceguruapp.com/v1/example-corp/reports/clients?start_date=2013-01-01&end_date=2013-01-07
```

### Client Report Response

```json
{
  "booked": 32640,
  "waiting_list": 0,
  "clients": [
    {
      "name": "Client A",
      "color": "#E8CB05",
      "booked": 0,
      "waiting_list": 0,
      "url": "https://api.resourceguruapp.com/v1/example-corp/clients/1"
    },
    {
      "name": "Client B",
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
clients | array | Report breakdown per Client. [(Details)](#clients-key)

#### Clients Key

Key | Type | Description
--- | --- | ---
name | string | Name of this Client.
color | string | Color used to highlight this Client.
booked | integer | Time booked in minutes for this Client.
waiting_list | integer | Time on waiting list in minutes for this Client.
url | string | URL shortcut to view this Client.
