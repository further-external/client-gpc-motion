# Save For Later

Event should fire whenever a user saves individual cart line item(s) for later from the cart.

## Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Save For Later",
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
| `numberOfItemsSaved` | integer | Count of items saved in the action | `1` |
| `product[].productInfo.sku` | string | SKU of the saved item | `07636651` |
| `product[].productInfo.productID` | string | Unique product identifier | `07636651` |
| `product[].productInfo.brand` | string | Product brand | `FESTO CORPORATION` |
| `product[].productInfo.inventoryStatus` | string | Inventory status | `in-stock-no-detail` |
| `product[].productInfo.productImage` | string | `"true"`/`"false"` — product has an image | `true` |
| `product[].productInfo.quoteRequired` | string | `"yes"`/`"no"` — item requires a quote | `no` |
| `product[].productInfo.productFindingVideo` | string | Video name when the item was saved from a video context (conditional) | `Eaton - MiHow2 - Hydraulic Sequencing Circuit` |
| `product[].productInfo.promoPricing` | string | `"yes"`/`"no"` — item shown at a promotional price | `no` |
| `product[].productInfo.specialPricingInitiative` | string | Special pricing flag; explicit fallback `false` | `false` |
| `product[].price.basePrice` | string | MSRP; unformatted, no thousands separators, ≤2 decimals; `"0"` when no price is available | `26.64` |
| `product[].price.sellingPrice` | string | Discounted price; same format rules as basePrice; `"0"` for quote items | `16.14` |
| `product[].quantity` | string | Units saved | `1` |
