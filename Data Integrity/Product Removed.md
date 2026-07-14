# Product Removed

Event should fire whenever a product is removed from the cart, including quantity decreases and cart clears.

## Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Product Removed",
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
    "quantity": "<quantity>"
  }]
});
```

## Variable Definition

| Variable | Type | Description | Example |
|---|---|---|---|
| `product[].productInfo.sku` | string | SKU of the removed product | `10484964` |
| `product[].productInfo.productID` | string | Unique product identifier | `10484964` |
| `product[].productInfo.brand` | string | Product brand | `SUMITOMO DRIVE TECH` |
| `product[].productInfo.inventoryStatus` | string | Inventory status | `not-in-stock` |
| `product[].productInfo.productImage` | string | `"true"`/`"false"` — product has an image | `true` |
| `product[].productInfo.quoteRequired` | string | `"yes"`/`"no"` — item requires a quote | `yes` |
| `product[].productInfo.promoPricing` | string | `"yes"`/`"no"` — item shown at a promotional price | `no` |
| `product[].productInfo.specialPricingInitiative` | string | Special pricing flag; explicit fallback `false` | `false` |
| `product[].price.basePrice` | string | MSRP; unformatted, no thousands separators, ≤2 decimals; `"0"` when no price is available (never an empty string) | `0` |
| `product[].price.sellingPrice` | string | Discounted price; same format rules as basePrice; `"0"` when no price is available | `0` |
| `product[].quantity` | string | Units removed | `25` |
