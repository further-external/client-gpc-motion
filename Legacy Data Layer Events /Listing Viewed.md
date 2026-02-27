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
appEventData || [];

appEventData.push({
  "event": "Listing Viewed",
  "listing": {
    "listingParams": {
      "pageNum": "<pageNum>"    
      "searchInfo": {
        "searchTermEntered": "<searchTermEntered>",
        "searchMethod": "<searchMethod>"
      },
      "refinements": {
        "refinementType": "<refinementType>",
        "refinementValue": "<refinementValue>"
      },
      "sorts": {
        "sortSequence": "<sortSequence>",
        "sortView": "<sortView>"
      }
    },
    "listingResults": {
      "resultsCount": "<resultsCount>",
      "resultsShown": "<resultsShown>",
      "itemListType": "<itemListType>",
      "item": {
        "productInfo": {
          "sku": "<sku>",
          "productID": "<productID>",
          "productImage": "<productImage>",
          "brand": "<brand>",
          "inventoryStatus": "<inventoryStatus>",
          "productFindingMethod": "<productFindingMethod>",
          "moqRequired": "<moqRequired>",
```

--- 

#Variable Definition
| field                    | type    | description                                                                                                                                                                                                                                                  | examples                                                                                                                                                                             |
| :----------------------- | :------ | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **searchTermEntered**    | string  | Describes the search keyword exactly as entered by the user.                                                                                                                                                                                                 | red lobster,red lboster,red lbstr. Zip code if search is for a retail/physical location                                                                                              |
| **searchMethod**         | string  | Describes the method of search.                                                                                                                                                                                                                              | Example values: - global (primary header search) - category:\[category name\] (if the visitor uses a search category in the global search)- search within - retailer- direct product |
| **resultsCount**         | integer | The total number of items returned that matched the search criteria. (Integer)                                                                                                                                                                               | 0, 20, 110, 165                                                                                                                                                                      |
| **resultsShown**         | integer | The number of items presented. Used with pagination, map, or lazyload UX. (Integer)                                                                                                                                                                          | 0, 5, 16, 32                                                                                                                                                                         |
| **sku**                  | string  | Stock Keeping Unit (SKU) Unique Identifier of specific item (typically) held in inventory. Must match the format of back-end systems if used as a key for import of product meta data. Most often, one level below productID for products with SKU variants. | 34567890, 4567890, 00155-large-cornflower                                                                                                                                            |
| **itemListType**         | string  | Indicates the presentation type for displaying products/items. Note that values here might closely mirror the Cart Type (addType) seen in the “Product Added” event specification.                                                                           | List types could include: - product listing (i.e. this is plp when browsing) - search results - product comparison - products demonstrated - related items - supported items         |
| **itemPosition**         | integer | Integer position of a property within a sorted result. The first returned is position 1. For map results, this value can be the rank by distance from POI.                                                                                                   | 1, 2, 3, 4, 5                                                                                                                                                                        |
| **productID**            | string  | Unique Identifier of a product or offering. Must match the format of back-end systems if used as a key for import of product meta data. Most often, one level above SKU for products with SKU variants.                                                      | 155, 65588, 987764448                                                                                                                                                                |
| **productImage**         |         |                                                                                                                                                                                                                                                              |                                                                                                                                                                                      |
| **refinementType**       | string  | Describes the parameter or facet of the refinement being applied.                                                                                                                                                                                            | brand, size, rating, color                                                                                                                                                           |
| **refinementValue**      | string  | Provides the value for the parameter or facet of the refinement being applied.                                                                                                                                                                               | Coors, L, M, S 3-5, Red                                                                                                                                                              |
| **sortSequence**         | integer | Integer number representing the dominance of a sort operator in a multi-sort scenario (sort by this, then that)                                                                                                                                              | 1, 2, 3, 4                                                                                                                                                                           |
| **productFindingMethod** | string  |                                                                                                                                                                                                                                                              | Knowledge Hub - Catalog, Knowledge Hub - Success Stories, Direct Search, bookmarked                                                                                                  |
| **moqRequired**          | string  | Set with a value of "yes" or "no" when a product is added to cart.                                                                                                                                                                                           | yes OR no                                                                                                                                                                            |
| **brand**                | string  | Set with the brand of the product                                                                                                                                                                                                                            | krylon                                                                                                                                                                               |
| **supplierInventory**    | string  | Set with “supplier inventory” or “other”                                                                                                                                                                                                                     | supplier inventory                                                                                                                                                                   |
| **impressionType**       | string  | Set with: Browse, Search, Brand Page, Best Sellers, Recommendations                                                                                                                                                                                          |                                                                                                                                                                                      |
| **promoPricing**         | string  | A flag representing if the product is currently seen or purchased at a promotional price.                                                                                                                                                                    | yes, no                                                                                                                                                                              |
| **priceChange**          | string  | With the 2025 conversion initiative, this is a dedicated field in place to indicate those products which are subject to that pricing initiative - the desired example field should be the month and year for the permanent price change                      | April2025, May2025, January2026                                                                                                                                                      |

