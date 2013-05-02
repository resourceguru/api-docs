# Projects

## Get Projects

* `GET /:subdomain/projects` returns an `Array` of **Active Projects**.
* `GET /:subdomain/projects/archived` returns an `Array` of **Archived Projects**.

### Query String Paramaters

Paramater | Default | Description
--- | --- | --- | ---
limit | 50 | Limit the number of results returned for pagination. To retrieve all the results use `0`.
offset | 0 | Offset the results for pagination, starting from the given record number.

**Example:**

```
https://api.resourceguruapp.com/v1/example-corp/projects?limit=30&offset=30
```

The above example will return the next 30 Projects.

```json
[
  {
    "id": 1,
    "color": "#FFCC00",
    "name": "Project A",
    "updated_at": "2013-04-30T12:00:00+00:00",
    "url": "https://api.resourceguruapp.com/v1/example-corp/projects/1",
    "account_id": 1,
    "client_id": 1
  },
  {
    "id": 2,
    "color": "#CCFF00",
    "name": "Project B",
    "updated_at": "2013-04-30T12:00:00+00:00",
    "url": "https://api.resourceguruapp.com/v1/example-corp/projects/2",
    "account_id": 1,
    "client_id": 1
  }
]
```

### Response

Attribute | Type | Description
--- | --- | ---
id | integer | Unique identifier for a Project.
color | string | Color used to highlight a Project.
name | string | Name of a Project.
updated_at | string | Last updated date and time in ISO 8601.
url | string | URL shortcut to view a Project.
account_id | integer | [Account](../endpoints/accounts.md) a Project belongs to.
client_id | integer | [Client](../endpoints/clients.md) a Project belongs to.

## Get Project

* `GET /:subdomain/projects/1` returns the specified Project.

```json
{
  "id": 1,
  "archived": false,
  "color:" "#FFCC00",
  "name": "Project A",
  "notes:" "Some notes",
  "updated_at": "2013-04-30T12:00:00+00:00",
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

### Response

Attribute | Type | Description
--- | --- | ---
id | integer | Unique identifier for this Project.
archived | boolean | If `true`, then this Project is archived.
color | string | Color used to highlight this Project.
name | string | Name of this Project.
notes | string | Notes about this Project.
updated_at | string | Last updated date and time in ISO 8601.
account | hash | [Account](../endpoints/accounts.md) this Project belongs to.
- id | integer | Unique identifier for this Account.
- name | string | Name of this Account.
- url | string | URL shortcut to view this Account.
client | hash | [Client](../endpoints/accounts.md) this Project belongs to. No `client` attribute will be returned if a Project has no Client.
- id | integer | Unique identifier for this Account.
- name | string | Name of this Account.
- url | string | URL shortcut to view this Client.
