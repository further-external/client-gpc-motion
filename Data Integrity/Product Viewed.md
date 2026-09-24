# Product Viewed

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

## Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Product Viewed",
  "product": [{
    "productInfo": {
      "sku": "<sku>",
      "productId": "<productId>",
      "name": "<name>",
      "brand": "<brand>",
      "inventoryStatus": "<inventoryStatus>",
      "isOutOfStock": "<isOutOfStock>",
      "productImage": "<productImage>",
      "productTabs": "<productTabs>",
      "productSearch": "<productSearch>",
      "productSearchPhrase": "<productSearchPhrase>",
      "quoteRequired": "<quoteRequired>",
      "promotionalPricing": "<promotionalPricing>",
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
| `product[].productInfo.productId` | string | Unique product identifier | `04225797` |
| `product[].productInfo.name` | string | Product name, 1:1 with `productId` | `Radial/Deep Groove Ball Bearing - Straight Bore, 30 mm ID, 62 mm OD, 16 mm Width, Double Sealed, Without Snap Ring` |
| `product[].productInfo.brand` | string | Product brand | `SKF` |
| `product[].productInfo.inventoryStatus` | string | Inventory status enum | `in-stock-no-detail` |
| `product[].productInfo.isOutOfStock` | boolean | Set only when every SKU is out of stock. **Must stay consistent with `inventoryStatus`:** a true value alongside `in-stock-no-detail` is contradictory and is a known open item. Note the `boolean` type here is inconsistent with every neighbouring field, which is `string` — to be confirmed. | `false` |
| `product[].productInfo.productImage` | string | `"TRUE"`/`"FALSE"`| `TRUE` |
| `product[].productInfo.productTabs` | string | `~`-delimited tabs available on the PDP | `specifications~literature-and-catalogs` |
| `product[].productInfo.productSearch` | string | `true` if the view resulted from a search landing directly on the PDP | `false` |
| `product[].productInfo.productSearchPhrase` | string | Exact phrase entered when `productSearch` is `TRUE`; empty/omitted otherwise | `quote` |
| `product[].productInfo.productFindingVideo` | string | Video name when PDP reached from a video page| `Eaton - MiHow2 - Hydraulic Sequencing Circuit` |
| `product[].productInfo.quoteRequired` | string | `"TRUE"`/`"FALSE"`| `FALSE` |
| `product[].productInfo.promotionalPricing` | string | `"TRUE"`/`"FALSE"`| `FALSE` |
| `product[].productInfo.specialPricingInitiative` | string | Special pricing flag; explicit fallback `FALSE`| `FALSE` |
| `product[].price.basePrice` | string | MSRP | `55.60` |
| `product[].price.sellingPrice` | string | Discounted price| `34.22` |
