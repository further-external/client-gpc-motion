# Product Added
Triggers when a user adds an item to their shopping cart.
---

```js
appEventData || [];
appEventData.push({
  "event": "Product Added",
  "product": [{
    "productInfo": {
      "sku": "<sku>",
      "productID": "<productID>",
      "productImage": "<productImage>",
      "productFindingVideo": "<productFindingVideo>",
      "inventoryStatus": "<inventoryStatus>",
      "cartThreshold": "<cartThreshold>",
      "quoteRequired": "<quoteRequired>",
      "fullFindingMethod": "<productFindingMethod>|<itemListType>",
      “promoPricing”: “<promoPricing>”,
      "priceChange": "<priceChange>"
    },
    "price": {
      "sellingPrice": "<sellingPrice>"
    },
    "quantity": "<quantity>",
    "addType": "<addType>",
    "daysSaved": "<daysSaved>"
  }]
});
```
---
# Variable Definitions
| field               | type    | description                                                                                                                                                                                                                                                  | examples                                                                                                                                                                                                                                   |
| :-----------------: | :-----: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| cartThreshold       | string  | Will provide details on if the threshold between cart add and request a quote has been met                                                                                                                                                                   | add to cart OR request a quote                                                                                                                                                                                                             |
| sku                 | string  | Stock Keeping Unit (SKU) Unique Identifier of specific item (typically) held in inventory. Must match the format of back-end systems if used as a key for import of product meta data. Most often, one level below productID for products with SKU variants. | 34567890, 4567890, 00155-large-cornflower                                                                                                                                                                                                  |
| sellingPrice        | string  | String representation of the price paid after coupons or discounts. Positive. Up to two decimal places for cents. No currency symbol.                                                                                                                        | 200, 29.99, 50, 0                                                                                                                                                                                                                          |
| quantity            | integer | Integer number of products being acted upon (added to a cart, removed from wishlist, purchased, reserved, moved to a cart from save for later or save to list)                                                                                               | 1, 2, 3, 4, 5                                                                                                                                                                                                                              |
| productID           | string  | Unique Identifier of a product or offering. Must match the format of back-end systems if used as a key for import of product meta data. Most often, one level above SKU for products with SKU variants.                                                      | 155, 65588, 987764448                                                                                                                                                                                                                      |
| productImage        | string  | Set with a value of “true” if the product has an image available. Otherwise, set to “false”.                                                                                                                                                                 |                                                                                                                                                                                                                                            |
| productFindingVideo | string  | If on cart add, the visitor adds a product to their cart from a video page, the name of the video will be set here.                                                                                                                                          | Eaton - MiHow2 - Steps Necessary to Effectively Set Up a Hydraulic Sequencing Circuit                                                                                                                                                      |
| addType             | string  | When a product is added to cart, this will be set to the add type used by the visitor                                                                                                                                                                        | product detail, supporting items, related items, product listing, search results, catalog, promotions, homepage featured, previous order, upload, demonstrated products, conversion, etc., **cart save for later, saved cart, saved list** |
| inventoryStatus     | string  | Set to the inventory status of the product                                                                                                                                                                                                                   | In stock, limited availability, not in stock/available to order                                                                                                                                                                            |
| quoteRequired       | string  | Set with a value of "yes" or "no" when a product is added to cart.                                                                                                                                                                                           | yes OR no                                                                                                                                                                                                                                  |
| daysSaved           | integer | number of days in saved for later before added to cart                                                                                                                                                                                                       | 1, 2, 3, 4, 5                                                                                                                                                                                                                              |
| fullFindingMethod   | string  | Set only on cart add from a recommendation widget (on home, PDP, cart, etc.) or PLP. This is set with a concatenated value of the productFindingMethod and the list type.                                                                                    | “Homepage: You May Also Like\|You May Also Like”                                                                                                                                                                                           |
| promoPricing        | string  | A flag representing if the product is currently seen or purchased at a promotional price.                                                                                                                                                                    | yes, no                                                                                                                                                                                                                                    |
| priceChange         | string  | With the 2025 conversion initiative, this is a dedicated field in place to indicate those products which are subject to that pricing initiative - the desired example field should be the month and year for the permanent price change                      | April2025, May2025, January2026                                                                                                                                                                                                            |
