# 🚨 🚨 🚨 Deprecated: please see [Resource Guru API documentation](https://resourceguruapp.com/docs/api) instead

# Projects Report

## Get Report

* `GET /v1/:account-id/reports/projects` returns a **Projects Report**.

### Required Query String Parameters

|Parameter | Description|
|---|---|
|start_date | Start date in ISO 8601 (`YYYY-MM-DD`).|
|end_date | End date in ISO 8601 (`YYYY-MM-DD`).|

**Example:**

```
https://api.resourceguruapp.com/v1/example-corp/reports/projects?start_date=2013-01-01&end_date=2013-01-07
```

### Projects Report Response

```json
{
  "booked": 32640,
  "waiting_list": 0,
  "max_usage": 3180,
  "projects": [
    {
      "id": 148,
      "name": "Project A",
      "project_code": "PA01",
      "client_name": "Client A",
      "client_id": 12,
      "color": "#FFCC00",
      "booked": 0,
      "waiting_list": 0,
      "url": "https://api.resourceguruapp.com/v1/example-corp/projects/1",
    },
    {
      "id": 149,
      "name": "Project B",
      "project_code": "PB02",
      "client_name": "Client A",
      "client_id": 12,
      "color": "#CCFF00",
      "booked": 4800,
      "waiting_list": 0,
      "url": "https://api.resourceguruapp.com/v1/example-corp/projects/2",
    }
  ]
}
```

|Key | Type | Description|
|---|---|---|
|booked | integer | Total time booked in minutes.|
|waiting_list | integer | Total time on waiting list in minutes.|
|max_usage | integer | Max usage for utilization bar. |
|projects | array | Report breakdown per Project. [(Details)](#projects-key)|

#### Projects Key

|Key | Type | Description|
|---|---|---|
|id  | integer | Unique identifier of Project.|
|name | string | Name of this Project.|
|project_code|string|This project's assigned project code.|
|client_name | string | Name of Client that this Project belongs to.|
|client_id | string | Unique identifier of Client that this Project belongs to. |
|color | string | Color used to highlight this Project.|
|booked | integer | Time booked in minutes for this Project.|
|waiting_list | integer | Time on waiting list in minutes for this Project.|
|url | string | URL shortcut to view this Project.|

# Project Report

## Get Report

* `GET /v1/:account-id/reports/projects/:project_id` returns a **Project Report**.

### Required Query String Parameters

|Parameter | Description|
|---|---|
|start_date | Start date in ISO 8601 (`YYYY-MM-DD`).|
|end_date | End date in ISO 8601 (`YYYY-MM-DD`).|

**Example:**

```
https://api.resourceguruapp.com/v1/example-corp/reports/projects/148?start_date=2013-01-01&end_date=2013-01-07
```

### Project Report Response

```json
{
  "id": 148,
  "name": "Project A",
  "project_code": "PA01",
  "client_name": "",
  "color": "#FFCC00",
  "booked": 0,
  "waiting_list": 0,
  "url": "https://api.resourceguruapp.com/v1/example-corp/projects/1",
  "resources": [
    {
      "id": 1685,
      "name": "John Doe",
      "image": "/images/fallback/resources/person/thumb_default.png",
      "booked": 5040,
      "waiting_list": 0,
      "job_title": "Developer",
      "resource_type": "Person",
      "earliest_available_period": "01 Aug 2014 to 31 Dec 2014 *",
      "utilization": 1,
      "url": "https://api.resourceguruapp.com/v1/example-corp/resources/1685"
    }
  ]
}
```

### Project Report for 'No project assigned'

* `GET /v1/:account-id/reports/projects/0` returns a **Project Report for 'No project assigned'**.

### Required Query String Parameters

|Parameter | Description|
|---|---|
|start_date | Start date in ISO 8601 (`YYYY-MM-DD`).|
|end_date | End date in ISO 8601 (`YYYY-MM-DD`).|

**Example:**

```
https://api.resourceguruapp.com/v1/example-corp/reports/projects/0?start_date=2013-01-01&end_date=2013-01-07
```

|Key | Type | Description|
|---|---|---|
|id  | integer | Unique identifier of Project.|
|name | string | Name of this Project.|
|project_code|string|The project's associated project code.|
|client_name | string | Name of Client that this Project belongs to.|
|color | string | Color used to highlight this Project.|
|booked | integer | Time booked in minutes for this Project.|
|waiting_list | integer | Time on waiting list in minutes for this Project.|
|url | string | URL shortcut to view this Project.|
|resources | array | Report breakdown per Resource. [(Details)](#resources-key)|

#### Resources Key

|Key | Type | Description|
|---|---|---|
|id | integer | Unique identifier of Resource.|
|name | string | Name of this Resource.|
|image | string | Image of this Resource.|
|booked | integer | Time booked in minutes for this Resource.|
|waiting_list | integer | Time on waiting list in minutes for this Resource.|
|job_title | string | Job title of the Resource.|
|resource_type | string | Resource type string.|
|earliest_available_period | string | Resource earlist available period.|
|utilization | number | Utilization ratio between `0` and `1` for this Resource.|
|url | string | URL shortcut to view this Resource.|
