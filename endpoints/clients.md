# Clients

## Get Clients

* `GET /{subdomain}/clients` returns an `Array` of active Clients.
* `GET /{subdomain}/clients/archived` returns an `Array` of archived Clients.

```json
[
  {
    "id": 1,
    "name": "Client A",
    "updated_at": "2013-04-30T12:00:00Z",
    "url": "https://api.resourceguruapp.com/v1/example-corp/clients/1"
  },
  {
    "id": 2,
    "name": "Client B",
    "updated_at": "2013-04-30T12:00:00Z",
    "url": "https://api.resourceguruapp.com/v1/example-corp/clients/2"
  }
]
```

## Get Client

* `GET /{subdomain}/clients/1` returns the specified Client.

```json
{
  "id": 1,
  "color:" "#FFCC00",
  "name": "Client A",
  "notes:" "Some notes",
  "updated_at": "2013-04-30T12:00:00Z"
}
```
