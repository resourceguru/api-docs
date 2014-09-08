# Webhooks

## Get Webhooks

* `GET /v1/:subdomain/webhooks` returns an `Array` of webhooks.

### Response

```json
[
  {
    "id": 1,
    "name": "Webhook Service",
    "payload_url:" "http://www.example-corp.com/endpoint",
    "account_id:" 1,
    "user_id:" 3,
    "events:" ["clients","projects"],
    "url": "https://api.resourceguruapp.com/v1/example-corp/webhooks/1",
    "created_at": "2013-04-30T12:00:00+00:00",
    "updated_at": "2013-04-30T12:00:00+00:00"
  },
  {
    "id": 2,
    "name": "Webhook Service 2",
    "payload_url:" "http://www.example-corp.com/endpoint2",
    "account_id:" 1,
    "user_id:" 3,
    "events:" ["clients","projects"],
    "url": "https://api.resourceguruapp.com/v1/example-corp/webhooks/2",
    "created_at": "2013-04-30T12:00:00+00:00",
    "updated_at": "2013-04-30T12:00:00+00:00"
  }
]
```

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier for a Webhook.
name | string | Name of a Webhook.
payload_url | string | Payload endpoint for the Webhook.
account_ud | integer | The id of the account to which the Webhook belongs to.
user_ud | integer | The id of the user who created the Webhook.
events | array | The events for the payloads to be sent to the Webhook payload url.
created_at | timestamp | Created date and time in ISO 8601.
updated_at | timestamp | Last updated date and time in ISO 8601.

## Get Webhook

* `GET /v1/:subdomain/webhooks/1` returns the specified Webhook.

### Response

```json
{
  "id": 1,
  "name": "Webhook Service",
  "payload_url:" "http://www.example-corp.com/endpoint",
  "account_id:" 1,
  "user_id:" 3,
  "events:" ["clients","projects"],
  "url": "https://api.resourceguruapp.com/v1/example-corp/webhooks/1",
  "created_at": "2013-04-30T12:00:00+00:00",
  "updated_at": "2013-04-30T12:00:00+00:00"
}
```

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier for a Webhook.
name | string | Name of this Webhook.
payload_url | string | Payload endpoint for this Webhook.
account_ud | integer | The id of the account to which this Webhook belongs to.
user_ud | integer | The id of the user who created this Webhook.
events | array | The events for the payloads to be sent to the Webhook payload url.
created_at | timestamp | Created date and time in ISO 8601.
updated_at | timestamp | Last updated date and time in ISO 8601.

## Create a Webhook

* `POST /v1/:subdomain/webhooks` will create a new Webhook from the parameters passed.

```json
{
  "name": "Webhook A",
  "payload_url": "http://www.example-corp.com/endpoint",
  "events": ["clients", "projects"]
}
```

This will return `201 Created`, with the location of the new Webhook in the Location header
along with the current JSON representation of the Webhook if the creation was successful.
If the user does not have administrative priveleges, you'll see `403 Forbidden`.

## Update a Webhook

* `PUT /v1/:subdomain/webhooks/1` will update the Webhook from the parameters passed and return
the JSON representation of the updated Webhook. If the user does not have administrative
priveleges, you'll see `403 Forbidden`.

## Delete a Webhook

* `DELETE /v1/:subdomain/webhooks/1` will delete the Webhook specified and return `204 No Content`
if that was successful. If the user does not have administrative
priveleges, you'll see `403 Forbidden`.

