# Related Products Viewed - Carousel

Canonical production name adopted (prior spec: "Related Products Viewed"). Fires when related/recommended product cards render, including on carousel cycling.

## Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Related Products Viewed - Carousel",
  "relatedProducts": {
    "item": [{
      "itemPosition": <itemPosition>,
      "productInfo": {
        "sku": "<sku>",
        "productID": "<productID>",
        "brand": "<brand>",
        "listType": "<listType>",
        "inventoryStatus": "<inventoryStatus>",
        "productImage": "<productImage>",
        "quoteRequired": "<quoteRequired>",
        "promoPricing": "<promoPricing>",
        "specialPricingInitiative": "<specialPricingInitiative>"
      },
      "price": {
        "basePrice": "<basePrice>",
        "sellingPrice": "<sellingPrice>"
      }
    }]
  }
});
```

## Variable Definition
| Variable | Type | Description | Example |
|---|---|---|---|
| `relatedProducts.item[].itemPosition` | integer | 1-based card position. Moved from inside `productInfo` to item level for consistency | `1` |
| `relatedProducts.item[].productInfo.sku` | string | SKU | `07408161` |
| `relatedProducts.item[].productInfo.productID` | string | Unique product identifier | `07408161` |
| `relatedProducts.item[].productInfo.brand` | string | Product brand | `TIMKEN` |
| `relatedProducts.item[].productInfo.listType` | string | Widget list type | `Substitute Products` |
| `relatedProducts.item[].productInfo.inventoryStatus` | string | Inventory status enum | `in-stock-no-detail` |
| `relatedProducts.item[].productInfo.productImage` | string | `"true"`/`"false"` | `true` |
| `relatedProducts.item[].productInfo.quoteRequired` | string | `"yes"`/`"no"` | `no` |
| `relatedProducts.item[].productInfo.promoPricing` | string | `"yes"`/`"no"` | `no` |
| `relatedProducts.item[].productInfo.specialPricingInitiative` | string | Explicit fallback `false` | `false` |
| `relatedProducts.item[].price.basePrice` | string | MSRP — `price` | `47.40` |
| `relatedProducts.item[].price.sellingPrice` | string | Discounted price | `29.17` |
