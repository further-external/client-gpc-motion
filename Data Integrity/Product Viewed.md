# Product Viewed

## Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Product Viewed",
  "product": [{
    "productInfo": {
      "sku": "<sku>",
      "productID": "<productID>",
      "name": "<name>",
      "brand": "<brand>",
      "inventoryStatus": "<inventoryStatus>",
      "isOutOfStock": "<isOutOfStock>",
      "productImage": "<productImage>",
      "productTabs": "<productTabs>",
      "productSearch": "<productSearch>",
      "productSearchPhrase": "<productSearchPhrase>",
      "quoteRequired": "<quoteRequired>",
      "promoPricing": "<promoPricing>",
      "specialPricingInitiative": "<specialPricingInitiative>"
    },
    "price": {
      "basePrice": "<basePrice>",
      "sellingPrice": "<sellingPrice>"
    }
  }]
});
```

## Variable Definition
| Variable | Type | Description | Example |
|---|---|---|---|
| `product[].productInfo.sku` | string | SKU of the viewed product | `04225797` |
| `product[].productInfo.productID` | string | Unique product identifier | `04225797` |
| `product[].productInfo.name` | string | Product name, 1:1 with `productID` | `Radial/Deep Groove Ball Bearing - Straight Bore, 30 mm ID, 62 mm OD, 16 mm Width, Double Sealed, Without Snap Ring` |
| `product[].productInfo.brand` | string | Product brand | `SKF` |
| `product[].productInfo.inventoryStatus` | string | Inventory status enum | `in-stock-no-detail` |
| `product[].productInfo.isOutOfStock` | boolean | `true` only when out of stock. **Must be consistent with `inventoryStatus` `true` alongside `in-stock-no-detail` | `false` |
| `product[].productInfo.productImage` | string | `"true"`/`"false"`| `true` |
| `product[].productInfo.productTabs` | string | `~`-delimited tabs available on the PDP | `specifications~literature-and-catalogs` |
| `product[].productInfo.productSearch` | string | `true` if the view resulted from a search landing directly on the PDP | `false` |
| `product[].productInfo.productSearchPhrase` | string | Exact phrase entered when `productSearch` is `true`; empty/omitted otherwise | `quote` |
| `product[].productInfo.productFindingVideo` | string | Video name when PDP reached from a video page| `Eaton - MiHow2 - Hydraulic Sequencing Circuit` |
| `product[].productInfo.quoteRequired` | string | `"yes"`/`"no"`| `no` |
| `product[].productInfo.promoPricing` | string | `"yes"`/`"no"`| `no` |
| `product[].productInfo.specialPricingInitiative` | string | Special pricing flag; explicit fallback `false`| `false` |
| `product[].price.basePrice` | string | MSRP | `55.60` |
| `product[].price.sellingPrice` | string | Discounted price| `34.22` |
