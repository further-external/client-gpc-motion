# Listing Clicked

When a listing item is clicked, the following information will want to be known for the individual item that was clicked. An item is considered “clicked” when the add to cart button is clicked or the visitor clicks through to PDP.

---

## Javascript Code

```js
window.appEventData = window.appEventData || [];
window.appEventData.push({
"event": "Listing Clicked",
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
      "item": [ {
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
        }],
      }
    })
```
---

## Variable Definitions


