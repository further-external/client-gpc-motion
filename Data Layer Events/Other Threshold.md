# Other Threshold

> **Status:** Current — Adobe Analytics Package 2
> **Contract validated:** 2026-09-02/03 on production beacons · 17 event families, 0 contract failures
> **Last updated:** 2026-09-16 — Package 2 field renames applied
>
> | From | To | Why |
> |---|---|---|
> | `productID` | `productId` | Package 2 rename — camelCase standardised across product fields |
> | `promoPricing` | `promotionalPricing` | Package 2 rename — full word, matches the SDR friendly name |
> | `moq` | `minimumPurchaseQuantityNotMet` | Package 2 rename — explicit name replaces the `moq` abbreviation |
> | `"yes"/"no"`, `"true"/"false"`, `"Y"/"N"` | `"TRUE"`/`"FALSE"` | Package 2 ruled these string booleans uppercase |
>
> Only fields present on this page are listed. See the repository README for the full Package 2 change set.
>
> ---
>
> **2026-09-24 — `findingWidget` / `findingPage` added.** Source: `further-adobe-changelog.md`,
> Zack Miller 2026-09-17.
>
> ⚠️ **NOT IN PRODUCTION.** Zack: *"None of these are in production just yet, pending our own
> internal QA testing and any necessary coordination with y'all."* The work ships in two phases:
> **Part 1** adds the pair, **Part 2** removes the superseded field. **Part 2 has no release date.**
>
> Vocabulary: **Appendix A** of the changelog is a *closed* 35-value `findingWidget` set.
> **`findingPage` introduces no new vocabulary** — it reuses the existing `pageType` values already
> sent on Page Loaded (Appendix B), where `''` means the URL maps to no known page type.
> 
> 🔴 **THIS EVENT HAS NO DUAL-WRITE WINDOW.** It **gains** the pair and **loses**
> `thresholdLocation` in the *same* change. No window exists where both are present, so validation
> must happen in a lower environment.
>
> 🔴 **PAYLOAD SHAPE DISCREPANCY — needs confirming with Zack before build.** The changelog states the
> pair are *"top-level siblings of `threshold`, not nested inside it"*, i.e. `product[].findingWidget`
> with `threshold` retaining only `thresholdType`. **That matches Quote Threshold Reached, which uses
> `product[].threshold.*` — but it does NOT match this page**, which carries every field flat inside
> `thresholdReached.product[].productInfo.*` with no `threshold` object at all. The two threshold
> events have divergent shapes today and the changelog describes only one of them. **Documented below
> against this page's existing shape; confirm which shape ships.**
>
> 🔴 **Part 1 also revives this event on the cart quantity box.** Minimum-order-quantity and
> minimum-transfer-quantity crossings from a cart stepper **never reached Adobe** — the dispatch was
> wrapped in a debounce that was constructed but never invoked. Now fixed. **Historical data for that
> surface is missing, not zero**, and the volume increase is a bug fix rather than a change in
> customer behaviour. Requires an Adobe annotation.
>
> ⚠️ Note the coverage fix lands in **Part 1** even though the attributes do not change until Part 2,
> so during a Part 1-only window the event fires with its existing payload including
> `thresholdLocation`.


Executed when a visitor changes the quantity of a product in the cart, resulting in one of the following:
1. MOQ messaging displayed
2. MTQ messaging displayed

Note that the action above could happen at the following times:
1. PDP
2. PLP
3. Cart

---

## Javascript Code

```javascript
appEventData || [];
appEventData.push({
  "event": "Other Threshold Reached",
  "thresholdReached": {
    "product": [{
      "productInfo": {
        "addType": "<addType>",
        "brand": "<brand>",
        "cartThreshold": "<cartThreshold>",
        "daysSaved": "<daysSaved>",
        "fullFindingMethod": "<productFindingMethod>|<itemListType>",
        "inventoryStatus": "<inventoryStatus>",
        "isOutOfStock": "<isOutOfStock>",
        "minimumPurchaseQuantityNotMet": "<minimumPurchaseQuantityNotMet>",
        "moqRequired": "<moqRequired>",
        "name": "<name>",
        "productFindingMethod": "<productFindingMethod>",
        "productFindingVideo": "<productFindingVideo>",
        "productId": "<productId>",
        "productImage": "<productImage>",
        "productSearch": "<productSearch>",
        "productSearchPhrase": "<productSearchPhrase>",
        "productTabs": "<productTabs>",
        "promotionalPricing": "<promotionalPricing>",
        "quantity": "<quantity>",
        "quoteRequired": "<quoteRequired>",
        "sku": "<sku>",
        "specialPricingCampaign": "<name of campaign>",
        "specialPricingDiscountAmount": "<discount amount>",
        "specialPricingFlag": "<true || false>",
        "supplierInventory": "<supplierInventory>",
        "findingWidget": "<findingWidget>",
        "findingPage": "<findingPage>",
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
| **minimumPurchaseQuantityNotMet** | string | Set with a value of “true” if the product’s minimum order quantity has not been met. Otherwise, this is set to “false”. | |
| **moqRequired** | string | Set with a value of "TRUE" or "FALSE" when a product is added to cart. | TRUE -OR- FALSE |
| **name** | string | Name of the product or offering. Should be unique and 1:1 with productId | Oceana, Corsica, Flame Tech, Air Jordan 88 |
| **productFindingMethod** | string | This will identify the finding method for the product | Knowledge Hub - Catalog, Knowledge Hub - Success Stories, Direct Search, bookmarked |
| **productFindingVideo** | string | If a product detail page is viewed after clicking through from a video page, the name of the video will be set here. | Eaton - MiHow2 - Steps Necessary to Effectively Set Up a Hydraulic Sequencing Circuit |
| **productId** | string | Unique Identifier of a product or offering. Must match the format of back-end systems if used as a key for import of product meta data. Most often, one level above SKU for products with SKU variants. | 15, 565, 588, 987, 764, 400 |
| **productImage** | string | If an image is present for a product, a unique image identifier should be present here | |
| **productSearch** | string | Set with a value of “true” if the product view is the result of a site search landing directly on a product detail page. Otherwise, this is set to “false”. | |
| **productSearchPhrase** | string | Describes the search keyword exactly as entered by the user. | red lobster, red lboster, red lbstr, Zip code if search is for a retail/physical location |
| **productTabs** | string | Delimited list of the tabs available for the product on the current product detail page. | overview~specifications~msds |
| **promotionalPricing** | string | A flag representing if the product is currently seen or purchased at a promotional price. | TRUE, FALSE |
| **quantity** | integer | Integer number of products being acted upon (added to a cart, removed from wishlist, purchased, reserved, moved to a cart from save for later or save to list) | 1, 2, 3, 4, 5 |
| **quoteRequired** | string | Set with a value of "TRUE" or "FALSE" for each item when a cart is saved, saved to a list, or products are moved to a cart from a saved cart/list. | TRUE -OR- FALSE |
| **sellingPrice** | string | This should be added as the price for the product including the discount amount. | 97.88, 805.09 |
| **sku** | string | Stock Keeping Unit (SKU) Unique Identifier of specific item (typically) held in inventory. | 34567890, 4567890, 00155-large-cornflower |
| **specialPricingCampaign** | string | Friendly name of special pricing event. | “Fall promotion”, “Summer discounts 2025” |
| **specialPricingDiscountAmount** | string | Discount difference amount based on the base price. | 0.65 |
| **specialPricingFlag** | boolean | Boolean flag to track if special pricing is enabled. | “true”, “false” |
| **supplierInventory** | string | Set with “supplier inventory” or “other” | supplier network |
| **findingWidget** | string | **Addition.** Widget or flow where the quantity change happened. Closed 35-value vocabulary, Appendix A of `further-adobe-changelog.md`. ⚠️ Payload path unconfirmed — see the shape discrepancy in the header | RESULTS_LIST, CART_FLYOUT, SUBSTITUTE_DIALOG_PRODUCTS |
| **findingPage** | string | **Addition.** Page classification of the URL at the moment of the event. Reuses the existing `pageType` vocabulary unchanged, Appendix B | SHOPPING_CART, PRODUCT_DETAIL, `''` |
| **thresholdLocation** | string | ⚠️ **PENDING REMOVAL — same change as the additions above, no dual-write window.** Superseded by findingWidget/findingPage. `'cart'`→DIRECT, `'pdp'`→DIRECT, `'plp'`→RESULTS_LIST, `'saved list'`→SAVED_LIST **or SUBSTITUTE_DIALOG_PRODUCTS (see correction below)**, `'Buy It Again'`→BUY_IT_AGAIN, `'cart flyout'`→CART_FLYOUT, `'cart overlay'`→CART_OVERLAY. Location where threshold change occurred | "pdp", "plp", "cart", "best sellers", "recommended items", etc. |
| **thresholdType** | string | Threshold type reached by visitor | "minimumPurchaseQuantityNotMet” OR “mtq” |

---

## Part 1/2 notes for this event (2026-09-24)

### 🔴 A correction, not a rename: substitute item cards were mislabeled

The substitute item card **hardcoded `thresholdLocation: 'saved list'`** on the component. Those cards
render only in the PDP out-of-stock dialog and the quick-order substitute dialog — **never in a
saved-list flow.**

**Every historical occurrence of `'saved list'` from this surface was mislabeled and must NOT be
mapped forward to `SAVED_LIST`.** Correct attribution going forward is `SUBSTITUTE_DIALOG_PRODUCTS`.

⚠️ **Historical `'saved list'` threshold volume is therefore a blend of two unrelated surfaces and
cannot be cleanly split.** Going forward they separate cleanly; the history does not.

### Five surfaces gain coverage that previously reported no location

Saved-list "Add Items" search results → `SAVED_LIST` · asset-management product details →
`ASSET_PROFILE` · compare dialog and compare page → `COMPARE_PRODUCTS` · SAYT recommended-product side
buttons → `SEARCH_AS_YOU_TYPE` · any carousel-embedded stepper → *that carousel's widget*.

### The cart-line stepper reports a different value here than on Product Added

Bumping quantity in the mini-cart sends `CART_FLYOUT_QUANTITY_BOX` on **Product Added** but
`CART_FLYOUT` on the **threshold** event from that same interaction. Intentional: the `*QUANTITY_BOX`
values mark *how* an item was added, which is only meaningful on Product Added.

### Three declared values never appeared on a threshold event

`thresholdLocation` shared an enum with Listing Clicked, so `'CSN'`, `'Order History'` and `'Quotes'`
were never threshold values.
