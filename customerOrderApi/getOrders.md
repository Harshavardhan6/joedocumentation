# GET orders

---
Retrieves a list of orders .
---


* This `curl` command will retrieve a list of orders 
```
Request :

Accept types : 
 - application/xml  - Returns a list of XML orders.
 - application/json - Returns a list of Json orders.

curl -sS -X GET -H "Accept: application/xml" https://api.jacob.run/1.0/joe?apikey=12345

curl -sS -X GET -H "Accept: application/json"  https://api.jacob.run/1.0/joe?apikey=12345

```

``` 
Responses :
    200 - Ok, Returns a list of orders for the given CustomerId.
    400 - Bad Request.
    406 - The request contained an unsupported 'Accept' header.

--------------------------------------------------------------------------------------

response xml example : List of all orders

