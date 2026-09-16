# Quote Threshold Reached

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

Event should fire whenever a quantity change crosses the quote threshold: either an increase that crosses into quote-required territory, or a decrease back below it.

## Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Quote Threshold Reached",
  "product": [{
    "productInfo": {
      "sku": "<sku>",
      "productId": "<productId>",
      "brand": "<brand>",
      "inventoryStatus": "<inventoryStatus>",
      "productImage": "<productImage>",
      "quoteRequired": "<quoteRequired>",
      "promotionalPricing": "<promotionalPricing>",
      "specialPricingInitiative": "<specialPricingInitiative>"
    },
    "price": {
      "basePrice": "<basePrice>",
      "sellingPrice": "<sellingPrice>"
    },
    "threshold": {
      "thresholdType": "<thresholdType>",
      "thresholdLocation": "<thresholdLocation>"
    },
    "quantity": "<quantity>"
  }]
});
```

## Variable Definition

| Variable | Type | Description | Example |
|---|---|---|---|
| `product[].productInfo.sku` | string | SKU of the product | `14369084` |
| `product[].productInfo.productId` | string | Unique product identifier | `14369084` |
| `product[].productInfo.brand` | string | Product brand | `PEER CHAIN` |
| `product[].productInfo.inventoryStatus` | string | Inventory status | `not-in-stock` |
| `product[].productInfo.productImage` | string | `"TRUE"`/`"FALSE"` — product has an image | `TRUE` |
| `product[].productInfo.quoteRequired` | string | `"TRUE"`/`"FALSE"` — item requires a quote | `TRUE` |
| `product[].productInfo.promotionalPricing` | string | `"TRUE"`/`"FALSE"` — item shown at a promotional price | `FALSE` |
| `product[].productInfo.specialPricingInitiative` | string | Special pricing flag; explicit fallback `FALSE` | `FALSE` |
| `product[].price.basePrice` | string | MSRP; unformatted, no thousands separators, ≤2 decimals; `"0"` when no price is available | `3.31` |
| `product[].price.sellingPrice` | string | Discounted price; same format rules as basePrice | `1.54` |
| `product[].threshold.thresholdType` | string | `quote required` (increase crossed the threshold) or `add to cart` (decrease back below it) | `quote required` |
| `product[].threshold.thresholdLocation` | string | Location of the quantity change: `pdp`, `plp`, `cart`, `best sellers`, `recommended items` | `plp` |
| `product[].quantity` | string | Quantity at the time of the threshold cross | `5600` |
