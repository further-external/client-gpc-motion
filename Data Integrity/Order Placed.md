# Order Placed

Event should fire whenever a user successfully completes an order and the order confirmation is displayed.

## Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Order Placed",
  "transaction": {
    "transactionID": "<transactionID>",
    "quote": "<quote>",
    "total": {
      "currency": "<currency>"
    },
    "email": "<email>",
    "profile": {
      "address": {
        "stateProvince": "<stateProvince>",
        "postalCode": "<postalCode>"
      }
    },
    "payment": {
      "paymentMethod": "<paymentMethod>"
    },
    "shippingCost": "<shippingCost>",
    "shippingGroup": {
      "shippingMethod": "<shippingMethod>"
    },
    "purchaseCompletion": {
      "contactEdit": "<contactEdit>",
      "poNumber": "<poNumber>",
      "releaseNumber": "<releaseNumber>",
      "attachment": "<attachment>",
      "changeShipping": "<changeShipping>",
      "motionAccountCC": "<motionAccountCC>"
    },
    "item": [{
      "productInfo": {
        "sku": "<sku>",
        "productID": "<productID>",
        "brand": "<brand>",
        "inventoryStatus": "<inventoryStatus>",
        "promoPricing": "<promoPricing>",
        "specialPricingInitiative": "<specialPricingInitiative>"
      },
      "price": {
        "basePrice": "<basePrice>",
        "sellingPrice": "<sellingPrice>"
      },
      "quantity": "<quantity>",
      "moq": "<moq>"
    }]
  }
});
```

## Variable Definition

Here's the table with the Required column removed:

| Variable | Type | Description | Example |
|---|---|---|---|
| `transaction.transactionID` | string | Unique order ID, 6–20 alphanumeric; key for post-transaction data upload | `0001582610` |
| `transaction.quote` | string | `"yes"` if submitted as a quote, else `"no"` | `no` |
| `transaction.total.currency` | string | ISO 4217, 3-char uppercase | `USD` |
| `transaction.email` | string | **SHA-256 hex hash** of purchaser email.| `b1c53f9a…e8f901` |
| `transaction.profile.address.stateProvince` | string | Billing state/province | `AL` |
| `transaction.profile.address.postalCode` | string | **Truncated**: 5-digit ZIP (US) / first-3-char FSA (CA). | `35211` |
| `transaction.payment.paymentMethod` | string | Payment method: `Credit Card`, `Motion Account`, `Motion Account using credit card`, etc. | `Motion Account using credit card` |
| `transaction.shippingCost` | string | Shipping cost | `20.00` |
| `transaction.shippingGroup.shippingMethod` | string | `[complete/partial]:[freight account yes/no]:[method detail]`. Exclude user-entered comment text | `Complete:no:CO:AAAC:AAA COURIER` |
| `transaction.purchaseCompletion.contactEdit` | string | `"Y"`/`"N"` — user edited contact information | `Y` |
| `transaction.purchaseCompletion.poNumber` | string | `"Y"`/`"N"` — user entered a P.O. number | `N` |
| `transaction.purchaseCompletion.releaseNumber` | string | `"Y"`/`"N"` — user entered a release number | `N` |
| `transaction.purchaseCompletion.attachment` | string | `"Y"`/`"N"` — user added an attachment | `N` |
| `transaction.purchaseCompletion.changeShipping` | string | `"Y"`/`"N"` — user changed shipping | `Y` |
| `transaction.purchaseCompletion.motionAccountCC` | string | `"Y"`/`"N"` — Motion Account used as payment method | `N` |
| `transaction.item[].productInfo.sku` | string | SKU of purchased item | `07636651` |
| `transaction.item[].productInfo.productID` | string | Unique product identifier | `07636651` |
| `transaction.item[].productInfo.brand` | string | Product brand | `FESTO CORPORATION` |
| `transaction.item[].productInfo.inventoryStatus` | string | Inventory status | `in-stock-no-detail` |
| `transaction.item[].productInfo.promoPricing` | string | `"yes"`/`"no"` — purchased at promotional price  | `no` |
| `transaction.item[].productInfo.specialPricingInitiative` | string | Explicit fallback `false` | `false` |
| `transaction.item[].price.basePrice` | string | MSRP; unformatted, ≤2 decimals, `"0"` fallback| `26.64` |
| `transaction.item[].price.sellingPrice` | string | Price paid after discounts | `16.14` |
| `transaction.item[].quantity` | string | Units purchased . | `1` |
| `transaction.item[].moq` | string | `true` if the product's MOQ has not been met  | `true` |
