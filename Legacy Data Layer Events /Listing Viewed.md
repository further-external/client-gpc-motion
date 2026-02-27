# Listing Viewed

The **Listing Viewed** event captures information about a product listing page (search results, browse results, brand pages, category pages, etc.).

This event includes:

- Search context (term + method)
- Search suggestions (if applicable)
- Applied refinements (facets)
- Sort configuration
- Pagination context
- Total results + results shown
- Product impression data for each item returned

---

## Event Specification

```javascript
window.appEventData = window.appEventData || [];
window.appEventData.push({
  "event": "Listing Viewed",
  "listing": {
    "listingParams": {
      "refinements": [
        {
          "refinementType": "<refinementType>",
          "refinementValue": "<refinementValue>"
        }
      ],
      "searchInfo": {
        "searchMethod": "<searchMethod>",
        "searchTermEntered": "<searchTermEntered>"
      },
      "searchSuggestions": {
        "termsReturned": "<termsReturned>",
        "suggestedTerms": [
          {
            "term": "<term>",
            "position": "<position>"
          }
        ]
      },
      "sorts": {
        "sortView": "<sortView>",
        "sortSequence": "<sortSequence>"
      },
      "pageNum": "<pageNum>"
    },
    "listingResults": {
      "item": [
        {
          "productInfo": {
            "sku": "<sku>",
            "productID": "<productID>",
            "brand": "<brand>",
            "inventoryStatus": "<inventoryStatus>",
            "productImage": "<productImage>",
            "promoPricing": "<promoPricing>",
            "specialPricingInitiative": "<specialPricingInitiative>",
            "quoteRequired": "<quoteRequired>",
            "productFindingMethod": "<productFindingMethod>"
          },
          "itemPosition": "<itemPosition>",
          "price": {
            "sellingPrice": "<sellingPrice>",
            "basePrice": "<basePrice>"
          },
          "isDisplayed": "<isDisplayed>",
          "itemListType": "<itemListType>"
        }
      ],
      "itemListType": "<itemListType>",
      "resultsCount": "<resultsCount>",
      "resultsShown": "<resultsShown>"
    }
  }
});
```
--- 

| Field                        | Type            | Description                                                                    | Example                                                 |
| ---------------------------- | --------------- | ------------------------------------------------------------------------------ | ------------------------------------------------------- |
| **pageNum**                  | integer         | Current page number of the listing results.                                    | `1`, `2`, `3`                                           |
| **searchTermEntered**        | string          | The search keyword exactly as entered by the user.                             | `test`, `hydraulic pump`, `90210`                       |
| **searchMethod**             | string          | Method used to perform the search.                                             | `global`, `search within`, `direct product`, `retailer` |
| **termsReturned**            | integer         | Total number of search suggestions returned by the suggestion service when no results are returned.        | `0`, `3`, `5`                                           |
| **term**                     | string          | Suggested alternative search term presented to the user when no results are returned.     | `hydraulic pumps`, `hydrualic pump`, `pump hydraulic`   |
| **position**                 | integer         | The ranking position of the suggestion within the suggestion list (1-indexed) when no results are returned. | `1`, `2`, `3`                                           |
| **refinementType**           | string          | The facet or filter category applied.                                          | `brand`, `size`, `rating`, `color`                      |
| **refinementValue**          | string          | The selected value for the applied refinement.                                 | `HYDAC`, `Large`, `3-5`, `Red`                          |
| **sortView**                 | string          | UI presentation format of results.                                             | `List`, `Grid`                                          |
| **sortSequence**             | integer         | Sort priority when multiple sorts are applied.                                 | `1`, `2`, `3`                                           |
| **resultsCount**             | integer         | Total number of results matching search/refinements.                           | `56504`, `120`, `0`                                     |
| **resultsShown**             | integer         | Number of results displayed on the current page/view.                          | `24`, `32`                                              |
| **itemListType**             | string          | Context/type of listing page.                                                  | `ITEM_LIST`, `search results`, `category listing`       |
| **itemPosition**             | integer         | Position of the product in the listing (1-indexed).                            | `1`, `2`, `24`                                          |
| **sku**                      | string          | Unique SKU identifier for the product.                                         | `02292353`                                              |
| **productID**                | string          | Product-level identifier (may match SKU depending on implementation).          | `02292353`, `987764448`                                 |
| **brand**                    | string          | Brand name of the product.                                                     | `HYDAC`, `SKF`, `Proto Tools`                           |
| **inventoryStatus**          | string          | Inventory availability descriptor.                                             | `in-stock-no-detail`, `out-of-stock`                    |
| **productImage**             | string/boolean  | Indicates whether the product has an image available.                          | `"true"`, `"false"`, `true`, `false`                    |
| **productFindingMethod**     | string          | Method through which the product was surfaced.                                 | `Internal Search`, `Direct Search`, `Navigation`        |
| **promoPricing**             | string          | Indicates if promotional pricing is active.                                    | `yes`, `no`                                             |
| **specialPricingInitiative** | string/boolean  | Indicates if the product is part of a pricing initiative.                      | `"true"`, `"false"`                                     |
| **quoteRequired**            | string          | Indicates if product requires a quote to purchase.                             | `yes`, `no`                                             |
| **sellingPrice**             | string/number   | Displayed selling price of the product.                                        | `42.32`, `6605.02`                                      |
| **basePrice**                | string/number   | Reference/base price of the product.                                           | `42.32`, `6605.02`                                      |
| **isDisplayed**              | integer/boolean | Indicates whether the item is rendered in the listing UI.                      | `1`, `0`, `true`, `false`                               |
