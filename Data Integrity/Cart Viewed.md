# Cart Viewed

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
  }
});
```

## Variable Definition

| Variable | Type | Description | Example |
|---|---|---|---|
| `cart.item[]` | array | One object per cart line | — |
| `cart.item[].productInfo.sku` | string | SKU of the cart line item | `00772756` |
| `cart.item[].productInfo.productId` | string | Unique product identifier | `00772756` |
| `cart.item[].productInfo.brand` | string | Product brand | `FESTO CORPORATION` |
| `cart.item[].productInfo.inventoryStatus` | string | Inventory status | `in-stock-no-detail` |
| `cart.item[].productInfo.productImage` | string | `"TRUE"`/`"FALSE"` — product has an image | `TRUE` |
| `cart.item[].productInfo.quoteRequired` | string | `"TRUE"`/`"FALSE"` — item requires a quote | `FALSE` |
| `cart.item[].productInfo.promotionalPricing` | string | `"TRUE"`/`"FALSE"` — item shown at a promotional price | `FALSE` |
| `cart.item[].productInfo.specialPricingInitiative` | string | Special pricing flag; explicit fallback `FALSE` | `FALSE` |
| `cart.item[].price.basePrice` | string | MSRP; unformatted, no thousands separators, ≤2 decimals; `"0"` when no price is available | `78.93` |
| `cart.item[].price.sellingPrice` | string | Discounted price; same format rules as basePrice | `35.08` |
| `cart.item[].quantity` | string | Units in cart for this line | `1` |
