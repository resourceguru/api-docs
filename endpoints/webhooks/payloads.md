# Payloads

Payloads are created for webhooks once any interaction with the application takes place. All payloads are created immediately once an action is performed for webhooks that are subscribed to that action. The format of a payload in the API is detailed below.

## Get Payloads

* `GET /v1/:subdomain/webhooks/:id/queue` returns an `Array` of payloads for the specified webhook.

### Query String Parameters

Parameter | Default | Description
--- | --- | --- | ---
limit | 1000 | Limit the number of results returned for pagination.
offset | 0 | Offset the results for pagination, starting from the given record number.

### Response

```json
[
  {
    "id": 1,
    "account_id": 1,
    "webhook_id": 1,
    "model": {
        "id": 1,
        "timestamp": 1423469363,
        "payload": {
            "id": 1234,
            "archived": false,
            "color": null,
            "name": "A client",
            "notes": "",
            "created_at": "2015-02-05T18:44:36.000Z",
            "updated_at": "2015-02-09T08:09:22.547Z",
            "action": "delete",
            "type": "client"
        }
    },
    "user": {
        "id": 1,
        "name": "Shaun Prestor",
        "email": "shaun@example.com"
    },
    "action": "delete",
    "attempts": 1,
    "status": "delivered",
    "last_sent_on": "2015-02-09T08:09:24.292Z",
    "created_at": "2015-02-09T08:09:23.047Z",
    "request_headers": {
        "User-Agent": "ResourceGuru/Webhooks",
        "Content-Type": "application/json",
        "X-ResourceGuru-Key": "secret",
        "X-ResourceGuru-Signature": "41812cd012a1abd5a594d8633ebb5501a5cb0d3ee56bb4a4069b9f9e3bf962d6"
    },
    "response_from_http_client": 201,
    "next_try": null
  },
  {
    "id": 2,
    "account_id": 1,
    "webhook_id": 1,
    "model": {
        "id": 1,
        "timestamp": 1423472753,
        "payload": {
            "id": 1234,
            "archived": false,
            "color": null,
            "name": "A client",
            "notes": "",
            "created_at": "2015-02-04T16:40:23.000Z",
            "updated_at": "2015-02-09T09:05:53.581Z",
            "action": "delete",
            "type": "client"
        }
    },
    "user": {
        "id": 1,
        "name": "Shaun Prestor",
        "email": "shaun@example.com"
    },
    "action": "delete",
    "attempts": 1,
    "status": "delivered",
    "last_sent_on": "2015-02-09T09:05:55.185Z",
    "created_at": "2015-02-09T09:05:53.684Z",
    "request_headers": {
        "User-Agent": "ResourceGuru/Webhooks",
        "Content-Type": "application/json",
        "X-ResourceGuru-Key": "secret",
        "X-ResourceGuru-Signature": "d0537e5b65fdd97c3722f53569ba2e89335889fa25f235c5d864f1d9422ec400"
    },
    "response_from_http_client": 201,
    "next_try": null
  }
]
```

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier for a payload.
account_id | integer | The id of the account to which the payload belongs.
webhook_id | integer | The id of the account to which the webhook belongs.
model | object | The data which has changed based on the events for the webhook.
user | object | The User that performed the action described by this payload.
action | string | The action which has taken place which can either be "create", "update" or "delete".
attempts | integer | The number of times which the delivery of the payload has been attempted.
status | string | Identifies the state the payload is currently in. Details in the [Payload statuses](#payload-statuses) table below.
created_at | timestamp | Date and time created in ISO8601.
last_sent_on | timestamp | Date and time last sent on in ISO8601. `null` if no attempt has been made to send the payload yet.
request_headers | object | The request headers sent with the payload.
response_from_http_client | integer | The response code received from the remote endpoint.
next_try | timestamp | Date and time of the next attempt to send the payload formatted as ISO8601. `null` if no further attempt is scheduled.

#### Payload Statuses

Status | Description
---    | ---
Pending   | No attempt has been made to send the payload yet.
Delivered | The payload has been successfully delivered (The remote server responded with 2XX).
Failing   | The attempt to send the payload has failed. (The remote server timed out or responded with non-2XX)
Failed    | The payload delivery has failed 100 times and will not automatically try again.
