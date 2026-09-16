# Product Added

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

Triggered when a user adds a product to their cart

# Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Product Added",
  "product": [{
    "productInfo": {
      "sku": "<sku>",
      "productId": "<productId>",
      "brand": "<brand>",
      "inventoryStatus": "<inventoryStatus>",
      "productImage": "<productImage>",
      "quoteRequired": "<quoteRequired>",
      "cartThreshold": "<cartThreshold>",
      "fullFindingMethod": "<productFindingMethod>|<itemListType>",
      "promotionalPricing": "<promotionalPricing>",
      "specialPricingInitiative": "<specialPricingInitiative>"
    },
    "price": {
      "basePrice": "<basePrice>",
      "sellingPrice": "<sellingPrice>"
    },
    "quantity": "<quantity>",
    "addType": "<addType>",
    "daysSaved": "<daysSaved>"
  }]
});
```

## Variable Definition

| Variable | Type | Description | Example |
|---|---|---|---|
| `product[].productInfo.sku` | string | SKU of added product | `10484964` |
| `product[].productInfo.productId` | string | Unique product identifier | `10484964` |
| `product[].productInfo.brand` | string | Product brand | `SUMITOMO DRIVE TECH` |
| `product[].productInfo.inventoryStatus` | string | Inventory status enum | `not-in-stock` |
| `product[].productInfo.productImage` | string | `"TRUE"`/`"FALSE"` | `TRUE` |
| `product[].productInfo.quoteRequired` | string | `"TRUE"`/`"FALSE"`  | `TRUE` |
| `product[].productInfo.fullFindingMethod` | string | `productFindingMethod|itemListType` concatenation | `Search Results|search results` |
| `product[].productInfo.productFindingVideo` | string | Video name when added from a video page | `Eaton - MiHow2 - Hydraulic Sequencing Circuit` |
| `product[].productInfo.promotionalPricing` | string | `"TRUE"`/`"FALSE"` | `FALSE` |
| `product[].productInfo.specialPricingInitiative` | string | Explicit fallback `FALSE` | `FALSE` |
| `product[].productInfo.cartThreshold` | string | when cart threshold is reached by a visitor changing the quantity of a product on PDP, PLP or the Cart.| `0`,`1`,`2` |
| `product[].price.basePrice` | string | MSRP `"0"` fallback on quote-required items | `0` |
| `product[].price.sellingPrice` | string | Discounted price | `0` |
| `product[].quantity` | string | Units added. For MOQ products added below the MOQ from a listing, reflects the actual quantity added | `1` |
| `product[].addType` | string | Add context: `product detail`, `search results`, `product listing`, `related items`, `previous order`, `saved list`, `cart save for later`, etc. | `search results` |
| `product[].daysSaved` | string | Days in Save For Later before re-add; only when moved from Save For Later | `3` |
