# Resources

## Get Resources

* `GET /v1/:account-id/resources` returns an `Array` of **Active Resources**.
* `GET /v1/:account-id/resources/archived` returns an `Array` of **Archived Resources**.

### Query String Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
|limit | 50 | Limit the number of results returned for pagination. To retrieve all the results use `0`.|
|offset | 0 | Offset the results for pagination, starting from the given record number.|
ids[] | null | Only retrieve Resources with the given array of IDs.

**Example:**

To return a page of 30 Resources:
```
https://api.resourceguruapp.com/v1/example-corp/resources?limit=30&offset=0
```

To return resources with IDs 1 and 2:
```
https://api.resourceguruapp.com/v1/example-corp/resources?limit=30&offset=30&ids[]=1&ids[]=2
```

### Response

```json
[
  {
    "id": 1,
    "color": "#CCFF00",
    "name": "Joe Soap",
    "updated_at": "2013-04-30T12:00:00+00:00",
    "url": "https://api.resourceguruapp.com/v1/example-corp/resources/1",
    "resource_type": {
      "id": 1,
      "name": "Name",
      "url": "https://api.resourceguruapp.com/v1/example-corp/resource_types/1"
    },
    "timezone": {
      "name": "London",
      "offset": 0
    }
  },
  {
    "id": 2,
    "color": "#FFCC00",
    "name": "Audi S5",
    "updated_at": "2013-04-30T12:00:00+00:00",
    "url": "https://api.resourceguruapp.com/v1/example-corp/resources/2",
    "resource_type": {
      "id": 1,
      "name": "Name",
      "url": "https://api.resourceguruapp.com/v1/example-corp/resource_types/1"
    },
    "timezone": {
      "name": "London",
      "offset": 0
    }
  }
]
```

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier for a Resource.
color | string | Color used to highlight a Resource.
name | string | Name of a Resource.
updated_at | timestamp | Last updated date and time in ISO 8601.
url | string | URL to view a Resource.
resource_type | hash | Resource Type information. [(Details)](#resource-type-key)
timezone | hash | Timezone this Resource uses. [(Details)](#timezone-key)

#### Resource Type Key

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier for this Resource Type.
name | string | Name of this Resource Type.
url | string | URL shortcut to view this Resource Type.

#### Timezone Key

Key | Type | Description
--- | --- | ---
name | string | Name of this Timezone
offset | integer | Offset in minutes from UTC

## Get Resource

* `GET /v1/:account-id/resources/:id` returns the specified Resource. If the special value `me` is given for the id parameter, it will return the resource for the user that authenticated the request.

```json
{
  "id": 2,
  "archived": false,
  "bookable": true,
  "available_periods": [
    {
      "week_day": 0,
      "start_time": 540,
      "end_time": 600,
      "valid_from": "2013-01-01",
      "valid_until": null
    }
  ],
  "color": "#CCFF00",
  "email": "joesoap@example.com",
  "phone": "12345678",
  "image": "https://resourceguru.s3.amazonaws.com/images/card_69cb-7f96ae8b2e17.png",
  "job_title": "Developer",
  "name": "Joe Soap",
  "notes": "Some notes",
  "updated_at": "2013-04-30T12:00:00+00:00",
  "account": {
    "id": 1,
    "name": "Example Corp",
    "url": "https://api.resourceguruapp.com/v1/accounts/1"
  },
  "resource_type": {
    "id": 1,
    "name": "Name",
    "url": "https://api.resourceguruapp.com/v1/example-corp/resource_types/1"
  },
  "selected_custom_field_options": [
    {
      "id": 1,
      "value": "Projector"
    },
    {
      "id": 2,
      "value": "Whiteboard"
    }
  ],
  "timezone": {
    "name": "London",
    "offset": 0
  },
  "phone": "123 456 7890"
}
```

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier for this Resource.
archived | boolean | If `true`, then this Resource is archived.
bookable | boolean | If `true`, then this Resource is bookable.
color | string | Color used to highlight this Resource.
email | string | Email address for this Resource. Only applicable to Resources linked to User Accounts.
phone | string | Phone number for this Resource.
image | string | Image of this Resource.
job_title | string | Job title on this Resource. Only applicable to Resources linked to User Accounts.
name | string | Name of this Resource.
notes | string | Notes about this Resource.
updated_at | timestamp | Last updated date and time in ISO 8601.
account | hash | -
resource_type | hash | -
selected_custom_field_options | array | Custom field IDs and values. Please note that these are only returned if a value exists for the custom field.
timezone | hash | -

## Get Resource Availability, Time Booked, Time Unbooked, Time on Waiting List and Utilization Rate

Use the [Resource Report endpoint](./reports/resources.md "Resource Report endpoint") to get the following for resources - total availability, time booked, time unbooked, time on waiting list and utilization rate.

## Create a Resource

* `POST /v1/:account-id/resources` will create a new Resource from the parameters passed.

``` javascript
{
  // For non human resources:
  "name": "Meeting Room One",

  // For human resources:
  "first_name": "John",
  "last_name": "Doe",
  "phone": "12345678",
  "email": "user@example.com",
  "invite": true,

  // Meeting rooms only:
  "capacity": 25,

  // Vehicles only:
  "registration_number": 'YK02 OML',


  // Other parameters:
  "resource_type_id": 1, // Retrieved from the resource_types endpoint
  "timezone": "UTC",
  "color": "f0f0f0",
  "bookable": true,
  "notes": "extra details",
  "archived": false,

  // Custom fields are shown in the resource_types endpoint
  "custom_field_option_ids": [ 1, 2, 3 ]
}
```

Key | Type | Description
--- | --- | ---
name | string | The name for a non-human resource.
first_name | string | The first name of a human resource.
last_name | string | The last name of a human resource.
phone | string | The phone number for a human resource.
email | string | The email for a human resource. Required if inviting the user to the account.
invite | boolean | If `true`, the user will be invited into the account via email.
capacity | integer | The capacity of a meeting room resource.
registration_number | string | The registration number of a vehicle.
resource_type_id | integer | The resource type ID retrieved from the [Resource Types endpoint](./resource_types.md).
timezone | string | A valid ActiveSupport::TimeZone name. [Complete list](../timezones.md).
color | string | Color used to highlight this resource.
bookable | boolean | Determines whether the resource is visible in the bookings calendar.
notes | string | Notes about this resource.
archived | boolean | Determines whether the resource is archived.
custom_field_option_ids | integer array | The custom fields selected for the resource. The list of available options is on the [Resource Types endpoint](./resource_types.md).

This will return `201 Created`, along with the current JSON representation of the Resource
if the creation was successful.

If the user does not have access to create a Resource, you'll see `403 Forbidden`.

If the account has hit its limit for the plan, you'll see `422 Unprocessable Entity`.

The "normal availability" for resources created via the API will be created with the default availability settings found in Settings within the app (menu top right with your name on it > Settings > Resources > Default availability). Unfortunately it is not currently possible to specify custom "normal availability" for a resource via the API.

## Update a Resource
* `PUT /v1/:account-id/resources/:id` will update the Resource from the given parameters and
return the JSON representation of the updated Resource. If the user does not have access to
update the project, you'll see `403 Forbidden`.

You can not change the type of a resource in the Update action. You also can not update the timezone directly, instead you can achieve that via the availability endpoint.

## Delete a Resource

* `DELETE /v1/:account-id/:resources/:id` will delete the specified Resource and return `204 No Content`
if that was successful. If the user does not have permission to delete the resource, you'll see `403 Forbidden`

Please note that, when you delete a resource, any future bookings where the resource is the booker will be transferred to the authenticated user. And any future bookings where the resource has been booked as the resource will be deleted.

## Changing availability

- `POST /v1/:account-id/:resources/:id/availability` will change the normal availability and/or the timezone of the resource.

```javascript
{
  "date": "2021-01-01",

  // changing normal weekly availability
  "available_periods": [{
    "week_day": 1,
    "start_time": 540,
    "end_time": 1020
  }],

  // changing timezone
  "timezone": "London",

  // optional clash management options - choose one only
  "allow_waiting": true,
  "delete_invalid_bookings": true
}
```

| Key                     | Type    | Description                                                                                        |
| ----------------------- | ------- | -------------------------------------------------------------------------------------------------- |
| date                    | string  | The ISO 8601 formatted date to apply the availability changes from.                                |
| timezone                | string  | A valid ActiveSupport::TimeZone name. [Complete list](../timezones.md).                            |
| allow_waiting           | boolean | If `true`, bookings that no longer fit the availability changes will be moved to the waiting list. |
| delete_invalid_bookings | boolean | If `true`, bookings that no longer fit the availability changes will be deleted.                   |

If you call the endpoint without any clash management options and there are booking clashes, the server will respond with a `400 Bad Request` and payload detailing the dates and bookings that are clashing. If there were no clashes or you provided a clash management option the server will respond with `200 OK`.
