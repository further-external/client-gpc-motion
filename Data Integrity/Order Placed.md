# Order Placed

> **Status:** Current — Adobe Analytics Package 2
> **Contract validated:** 2026-09-02/03 on production beacons · 17 event families, 0 contract failures
> **Last updated:** 2026-09-16 — Package 2 field renames applied
>
> | From | To | Why |
> |---|---|---|
> | `productID` | `productId` | Package 2 rename — camelCase standardised across product fields |
> | `promoPricing` | `promotionalPricing` | Package 2 rename — full word, matches the SDR friendly name |
> | `moq` | `minimumPurchaseQuantityNotMet` | Package 2 rename — explicit name replaces the `moq` abbreviation |
> | `transactionID` | `transactionId` | Package 2 rename — camelCase standardised |
> | `poNumber` | `purchaseOrderNumber` | Package 2 rename — explicit name replaces the `poNumber` abbreviation |
> | `"yes"/"no"`, `"true"/"false"`, `"Y"/"N"` | `"TRUE"`/`"FALSE"` | Package 2 ruled these string booleans uppercase |
>
> Only fields present on this page are listed. See the repository README for the full Package 2 change set.

Event should fire whenever a user successfully completes an order and the order confirmation is displayed.

## Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Order Placed",
  "transaction": {
    "transactionId": "<transactionId>",
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
      "purchaseOrderNumber": "<purchaseOrderNumber>",
      "releaseNumber": "<releaseNumber>",
      "attachment": "<attachment>",
      "changeShipping": "<changeShipping>",
      "motionAccountCC": "<motionAccountCC>"
    },
    "item": [{
      "productInfo": {
        "sku": "<sku>",
        "productId": "<productId>",
        "brand": "<brand>",
        "inventoryStatus": "<inventoryStatus>",
        "promotionalPricing": "<promotionalPricing>",
        "specialPricingInitiative": "<specialPricingInitiative>"
      },
      "price": {
        "basePrice": "<basePrice>",
        "sellingPrice": "<sellingPrice>"
      },
      "quantity": "<quantity>",
      "minimumPurchaseQuantityNotMet": "<minimumPurchaseQuantityNotMet>"
    }]
  }
});
```

## Variable Definition

| Variable | Type | Description | Example |
|---|---|---|---|
| `transaction.transactionId` | string | Unique order ID, 6–20 alphanumeric; key for post-transaction data upload | `0001582610` |
| `transaction.quote` | string | `"TRUE"` if submitted as a quote, else `"FALSE"` | `FALSE` |
| `transaction.total.currency` | string | ISO 4217, 3-char uppercase | `USD` |
| `transaction.email` | string | **SHA-256 hex hash** of purchaser email.| `b1c53f9a…e8f901` |
| `transaction.profile.address.stateProvince` | string | Billing state/province | `AL` |
| `transaction.profile.address.postalCode` | string | **Truncated**: 5-digit ZIP (US) / first-3-char FSA (CA). | `35211` |
| `transaction.payment.paymentMethod` | string | Payment method: `Credit Card`, `Motion Account`, `Motion Account using credit card`, etc. | `Motion Account using credit card` |
| `transaction.shippingCost` | string | Shipping cost | `20.00` |
| `transaction.shippingGroup.shippingMethod` | string | `[complete/partial]:[freight account yes/no]:[method detail]`. Exclude user-entered comment text | `Complete:no:CO:AAAC:AAA COURIER` |
| `transaction.purchaseCompletion.contactEdit` | string | `"Y"`/`"N"` — user edited contact information | `Y` |
| `transaction.purchaseCompletion.purchaseOrderNumber` | string | `"TRUE"`/`"FALSE"` — user entered a P.O. number | `N` |
| `transaction.purchaseCompletion.releaseNumber` | string | `"TRUE"`/`"FALSE"` — user entered a release number | `N` |
| `transaction.purchaseCompletion.attachment` | string | `"TRUE"`/`"FALSE"` — user added an attachment | `N` |
| `transaction.purchaseCompletion.changeShipping` | string | `"Y"`/`"N"` — user changed shipping | `Y` |
| `transaction.purchaseCompletion.motionAccountCC` | string | `"Y"`/`"N"` — Motion Account used as payment method | `N` |
| `transaction.item[].productInfo.sku` | string | SKU of purchased item | `07636651` |
| `transaction.item[].productInfo.productId` | string | Unique product identifier | `07636651` |
| `transaction.item[].productInfo.brand` | string | Product brand | `FESTO CORPORATION` |
| `transaction.item[].productInfo.inventoryStatus` | string | Inventory status | `in-stock-no-detail` |
| `transaction.item[].productInfo.promotionalPricing` | string | `"TRUE"`/`"FALSE"` — purchased at promotional price  | `FALSE` |
| `transaction.item[].productInfo.specialPricingInitiative` | string | Explicit fallback `FALSE` | `FALSE` |
| `transaction.item[].price.basePrice` | string | MSRP; unformatted, ≤2 decimals, `"0"` fallback| `26.64` |
| `transaction.item[].price.sellingPrice` | string | Price paid after discounts | `16.14` |
| `transaction.item[].quantity` | string | Units purchased | `1` |
| `transaction.item[].minimumPurchaseQuantityNotMet` | string | `TRUE` if the product's MOQ has not been met  | `TRUE` |
