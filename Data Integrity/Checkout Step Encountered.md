# Checkout Step Encountered

Event should fire on every checkout step render, including pre-filled steps for returning users and re-entry after a user edits a previous step.

## Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Checkout Step Encountered",
  "eventDetails": {
    "checkoutStep": "<checkoutStep>"
  },
  "product": [{
    "productInfo": {
      "sku": "<sku>",
      "productID": "<productID>",
      "brand": "<brand>",
      "inventoryStatus": "<inventoryStatus>",
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
| `eventDetails.checkoutStep` | string | Checkout step: `Checkout Start`, `Contact & Order Information`, `Shipping Details`, `Payment Information`, `Review Order`, `Quick Checkout`, `Quick Checkout Edit`, `Continue as Guest` | `Checkout Start` |
| `product[]` | array | One object per cart line | — |
| `product[].productInfo.sku` | string | SKU of the cart line item | `00772756` |
| `product[].productInfo.productID` | string | Unique product identifier | `00772756` |
| `product[].productInfo.brand` | string | Product brand | `FESTO CORPORATION` |
| `product[].productInfo.inventoryStatus` | string | Inventory status | `in-stock-no-detail` |
| `product[].productInfo.quoteRequired` | string | `"yes"`/`"no"` — item requires a quote | `no` |
| `product[].productInfo.promoPricing` | string | `"yes"`/`"no"` — item shown at a promotional price | `no` |
| `product[].productInfo.specialPricingInitiative` | string | Special pricing flag; explicit fallback `false` | `false` |
| `product[].price.basePrice` | string | MSRP; unformatted, no thousands separators, ≤2 decimals; `"0"` when no price is available | `78.93` |
| `product[].price.sellingPrice` | string | Discounted price; same format rules as basePrice | `35.08` |
| `product[].quantity` | string | Units for this cart line | `1` |
