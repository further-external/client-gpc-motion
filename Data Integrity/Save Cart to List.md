# Save Cart to List

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

Event should fire whenever a user saves the entire cart contents to a named list. Each distinct cart line appears exactly once in `product[]`, with its own `quantity`.

## Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Save Cart to List",
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
| `listName` | string | Name of the destination list | `Automation - Search Tests` |
| `numberOfItemsSaved` | integer | Count of items saved in the action | `3` |
| `product[]` | array | One object per distinct cart line; no duplicate lines | — |
| `product[].productInfo.sku` | string | SKU of the saved item | `09436048` |
| `product[].productInfo.productId` | string | Unique product identifier | `09436048` |
| `product[].productInfo.brand` | string | Product brand | `BOSTON GEAR` |
| `product[].productInfo.inventoryStatus` | string | Inventory status | `not-in-stock` |
| `product[].productInfo.productImage` | string | `"TRUE"`/`"FALSE"` — product has an image | `FALSE` |
| `product[].productInfo.quoteRequired` | string | `"TRUE"`/`"FALSE"` — item requires a quote | `FALSE` |
| `product[].productInfo.productFindingVideo` | string | Video name when the item was saved from a video context (conditional) | `Eaton - MiHow2 - Hydraulic Sequencing Circuit` |
| `product[].productInfo.promotionalPricing` | string | `"TRUE"`/`"FALSE"` — item shown at a promotional price | `FALSE` |
| `product[].productInfo.specialPricingInitiative` | string | Special pricing flag; explicit fallback `FALSE` | `FALSE` |
| `product[].price.basePrice` | string | MSRP; unformatted, no thousands separators, ≤2 decimals; `"0"` when no price is available | `1764.02` |
| `product[].price.sellingPrice` | string | Discounted price; same format rules as basePrice | `820.47` |
| `product[].quantity` | string | Units saved for this cart line | `1` |
