# Webhooks

Resource Guru supports integration with other services using outgoing webhooks.
Account owners and users with administrative privileges can create new webhooks
for services by posting to the webhooks endpoint with a name of the webhook,
the payload URL which receives the payloads,
and the types of events which should be sent to the payload URL.

**Update:** Account owners and users with administrative privileges can 
now manage webhooks through the settings page in the Resource Guru application.

The supported event types are:

- Bookings
- Clients
- Projects
- Resources
- Resource Types
- Accounts

Payloads are sent immediately when changes are made within the application
and the webhook is subscribed to those changes. Changes made through the API
will also trigger webhook payloads.

For added security, you can provide a secret string which will be combined 
with the payload's request body to create a HMAC SHA256 digest and added as a
request header.

Payloads are sent as JSON with the following headers:

Header | Description
--- | ---
User-Agent | The string `ResourceGuru/Webhooks` identifies Resource Guru as the sender.
Content-Type | The string `application/json` identifies the content type of the payload.
X-ResourceGuru-Key | The secret provided when creating the webhook. This is only sent if a webhook secret is set.
X-ResourceGuru-Signature | A HMAC SHA256 digest of the request body, signed by the webhook secret. This is only sent if a webhook secret is set.

The signature is generated on our side using the OpenSSL library using the following code:

``` ruby
OpenSSL::HMAC.hexdigest(OpenSSL::Digest.new('sha256'), webhook_, request_body)
```

## Payload format

Payloads are sent as JSON.

Key | Type |Description
--- | --- |---
id  | integer | Each payload has a unique incrementing ID
timestamp | integer | A UNIX epoch timestamp when the event occurred.
payload | object | Format varies based on the type of event. We use the same formatting as in the API for each type of object. The keys `action` and `type` are added.

The payload `action` will be one of:

- create
- update
- delete

The payload `type` will be one of:

- account
- booking
- client
- project
- resource
- resource_type

An example payload when a new client is created:

``` json
{
  "id": 1,
  "timestamp": 1423472753,
  "payload": {
    "id": 1234,
    "archived": false,
    "color": null,
    "name": "A client",
    "notes": "",
    "created_at": "2015-02-04T16:40:23.000Z",
    "updated_at":"2015-02-09T09:05:53.581Z",
    "action": "delete",
    "type": "client"
  }
}
```

## Get Webhooks

* `GET /v1/:subdomain/webhooks` returns an `Array` of webhooks.

### Response

```json
[
  {
    "id": 1,
    "name": "Webhook Service",
    "payload_url": "http://www.example-corp.com/endpoint",
    "account_id": 1,
    "user_id": 3,
    "events": ["clients", "projects", "accounts", "resources", "resource_types", "bookings"],
    "url": "https://api.resourceguruapp.com/v1/example-corp/webhooks/1",
    "created_at": "2013-04-30T12:00:00+00:00",
    "updated_at": "2013-04-30T12:00:00+00:00",
    "status": "ready",
    "paused": false
  },
  {
    "id": 2,
    "name": "Webhook Service 2",
    "payload_url": "http://www.example-corp.com/endpoint2",
    "account_id": 1,
    "user_id": 3,
    "events": ["clients", "projects", "accounts", "resources", "resource_types", "bookings"],
    "url": "https://api.resourceguruapp.com/v1/example-corp/webhooks/2",
    "created_at": "2013-04-30T12:00:00+00:00",
    "updated_at": "2013-04-30T12:00:00+00:00",
    "status": "ready",
    "paused": false
  }
]
```

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier for a webhook.
name | string | Name of a webhook.
payload_url | string | Payload (receiving) URL for the webhook.
account_id | integer | The id of the account to which the webhook belongs.
user_id | integer | The id of the user who created the webhook.
events | array | The events for the payloads to be sent to the payload (receiving) URL.
created_at | timestamp | Date and time created in ISO 8601.
updated_at | timestamp | Date and time last updated in ISO 8601.
status | string | Status which identifies what state the current webhook is in.
paused | boolean | A boolean denoting whether or not the webhook is paused.

### Status
The status of a webhook is reflective of the latest activity in terms of payloads delivered. The status can be either "ready", which signifies that no payloads have been sent yet, "success", which signifies that the webhook is successfully delivering payloads, "retrying", which signifies that a payload is not being successfully delivered and is being retried, and "failed", which signifies that the payload which is failing has reached the maximum number of
attempts, which results in this payload not being automatically retried.

## Get Webhook

* `GET /v1/:subdomain/webhooks/1` returns the specified webhook.

### Response

```json
{
  "id": 1,
  "name": "Webhook Service",
  "payload_url": "http://www.example-corp.com/endpoint",
  "account_id": 1,
  "user_id": 3,
  "events": ["clients", "projects", "accounts", "resources", "resource_types", "bookings"],
  "url": "https://api.resourceguruapp.com/v1/example-corp/webhooks/1",
  "created_at": "2013-04-30T12:00:00+00:00",
  "updated_at": "2013-04-30T12:00:00+00:00",
  "status": "ready",
  "paused": false
}
```

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier for a webhook.
name | string | Name of this webhook.
payload_url | string | Payload (receiving) URL for this webhook.
account_id | integer | The id of the account to which this webhook belongs.
user_id | integer | The id of the user who created this webhook.
events | array | The events for the payloads to be sent to the payload (receiving) URL.
created_at | timestamp | Date and time created in ISO 8601.
updated_at | timestamp | Date and time last updated in ISO 8601.
status | string | Status which identifies what state the current webhook is in.
paused | boolean | A boolean denoting whether or not the webhook is paused.

## Create a Webhook

* `POST /v1/:subdomain/webhooks` will create a new webhook from the parameters passed.
* Supported events are:
  * accounts
  * bookings
  * clients
  * projects
  * resources
  * resource_types

```json
{
  "name": "Webhook A",
  "payload_url": "http://www.example-corp.com/endpoint",
  "events": ["clients", "projects", "accounts", "resources", "resource_types", "bookings"],
  "secret": "optional secret"
}
```

This will return `201 Created`, with the location of the new webhook in the Location header
along with the current JSON representation of the webhook if the creation was successful.
If the user does not have administrative priveleges, you'll see `403 Forbidden`.

## Update a Webhook

* `PUT /v1/:subdomain/webhooks/1` will update the webhook from the parameters passed and return
the JSON representation of the updated webhook. If the user does not have administrative
priveleges, you'll see `403 Forbidden`.
If the user tries to specify a user_id when updating the webhook, '422 Unprocessable Entity'
will be returned as the user_id is the point of reference to the creator of the webhook
which should not be modified.

## Delete a Webhook

* `DELETE /v1/:subdomain/webhooks/1` will delete the webhook specified and return `204 No Content`
if that was successful. If the user does not have administrative
priveleges, you'll see `403 Forbidden`.

## Test a Webhook

* `GET /v1/:subdomain/webhooks/1/test` sends a test payload to the payload endpoint.

This will return a status code which depends on the endpoint interacting with.
Some endpoints, such as requestb.in for example, will return either 200 or 201 if successful.
If unsuccessful, the service should return either 404 or 422.
