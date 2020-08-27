# GET documents

---
Retrieves the different documents related to a particular order with the given orderId.
---

* This curl command retrieves the different documents related to a particular order.

```
Document types : Order, Invoice, Dispatch, Response.

Request :
    curl -sS -X GET -H "Accept: application/xml" https://api.jacob.services/1.0/joe/orderId/document?apikey=9876

```

``` 
Responses :
    200 - Ok, Returns the XML document (Order/Invoice/Dispatch/Response).
    204 - The requested document is currently not available.
    400 - Bad Request.
    406 - The request contained an unsupported 'Accept' header.
```
--------------------------------------------------------------------------------------
Example Response : 