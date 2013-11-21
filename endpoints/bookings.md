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
      "color": "#FFCC00",
      "email": "Email",
      "name": "Name"
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
duration | integer | Duration in minutes for the Booking Duration.
end_time | integer | End time in minutes from midnight for this Booking Duration. (Can be `null`)
start_time | integer | Start time in minutes from midnight for this Booking Duration. (Can be `null`)
waiting | boolean | If `true`, then this Booking Duration is on the Waiting List.


## Get Bookings for a Specific Project

* `GET /v1/:subdomain/projects/:project_id/bookings` returns an `Array` of **Bookings** for the specified project.

## Get Bookings for a Specific Client

* `GET /v1/:subdomain/clients/:client_id/bookings` returns an `Array` of **Bookings** for the specified client.

## Get Bookings for a Specific Resource

* `GET /v1/:subdomain/resources/:resource_id/bookings` returns an `Array` of **Bookings** for the specified resource.


## Create a Booking

* `POST /v1/:subdomain/bookings` will create a new Booking from the parameters passed.

```json
{
  "start_date": "2013-03-01",
  "end_date": "2013-03-31",
  "duration": 20,
  "resource_id": 1,
  "allow_waiting": true,
  "project_id": 1,
  "client_id": 2,
  "details": "Optional details"
}
```

Key | Type | Description
--- | --- | ---
start_date | string | The ISO 8601 formatted first date for the booking.
end_date | string | The ISO 8601 formatted last date for the booking.
duration | integer | The length of the booking
start_time | integer | For time-specific bookings - the time the booking must start, in minutes from midnight.
resource_id | integer | The resource that is being booked
allow_waiting | boolean | Optional: The booking will fail validation if it has to go onto the waiting list, unless this parameter is supplied and is `true`
project_id | integer | Optional: The project the booking is assigned to. Pass either project_id or client_id, not both.
client_id | integer | Optional: The client the booking is assigned to. Pass either project_id or client_id, not both.
details | string | Optional plain text details for the booking.
This will return `201 Created`, with the location of the new Booking in the Location header
along with the current JSON representation of the Booking if the creation was successful.
If there is a problem with the request, you'll get a `422 Unprocessable Entity` and get a JSON object explaining the validation errors.
If the user does not have access to update the Booking, you'll see `403 Forbidden`.

## Update a Booking

* `PUT /v1/:subdomain/bookings/1` will update the Booking from the parameters passed and return
the JSON representation of the updated Booking. If the user does not have access to update
the Booking, you'll see `403 Forbidden`.

## Delete a Booking

* `DELETE /v1/:subdomain/bookings/1` will delete the Booking specified and return `204 No Content`
if that was successful. If the user does not have access to delete the Booking, you'll see `403 Forbidden`.
