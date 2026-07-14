# Listing Viewed More

Event should fire whenever additional listing results load (pagination or "load more"). The `item[]` array contains only the newly shown items.

## Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Listing Viewed More",
  "listing": {
    "listingParams": {
      "pageNum": <pageNum>,
      "searchInfo": {
        "searchTermEntered": "<searchTermEntered>",
        "searchMethod": "<searchMethod>"
      },
      "refinements": [{
        "refinementType": "<refinementType>",
        "refinementValue": "<refinementValue>"
      }],
      "sorts": {
        "sortSequence": <sortSequence>,
        "sortView": "<sortView>"
      }
    },
    "listingResults": {
      "resultsCount": <resultsCount>,
      "resultsShown": <resultsShown>,
      "itemListType": "<itemListType>",
      "item": [{
        "itemPosition": <itemPosition>,
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
        }
      }]
    }
  }
});
```

## Variable Definition

| Variable | Type | Description | Example |
|---|---|---|---|
| `listing.listingParams.pageNum` | integer | Result page number; increments as additional results load | `2` |
| `listing.listingParams.searchInfo.searchTermEntered` | string | Keyword exactly as entered; `""` for browse contexts | `quotes` |
| `listing.listingParams.searchInfo.searchMethod` | string | `global`, `category:[name]`, `search within results`, `retailer`, `direct product` | `global` |
| `listing.listingParams.refinements[]` | array | One object per applied refinement; `[]` when none applied | — |
| `listing.listingParams.refinements[].refinementType` | string | Facet name | `inStockOnly` |
| `listing.listingParams.refinements[].refinementValue` | string | Applied facet value | `allDc` |
| `listing.listingParams.sorts.sortSequence` | integer | Sort dominance when multiple sorts are applied (conditional) | `1` |
| `listing.listingParams.sorts.sortView` | string | Presentation view | `Grid` |
| `listing.listingResults.resultsCount` | integer | Total matching items | `40` |
| `listing.listingResults.resultsShown` | integer | Items rendered in this load | `24` |
| `listing.listingResults.itemListType` | string | List type: `search results`, `product listing`, `product comparison`, `products demonstrated`, `related items`, `supported items` | `search results` |
| `listing.listingResults.item[].itemPosition` | integer | 1-based position within the newly shown items | `1` |
| `listing.listingResults.item[].productInfo.sku` | string | SKU | `11864702` |
| `listing.listingResults.item[].productInfo.productID` | string | Unique product identifier | `11864702` |
| `listing.listingResults.item[].productInfo.brand` | string | Product brand | `TOPWORX` |
| `listing.listingResults.item[].productInfo.inventoryStatus` | string | Inventory status | `not-in-stock` |
| `listing.listingResults.item[].productInfo.productImage` | string | `"true"`/`"false"` — product has an image | `true` |
| `listing.listingResults.item[].productInfo.quoteRequired` | string | `"yes"`/`"no"` — item requires a quote | `no` |
| `listing.listingResults.item[].productInfo.promoPricing` | string | `"yes"`/`"no"` — item shown at a promotional price | `no` |
| `listing.listingResults.item[].productInfo.specialPricingInitiative` | string | Special pricing flag; explicit fallback `false` | `false` |
| `listing.listingResults.item[].price.basePrice` | string | MSRP; unformatted, no thousands separators, ≤2 decimals; `"0"` when no price is available (never an empty string) | `1541.26` |
| `listing.listingResults.item[].price.sellingPrice` | string | Discounted price; same format rules as basePrice; `"0"` for quote-required items | `934.10` |
