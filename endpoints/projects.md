# Projects

## Get Projects

* `GET /v1/:subdomain/projects` returns an `Array` of **Active Projects**.
* `GET /v1/:subdomain/projects/archived` returns an `Array` of **Archived Projects**.

### Query String Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| limit | 50 | Limit the number of results returned for pagination. To retrieve all the results use `0`. |
| offset | 0 | Offset the results for pagination, starting from the given record number. |

**Example:**

```
https://api.resourceguruapp.com/v1/example-corp/projects?limit=30&offset=30
```

The above example will return the next 30 Projects.

### Response

```json
[
  {
    "id": 1,
    "creator_id": 1,
    "color": "#FFCC00",
    "name": "Project A",
    "project_code": "PA02",
    "notes": "Project A Notes",
    "default_billable": true,
    "updated_at": "2013-04-30T12:00:00+00:00",
    "url": "https://api.resourceguruapp.com/v1/example-corp/projects/1",
    "account_id": 1,
    "client_id": 1
  },
  {
    "id": 2,
    "creator_id": 1,
    "color": "#CCFF00",
    "name": "Project B",
    "project_code": "PB05",
    "notes": "Project B Notes",
    "default_billable": true,
    "updated_at": "2013-04-30T12:00:00+00:00",
    "url": "https://api.resourceguruapp.com/v1/example-corp/projects/2",
    "account_id": 1,
    "client_id": 1
  }
]
```

| Key | Type | Description |
|-----|------|-------------|
| id | integer | Unique identifier for a Project. |
| creator_id | integer | Unique identifier of the User this project was created by. |
| color | string | Color used to highlight a Project. |
| name | string | Name of a Project. |
| project_code | string | The project code assigned to the project. |
| notes | string | Notes about this Project. |
| default_billable | boolean | Bookings for this project should default to billable or non-billable. |
| updated_at | timestamp | Last updated date and time in ISO 8601. |
| url | string | URL to view a Project. |
| account_id | integer | [Account] a Project belongs to. |
| client_id | integer | [Client] a Project belongs to. |

## Get Project

* `GET /v1/:subdomain/projects/1` returns the specified Project.

### Response

```json
{
  "id": 1,
  "archived": false,
  "color": "#FFCC00",
  "name": "Project A",
  "project_code": "PA02",
  "notes": "Some notes",
  "default_billable": true,
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

| Key | Type | Description |
|-----|------|-------------|
| id | integer | Unique identifier for this Project. |
| archived | boolean | If `true`, then this Project is archived. |
| color | string | Color used to highlight this Project. |
| name | string | Name of this Project. |
| project_code | string | The project code assigned to this project. |
| notes | string | Notes about this Project. |
| default_billable | boolean | Bookings for this project should default to billable or |  |non-billable. |
| updated_at | timestamp | Last updated date and time in ISO 8601. |
| account | hash | [Account] this Project belongs to. [(Details)](#account-key) |
| client | hash | [Client] this Project belongs to. [(Details)](#client-key) |

#### Account Key

| Key | Type | Description |
|-----|------|-------------|
| id | integer | Unique identifier for this Account. |
| name | string | Name of this Account. |
| url | string | URL shortcut to view this Account. |

#### Client Key

*No `client` key will be returned if a Project has no Client.*

| Key | Type | Description |
|-----|------|-------------|
| id | integer | Unique identifier for this Client. |
| name | string | Name of this Client. |
| url | string | URL shortcut to view this Client. |

[Account]: ../endpoints/accounts.md "Account Documentation"
[Client]: ../endpoints/clients.md "Client Documentation"

## Create a Project

* `POST /v1/:subdomain/projects` will create a new Project from the parameters passed.

```json
{
  "color": "#FF00CC",
  "name": "Project C",
  "notes": "Some notes",
  "default_billable": true,
  "project_code": "PC1",
  "client_id": 1
}
```

This will return `201 Created`, with the location of the new Project in the Location header
along with the current JSON representation of the Project if the creation was successful.
If the user does not have access to update the Project, you'll see `403 Forbidden`.

## Update a Project

* `PUT /v1/:subdomain/projects/1` will update the Project from the parameters passed and return
the JSON representation of the updated Project. If the user does not have access to update
the Project, you'll see `403 Forbidden`.

## Delete a Project

* `DELETE /v1/:subdomain/projects/1` will delete the Project specified and return `204 No Content`
if that was successful. If the user does not have access to delete the Project, you'll see `403 Forbidden`.
