# Accounts

## Get Accounts

* `GET /accounts` returns an `Array` of active Accounts.

```json
[
  {
    "id": 1,
    "name": "Example Corp",
    "url": "/accounts/1"
  },
  {
    "id": 2,
    "name": "ACME",
    "url": "/accounts/2"
  }
]
```

## Get Account

* `GET /accounts/1` returns the specified Account.

```json
{
  "id": 1,
  "name": "Example Corp",
  "subdomain": "example-corp",
  "owner": {
    "name": "John Doe",
    "email": "johndoe@example.com",
    "image": "https://resourceguru.s3.amazonaws.com/images/user/1/image/card_69cb-7f96ae8b2e17.png",
    "timezone": "London"
  }
}
```
