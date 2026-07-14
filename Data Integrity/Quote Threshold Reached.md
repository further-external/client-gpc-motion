# Quote Threshold Reached

Event should fire whenever a quantity change crosses the quote threshold: either an increase that crosses into quote-required territory, or a decrease back below it.

## Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Quote Threshold Reached",
  "product": [{
    "productInfo": {
      "sku": "<sku>",
      "productID": "<productID>",
      "brand": "<brand>",
      "inventoryStatus": "<inventoryStatus>",
      "productImage": "<productImage>",
      "quoteRequired": "<quoteRequired>",
      "promoPricing": "<promoPricing>",
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
| `product[].productInfo.productID` | string | Unique product identifier | `14369084` |
| `product[].productInfo.brand` | string | Product brand | `PEER CHAIN` |
| `product[].productInfo.inventoryStatus` | string | Inventory status | `not-in-stock` |
| `product[].productInfo.productImage` | string | `"true"`/`"false"` — product has an image | `true` |
| `product[].productInfo.quoteRequired` | string | `"yes"`/`"no"` — item requires a quote | `yes` |
| `product[].productInfo.promoPricing` | string | `"yes"`/`"no"` — item shown at a promotional price | `no` |
| `product[].productInfo.specialPricingInitiative` | string | Special pricing flag; explicit fallback `false` | `false` |
| `product[].price.basePrice` | string | MSRP; unformatted, no thousands separators, ≤2 decimals; `"0"` when no price is available | `3.31` |
| `product[].price.sellingPrice` | string | Discounted price; same format rules as basePrice | `1.54` |
| `product[].threshold.thresholdType` | string | `quote required` (increase crossed the threshold) or `add to cart` (decrease back below it) | `quote required` |
| `product[].threshold.thresholdLocation` | string | Location of the quantity change: `pdp`, `plp`, `cart`, `best sellers`, `recommended items` | `plp` |
| `product[].quantity` | string | Quantity at the time of the threshold cross | `5600` |
