# Resource Guru API

This is a REST-style API that uses serialized JSON and OAuth 2 authentication.

## Making Requests

### The Base URL

All requests start with the `https://api.resourceguruapp.com/{version}` base URL.

* `version`: API version. Current version is `v1`.
* All requests are done via SSL.
* All responses are in JSON.

### Making a Basic Request

With the exception of [Accounts](./endpoints/accounts.md) all requests must be appended with the `account subdomain`
and the path.

To make a request for all the [Resources](./endpoints/resources.md) on the Example Corp account, the request URL will look
something like this `https://api.resourceguruapp.com/v1/example-corp/resources`.

## Authentication

## Limits

## Response Codes

## Endpoints

* [Accounts](./endpoints/accounts.md)
* [Clients](./endpoints/clients.md)
* [Resources](./endpoints/resources.md)
