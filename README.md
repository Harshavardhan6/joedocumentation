# JOE Order Documentation

---
The Main idea behind this API is to allow users to place orders by themselves with Jacob Elektronik, which potentially cuts short the long Customer EDI integration time.
---

## CustomerOrder API

Users have the opportunity to place the orders via this Customer order API. All the user needs to have is a [OpenTRANS](https://www.digital.iao.fraunhofer.de/de/publikationen/OpenTRANS21.html) XML file. This API takes the user's XML file and places the order at Jacob. If the order was successfully placed, the user receives a success response. If the order has any errors, the user gets notified about the problem, enabling him/her to make appropriate changes to the order.

```plantuml
@startuml

actor User

User -> CustomerOrderApi : OpenTRANS XML

CustomerOrderApi --> User : if "Order Ok" then "Order successfully placed."

CustomerOrderApi --> User : if "Order Error" then " Sorry, the Order XML has some errors, please make the following changes to continue"

@enduml

```  

## Order Information
Base-url : https://api.jacob.run/1.0/joe

| Url | Method | Short Description | Details Page |
| :--- | :--- | :--- | :--- |
| `Base-url?apikey=4711` | `GET` | Retrieves a list of all orders. | [Link](customerOrderApi/getOrders.md) |
| `Base-url?apikey=4711` | `POST` | Creates a new order. | [Link](customerOrderApi/createOrder.md) |

----------------------------------------------------------------------------------------------------------------------------------------

## Document Polling

The CustomerOrder API also serves its users with documents like, Orders, Invoices, DispatchNotes, OrderResponses. After successfully placing the order, the user can use the orderId to retrieve different documents related to the placed order. This also allows means for checking if a certain document is available yet.

```plantuml
@startuml

actor User

User -> CustomerOrderApi : makes a request for documents with an orderId (order,invoice, dispatch, orderresponse)

CustomerOrderApi --> User : returns the XML documents  

@enduml
```

## Documents Polling Information
Base-url : https://api.jacob.run/1.0/joe

| Url | Method | Short Description | Details Page |
| :--- | :--- | :--- | :--- |
| `Base-url/orderId/document?apikey=4711` | `GET` | Retrieves the different documents related to a particular order with the given orderId. | [Link](documentPolling/documentPolling.md) |

----------------------------------------------------------------------------------------------------------------------

## Subscription API

The Users also have a possibility of registering their endpoint's/url's, which gets notified whenever there is change in the state of the order.

Example events : 
- dispatch.generated
- invoice.generated
- response.generated

For this, the User has to make a subscription. Subscription API allows users to make subscriptions (or) register their endpoints and subscribe to specific events/state changes of the order, this registered endpoint is then notified letting the user know about the changes in their order.

```plantuml
@startuml

actor User

User -> SubscriptionApi : register their endpoint by making a subscription

SubscriptionApi --> User : if "Subscription Ok" then "Successfully subscribed"

@enduml
```
Users have the possibility to subscribe to specific events or can subscribe to all the available events.

A Subscription looks like this : 
 ```json
 {
  "event": "invoice.generated",
  "creator": "4711|tool|manual",
  "identifier": {
       "type": "customerId",
       "value": "4711"
   },
   "webhook": {
       "url": "https://example.customerendpoint.com/webhook"
   }
}
 ```

Subscription with Webhook Authentication type basic :
```json
{
  "event": "invoice.generated",
  "creator": "4711|tool|manual",
  "identifier": {
       "type": "customerId",
       "value": "4711"
   },
   "webhook": {
       "url": "https://example.customerendpoint.com/webhook",
       "authentication": {
           "type" : "basic",
           "user" : "foo",
           "password": "baa",
       }
   }
}
```

Subscription with Webhook Authentication type header :
```json
{
  "event": "invoice.generated",
  "creator": "4711|tool|manual",
  "identifier": {
       "type": "customerId",
       "value": "4711"
   },
   "webhook": {
       "url": "https://example.customerendpoint.com/webhook",
       "authentication": {
           "type" : "header",
           "header" : "x-api-key",
           "key": "fooBaa4711Lulu",
       }
   }
}
```

Subscription with Webhook Authentication type queryParam :
```json
{
  "event": "invoice.generated",
  "creator": "4711|tool|manual",
  "identifier": {
       "type": "customerId",
       "value": "4711"
   },
   "webhook": {
       "url": "https://example.customerendpoint.com/webhook",
       "authentication": {
           "type" : "queryParam",
           "queryParam" : "apikey",
           "key": "fooBaa4711Lulu",
       }
   }
}
```
 
```
* event          - It is the event on which the user wants to subscribe for.
* creator        - name of the creator.
* identifier     - Identifier has a type, which can be a customerId or an orderId and its corresponding value.
* webhook        - url here is the user's endpoint, which they want to register and this url gets notified whenever there is a change in the state of the order , depending on the events which the user subscribed to.

```

# Subscription Information
Base-url : https://api.jacob.run/1.0/events/subscriptions

| Url | Method | Short Description | Details Page |
| :--- | :--- | :--- | :--- |
| `Base-url?apikey=abcdefghijklmnop` | `GET` | Retrieves all the subscriptions of a user. | [Link](webhookSubscriptionApi/getSubscriptions.md)|
| `Base-url?apikey=abcdefghijklmnop` | `POST` | Creates a subscription. | [Link](webhookSubscriptionApi/createSubscription.md)|
| `Base-url/{subscriptionId}?apikey=abcdefghijklmnop` | `GET` | Retrieves a specific subscription with a subscriptionId. | [Link](webhookSubscriptionApi/getSubscription.md)|
| `Base-url/{subscriptionId}?apikey=abcdefghijklmnop` | `PUT` | Replaces the whole subscription and updates it | [Link](webhookSubscriptionApi/putSubscription.md)|
| `Base-url/{subscriptionId}?apikey=abcdefghijklmnop` | `PATCH` | Checks for update and if necessary, updates the subscription | [Link](webhookSubscriptionApi/patchSubscription.md)|
| `Base-url/{subscriptionId}?apikey=abcdefghijklmnop` | `DELETE` | Deletes a subscription | [Link](webhookSubscriptionApi/deleteSubscription.md)|