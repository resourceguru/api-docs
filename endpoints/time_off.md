# Time Off

## Get Downtimes

* `GET /v1/:subdomain/downtimes` returns an `Array` of **Downtimes**.

### Query String Parameters

Parameter | Default | Description
--- | --- | --- | ---
resource_ids | | Only retrieve Downtimes for the given resources 
limit | 50 | Limit the number of results returned for pagination. To retrieve all the results use `0`.
offset | 0 | Offset the results for pagination, starting from the given record number.
from | | Set a start date range for Downtimes.
to | | Set an end date range for Downtimes.

**Example:**

```
https://api.resourceguruapp.com/v1/example-corp/downtimes?resource_ids[]=123&resource_ids[]=122&from=2016-02-16&to=2016-02-22
```
The above example will return the next Downtimes between `2016-02-16` and `2016-02-22` where the resource ids are 123 and 122.

### Response

```json
[
	{
		"account_id": 1,
		"created_at": "2016-02-16T12:55:19.072Z",
		"creator_id": 2,
		"deleted": false,
		"details": "Christmas Eve",
		"downtime_type_id": 3,
		"end_time": 1440,
		"from": "2016-12-25",
		"id": 123,
		"leave": null,
		"resource_ids": {
			"0": "123"
		},
		"start_time": 0,
		"state": "Approved",
		"timezone": null,
		"to": "2016-12-25",
		"updated_at": "2016-02-16T12:55:19.072Z",
	},
	{
		"account_id": 1,		
		"created_at": "2016-02-04T09:48:24.000Z",
		"creator_id": 2,		
		"deleted": false,		
		"details": "Details",		
		"downtime_type_id": null,		
		"end_time": 1440,		
		"from": "2016-02-22",		
		"id": 124,		
		"leave": null,		
		"resource_ids": {
			"0": 123
		},
		"start_time": 0,		
		"state": "Approved",		
		"timezone": null,	
		"to": "2016-02-22",	
		"updated_at": "2016-02-12T11:46:54.000Z"
	}

	{
		"account_id": 1,		
		"created_at": "2015-12-17T13:00:40.000Z",		
		"creator_id": 2,		
		"deleted": false,		
		"details": "",		
		"downtime_type_id": null,		
		"end_time": 1440,		
		"from": "2016-02-22",		
		"id": 125,		
		"leave": null,		
		"resource_ids": {
			"0": 122
		},
		"start_time": 0,		
		"state": "Approved",		
		"timezone": null,	
		"to": "2016-02-22",	
		"updated_at": "2015-12-17T13:02:01.000Z,	
	}
]
```

Key | Type | Description
--- | --- | ---
created_at | string | Downtime creation date and time.
creator_id | integer | Unique identifier of the User this Downtime was created by.
deleted | boolean | Denoted whether the Downtime has been deleted.
details | string | Extra details about this Downtime.
downtime_type_id | integer | Unique identifier of the Downtime Type this Downtime is for. (Can be `null`)
end_time | integer | End time in minutes from midnight for this Downtime duration (Can't be null)
from | string | Start date for the Downtime.
id | integer | Unique identifier for a Downtime.
resource_ids| array of intergers | Unique identifiers of the Resources this Downtime is for.
start_time | integer | Start time in minutes from midnight for this Downtime duration (Can't be null)
state | string | Status details about the Downtime.
timezone | string | Specified time zone for the Downtime.
to | string | End date for the Downtime.
updated_at | String | Last updated date and time.


## Get a Specific Downtime

*  `GET /v1/:subdomain/downtimes/id` returns a specific Downtime.

## Create a Downtime

* `POST /v1/:subdomain/downtimes` will create a new Downtime from the parameters passed.

### Response

```json
[
	{
		"account_id": 1,
		"created_at": "2016-02-16T12:55:19.072Z",
		"creator_id": 2,
		"deleted": false,
		"details": "Christmas Eve",
		"downtime_type_id": 444,
		"end_time": 1440,
		"from": "2016-12-25",
		"id": 123,
		"leave": null,
		"resource_ids": {
			"0": "122"
		},
		"start_time": 0,
		"state": "Approved",
		"timezone": "London",
		"to": "2016-12-25",
		"updated_at": "2016-02-16T12:55:19.072Z",
	}
]

```
Key | Type | Description
--- | --- | --- | ---
resource_ids| array of intergers | The resources that the Downtime is being created for.
creator_id | integer | Unique identifier of the User this Downtime is for.
from | string | The ISO 8601 formatted first date for the Downtime.
to | string | The ISO 8601 formatted last date for the Downtime.
start_time | integer | Start time in minutes from midnight for this Downtime duration (Can't be null)
end_time | integer | End time in minutes from midnight for this Downtime duration (Can't be null)
details | string | Optional plain text details for the Downtime.
downtime_type_id | integer | Unique identifier of the Downtime Type this Downtime is for. (Can be `null`)
timezone | string | String denoting the time zone for which the Downtime is created for. [(Details)](#timezones)

#### Time zones

When creating a new Downtime, a time zone may be specified if the Downtime is being created for multiple resources. If left blank, it will default to the time zone of each resource.
The time zone values are based off of Ruby On Rails's ActiveSupport::TimeZone's key mappings. For example, to create a Downtime for (GMT +0) London, the value would be "London". See http://api.rubyonrails.org/classes/ActiveSupport/TimeZone.html - Constants.


## Update a Downtime
* `PUT /v1/:subdomain/downtimes/5` will update the Downtime from the parameters passed and return
the JSON representation of the updated Downtime. If the user does not have access to update
the Downtime, you'll see `403 Forbidden`.


## Delete a Downtime

* `DELETE /v1/:subdomain/downtimes/5` will delete the Downtime specified and return `204 No Content`
if that was successful. If the user does not have access to delete the Downtime, you'll see `403 Forbidden`.


## Get Downtime Types

* `GET /v1/:subdomain/downtime_types` returns an `Array` of **Downtimes**.

```json
[
	{
	  "id": 1555,
	  "name": "Compassionate leave",
	  "account_id": 348,
	  "created_at": "2016-02-02T11:17:45.000Z",
	  "updated_at": "2016-02-02T11:17:45.000Z",
	  "default": true
	}
]

```
Key | Type | Description
--- | --- | --- | ---
id | integer | Unique identifier of the Downtime type.
name | string | Name of this Downtime type.
account_id | integer | Unique identifier of the Account to which this Downtime type belongs.
created_at | string | Downtime type creation date and time.
updated_at | string | Last updated date and time.
default | boolean | Denotes whether the Downtime type is a default type.
