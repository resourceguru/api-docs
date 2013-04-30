# Accounts

## Get Accounts

* `GET /accounts` returns an `Array` of active Accounts.

```json
[
  {
    "id": 1,
    "name": "Example Corp"
    "url": "/accounts/1"
  },
  {
    "id": 2,
    "name": "ACME"
    "url": "/accounts/2"
  }
]
```

## Get Account

* `GET /account/1` returns the specified Account.

```json
{
  "id": 1
  "name": "Example Corp"
  "subdomain": "example-corp"
  "owner": {
    "name": "John Doe"
    "email": "johndoe@example.com"
  }
}
```
