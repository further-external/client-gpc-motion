# Order Placed

This event is set whenever an order is completed.

---

## Javascript Code

```js
appEventData || [];
appEventData.push({
  "event": "Order Placed",
  "transaction": {
    "total": {
      "currency": "<currency>"
    },
    "transactionID": "<transactionID>",
    "quote": "<quote>",
    "profile": {
      "address": {
        "stateProvince": "<stateProvince>",
        "postalCode": "<postalCode>"
      }
    },
    "payment": {
      "paymentMethod": "<paymentMethod>"
    },
    "item": [{
      "price": {
        "sellingPrice": "<sellingPrice>"
      },
      "productInfo": {
        "productID": "<productID>",
        "sku": "<sku>"
      },
      "quantity": "<quantity>",
      "moq": "<moq>",
      "moqRequired": "<moqRequired>",
      "promoPricing": “<promoPricing>”,
      "priceChange": "<priceChange>"
    }],
    "shippingCost": "<shippingCost>",
    "shippingGroup": {
      "shippingMethod": "<shippingMethod>"
    },
    "purchaseCompletion": {
      "checkoutOptions": "<checkoutOptions>", 
      "contactEdit": "<contactEdit>",
      "poNumber": "<poNumber>",
      "releaseNumber": "<releaseNumber>",
      "attachment": "<attachment>",
      "changeShipping": "<changeShipping>",
      "motionAccountCC": "<motionAccountCC>”
  }
});
```
---

## Variable Definitions


| field           | type    | description                                                                                                                                                                                                                                                  | examples                                                                                               | pattern                                                                                             | minLength | maxLength |
| :-------------: | :-----: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------------------: | :-------: | :-------: |
| currency        | string  | Currency of the transaction. ISO 4217 (3 character alpha), uppercase                                                                                                                                                                                         | USD,CAD,GBP,CHF                                                                                        | ^\[A-Z\]{3}$                                                                                        | 3         | 3         |
| transactionID   | string  | Unique identifier of the transaction. Max Length 20. Used as a key for upload of post transaction data.                                                                                                                                                      |                                                                                                        | ^\[a-zA-Z0-9\]{6,20}$                                                                               | 6         | 20        |
| stateProvince   | string  | The mailing state or province associated with billing address.                                                                                                                                                                                               | WI,GA,NB,ON                                                                                            |                                                                                                     |           |           |
| postalCode      | string  | The mailing zip or postal code associated with the billing address.                                                                                                                                                                                          | 53533,30381,M1R 0E9,M3C 0C1                                                                            |                                                                                                     |           |           |
| paymentMethod   | string  | Describes the method of payment for a transaction.                                                                                                                                                                                                           | Credit Card,PayPal,Mastercard,Visa,Amex,Discover, **Motion Account, Motion Account using credit card** |                                                                                                     |           |           |
| sellingPrice    | string  | String representation of the price paid after coupons or discounts. Positive. Up to two decimal places for cents. No currency symbol.                                                                                                                        | 200,29.99,50,0                                                                                         | ^\[0-9\]\*(.\[0-9\]{1,2})?$                                                                         |           |           |
| productID       | string  | Unique Identifier of a product or offering. Must match the format of back-end systems if used as a key for import of product meta data. Most often, one level above SKU for products with SKU variants.                                                      | 155,65588,987764448                                                                                    |                                                                                                     |           |           |
| sku             | string  | Stock Keeping Unit (SKU) Unique Identifier of specific item (typically) held in inventory. Must match the format of back-end systems if used as a key for import of product meta data. Most often, one level below productID for products with SKU variants. | 34567890,4567890,00155-large-cornflower                                                                |                                                                                                     |           |           |
| quantity        | integer | Integer number of products being acted upon (added to a cart, removed from wishlist, purchased, reserved, moved to a cart from save for later or save to list)                                                                                               | 1,2,3,4,5                                                                                              |                                                                                                     |           |           |
| moq             | string  | Set with a value of “true” if the product’s minimum order quantity has not been met. Otherwise, this is set to “false”.                                                                                                                                      |                                                                                                        |                                                                                                     |           |           |
| moqRequired     | string  | Set with a value of "yes" or "no" when a product is added to cart.                                                                                                                                                                                           | yes OR no                                                                                              |                                                                                                     |           |           |
| quote           | string  | Set with “yes” if the order was submitted as a quote. Otherwise, set to “no”.                                                                                                                                                                                | Yes/No
| **shippingCost** | string | This is the cost associated with the shipping option a user selects.| 0.00, 20.00, 15.00 ||                                                                                                     |           |           |
| shippingMethod  | string  | Describes the method or carrier and method of shipment. Should be common terminology within your business.                                                                                                                                                   | Complete:No:Fedex - Overnight                                                                          | \[complete/partial shipping\]:\[yes/no for freight account used\]:\[detailed shipping method info\] |           |           |
| checkoutOptions | string  | Describes the selected                                                                                                                                                                                                                                       | Yes/No                                                                                                 |                                                                                                     |           |           |
| contactEdit     | string  | If the user made an edit to the contact information                                                                                                                                                                                                          | Yes/No                                                                                                 |                                                                                                     |           |           |
| poNumber        | string  | Set with “yes” if the user entered a P.O. Number, set to “no” otherwise                                                                                                                                                                                      | Yes/No                                                                                                 |                                                                                                     |           |           |
| releaseNumber   | string  | Set with “yes” if the user entered a release number, set to “no” otherwise                                                                                                                                                                                   | Yes/No                                                                                                 |                                                                                                     |           |           |
| attachment      | string  | Set with “yes” if the user added an attachment, set to “no” otherwise                                                                                                                                                                                        | Yes/No                                                                                                 |                                                                                                     |           |           |
| changeShipping  | string  | Set with “yes” if the user changed the shipping, set to “no” otherwise                                                                                                                                                                                       | Yes/No                                                                                                 |                                                                                                     |           |           |
| motionAccountCC | string  | Set with “yes” if the user used the Motion Account for payment method, set to “no” otherwise                                                                                                                                                                 | Yes/No                                                                                                 |                                                                                                     |           |           |
| promoPricing    | string  | A flag representing if the product is currently seen or purchased at a promotional price.                                                                                                                                                                    | yes, no                                                                                                |                                                                                                     |           |           |
| priceChange     | string  | With the 2025 conversion initiative, this is a dedicated field in place to indicate those products which are subject to that pricing initiative - the desired example field should be the month and year for the permanent price change                      | April2025, May2025, January2026                                                                        |                                                                                                     |           |           |
