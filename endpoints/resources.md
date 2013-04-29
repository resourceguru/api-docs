# Resources

## Get Resources

* {GET /resources} returns all active Resources.
* {GET /resources/archived} returns all archived Resources.

```json
[
  {
    "id": 1,
    "url": "/resources/1"
  },
  {
    "id": 2,
    "url": "/resources/2"
  }
]
```

## Get Resource

* {GET /resources/1} returns the specified Resource.

```json
{
  "id": 1
}
```
