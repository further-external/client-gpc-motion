# Listing Viewed

The listing viewed event will be used to gather information about the listing of several types of data, including:
- Search results
- Redirected search - direct product search
- Product impressions (by type - supporting items, )
- Brand Pages
- PLP Browse
- Search Within Results
- Comparison PLP (April/May 2026)


---

## Javascript Code

```js
window.appEventData = window.appEventData || [];
window.appEventData.push({
"event": "Listing Viewed",
"listing": {
    "listingParams": {
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
        "sortView": "<sortView>",
      }
    },
    "listingResults": {
      "resultsCount": "<resultsCount>",
      "resultsShown": "<resultsShown>",
      "itemListType": "<itemListType>",
      "item": [{
        "isDisplayed": "<isDisplayed>",
        "itemListType": "<itemListType>",
        "itemPosition": "<itemPosition>",
          "price":{
            "sellingPrice":"<sellingPrice>",
            "basePrice":"<basePrice>",
          },  
          "productInfo": {
            "sku": "<sku>",
            "productID": "<productID>",
            "productImage": "<productImage>"
            "brand": "<brand>",
            "inventoryStatus": "<inventoryStatus>",
            “promoPricing”: “<promoPricing>”,
            "specialPricingInitiative":"<specialPricingInitiative>",
            "quoteRequired":"<quoteRequired>",          
          },
      }]
    })
```
---

## Variable Definitions

| field | type | description | examples |
| :--- | :--- | :--- | :--- |
| **searchTermEntered** | string | Describes the search keyword exactly as entered by the user. | red lobster, red lboster, red lbstr, Zip code if search is for a retail/physical location |
| **searchMethod** | string | Describes the method of search. | global (primary header search), category:[category name], search within, retailer, direct product |
| **refinementType** | string | Describes the parameter or facet of the refinement being applied. | brand, size, rating, color |
| **refinementValue** | string | Provides the value for the parameter or facet of the refinement being applied. | Coors, L, M, S 3-5, Red |
| **sortSequence** | string | Not defined in the newer Listing Clicked specification. Legacy field used for sort order or sequence. |  |
| **sortView** | string | Not defined in the newer Listing Clicked specification. Legacy field used for selected sort view. |  |
| **resultsCount** | integer | The total number of items returned that matched the search criteria. | 0, 20, 110, 165 |
| **resultsShown** | integer | The number of items presented. Used with pagination, map, or lazyload UX. | 0, 5, 16, 32 |
| **itemListType** | string | Indicates the presentation type for displaying products/items. | product listing, search results, product comparison, products demonstrated, related items, supported items |
| **itemPosition** | integer | Integer position of a property within a sorted result. The first returned is position 1. | 1, 2, 3, 4, 5 |
| **sellingPrice** | string | This should be added as the price for the product including the discount amount. | 97.88, 805.09 |
| **basePrice** | string | Total price of the product, each of these fields exists depending on the event and context. | 97.88, 805.09 |
| **sku** | string | Stock Keeping Unit (SKU) Unique Identifier of specific item typically held in inventory. | 34567890, 4567890, 00155-large-cornflower |
| **productID** | string | Unique Identifier of a product or offering. Must match the format of back-end systems if used as a key for import of product metadata. | 15, 565, 588, 987, 764, 400 |
| **productImage** | string | If an image is present for a product, a unique image identifier should be present here. |  |
| **brand** | string | Set with the brand of the product. | krylon |
| **inventoryStatus** | string | Set to the inventory status of the product. | In stock, limited availability, not in stock/available to order |
| **promoPricing** | string | A flag representing if the product is currently seen or purchased at a promotional price. | yes, no |
| **specialPricingInitiative** | string | Closest newer match: specialPricingCampaign. Friendly name of special pricing event. | “Fall promotion”, “Summer discounts 2025” |
| **quoteRequired** | string | Set with a value of "yes" or "no" for each item when applicable. | yes -OR- no |

