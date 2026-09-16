# Related Products Viewed - Carousel

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
        "productId": "<productId>",
        "brand": "<brand>",
        "listType": "<listType>",
        "inventoryStatus": "<inventoryStatus>",
        "productImage": "<productImage>",
        "quoteRequired": "<quoteRequired>",
        "promotionalPricing": "<promotionalPricing>",
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
| `relatedProducts.item[].productInfo.productId` | string | Unique product identifier | `07408161` |
| `relatedProducts.item[].productInfo.brand` | string | Product brand | `TIMKEN` |
| `relatedProducts.item[].productInfo.listType` | string | Widget list type identifying the experience (e.g. `Substitute Products`, `You May Also Like`, `Recently Viewed`) | `Substitute Products` |
| `relatedProducts.item[].productInfo.inventoryStatus` | string | Inventory status enum | `in-stock-no-detail` |
| `relatedProducts.item[].productInfo.productImage` | string | `"TRUE"`/`"FALSE"` | `TRUE` |
| `relatedProducts.item[].productInfo.quoteRequired` | string | `"TRUE"`/`"FALSE"` | `FALSE` |
| `relatedProducts.item[].productInfo.promotionalPricing` | string | `"TRUE"`/`"FALSE"` | `FALSE` |
| `relatedProducts.item[].productInfo.specialPricingInitiative` | string | Explicit fallback `FALSE` | `FALSE` |
| `relatedProducts.item[].price.basePrice` | string | MSRP | `47.40` |
| `relatedProducts.item[].price.sellingPrice` | string | Discounted price | `29.17` |
