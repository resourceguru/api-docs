# Resources Report

## Get Report

* `GET /v1/:subdomain/reports/resources` returns a **Resources Report**.

### Required Query String Parameters

Parameter | Description
--- | --- | ---
start_date | Start date in ISO 8601 (`YYYY-MM-DD`).
end_date | End date in ISO 8601 (`YYYY-MM-DD`).

**Example:**

```
https://api.resourceguruapp.com/v1/example-corp/reports/resources?start_date=2013-01-01&end_date=2013-01-07
```

### Resources Report Response

```json
{
  "booked": 32640,
  "unbooked": 3360,
  "availability": 36000,
  "waiting_list": 0,
  "utilization": 0.9,
  "resources": [
    {
      "id": "1",
      "name": "John Doe",
      "image": "https://resourceguru.s3.amazonaws.com/images/card_69cb-7f96ae8b2e17.png",
      "booked": 0,
      "unbooked": 2400,
      "availability": 2400,
      "waiting_list": 0,
      "utilization": 0,
      "url": "https://api.resourceguruapp.com/v1/example-corp/resources/1",
      "resource_type": "Person",
      "earliest_available_period": "25 Aug 2014 - 31 Aug 2014",
      "job_title": "Developer",
      "custom_fields": [] 
    },
    {
      "id": "2",
      "name": "Joe Soap",
      "image": "https://resourceguru.s3.amazonaws.com/images/card_12cb-7f968wehjfi2e17.png",
      "booked": 2400,
      "unbooked": 0,
      "availability": 2400,
      "waiting_list": 0,
      "utilization": 1,
      "url": "https://api.resourceguruapp.com/v1/example-corp/resources/2",
      "resource_type": "Person",
      "earliest_available_period": "25 Aug 2014 - 31 Aug 2014",
      "job_title": null,
      custom_fields: {
        22: [
          "33"
        ]
      }
    }
  ]
}
```

Key | Type | Description
--- | --- | ---
booked | integer | Total time booked in minutes.
unbooked | integer | Total time unbooked in minutes.
availability | integer | Total availability in minutes: `booked + unbooked`.
waiting_list | integer | Total time on waiting list in minutes.
utilization | integer | Total Utilization ratio between `0` and `1`.
resources | array | Report breakdown per Resource. [(Details)](#resources-key)

#### Resources Key

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier of Resource.
name | string | Name of this Resource.
image | string | Image of this Resource.
booked | integer | Time booked in minutes for this Resource.
unbooked | integer | Time unbooked in minutes for this Resource.
availability | integer | Availability in minutes for this Resource: `booked + unbooked`.
waiting_list | integer | Time on waiting list in minutes for this Resource.
utilization | integer | Utilization ratio between `0` and `1` for this Resource.
url | string | URL shortcut to view this Resource.
resource_type | string | Resource Type String.
earliest_available_period | string | Resource Earlist Available Period.
job_title | string | Resource Job Title.
custom_fields | array | All custom field ids for resource. [(Details)](#custom-fields-key)

#### Custom Fields Key

# The custom fields array contains the id of the custom field and nested within is the selected custom field option for this resource