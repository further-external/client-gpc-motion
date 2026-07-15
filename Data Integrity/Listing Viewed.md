# Listing Viewed
Captures when a user views a search results listing after performing a search.

# Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Listing Viewed",
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
| `listing.listingParams.pageNum` | integer | Result page number| `1` |
| `listing.listingParams.searchInfo.searchTermEntered` | string | Keyword exactly as entered; `""` for browse | `ears` |
| `listing.listingParams.searchInfo.searchMethod` | string | `global`, `category:[name]`, `search within results`, `retailer`, `direct product` | `global` |
| `listing.listingParams.refinements[].refinementType` | string | Facet name | `inStockOnly` |
| `listing.listingParams.refinements[].refinementValue` | string | Applied facet value | `allDc` |
| `listing.listingParams.sorts.sortSequence` | integer | Sort dominance in multi-sort.| `1` |
| `listing.listingParams.sorts.sortView` | string | Presentation view — newly documented | `List` |
| `listing.listingResults.resultsCount` | integer | Total matching items | `79` |
| `listing.listingResults.resultsShown` | integer | Items rendered | `24` |
| `listing.listingResults.itemListType` | string | Human-readable list type: `search results`, `product listing`, `product comparison`, `products demonstrated`, `related items`, `supported items``ITEM_LIST`| `search results` |
| `listing.listingResults.item[].itemPosition` | integer | 1-based item position, sibling of `productInfo` | `1` |
| `listing.listingResults.item[].productInfo.sku` | string | SKU | `02354888` |
| `listing.listingResults.item[].productInfo.productID` | string | Unique product identifier | `02354888` |
| `listing.listingResults.item[].productInfo.brand` | string | Product brand | `LOVEJOY INC` |
| `listing.listingResults.item[].productInfo.inventoryStatus` | string | Inventory status enum | `in-stock-no-detail` |
| `listing.listingResults.item[].productInfo.productImage` | string | `"true"`/`"false"` | `true` |
| `listing.listingResults.item[].productInfo.quoteRequired` | string | `"yes"`/`"no"` | `no` |
| `listing.listingResults.item[].productInfo.promoPricing` | string | `"yes"`/`"no"` | `no` |
| `listing.listingResults.item[].productInfo.specialPricingInitiative` | string | Explicit fallback `false` | `false` |
| `listing.listingResults.item[].price.basePrice` | string | MSRP.| `1520.79` |
| `listing.listingResults.item[].price.sellingPrice` | string | Discounted price / actual price | `67.91` |
