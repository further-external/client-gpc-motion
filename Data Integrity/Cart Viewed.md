# Cart Viewed

Event should fire whenever a user views the shopping cart page.

## Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Cart Viewed",
  "cart": {
    "item": [{
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
  }
});
```

## Variable Definition

| Variable | Type | Description | Example |
|---|---|---|---|
| `cart.item[]` | array | One object per cart line | — |
| `cart.item[].productInfo.sku` | string | SKU of the cart line item | `00772756` |
| `cart.item[].productInfo.productID` | string | Unique product identifier | `00772756` |
| `cart.item[].productInfo.brand` | string | Product brand | `FESTO CORPORATION` |
| `cart.item[].productInfo.inventoryStatus` | string | Inventory status | `in-stock-no-detail` |
| `cart.item[].productInfo.productImage` | string | `"true"`/`"false"` — product has an image | `true` |
| `cart.item[].productInfo.quoteRequired` | string | `"yes"`/`"no"` — item requires a quote | `no` |
| `cart.item[].productInfo.promoPricing` | string | `"yes"`/`"no"` — item shown at a promotional price | `no` |
| `cart.item[].productInfo.specialPricingInitiative` | string | Special pricing flag; explicit fallback `false` | `false` |
| `cart.item[].price.basePrice` | string | MSRP; unformatted, no thousands separators, ≤2 decimals; `"0"` when no price is available | `78.93` |
| `cart.item[].price.sellingPrice` | string | Discounted price; same format rules as basePrice | `35.08` |
| `cart.item[].quantity` | string | Units in cart for this line | `1` |
