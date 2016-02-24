# Resource Guru API

This is a REST-style API that uses serialized JSON and OAuth 2 authentication.

## Making Requests

### Encoding

The API expects all data to be UTF-8 encoded.

### The Base URL

All requests start with the `https://api.resourceguruapp.com/` base URL.

* All requests are done via SSL.
* All responses are in JSON.

### Making a Basic Request

With the exception of [Accounts](./endpoints/accounts.md) all requests must be appended with the `account subdomain`
and the path.

To make a request for all the [Resources](./endpoints/resources.md) on the Example Corp account, the request URL will look
something like this `https://api.resourceguruapp.com/v1/example-corp/resources`.

## Authentication

In order to make authorized calls to Resource Guru's API, your application must first obtain an OAuth access token.
To register your app go to https://developers.resourceguruapp.com.

Resource Guru implements OAuth2 with the authentication code flow.

Read our [OAuth2 authentication guide](./sections/authentication.md) to get started.

Once you have authenticated, you can get information about the authenticated user by calling `GET https://api.resourceguruapp.com/v1/me`. More details about the request and response are available on the [endpoint page](./endpoints/me.md).

## Rate Limiting

You can perform up to 33 requests per 10 second period on a registered application. If you exceed this limit, you'll get a 403 Rate Limit Exceeded response for subsequent requests. Check the Retry-After header to see how many seconds to wait before retrying the request.

## Response Codes

* `200` OK
* `201` Created
* `204` No Content
* `401` Unauthorized
* `403` Forbidden
* `404` Not Found
* `422` Unprocessable Entity
* `5xx` Resource Guru is having trouble

## Endpoints

* [Accounts](./endpoints/accounts.md)
* [Bookings](./endpoints/bookings.md)
* [Time Off](./endpoints/time_off.md)
* [Clients](./endpoints/clients.md)
* [Me](./endpoints/me.md)
* [Projects](./endpoints/projects.md)
* [Resources](./endpoints/resources.md)
* [Resource Types](./endpoints/resource_types.md)
* Reports
  * [Resources](./endpoints/reports/resources.md)
  * [Projects](./endpoints/reports/projects.md)
  * [Clients](./endpoints/reports/clients.md)
* [Users](./endpoints/users.md)
* [Webhooks](./endpoints/webhooks.md)
  * [Payloads](./endpoints/webhooks/payloads.md)
