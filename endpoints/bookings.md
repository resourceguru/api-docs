# Bookings

## Get Bookings

* `GET /v1/:subdomain/bookings` returns an `Array` of **Bookings**.

### Query String Parameters

Parameter | Default | Description
--- | --- | --- | ---
start_date |  | Set a start_date for a range of Bookings
end_date |  | Set and end_date for a range of Bookings
limit | 50 | Limit the number of results returned for pagination. To retrieve all the results use `0`.
offset | 0 | Offset the results for pagination, starting from the given record number.

**Example:**

```
https://api.resourceguruapp.com/v1/example-corp/bookings?start_date=2013-01-01&end_date=2013-04-10
```

The above example will return the next Boookings between `2013-01-01` and `2013-04-10`

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
      "color": "#FFCC00"
      "email": "Email",
      "name": "Name",
    },
    "durations": [
      {
        "date": "2013-01-01",
        "duration": 180,
        "end_time": 720,
        "start_time": 540,
        "waiting": false
      },
      {
        "date": "2013-01-02",
        "duration": 180,
        "end_time": 720,
        "start_time": 540,
        "waiting": false
      },
      {
        "date": "2013-01-03",
        "duration": 180,
        "end_time": 720,
        "start_time": 540,
        "waiting": false
      }
    ]
  }
]
```

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier for a Booking.
client_id | integer | Unique identifier of the Client this Booking is for. (Can be `null`)
project_id | integer | Unique identifier of the Project this Booking is for. (Can be `null`)
notes | string | Notes about this Booking.
project_id | integer | Unique identifier of the Resource this Booking is for.
booker | hash | Booker information. [(Details)](#booker-key)
durations | array | Bookings Durations information. [(Details)](#durations-key)

#### Booker Key

Key | Type | Description
--- | --- | ---
color | string | Color used to highlight this Booker.
email | string | Email address of this Booker.
name | string | Name of this Booker.

#### Durations Key

Key | Type | Description
--- | --- | ---
date | string | The date for this booking in ISO 8601.
duration | string | Duration in minutes for the Booking Duration.
end_date | string | End time in minutes from midnight for this Booking Duration. (Can be `null`)
start_date | string | Start time in minutes from midnight for this Booking Duration. (Can be `null`)
waiting | boolean | If `true`, then this Booking Duration is on the Waiting List.
