# Projects

## Get Projects

* `GET /{subdomain}/projects` returns an `Array` of active Projects.
* `GET /{subdomain}/projects/archived` returns an `Array` of archived Projects.

```json
[
  {
    "id": 1,
    "name": "Project A",
    "updated_at": "2013-04-30T12:00:00Z",
    "url": "https://api.resourceguruapp.com/v1/example-corp/projects/1"
  },
  {
    "id": 2,
    "name": "Project B",
    "updated_at": "2013-04-30T12:00:00Z",
    "url": "https://api.resourceguruapp.com/v1/example-corp/projects/2"
  }
]
```

## Get Project

* `GET /{subdomain}/projects/1` returns the specified Project.

```json
{
  "id": 1,
  "archived": false,
  "color:" "#FFCC00",
  "name": "Project A",
  "notes:" "Some notes",
  "updated_at": "2013-04-30T12:00:00Z",
  "account": {
    "id": 1,
    "name": "Example Corp",
    "url": "https://api.resourceguruapp.com/v1/accounts/1"
  },
  "client": {
    "id": 1,
    "name": "Client A",
    "url": "https://api.resourceguruapp.com/v1/example-corp/clients/1"
  }
}
```

### Notes

* `Projects` that don't have a `Client` **will not** have `client` attribute.
