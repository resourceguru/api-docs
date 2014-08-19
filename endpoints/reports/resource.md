# Resource Report

## Get Report

* `GET /v1/:subdomain/reports/resource/resource_id` returns a **Resource Report**.

### Required Query String Parameters

Parameter | Description
--- | --- | ---
start_date | Start date in ISO 8601 (`YYYY-MM-DD`).
end_date | End date in ISO 8601 (`YYYY-MM-DD`).

**Example:**

```
https://api.resourceguruapp.com/v1/example-corp/reports/resource/1685?start_date=2013-01-01&end_date=2013-01-07
```

### Resource Report Response

```json
{
  id: 1686,
  name: "Justinus Adriaanse",
  image: "/uploads/development/images/human_resource_instance/1686/image/thumb_71fe0036-f9d3-4708-993d-f023037ab71b.jpg",
  booked: 2040,
  unbooked: 900,
  availability: 2940,
  waiting_list: 360,
  utilization: 0.6938775510204082,
  url: "https://api.resourceguruapp.com/v1/platform45/resources/1686",
  projects: [
    {
      name: "asjdjas",
      client_name: "Apple Green",
      booked: 60,
      waiting_list: 0
    },
    {
      name: "Wellness recruit",
      client_name: "",
      booked: 0,
      waiting_list: 0
    },
    {
      name: "Winter Scarfs",
      client_name: "",
      booked: 0,
      waiting_list: 360
    }
  ],
  clients: [
    {
      name: "Andrew Rogoff",
      booked: 240,
      waiting_list: 0
    },
    {
      name: "Apple Green",
      booked: 300,
      waiting_list: 0
    },
    {
      name: "Archived",
      booked: 240,
      waiting_list: 0
    }
  ]
}
```
#### Resource Keys

Key | Type | Description
--- | --- | ---
name | string | Name of resource
image | string | Resource Avatar
booked | integer | Total time booked in minutes.
unbooked | integer | Total time unbooked in minutes.
availability | integer | Total availability in minutes: `booked + unbooked`.
waiting_list | integer | Total time on waiting list in minutes.
utilization | integer | Total Utilization ratio between `0` and `1`.
url | string | URL shortcut to view this Resource.

#### Projects Keys
name | string | Name of project
client | string | Name of client if there is one
booked | integer | Total time booked in minutes.
waiting_list | integer | Total time on waiting list in minutes.

#### Clients Keys
name | string | Name of project
booked | integer | Total time booked in minutes.
waiting_list | integer | Total time on waiting list in minutes.
