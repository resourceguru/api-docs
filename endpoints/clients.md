# Clients

## Get Clients

* `GET /v1/:subdomain/clients` returns an `Array` of **Active Clients**.
* `GET /v1/:subdomain/clients/archived` returns an `Array` of **Archived Clients**.

### Query String Parameters

Parameter | Default | Description
--- | --- | --- | ---
limit | 50 | Limit the number of results returned for pagination. To retrieve all the results use `0`.
offset | 0 | Offset the results for pagination, starting from the given record number.

**Example:**

```
https://api.resourceguruapp.com/v1/example-corp/clients?limit=30&offset=30
```

The above example will return the next 30 Clients.

### Response

```json
[
  {
    "id": 1,
    "name": "Client A",
    "notes": "Client A Notes",
    "updated_at": "2013-04-30T12:00:00+00:00",
    "url": "https://api.resourceguruapp.com/v1/example-corp/clients/1"
  },
  {
    "id": 2,
    "name": "Client B",
    "notes": "Client B Notes",
    "updated_at": "2013-04-30T12:00:00+00:00",
    "url": "https://api.resourceguruapp.com/v1/example-corp/clients/2"
  }
]
```

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier for a Client.
name | string | Name of a Client.
updated_at | timestamp | Last updated date and time in ISO 8601.
url | string | URL to view a Client.

## Get Client

* `GET /v1/:subdomain/clients/1` returns the specified Client.

### Response

```json
{
  "id": 1,
  "archived": false,
  "color": "#FFCC00",
  "name": "Client A",
  "notes": "Some notes",
  "updated_at": "2013-04-30T12:00:00+00:00"
}
```

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier for this Client.
archived | boolean | If `true`, then this Client is archived.
color | string | Color used to highlight this Client.
name | string | Name of this Client.
notes | string | Notes about this Client.
updated_at | string | Last updated date and time in ISO 8601.

## Create a Client

* `POST /v1/:subdomain/clients` will create a new Client from the parameters passed.

```json
{
  "color": "#FF00CC",
  "name": "Client C",
  "notes": "Some notes"
}
```

This will return `201 Created`, with the location of the new Client in the Location header
along with the current JSON representation of the Client if the creation was successful.
If the user does not have access to update the Client, you'll see `403 Forbidden`.

## Update a Client

* `PUT /v1/:subdomain/clients/1` will update the Client from the parameters passed and return
the JSON representation of the updated Client. If the user does not have access to update
the Client, you'll see `403 Forbidden`.

## Delete a Client

* `DELETE /v1/:subdomain/clients/1` will delete the Client specified and return `204 No Content`
if that was successful. If the user does not have access to delete the Client, you'll see `403 Forbidden`.

