# Webhooks

**Please note that Webhooks are still currently in beta and that development is still ongoing.**

Resource Guru supports integration with other services using webhooks.
Account owners and users with administrative priveledges may create new webhooks
for services by posting to the webhooks endpoint with a name of the webhook,
the payload url which is the intended endpoint,
and the events for which payloads should be sent.
Event types supported by Resource Guru include Bookings, Clients, Projects,
Resources, Resource Types and Accounts.

Payloads are created every minute, which includes any and all changes made
within the application for the event types specified within the created
webhooks.

The user also has the option of providing an additional secret string
which is combined with the payload to be delivered to create
a HMAC SHA256 digest as an added security header.

The content type of payloads being sent is JSON, with the following headers:

Header | Description
--- | ---
X-Rate-Limit-Limit | The current rate limit of our API.
X-Rate-Limit-Remaining | The amount of requests left before rate limiting is triggered.
X-ResourceGuru-Key | The secret of the created webhook.
X-ResourceGuru-Signature | A HMAC SHA256 digest of the webhook secret and the payload to be delivered.

At the end of every minute, all changes made on events for the current account will
be sent as a payload to the payload endpoint.

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
    "events:" ["clients","projects", "accounts", "resources", "resource_types", "bookings"],
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
    "events:" ["clients","projects", "accounts", "resources", "resource_types", "bookings"],
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
account_id | integer | The id of the account to which the Webhook belongs to.
user_id | integer | The id of the user who created the Webhook.
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
  "events:" ["clients","projects", "accounts", "resources", "resource_types", "bookings"],
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
account_id | integer | The id of the account to which this Webhook belongs to.
user_id | integer | The id of the user who created this Webhook.
events | array | The events for the payloads to be sent to the Webhook payload url.
created_at | timestamp | Created date and time in ISO 8601.
updated_at | timestamp | Last updated date and time in ISO 8601.

## Create a Webhook

* `POST /v1/:subdomain/webhooks` will create a new Webhook from the parameters passed.
* Supported events include:
  * "accounts"
  * "bookings"
  * "clients"
  * "projects"
  * "resources"
  * "resource_types"

```json
{
  "name": "Webhook A",
  "payload_url": "http://www.example-corp.com/endpoint",
  "events": ["clients", "projects", "accounts", "resources", "resource_types", "bookings"],
  "secret": "optional secret"
}
```

This will return `201 Created`, with the location of the new Webhook in the Location header
along with the current JSON representation of the Webhook if the creation was successful.
If the user does not have administrative priveleges, you'll see `403 Forbidden`.

## Update a Webhook

* `PUT /v1/:subdomain/webhooks/1` will update the Webhook from the parameters passed and return
the JSON representation of the updated Webhook. If the user does not have administrative
priveleges, you'll see `403 Forbidden`.
If the user tries to specify a user_id when updating the webhook, '422 Unprocessable Entity'
will be returned as the user_id is the point of reference to the creator of the webhook
which should not be modified.

## Delete a Webhook

* `DELETE /v1/:subdomain/webhooks/1` will delete the Webhook specified and return `204 No Content`
if that was successful. If the user does not have administrative
priveleges, you'll see `403 Forbidden`.

## Test a Webhook

* `GET /v1/:subdomain/webhooks/1/test` sends a test payload to the payload endpoint.

This will return a status code which depends on the endpoint interacting with.
Some endpoints, such as requestb.in for example, will return either 200 or 201 if successful.
If unsuccessful, the service should return either 404 or 422.

