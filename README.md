# Resource Guru API

This is a REST-style API that uses serialized JSON and OAuth 2 authentication.

## Making Requests

### The Base URL

All requests start with the `https://{subdomain}.resourceguruapp.com/api/{version}` base URL.

* `subdomain`: Account subdomain
* `version`: API version. Current version is `v1`.
* All requests are done via SSL.
* All responses are in JSON.

### Making a Basic Request

To make a request for all the Resources on the ACME account, you would append the `/resources` path
to the base URL: `https://acme.resourceguruapp.com/api/v1/resources`
