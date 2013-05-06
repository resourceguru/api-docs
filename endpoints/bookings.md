# Bookings

```json
[
  {
    "id": 1,
    "client_id": null,
    "project_id": 1,
    "notes": "Some notes",
    "resource_id": 1,
    "durations": [
      {
        "date": "2013-01-01",
        "duration": 180,
        "start_time": 540,
        "end_time": 720
      },
      {
        "date": "2013-01-02",
        "duration": 180,
        "start_time": 540,
        "end_time": 720
      },
      {
        "date": "2013-01-03",
        "duration": 180,
        "start_time": 540,
        "end_time": 720
      }
    ],
    "booker": {
      "name": "Name",
      "email": "Email",
      "color": "#FFCC00"
    }
  }
]
```

## Notes

`duration`: Minutes
`start_time`: Minutes from midnight, Can be null
`durations[0].start_time`: Minutes from midnight
`durations[0].end_time`: `start_time` + `duration`
