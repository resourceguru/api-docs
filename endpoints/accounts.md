# Accounts

## Get Accounts

* `GET /v1/accounts` returns an `Array` of **Active Accounts** and **Suspended Accounts**.

### Response

```json
[
  {
    "id": 1,
    "name": "Example Corp",
    "subdomain": "example",
    "rootdomain":  "resourceguruapp.com",
    "url": "https://api.resourceguruapp.com/v1/accounts/1",
    "created_at": "2018-05-01T11:52:19.000Z",
    "updated_at": "2018-05-01T14:21:57.000Z"
  },
  {
    "id": 2,
    "name": "ACME",
    "subdomain": "acme",
    "rootdomain":  "resourceguruapp.com",
    "url": "https://api.resourceguruapp.com/v1/accounts/2",
    "created_at": "2015-05-01T11:52:19.000Z",
    "updated_at": "2018-06-01T14:21:57.000Z"
  }
]
```

Key | Type | Description
--- | --- | ---
id | integer | Unique identifier for an Account.
name | string | Name of an Account.
subdomain | string | The Account URL ID for the account. The account could previously be accessed on this subdomain.
rootdomain | string | Root domain account is served from.
url | string | URL to view an Account.
created_at | timestamp | Account created time in ISO 8601.
updated_at | datetime |  Last updated date and time in ISO 8601.

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
subdomain | string | The Account URL ID for the account. The account could previously be accessed on this subdomain.
updated_at | timestamp | Last updated date and time in ISO 8601.
owner | hash | Owner of this Account. [(Details)](#owner-key)

#### Owner Key

Key | Type | Description
--- | --- | ---
name | string | Name of the Account Owner.
email | string | Email address of the Account Owner.
image | string | Profile image of the Account Owner.
timezone | string | Timezone of the Account Owner.

