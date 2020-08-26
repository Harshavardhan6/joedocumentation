# GET SUBSCRIPTIONS

---
Retrieves all the subscriptions of a user.
---

* This `curl` command retrieves all the subscriptions of a user.

```
Request :
curl -sS -X GET -H "Accept: application/json"  https://api.jacob.run/1.0/events/subscriptions?apikey=abcdefghijklmnop

```

``` 
Responses :
    200 - Ok, Return a list of all the subscriptions of a user.
    400 - Bad Request.
    404 - Notfound.
```

Example Response for 200-Ok: Returns a list of 

```json
[
  {
    "createdAt": "string",
    "creator": "string",
    "event": "string",
    "identifier": {
      "type": "string",
      "value": "string"
    },
    "subscriptionId": "string",
    "webhook": {
      "authentication": {
        "header": "string",
        "key": "string",
        "password": "string",
        "queryParam": "string",
        "type": "string",
        "user": "string"
      },
      "url": "string"
    }
  }
] 
```