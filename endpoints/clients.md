# Clients

## Get Clients

* `GET /:subdomain/clients` returns an `Array` of active Clients.
* `GET /:subdomain/clients/archived` returns an `Array` of archived Clients.

### Query String Paramater

Paramater | Default | Description
--- | --- | --- | ---
`limit` | `50` | Limit the number of results returned. To retrieve all the results use `0`.
`offset` | `0` | Return `limit` results starting on a specific record.

**Example:**

```
https://api.resourceguruapp.com/v1/example-corp/clients?limit=30&offset=10
```

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

## Get Client

* `GET /:subdomain/clients/1` returns the specified Client.

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

### Response

Attribute | Type | Description
--- | --- | ---
`id` | `integer` | Unique identifier of this Client.
`archived` | `boolean` | If `true`, then this Client is archived.
`color` | `string` | Color used to highlight this Client.
`name` | `string` | Name of this Client.
`notes` | `string` | Notes about this Client.
`updated_at` | `string` | Last updated time in ISO 8601.
