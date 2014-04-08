# Resource Guru API

This is a REST-style API that uses serialized JSON and OAuth 2 authentication.

## Making Requests

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
* [Clients](./endpoints/clients.md)
* [Projects](./endpoints/projects.md)
* [Resources](./endpoints/resources.md)
* [Resource Types](./endpoints/resource_types.md)
* [Users](./endpoints/users.md)
* Reports
  * [Resources](./endpoints/reports/resources.md)
  * [Projects](./endpoints/reports/projects.md)
  * [Clients](./endpoints/reports/clients.md)
