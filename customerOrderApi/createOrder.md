# PLACE ORDER

---
Creates an order with the orderId of the user.
---

This is an example of a OpenTRANS XML document:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ORDER>
	<ORDER_HEADER>
		<CONTROL_INFO>
			<GENERATION_DATE>2020-08-10T10:05:38</GENERATION_DATE>
		</CONTROL_INFO>
		<ORDER_INFO>
			<ORDER_ID>987654321</ORDER_ID>
			<ORDER_DATE>2020-08-10T10:05:37</ORDER_DATE>
			<LANGUAGE>ger</LANGUAGE>
			<PARTIES>
				<PARTY>
					<PARTY_ID>1234567</PARTY_ID>
					<PARTY_ROLE>buyer</PARTY_ROLE>
					<ADDRESS>
						<NAME>Herr</NAME>
						<NAME2>Max Mustermann</NAME2>
						<STREET>Musterstraße 123</STREET>
						<ZIP>12345</ZIP>
						<CITY>Musterstadt</CITY>
						<COUNTRY>Deutschland</COUNTRY>
						<COUNTRY_CODED>DE</COUNTRY_CODED>
						<EMAIL>someone@example.com</EMAIL>
					</ADDRESS>
				</PARTY>
				<PARTY>
					<PARTY_ID>556677</PARTY_ID>
					<PARTY_ROLE>supplier</PARTY_ROLE>
					<ADDRESS>
						<NAME>JACOB Elektronik GmbH</NAME>
						<STREET>An der Roßweid 5</STREET>
						<ZIP>76229</ZIP>
						<CITY>Karlsruhe</CITY>
						<COUNTRY>Deutschland</COUNTRY>
						<COUNTRY_CODED>DE</COUNTRY_CODED>
						<EMAIL>info@jacob.de</EMAIL>
					</ADDRESS>
				</PARTY>
				<PARTY>
					<PARTY_ID>1234567</PARTY_ID>
					<PARTY_ROLE>delivery</PARTY_ROLE>
					<ADDRESS>
						<NAME>Herr</NAME>
						<NAME2>Max Mustermann</NAME2>
						<STREET>Musterstraße 123</STREET>
						<ZIP>12345</ZIP>
						<CITY>Musterstadt</CITY>
						<COUNTRY>Deutschland</COUNTRY>
						<COUNTRY_CODED>DE</COUNTRY_CODED>
						<EMAIL>someone@example.com</EMAIL>
					</ADDRESS>
				</PARTY>
			</PARTIES>
			<CUSTOMER_ORDER_REFERENCE>
				<ORDER_ID>987654321</ORDER_ID>
			</CUSTOMER_ORDER_REFERENCE>
			<ORDER_PARTIES_REFERENCE>
				<BUYER_IDREF>112233</BUYER_IDREF>
				<SUPPLIER_IDREF>556677</SUPPLIER_IDREF>
			</ORDER_PARTIES_REFERENCE>
			<CURRENCY>EUR</CURRENCY>
		</ORDER_INFO>
	</ORDER_HEADER>
	<ORDER_ITEM_LIST>
		<ORDER_ITEM>
			<LINE_ITEM_ID>1</LINE_ITEM_ID>
			<PRODUCT_ID>
				<SUPPLIER_PID>430324</SUPPLIER_PID>
				<BUYER_PID>999999999</BUYER_PID>
				<DESCRIPTION_SHORT>Haselnusstafel</DESCRIPTION_SHORT>
			</PRODUCT_ID>
			<QUANTITY>2</QUANTITY>
			<ORDER_UNIT>C62</ORDER_UNIT>
			<PRODUCT_PRICE_FIX>
				<PRICE_AMOUNT>10.45</PRICE_AMOUNT>
			</PRODUCT_PRICE_FIX>
			<PRICE_LINE_AMOUNT>20.90</PRICE_LINE_AMOUNT>
		</ORDER_ITEM>
	</ORDER_ITEM_LIST>
	<ORDER_SUMMARY>
		<TOTAL_ITEM_NUM>1</TOTAL_ITEM_NUM>
		<TOTAL_AMOUNT>20.90</TOTAL_AMOUNT>
	</ORDER_SUMMARY>
</ORDER>
``` 
  
- POST:
      consumes:
      - application/json
      - application/xml

* This `curl` command will create an Order in the CustomerOrder Api with the contents of the joe_order.user_order.xml : 

```
Request :
curl -vsS -X POST -H "Content-Type: application/xml" -d @joe_order.user_order.xml https://api.jacob.run/1.0/joe?apikey=12345

```

``` 
Responses :
    201 - Status created, for a successfully placed order.
    400 - Bad Request.
    409 - An order with this Id already exists.
```

XML Definition : 


| XML Field | Description | More information | data type | example value |
| -------------- | :--------- | ----------:| ----------:|----------:|
| ORDER_INFO |  administrative information on the order is summarized | - | - | - |
| ORDER_ID | The orderId of the user | - | string | 987654321 |
| ORDER_DATE | Date of the order  | format :yyyy-MM-dd'T'HH:mm:ss | date | 2020-08-10T10:05:38 |
| LANGUAGE  | Language | - | string | ger(german) |
| ------  | ----- | ------ | ----- | ----- |
| PARTIES |  List of parties that are relevant to this business document | - | - | - |
| PARTY |   Information about a business partner | - | - | - |
| PARTY_ID |    Unique identifier ID of the business partner |  buyer_specific/customer_specific/supplier_specific  | string | 1234567 |
| PARTY_ROLE |     Role of the business partner in the context of this document | - | string | buyer/supplier/delivery |
| ADDRESS |     Address information of a business partner  | - | - | - |
| NAME |      Name of the organisation/salutation   | - | string | JACOB Elektronik GmbH/ Herr |
| NAME2 |      Additional space for name   |  name of the specific individual | string | Max Mustermann |
| STREET |      Street name and house number  | - | string | Musterstraße 123 |
| ZIP |      ZIP code of address   | - | string | 12345 |
| CITY |       Town or city of the company   | - | string | Musterstadt |
| COUNTRY |       Country   | - | string | Deutschland |
| COUNTRY_CODED |       Code of the Country   | - | string | DE |
| EMAIL |       e-mail address   | - | string | someone@example.com |
| ------  | ----- | ------ | ----- | ----- |
| CUSTOMER_ORDER_REFERENCE  |  related to an item and refers to the previous order where the item was ordered by the customer (purchasing party) | ------ | ----- | ----- |
| ORDER_ID |  Unique order number of the buyer/ orderId of the user  | Same as mentioned in the ORDER_INFO->ORDER_ID | string | 987654321 |
| ------  | ----- | ------ | ----- | ----- |
| ORDER_PARTIES_REFERENCE  |  related to an item and refers to the previous order where the item was ordered by the customer (purchasing party) | ------ | ----- | ----- |
| BUYER_IDREF  |  reference to the buyer|  The reference has to point to a (PARTY_ID) that is defined in the document (PARTY element buyer) | string | 112233 |
| SUPPLIER_IDREF | reference to the supplier| The reference has to point to a (PARTY_ID) that is defined in the document (PARTY element supplier) | string | 556677 |
| CURRENCY  | Currency information | ------ | string | EUR |
| ------  | ----- | ------ | ----- | ----- |
| ORDER_ITEM_LIST  |  represents the lists of items in the order | ------ | ----- | ----- |
| ORDER_ITEM  | contains order information about exactly one item |  Any number of item lines can be used, although at least one item line must be used | ----- | ----- |
| LINE_ITEM_ID  |  The item ID number is used to uniquely identify the item line of an order within that order | ------ | string | 1 |
| PRODUCT_ID  |  Identifier of the product | ------ | ----- | ----- |
| SUPPLIER_PID  | Supplier's product ID | ------ | string | 430324 |
| BUYER_PID  | Product ID of the buying company  | ------ | string | 999999999 |
| DESCRIPTION_SHORT  | short description of the product | ------ | string | Haselnusstafel |
| QUANTITY  |  Quantity  | ------ | ----- | 2 |
| ORDER_UNIT  | Unit in which the product can be ordered | It is only possible to order multiples of the product unit. | string | C62 |
| PRODUCT_PRICE_FIX  |  A fixed product price  | ------ | ----- | ----- |
| PRICE_AMOUNT  |  Amount of the price of order item  | ------ | int | 10.45 |
| PRICE_LINE_AMOUNT  | The total price of the item-line | (PRICE_AMOUNT*QUANTITY) | int | 20.90 |
| ORDER_SUMMARY  | The summary contains information on the number of item lines in the order | This figure is used for control purposes to make sure that all items have been transferred | ----- | ----- |
| TOTAL_ITEM_NUM  |  Contains the total number of item lines in the business document | ------ | count | 1 |
| TOTAL_AMOUNT  |  Total amount covering all items in this business document.  | ------ | ----- | 20.90 |

```
* PRICE_LINE_AMOUNT In the normal case the value results from multiplying  but has to be explicitly quoted. The element PRICE_LINE_ AMOUNT can result from multiplying PRICE_AMOUNT and PRICE_UNIT_VALUE if the price is not connected to the ordered unit but to another price-unit.
```

