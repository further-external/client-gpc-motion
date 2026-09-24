# Checkout Step Encountered

> **Status:** Current — Adobe Analytics Package 2
> **Contract validated:** 2026-09-02/03 on production beacons · 17 event families, 0 contract failures
> **Last updated:** 2026-09-16 — Package 2 field renames applied
>
> | From | To | Why |
> |---|---|---|
> | `productID` | `productId` | Package 2 rename — camelCase standardised across product fields |
> | `promoPricing` | `promotionalPricing` | Package 2 rename — full word, matches the SDR friendly name |
> | `"yes"/"no"`, `"true"/"false"`, `"Y"/"N"` | `"TRUE"`/`"FALSE"` | Package 2 ruled these string booleans uppercase |
>
> Only fields present on this page are listed. See the repository README for the full Package 2 change set.

Event should fire on every checkout step render, including pre-filled steps for returning users and re-entry after a user edits a previous step.

## Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Checkout Step Encountered",
  "eventDetails": {
    "checkoutStep": "<checkoutStep>"
  },
  "product": [{
    "productInfo": {
      "sku": "<sku>",
      "productId": "<productId>",
      "brand": "<brand>",
      "inventoryStatus": "<inventoryStatus>",
      "quoteRequired": "<quoteRequired>",
      "promotionalPricing": "<promotionalPricing>",
      "specialPricingInitiative": "<specialPricingInitiative>"
    },
    "price": {
      "basePrice": "<basePrice>",
      "sellingPrice": "<sellingPrice>"
    },
    "quantity": "<quantity>"
  }]
});
```

## Variable Definition

| Variable | Type | Description | Example |
|---|---|---|---|
| `eventDetails.checkoutStep` | string | Checkout step: `Checkout Start`, `Contact & Order Information`, `Shipping Details`, `Payment Information`, `Review Order`, `Quick Checkout`, `Quick Checkout Edit`, `Continue as Guest` | `Checkout Start` |
| `product[]` | array | One object per cart line | — |
| `product[].productInfo.sku` | string | SKU of the cart line item | `00772756` |
| `product[].productInfo.productId` | string | Unique product identifier | `00772756` |
| `product[].productInfo.brand` | string | Product brand | `FESTO CORPORATION` |
| `product[].productInfo.inventoryStatus` | string | Inventory status | `in-stock-no-detail` |
| `product[].productInfo.quoteRequired` | string | `"TRUE"`/`"FALSE"` — item requires a quote | `FALSE` |
| `product[].productInfo.promotionalPricing` | string | `"TRUE"`/`"FALSE"` — item shown at a promotional price | `FALSE` |
| `product[].productInfo.specialPricingInitiative` | string | Special pricing flag; explicit fallback `FALSE` | `FALSE` |
| `product[].price.basePrice` | string | MSRP; unformatted, no thousands separators, ≤2 decimals; `"0"` when no price is available | `78.93` |
| `product[].price.sellingPrice` | string | Discounted price; same format rules as basePrice | `35.08` |
| `product[].quantity` | string | Units for this cart line | `1` |
