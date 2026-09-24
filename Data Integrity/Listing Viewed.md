# Listing Viewed

> **Status:** Current — Adobe Analytics Package 2
> **Contract validated:** 2026-09-02/03 on production beacons · 17 event families, 0 contract failures
> **Last updated:** 2026-09-16 — Package 2 field renames applied
>
> | From | To | Why |
> |---|---|---|
> | `productID` | `productId` | Package 2 rename — camelCase standardised across product fields |
> | `promoPricing` | `promotionalPricing` | Package 2 rename — full word, matches the SDR friendly name |
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
> **On this event the pair sits at `listing.listingResults`.** `findingWidget` is always
> `RESULTS_LIST` here; `findingPage` carries the distinction (`SEARCH_RESULTS`, `PRODUCT_CATEGORY`,
> `BRAND_DETAIL`, `NO_RESULTS`).
>
> ⚠️ **One deliberate oddity:** when SAYT resolves to exactly one product the customer is redirected
> straight to the PDP and a synthetic Listing Viewed is emitted. Its `findingPage` is deliberately
> **`SEARCH_RESULTS`** — the conceptual origin — **not `PRODUCT_DETAIL`**, the physical landing URL.
> Pre-existing behaviour, not introduced by this work.


Captures when a user views a search results listing after performing a search.

# Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Listing Viewed",
  "listing": {
    "listingParams": {
      "pageNum": <pageNum>,
      "searchInfo": {
        "searchTermEntered": "<searchTermEntered>",
        "searchMethod": "<searchMethod>"
      },
      "refinements": [{
        "refinementType": "<refinementType>",
        "refinementValue": "<refinementValue>"
      }],
      "sorts": {
        "sortSequence": <sortSequence>,
        "sortView": "<sortView>"
      }
    },
    "listingResults": {
      "resultsCount": <resultsCount>,
      "resultsShown": <resultsShown>,
      "itemListType": "<itemListType>",
      "findingWidget": "<findingWidget>",
      "findingPage": "<findingPage>",
      "item": [{
        "itemPosition": <itemPosition>,
        "productInfo": {
          "sku": "<sku>",
          "productId": "<productId>",
          "brand": "<brand>",
          "inventoryStatus": "<inventoryStatus>",
          "productImage": "<productImage>",
          "quoteRequired": "<quoteRequired>",
          "promotionalPricing": "<promotionalPricing>",
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
| `listing.listingParams.pageNum` | integer | Result page number| `1` |
| `listing.listingParams.searchInfo.searchTermEntered` | string | Keyword exactly as entered; `""` for browse | `ears` |
| `listing.listingParams.searchInfo.searchMethod` | string | `global`, `category:[name]`, `search within results`, `retailer`, `direct product` | `global` |
| `listing.listingParams.refinements[].refinementType` | string | Facet name | `inStockOnly` |
| `listing.listingParams.refinements[].refinementValue` | string | Applied facet value | `allDc` |
| `listing.listingParams.sorts.sortSequence` | integer | Sort dominance in multi-sort.| `1` |
| `listing.listingParams.sorts.sortView` | string | Presentation view — newly documented | `List` |
| `listing.listingResults.resultsCount` | integer | Total matching items | `79` |
| `listing.listingResults.resultsShown` | integer | Items rendered | `24` |
| `listing.listingResults.findingWidget` | string | **Part 1 addition.** Always `RESULTS_LIST` on this event. Closed 35-value vocabulary, Appendix A | `RESULTS_LIST` |
| `listing.listingResults.findingPage` | string | **Part 1 addition.** Page classification of the URL. Reuses the `pageType` vocabulary, Appendix B | `SEARCH_RESULTS` |
| `listing.listingResults.itemListType` | string | ⚠️ **PENDING REMOVAL in Part 2** — superseded by the pair above. **Was hardcoded to the literal `'ITEM_LIST'` at both dispatch sites and never varied**, so removing it loses no information. Human-readable list type: `search results`, `product listing`, `product comparison`, `products demonstrated`, `related items`, `supported items``ITEM_LIST`| `search results` |
| `listing.listingResults.item[].itemPosition` | integer | 1-based item position, sibling of `productInfo` | `1` |
| `listing.listingResults.item[].productInfo.sku` | string | SKU | `02354888` |
| `listing.listingResults.item[].productInfo.productId` | string | Unique product identifier | `02354888` |
| `listing.listingResults.item[].productInfo.brand` | string | Product brand | `LOVEJOY INC` |
| `listing.listingResults.item[].productInfo.inventoryStatus` | string | Inventory status enum | `in-stock-no-detail` |
| `listing.listingResults.item[].productInfo.productImage` | string | `"TRUE"`/`"FALSE"` | `TRUE` |
| `listing.listingResults.item[].productInfo.quoteRequired` | string | `"TRUE"`/`"FALSE"` | `FALSE` |
| `listing.listingResults.item[].productInfo.promotionalPricing` | string | `"TRUE"`/`"FALSE"` | `FALSE` |
| `listing.listingResults.item[].productInfo.specialPricingInitiative` | string | Explicit fallback `FALSE` | `FALSE` |
| `listing.listingResults.item[].price.basePrice` | string | MSRP.| `1520.79` |
| `listing.listingResults.item[].price.sellingPrice` | string | Discounted price / actual price | `67.91` |
