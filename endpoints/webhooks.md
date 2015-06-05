# Webhooks

Resource Guru supports integration with other services using outgoing webhooks. In a nutshell, webhooks provide a way for Resource Guru to send real-time information to other apps. For example, when a booking is made in Resource Guru, webhooks can be used to post information (payloads) about that booking to a payload (receiving) URL. Getting this information was always possible via our basic API, but webhooks proactively post the changes instead. This means that apps no longer need to keep polling the API to check what's changed - resulting in much greater efficiency.

Account owners and users with administrative privileges can create new webhooks either via the API endpoint or via settings in their Resource Guru account. Simply specify the name of the webhook, the payload URL which receives the payloads, and the types of events which should be sent to the payload URL. For added security, you can provide a secret string which will be combined with the payload's request body to create a HMAC SHA256 digest and added as a request header.

The supported event types are:

- Bookings
- Clients
- Projects
- Resources
- Resource Types
- Accounts

As soon as changes are made within a relevant Resource Guru acccout, payloads are sent immediately for any of the events that have been subscribed to in the webhook. We will automatically try to deliver a payload 100 times before marking it as failed. More detail on payload statuses can be found in the [payloads endpoint documentation](webhooks/payloads.md). Payloads are dropped from Resource Guru's history after 30 days. **Unsuccessful payloads will be lost after failing for 30 days**.

Payloads are sent as JSON with the following headers:

Header | Description
--- | ---
User-Agent | The string `ResourceGuru/Webhooks` identifies Resource Guru as the sender.
Content-Type | The string `application/json` identifies the content type of the payload.
X-ResourceGuru-Key | The secret provided when creating the webhook. This is only sent if a webhook secret is set.
X-ResourceGuru-Signature | A HMAC SHA256 digest of the request body, signed by the webhook secret. This is only sent if a webhook secret is set.

The signature is generated on our side using the OpenSSL library using the following code:

``` ruby
OpenSSL::HMAC.hexdigest(OpenSSL::Digest.new('sha256'), webhook_secret, request_body)
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
    "notes": "Some notes",
    "created_at": "2015-02-04T16:40:23.000Z",
    "updated_at":"2015-02-09T09:05:53.581Z",
    "action": "create",
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
events | array | The events for which payloads will be sent to the payload (receiving) URL.
created_at | timestamp | Date and time created in ISO8601.
updated_at | timestamp | Date and time last updated in ISO8601.
status | string | Identifies the state the webhook is currently in. Details in the [Webhook statuses](#webhook-statuses) table below.
paused | boolean | A boolean denoting whether or not the webhook is paused.

### Webhook Statuses
Status | Description
--- | ---
Ready | No payloads have been sent yet.
Success | The last attempted payload has been delivered successfully. (See [Payload Statuses](webhooks/payloads.md#payload-statuses))
Retrying | The last attempted payload has failed to be delivered.
Failed | The last attempted payload has failed 100 times and no further attempt will be made to deliver payloads automatically.

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
events | array | The events for which payloads will be sent to the payload (receiving) URL.
created_at | timestamp | Date and time created in ISO8601.
updated_at | timestamp | Date and time last updated in ISO8601.
status | string | Identifies the state the webhook is currently in. Details in the [Webhook statuses](#webhook-statuses) table below.
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

This will return `201 Created`, with the location of the new webhook in the `Location` header
along with the current JSON representation of the webhook if the creation was successful.
If the user does not have administrative privileges, you'll see `403 Forbidden`.

## Update a Webhook

* `PUT /v1/:subdomain/webhooks/1` will update the webhook from the parameters passed and return
the JSON representation of the updated webhook. If the user does not have administrative
privileges, you'll see `403 Forbidden`.
If the user tries to specify a `user_id` when updating the webhook, `422 Unprocessable Entity`
will be returned as the `user_id` is the read-only point of reference to the creator of the webhook.

## Delete a Webhook

* `DELETE /v1/:subdomain/webhooks/1` will delete the webhook specified and return `204 No Content`
if the operation was successful. If the user does not have administrative
privileges, you'll see `403 Forbidden`.

## Test a Webhook

* `GET /v1/:subdomain/webhooks/1/test` sends a test payload to the payload endpoint.

This will return a status code which depends on the endpoint the webhook is interacting with.
Some services, such as http://requestb.in, will return either 200 or 201 if successful.
If unsuccessful, the service should return any non-2XX code. HTTP semantics suggest using 422
for this purpose.

## Deprecations

| Payload type | Field | Note |
| --- | --- | --- |
| Bookings | notes | The notes field is deprecated in favour of the details field. Booking notes will not appear in future versions of the API or webhooks |
