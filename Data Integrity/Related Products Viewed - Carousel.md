# Related Products Viewed - Carousel

Fires whenever a related-product recommendation module loads its product cards, including on carousel cycling. This is an umbrella event covering all related-product experiences on the site, such as Substitute Products (PDP), You May Also Like (PDP), and Recently Viewed (homepage); the specific experience is identified by `listType`.

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
| `relatedProducts.item[].productInfo.listType` | string | Widget list type identifying the experience (e.g. `Substitute Products`, `You May Also Like`, `Recently Viewed`) | `Substitute Products` |
| `relatedProducts.item[].productInfo.inventoryStatus` | string | Inventory status enum | `in-stock-no-detail` |
| `relatedProducts.item[].productInfo.productImage` | string | `"true"`/`"false"` | `true` |
| `relatedProducts.item[].productInfo.quoteRequired` | string | `"yes"`/`"no"` | `no` |
| `relatedProducts.item[].productInfo.promoPricing` | string | `"yes"`/`"no"` | `no` |
| `relatedProducts.item[].productInfo.specialPricingInitiative` | string | Explicit fallback `false` | `false` |
| `relatedProducts.item[].price.basePrice` | string | MSRP | `47.40` |
| `relatedProducts.item[].price.sellingPrice` | string | Discounted price | `29.17` |
