# DELETE SUBSCRIPTION

---
Unsubscribing/Deleting a subscription.
---

* This `curl` command is used for unsubscribing/deleting a subscription.

```
Request :
curl -sS -X DELETE https://api.jacob.run/1.0/events/subscriptions/{subscriptionId}?apikey=abcdefghijklmnop

```

```
Responses :
    200 - Ok, Successfully deleted subscription.
    400 - Bad Request.
    404 - Notfound.
```
