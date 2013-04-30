# Clients

## Get Clients

* `GET /{subdomain}/client` returns an `Array` of active Clients.
* `GET /{subdomain}/clients/archived` returns an `Array` of archived Clients.

```json
[
  {
    "id": 1,
    "name": "Client A",
    "url": "https://api.resourceguruapp.com/v1/example-corp/clients/1"
  },
  {
    "id": 2,
    "name": "Client B",
    "url": "https://api.resourceguruapp.com/v1/example-corp/clients/2"
  }
]
```

## Get Client

* `GET /{subdomain}/clients/1` returns the specified Client.

```json
{
  "id": 1,
  "name": "Client A",
  "color:" "#FFCC00"

}
```
