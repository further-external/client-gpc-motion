# Save to List

This event is set when the site visitor executes a save to list action.

---

## Javascript Code

```javascript
window.appEventData = window.appEventData || [];
window.appEventData.push({
  "event": "Save To List",
  "listName": "<listName>",
  "numberOfItemsSaved": "<numberOfItemsSaved>",
  "product": [
    {
      "productInfo": {
        "sku": "<sku>",
        "productID": "<productID>",
        "brand": "<brand>",
        "inventoryStatus": "<inventoryStatus>",
        "productImage": "<productImage>",
        "quoteRequired": "<quoteRequired>",
        "promoPricing": "<promoPricing>",
        "specialPricingInitiative": "<specialPricingInitiative>",
        "cartThreshold": "<cartThreshold>"
      },
      "price": {
        "sellingPrice": "<sellingPrice>",
        "basePrice": "<basePrice>"
      },
      "quantity": "<quantity>",
      "addType":"<addType>",
      "daysSaved": "<daysSaved>"
    }
  ]
});
```

---

## Variable Definitions

| field | type | description | examples |
| :--- | :--- | :--- | :--- |
| **addType** | string | When a product is added to cart, this will be set to the add type used by the visitor | product detail, supporting items, saved list |
| **basePrice** | string | Total price of the product, each of these fields exists depending on the event and context. | 97.88, 483.87 |
| **brand** | string | Set with the brand of the product | HYDAC, krylon |
| **cartThreshold** | string | Will provide details on if the threshold between cart add and request a quote has been met | add to cart -OR- request a quote |
| **daysSaved** | integer | number of days in saved for later before added to cart | 1,2,3,4,5 |
| **inventoryStatus** | string | Set to the inventory status of the product | In stock, in-stock-no-detail, limited availability |
| **listName** | string | The name of the list where a product was saved | my custom list, Bearings, Bolts |
| **numberOfItemsSaved** | integer | Capture the number of items saved in a cart | 1,2,3,4,5 |
| **productID** | string | Unique Identifier of a product or offering. Must match the format of back-end systems if used as a key for import of product meta data. | 02651684, 15565588 |
| **productImage** | string | If an image is present for a product, a unique image identifier or flag should be present here | true |
| **promoPricing** | string | A flag representing if the product is currently seen or purchased at a promotional price. | yes, no |
| **quantity** | integer | Integer number of products being acted upon | 1,2,3,4,5 |
| **quoteRequired** | string | Set with a value of "yes" or "no" for each item when a cart is saved, saved to a list, or products are moved to a cart from a saved cart/list. | yes, no |
| **sellingPrice** | string | This should be added as the price for the product including the discount amount. | 293.25, 97.88 |
| **sku** | string | Stock Keeping Unit (SKU) Unique Identifier of specific item (typically) held in inventory. | 02651684, 34567890 |
