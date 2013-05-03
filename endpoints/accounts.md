# Accounts

## Get Accounts

* `GET /v1/accounts` returns an `Array` of **Active Accounts**.

### Response

```json
[
  {
    "id": 1,
    "name": "Example Corp",
    "url": "https://api.resourceguruapp.com/v1/accounts/1"
  },
  {
    "id": 2,
    "name": "ACME",
    "url": "https://api.resourceguruapp.com/v1/accounts/2"
  }
]
```

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier for an Account.
name | string | Name of an Account.
url | string | URL to view an Account.

## Get Account

* `GET /v1/accounts/1` returns the specified Account.

### Response

```json
{
  "id": 1,
  "name": "Example Corp",
  "subdomain": "example-corp",
  "updated_at": "2013-04-30T12:00:00+00:00",
  "owner": {
    "name": "John Doe",
    "email": "johndoe@example.com",
    "image": "https://resourceguru.s3.amazonaws.com/images/card_69cb-7f96ae8b2e17.png",
    "timezone": "London"
  }
}
```

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier for this Account.
name | string | Name of this Account.
subdomain | string | Subdomain for this Account.
updated_at | string | Last updated date and time in ISO 8601.
owner | hash | Owner of this Account. [(Details)](#owner-key)

#### Owner Key

Key | Type | Description
--- | --- | ---
name | string | Name of the Account Owner.
email | string | Email address of the Account Owner.
image | string | Profile image of the Account Owner.
timezone | string | Timezone of the Account Owner.

