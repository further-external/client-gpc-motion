# Save To List

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

Saving a product to a named list from PDP, listing, or cart line.

## Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Save To List",
  "listName": "<listName>",
  "numberOfItemsSaved": <numberOfItemsSaved>,
  "product": [{
    "productInfo": {
      "sku": "<sku>",
      "productId": "<productId>",
      "brand": "<brand>",
      "inventoryStatus": "<inventoryStatus>",
      "productImage": "<productImage>",
      "quoteRequired": "<quoteRequired>",
      "promotionalPricing": "<promotionalPricing>",
      "specialPricingInitiative": "<specialPricingInitiative>",
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
| `listName` | string | Name of the destination list. | `Automation - Search Tests` |
| `numberOfItemsSaved` | integer | Items saved in the action | `1` |
| `product[].productInfo.sku` | string | SKU of saved item | `09436048` |
| `product[].productInfo.productId` | string | Unique product identifier | `09436048` |
| `product[].productInfo.brand` | string | Product brand | `BOSTON GEAR` |
| `product[].productInfo.inventoryStatus` | string | Inventory status enum | `not-in-stock` |
| `product[].productInfo.productImage` | string | `"TRUE"`/`"FALSE"` | `FALSE` |
| `product[].productInfo.quoteRequired` | string | `"TRUE"`/`"FALSE"`| `FALSE` |
| `product[].productInfo.productFindingVideo` | string | Video name if saved from a video context. | `Eaton - MiHow2 - Hydraulic Sequencing Circuit`|
| `product[].productInfo.promotionalPricing` | string | `"TRUE"`/`"FALSE"` | `FALSE` |
| `product[].productInfo.specialPricingInitiative` | string | Explicit fallback `FALSE` | `FALSE` |
| `product[].productInfo.cartThreshold` | string | Will provide details on if the threshold between cart add and request a quote has been met | `add to cart`, `Requste a quote` |
| `product[].price.basePrice` | string | MSRP | `1764.02` |
| `product[].price.sellingPrice` | string | Discounted price. | `820.47` |
| `product[].quantity` | string | Units saved | `1` |
