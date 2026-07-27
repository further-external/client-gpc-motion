# Save To List

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
      "productID": "<productID>",
      "brand": "<brand>",
      "inventoryStatus": "<inventoryStatus>",
      "productImage": "<productImage>",
      "quoteRequired": "<quoteRequired>",
      "promoPricing": "<promoPricing>",
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
| `product[].productInfo.productID` | string | Unique product identifier | `09436048` |
| `product[].productInfo.brand` | string | Product brand | `BOSTON GEAR` |
| `product[].productInfo.inventoryStatus` | string | Inventory status enum | `not-in-stock` |
| `product[].productInfo.productImage` | string | `"true"`/`"false"` | `false` |
| `product[].productInfo.quoteRequired` | string | `"yes"`/`"no"`| `no` |
| `product[].productInfo.productFindingVideo` | string | Video name if saved from a video context. | `Eaton - MiHow2 - Hydraulic Sequencing Circuit`|
| `product[].productInfo.promoPricing` | string | `"yes"`/`"no"` | `no` |
| `product[].productInfo.specialPricingInitiative` | string | Explicit fallback `false` | `false` |
| `product[].productInfo.cartThreshold` | string | Will provide details on if the threshold between cart add and request a quote has been met | `add to cart`, `Requste a quote` |
| `product[].price.basePrice` | string | MSRP | `1764.02` |
| `product[].price.sellingPrice` | string | Discounted price. | `820.47` |
| `product[].quantity` | string | Units saved | `1` |
