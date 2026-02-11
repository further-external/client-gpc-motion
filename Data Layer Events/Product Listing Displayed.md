# Product Listing Displayed

This event would be set whenever multiple products are shown.

Some of the parameters here will be optional, based on the manner in which a visitor would have arrived at the product listing.

This event is part of the page load sequence, including virtual page loads in the case of single page apps, and must be pushed between the Page Load Started and Page Load Completed events, including:

* Search results
* Redirected search - direct product search
* Product impressions (by type - supporting items)
* Brand Pages
* PLP Browse
* Search Within Results

---

## Javascript Code

```javascript
appEventData || [];
appEventData.push({
  "event": "Product Listing Displayed",
  "listingDisplayed": {
    "productListType": "<productListType>",
    "productPosition": "<productPosition>",
    "refinementType": "<refinementType>",
    "refinementValue": "<refinementValue>",
    "resultsCount": "<resultsCount>",
    "resultsShown": "<resultsShown>",
    "searchTermEntered": "<searchTermEntered>",
    "searchMethod": "<searchMethod>",
    "sortSequence": "<sortSequence>",
    "sortView": "<sortView>",
    "product": [{
      "productInfo": {
        "addType": "<addType>",
        "brand": "<brand>",
        "cartThreshold": "<cartThreshold>",
        "daysSaved": "<daysSaved>",
        "fullFindingMethod": "<productFindingMethod>|<itemListType>",
        "inventoryStatus": "<inventoryStatus>",
        "isOutOfStock": "<isOutOfStock>",
        "moq": "<moq>",
        "moqRequired": "<moqRequired>",
        "name": "<name>",
        "productFindingMethod": "<productFindingMethod>",
        "productFindingVideo": "<productFindingVideo>",
        "productID": "<productID>",
        "productImage": "<productImage>",
        "productSearch": "<productSearch>",
        "productSearchPhrase": "<productSearchPhrase>",
        "productTabs": "<productTabs>",
        "promoPricing": "<promoPricing>",
        "quantity": "<quantity>",
        "quoteRequired": "<quoteRequired>",
        "sku": "<sku>",
        "specialPricingCampaign": "<name of campaign>",
        "specialPricingDiscountAmount": "<discount amount>",
        "specialPricingFlag": "<true || false>",
        "supplierInventory": "<supplierInventory>",
        "thresholdLocation": "<thresholdLocation>",
        "thresholdType": "<thresholdType>"
      },
      "price": {
        "sellingPrice": "<discountedPrice>",
        "basePrice": "<originalPrice>"
      }
    }] 
  }
});
```

---

## Variable Definitions

| field | type | description | examples |
| :--- | :--- | :--- | :--- |
| **addType** | string | When a product is added to cart, this will be set to the add type used by the visitor | product detail, supporting items, related items, product listing, search results, catalog, promotions, homepage featured, previous order, upload, demonstrated products, conversion, etc., cart save for later, saved cart, saved list |
| **basePrice** | string | Total price of the product, each of these fields exists depending on the event and context. | 97.88, 805.09 |
| **brand** | string | Set with the brand of the product | krylon |
| **cartThreshold** | string | Will provide details on if the threshold between cart add and request a quote has been met | add to cart -OR- request a quote |
| **daysSaved** | integer | number of days in saved for later before added to cart | 1, 2, 3, 4, 5 |
| **fullFindingMethod** | string | This is set with a concatenated value of the productFindingMethod and the list type where both are available | “Homepage: You May Also Like\|You May Also Like” |
| **inventoryStatus** | string | Set to the inventory status of the product | In stock, limited availability, not in stock/available to order |
| **isOutOfStock** | boolean | Flag that indicates whether a product is out of stock or no longer available | true, false |
| **itemListType** | string | Indicates the presentation type for displaying products/items. Note that values here might closely mirror the Cart Type (addType) seen in the “Product Added” event specification. | product listing (i.e. this is plp when browsing), search results, product comparison, products demonstrated, related items, supported items |
| **itemPosition** | integer | Integer position of a property within a sorted result. The first returned is position 1. For map results, this value can be the rank by distance from POI. | 1, 2, 3, 4, 5 |
| **moq** | string | Set with a value of “true” if the product’s minimum order quantity has not been met. Otherwise, this is set to “false”. | |
| **moqRequired** | string | Set with a value of "yes" or "no" when a product is added to cart. | yes -OR- no |
| **name** | string | Name of the product or offering. Should be unique and 1:1 with productID | Oceana, Corsica, Flame Tech, Air Jordan 88 |
| **productFindingMethod** | string | This will identify the finding method for the product | Knowledge Hub - Catalog, Knowledge Hub - Success Stories, Direct Search, bookmarked |
| **productFindingVideo** | string | If a product detail page is viewed after clicking through from a video page, the name of the video will be set here. | Eaton - MiHow2 - Steps Necessary to Effectively Set Up a Hydraulic Sequencing Circuit |
| **productID** | string | Unique Identifier of a product or offering. Must match the format of back-end systems if used as a key for import of product meta data. Most often, one level above SKU for products with SKU variants. | 15, 565, 588, 987, 764, 400 |
| **productImage** | string | If an image is present for a product, a unique image identifier should be present here | |
| **productListType** | string | Indicates the presentation type for displaying products/items. | product listing (i.e. this is plp when browsing), search results, product comparison, products demonstrated, related items, supported items |
| **productPosition** | integer | Integer position of a property within a sorted result. The first returned is position 1. For map results, this value can be the rank by distance from POI. | 1, 2, 3, 4, 5 |
| **productSearch** | string | Set with a value of “true” if the product view is the result of a site search landing directly on a product detail page. Otherwise, this is set to “false”. | |
| **productSearchPhrase** | string | Describes the search keyword exactly as entered by the user. | red lobster, red lboster, red lbstr, Zip code if search is for a retail/physical location |
| **productTabs** | string | Delimited list of the tabs available for the product on the current product detail page. | overview~specifications~msds |
| **promoPricing** | string | A flag representing if the product is currently seen or purchased at a promotional price. | yes, no |
| **quantity** | integer | Integer number of products being acted upon (added to a cart, removed from wishlist, purchased, reserved, moved to a cart from save for later or save to list) | 1, 2, 3, 4, 5 |
| **quoteRequired** | string | Set with a value of "yes" or "no" for each item when a cart is saved, saved to a list, or products are moved to a cart from a saved cart/list. | yes -OR- no |
| **refinementType** | string | Describes the parameter or facet of the refinement being applied. | brand, size, rating, color |
| **refinementValue** | string | Provides the value for the parameter or facet of the refinement being applied. | Coors, L, M, S 3-5, Red |
| **resultsCount** | integer | The total number of items returned that matched the search criteria. (Integer) | 0, 20, 110, 165 |
| **resultsShown** | integer | The number of items presented. Used with pagination, map, or lazyload UX. (Integer) | 0, 5, 16, 32 |
| **searchTermEntered** | string | Describes the search keyword exactly as entered by the user. | red lobster, red lboster, red lbstr, Zip code if search is for a retail/physical location |
| **searchMethod** | string | Describes the method of search. | global (primary header search), category:[category name], search within, retailer, direct product |
| **sellingPrice** | string | This should be added as the price for the product including the discount amount. | 97.88, 805.09 |
| **sku** | string | Stock Keeping Unit (SKU) Unique Identifier of specific item (typically) held in inventory. | 34567890, 4567890, 00155-large-cornflower |
| **sortSequence** | string | The type of sort order in place for the list | |
| **sortView** | string | The active toggle of sort view | grid, list |
| **specialPricingCampaign** | string | Friendly name of special pricing event. | “Fall promotion”, “Summer discounts 2025” |
| **specialPricingDiscountAmount** | string | Discount difference amount based on the base price. | 0.65 |
| **specialPricingFlag** | boolean | Boolean flag to track if special pricing is enabled. | “true”, “false” |
| **supplierInventory** | string | Set with “supplier inventory” or “other” | supplier network |
| **thresholdLocation** | string | Location where threshold change occurred | "pdp", "plp", "cart", "best sellers", "recommended items", etc. |
| **thresholdType** | string | Threshold type reached by visitor | "moq” OR “mtq” |
