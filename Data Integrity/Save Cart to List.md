# Save Cart to List

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
| `listName` | string | Name of the destination list | `Automation - Search Tests` |
| `numberOfItemsSaved` | integer | Count of items saved in the action | `3` |
| `product[]` | array | One object per distinct cart line; no duplicate lines | — |
| `product[].productInfo.sku` | string | SKU of the saved item | `09436048` |
| `product[].productInfo.productID` | string | Unique product identifier | `09436048` |
| `product[].productInfo.brand` | string | Product brand | `BOSTON GEAR` |
| `product[].productInfo.inventoryStatus` | string | Inventory status | `not-in-stock` |
| `product[].productInfo.productImage` | string | `"true"`/`"false"` — product has an image | `false` |
| `product[].productInfo.quoteRequired` | string | `"yes"`/`"no"` — item requires a quote | `no` |
| `product[].productInfo.productFindingVideo` | string | Video name when the item was saved from a video context (conditional) | `Eaton - MiHow2 - Hydraulic Sequencing Circuit` |
| `product[].productInfo.promoPricing` | string | `"yes"`/`"no"` — item shown at a promotional price | `no` |
| `product[].productInfo.specialPricingInitiative` | string | Special pricing flag; explicit fallback `false` | `false` |
| `product[].price.basePrice` | string | MSRP; unformatted, no thousands separators, ≤2 decimals; `"0"` when no price is available | `1764.02` |
| `product[].price.sellingPrice` | string | Discounted price; same format rules as basePrice | `820.47` |
| `product[].quantity` | string | Units saved for this cart line | `1` |
