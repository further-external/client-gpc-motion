# Quote Placed

> **Status:** Current — Adobe Analytics Package 2
> **Contract validated:** 2026-09-02/03 on production beacons · 17 event families, 0 contract failures
> **Last updated:** 2026-09-16 — Package 2 field renames applied
>
> | From | To | Why |
> |---|---|---|
> | `productID` | `productId` | Package 2 rename — camelCase standardised across product fields |
> | `promoPricing` | `promotionalPricing` | Package 2 rename — full word, matches the SDR friendly name |
> | `moq` | `minimumPurchaseQuantityNotMet` | Package 2 rename — explicit name replaces the `moq` abbreviation |
> | `"yes"/"no"`, `"true"/"false"`, `"Y"/"N"` | `"TRUE"`/`"FALSE"` | Package 2 ruled these string booleans uppercase |
>
> Only fields present on this page are listed. See the repository README for the full Package 2 change set.

when a user successfully submits a quote request. Marks the start of the quote-to-order funnel and is used to measure quote volume and conversion.

## Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Quote Placed",
  "transaction": {
    "quoteId": "<quoteId>",
    "value": "<value>",
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
| `transaction.quoteId` | string | Unique quote identifier | `0001582493` |
| `transaction.value` | string | Total quote value; `"0"` as a fallback if quote order total is not available | `1000.00`, `0` |
| `transaction.total.currency` | string | ISO 4217, uppercase. | `USD` |
| `transaction.email` | string | SHA-256 hex hash. Capture shows clear text | `b1c53f9a…e8f901` |
| `transaction.profile.address.stateProvince` | string | Billing state/province | `AL` |
| `transaction.profile.address.postalCode` | string | Truncated: 5-digit ZIP (US) / 3-char FSA (CA) | `35211` |
| `transaction.item[].productInfo.sku` | string | SKU of quoted item | `10484964` |
| `transaction.item[].productInfo.productId` | string | Unique product identifier | `10484964` |
| `transaction.item[].productInfo.brand` | string | Product brand | `SUMITOMO DRIVE TECH` |
| `transaction.item[].productInfo.inventoryStatus` | string | Inventory status | `not-in-stock` |
| `transaction.item[].productInfo.promotionalPricing` | string | `"TRUE"`/`"FALSE"` | `FALSE` |
| `transaction.item[].productInfo.specialPricingInitiative` | string | Explicit fallback `FALSE` | `FALSE` |
| `transaction.item[].price.basePrice` | string | If the base price information is available provide it else `"0"` on unpriced quote items | `21.50`,`0` |
| `transaction.item[].price.sellingPrice` | string | If the selling price information is available provide it else `"0"` on unpriced quote items | `21.50`, `0` |
| `transaction.item[].quantity` | string | Units quoted | `1` |
| `transaction.item[].minimumPurchaseQuantityNotMet` | string | MOQ-not-met flag | `TRUE` |
