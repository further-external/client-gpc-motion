# Listing Clicked

Fires when a listing item is clicked (click-through to PDP or add-to-cart from listing). Contains only the clicked item.

## Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Listing Clicked",
  "listing": {
    "listingParams": {
      "searchInfo": {
        "searchTermEntered": "<searchTermEntered>",
        "searchMethod": "<searchMethod>"
      },
      "refinements": [{
        "refinementType": "<refinementType>",
        "refinementValue": "<refinementValue>"
      }],
      "sorts": {
        "sortSequence": "<sortSequence>",
        "sortView": "<sortView>"
      }
    },
    "listingResults": {
      "resultsCount": "<resultsCount>",
      "resultsShown": "<resultsShown>",
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
          "fullFindingMethod": "<productFindingMethod>|<itemListType>",
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
| `listing.listingParams.searchInfo.searchTermEntered` | string | Keyword exactly as entered; `""` when the click is not from a search context | `ears` |
| `listing.listingParams.searchInfo.searchMethod` | string | `global`, `category:[name]`, `search within results`, `retailer`, `direct product`; `""` when not from search | `global` |
| `listing.listingParams.refinements[].refinementType` | string | Facet name | `inStockOnly` |
| `listing.listingParams.refinements[].refinementValue` | string | Applied facet value | `allDc` |
| `listing.listingParams.sorts.sortView` | string | Presentation view — newly documented for this event| `List` |
| `listing.listingParams.sorts.sortSequence` | string | Sort dominance in multi-sort | `1` |
| `listing.listingResults.resultsCount` | string | Total matching items. | `4` |
| `listing.listingResults.resultsShown` | string | Items rendered | `4` |
| `listing.listingResults.itemListType` | string | List type of the clicked item's widget | `You May Also Like` |
| `listing.listingResults.item[].itemPosition` | integer | 1-based position of the clicked item | `3` |
| `listing.listingResults.item[].productInfo.sku` | string | SKU of clicked item | `04225797` |
| `listing.listingResults.item[].productInfo.productID` | string | Unique product identifier | `04225797` |
| `listing.listingResults.item[].productInfo.brand` | string | Product brand | `SKF` |
| `listing.listingResults.item[].productInfo.inventoryStatus` | string | Inventory status enum | `in-stock-no-detail` |
| `listing.listingResults.item[].productInfo.productImage` | string | `"true"`/`"false"` | `true` |
| `listing.listingResults.item[].productInfo.quoteRequired` | string | `"yes"`/`"no"`| `no` |
| `listing.listingResults.item[].productInfo.fullFindingMethod` | string | Concatenated `productFindingMethod|itemListType` for widget attribution| `PDP: You May Also Like|You May Also Like` |
| `listing.listingResults.item[].productInfo.promoPricing` | string | `"yes"`/`"no"`| `no` |
| `listing.listingResults.item[].productInfo.specialPricingInitiative` | string | Explicit fallback `false`| `false` |
| `listing.listingResults.item[].price.basePrice` | string | MSRP| `55.60` |
| `listing.listingResults.item[].price.sellingPrice` | string | Discounted price| `34.22` |
