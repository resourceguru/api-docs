# Resources

## Get Resources

* `GET /{subdomain}/resources` returns an `Array` of active Resources.
* `GET /{subdomain}/resources/archived` returns an `Array` of archived Resources.

```json
[
  {
    "id": 1,
    "url": "https://api.resourceguruapp.com/v1/example-corp/resources/1"
  },
  {
    "id": 2,
    "url": "https://api.resourceguruapp.com/v1/example-corp/resources/2"
  }
]
```

## Get Resource

* `GET /{subdomain}/resources/1` returns the specified Resource.

```json
{
  "id": 1
}
```
