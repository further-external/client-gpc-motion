# Listing Viewed

The listing viewed event will be used to gather information about the listing of several types of data, including:
Search results:

Redirected search - direct product search
Product impressions (by type - supporting items, )
Brand Pages
PLP Browse
Search Within Results


---

```js
appEventData = window.appEventData || [];
appEventData.push({
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

#Variable Definition
| field                        | type            | description                                                                              | examples                                                              |
| :--------------------------- | :-------------- | :--------------------------------------------------------------------------------------- | :-------------------------------------------------------------------- |
| **pageNum**                  | integer         | The current page number of results (pagination).                                         | `1`, `2`, `3`                                                         |
| **searchTermEntered**        | string          | Search keyword exactly as entered by the user.                                           | `test`, `red lobster`, `90210`                        |
| **searchMethod**             | string          | Method of search.                                                                        | `global`, `search within`, `direct product`, `retailer` ( |
| **refinementType**           | string          | The facet/parameter being refined.                                                       | `brand`, `size`, `rating`, `color`                      |
| **refinementValue**          | string          | The selected value for the refinement.                                                   | `HYDAC`, `L`, `3-5`, `Red`                             |
| **sortView**                 | string          | UI presentation for results.                                                             | `List`, `Grid`                                                        |
| **sortSequence**             | integer         | Sort priority in multi-sort scenarios (sort by X then Y).                                | `1`, `2`, `3`                                      |
| **resultsCount**             | integer         | Total number of items matching the criteria.                                             | `0`, `20`, `56504`                                      |
| **resultsShown**             | integer         | Number of items shown in the current view/page (pagination / lazyload).                  | `0`, `24`, `32`                                      |
| **itemListType**             | string          | Presentation/type of listing context.                                                    | `ITEM_LIST`, `search results`, `product listing`       |
| **itemPosition**             | integer         | Rank/position of the item within the returned list (1-indexed).                          | `1`, `2`, `24`                                      |
| **sku**                      | string          | SKU unique identifier (often one level below productID for variant SKUs).                | `02292353`, `00155-large-cornflower`                                  |
| **productID**                | string          | Product identifier (often one level above SKU).                                          | `02292353`, `155`, `987764448`                                        |
| **brand**                    | string          | Brand of the product.                                                                    | `HYDAC`, `SKF`                                                        |
| **inventoryStatus**          | string          | Inventory status descriptor for the item.                                                | `in-stock-no-detail`, `out-of-stock`                                  |
| **productImage**             | string/boolean  | Flag indicating whether an image is present for the product.                             | `"true"`, `"false"`, `true`, `false`                                  |
| **productFindingMethod**     | string          | How the product was found/returned (source/channel).                                     | `Internal Search`, `Direct Search`, `bookmarked`                      |
| **promoPricing**             | string          | Flag representing if product is currently at a promotional price.                        | `yes`, `no`                                                           |
| **specialPricingInitiative** | string/boolean  | Flag indicating if product is part of a special pricing initiative (site-specific flag). | `"true"`, `"false"`                                                   |
| **quoteRequired**            | string          | Flag indicating if quote is required for purchase.                                       | `yes`, `no`                                                           |
| **sellingPrice**             | string/number   | Current selling price displayed for the product.                                         | `42.32`, `6605.02`                                                    |
| **basePrice**                | string/number   | Base/reference price displayed for the product.                                          | `42.32`, `6605.02`                                                    |
| **isDisplayed**              | integer/boolean | Flag indicating item is displayed in the UI result set.                                  | `1`, `0`, `true`, `false`                                             |
