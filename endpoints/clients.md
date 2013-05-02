# Clients

## Get Clients

* `GET /:subdomain/clients` returns an `Array` of **Active Clients**.
* `GET /:subdomain/clients/archived` returns an `Array` of **Archived Clients**.

### Query String Paramaters

Paramater | Default | Description
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
    "updated_at": "2013-04-30T12:00:00+00:00",
    "url": "https://api.resourceguruapp.com/v1/example-corp/clients/1"
  },
  {
    "id": 2,
    "name": "Client B",
    "updated_at": "2013-04-30T12:00:00+00:00",
    "url": "https://api.resourceguruapp.com/v1/example-corp/clients/2"
  }
]
```

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier for a Client.
name | string | Name of a Client.
updated_at | string | Last updated date and time in ISO 8601.
url | string | URL to view a Client.

## Get Client

* `GET /:subdomain/clients/1` returns the specified Client.

### Response

```json
{
  "id": 1,
  "archived": false,
  "color:" "#FFCC00",
  "name": "Client A",
  "notes:" "Some notes",
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
