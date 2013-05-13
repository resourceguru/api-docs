# Bookings

## Get Bookings

* `GET /v1/:subdomain/bookings` returns an `Array` of **Bookings**.

### Query String Parameters

Parameter | Default | Description
--- | --- | --- | ---
start_date | - | Set a start_date for a range of Bookings
end_date | - | Set and end_date for a range of Bookings
limit | 50 | Limit the number of results returned for pagination. To retrieve all the results use `0`.
offset | 0 | Offset the results for pagination, starting from the given record number.

**Example:**

```
https://api.resourceguruapp.com/v1/example-corp/bookings?start_date=2013-01-01&end_date=2013-04-10
```

The above example will return the next Boookings between `2013-01-01` and `2013-  04-10`

### Response

```json
[
  {
    "id": 1,
    "client_id": null,
    "project_id": 1,
    "notes": "Some notes",
    "resource_id": 1,
    "booker": {
      "name": "Name",
      "email": "Email",
      "color": "#FFCC00"
    },
    "durations": [
      {
        "date": "2013-01-01",
        "duration": 180,
        "start_time": 540,
        "end_time": 720
      },
      {
        "date": "2013-01-02",
        "duration": 180,
        "start_time": 540,
        "end_time": 720
      },
      {
        "date": "2013-01-03",
        "duration": 180,
        "start_time": 540,
        "end_time": 720
      }
    ]
  }
]
```

## Notes

`duration`: Minutes
`start_time`: Minutes from midnight, Can be null
`durations[0].start_time`: Minutes from midnight
`durations[0].end_time`: `start_time` + `duration`
