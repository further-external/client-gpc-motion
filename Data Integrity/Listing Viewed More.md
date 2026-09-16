# Listing Viewed More

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
| `listing.listingResults.item[].productInfo.productId` | string | Unique product identifier | `11864702` |
| `listing.listingResults.item[].productInfo.brand` | string | Product brand | `TOPWORX` |
| `listing.listingResults.item[].productInfo.inventoryStatus` | string | Inventory status | `not-in-stock` |
| `listing.listingResults.item[].productInfo.productImage` | string | `"TRUE"`/`"FALSE"` — product has an image | `TRUE` |
| `listing.listingResults.item[].productInfo.quoteRequired` | string | `"TRUE"`/`"FALSE"` — item requires a quote | `FALSE` |
| `listing.listingResults.item[].productInfo.promotionalPricing` | string | `"TRUE"`/`"FALSE"` — item shown at a promotional price | `FALSE` |
| `listing.listingResults.item[].productInfo.specialPricingInitiative` | string | Special pricing flag; explicit fallback `FALSE` | `FALSE` |
| `listing.listingResults.item[].price.basePrice` | string | MSRP; unformatted, no thousands separators, ≤2 decimals; `"0"` when no price is available (never an empty string) | `1541.26` |
| `listing.listingResults.item[].price.sellingPrice` | string | Discounted price; same format rules as basePrice; `"0"` for quote-required items | `934.10` |
