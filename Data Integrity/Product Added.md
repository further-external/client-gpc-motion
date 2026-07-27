# Product Added
Triggered when a user adds a product to their cart

# Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Product Added",
  "product": [{
    "productInfo": {
      "sku": "<sku>",
      "productID": "<productID>",
      "brand": "<brand>",
      "inventoryStatus": "<inventoryStatus>",
      "productImage": "<productImage>",
      "quoteRequired": "<quoteRequired>",
      "cartThreshold": "<cartThreshold>",
      "fullFindingMethod": "<productFindingMethod>|<itemListType>",
      "promoPricing": "<promoPricing>",
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
| `product[].productInfo.productID` | string | Unique product identifier | `10484964` |
| `product[].productInfo.brand` | string | Product brand | `SUMITOMO DRIVE TECH` |
| `product[].productInfo.inventoryStatus` | string | Inventory status enum | `not-in-stock` |
| `product[].productInfo.productImage` | string | `"true"`/`"false"` | `true` |
| `product[].productInfo.quoteRequired` | string | `"yes"`/`"no"`  | `yes` |
| `product[].productInfo.fullFindingMethod` | string | `productFindingMethod|itemListType` concatenation | `Search Results|search results` |
| `product[].productInfo.productFindingVideo` | string | Video name when added from a video page | `Eaton - MiHow2 - Hydraulic Sequencing Circuit` |
| `product[].productInfo.promoPricing` | string | `"yes"`/`"no"` | `no` |
| `product[].productInfo.specialPricingInitiative` | string | Explicit fallback `false` | `false` |
| `product[].productInfo.cartThreshold` | string | when cart threshold is reached by a visitor changing the quantity of a product on PDP, PLP or the Cart.| `0`,`1`,`2` |
| `product[].price.basePrice` | string | MSRP `"0"` fallback on quote-required items | `0` |
| `product[].price.sellingPrice` | string | Discounted price | `0` |
| `product[].quantity` | string | Units added. For MOQ products added below the MOQ from a listing, reflects the actual quantity added | `1` |
| `product[].addType` | string | Add context: `product detail`, `search results`, `product listing`, `related items`, `previous order`, `saved list`, `cart save for later`, etc. | `search results` |
| `product[].daysSaved` | string | Days in Save For Later before re-add; only when moved from Save For Later | `3` |
