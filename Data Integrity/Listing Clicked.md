# Listing Clicked

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
> **On this event the pair sits at `listing.listingResults`.**
>
> 🔴 **Part 1 also changes volume on this event.** Listing Clicked now fires from **six surfaces that
> never dispatched it** — see the coverage note below. Expect a step change that is a coverage fix,
> not customer behaviour.


Fires when a listing item is clicked (click-through to PDP or add-to-cart from listing). Contains only the clicked item.

## Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Listing Clicked",
  "listing": {
    "listingParams": {
      "searchInfo": {
        "searchTermEntered": "<searchTermEntered>",
        "searchMethod": "<searchMethod>"
      },
      "refinements": [{
        "refinementType": "<refinementType>",
        "refinementValue": "<refinementValue>"
      }],
      "sorts": {
        "sortSequence": "<sortSequence>",
        "sortView": "<sortView>"
      }
    },
    "listingResults": {
      "resultsCount": "<resultsCount>",
      "resultsShown": "<resultsShown>",
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
          "fullFindingMethod": "<productFindingMethod>|<itemListType>",
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
| `listing.listingParams.searchInfo.searchTermEntered` | string | Keyword exactly as entered; `""` when the click is not from a search context | `ears` |
| `listing.listingParams.searchInfo.searchMethod` | string | `global`, `category:[name]`, `search within results`, `retailer`, `direct product`; `""` when not from search | `global` |
| `listing.listingParams.refinements[].refinementType` | string | Facet name | `inStockOnly` |
| `listing.listingParams.refinements[].refinementValue` | string | Applied facet value | `allDc` |
| `listing.listingParams.sorts.sortView` | string | Presentation view — newly documented for this event| `List` |
| `listing.listingParams.sorts.sortSequence` | string | Sort dominance in multi-sort | `1` |
| `listing.listingResults.resultsCount` | string | Total matching items. | `4` |
| `listing.listingResults.resultsShown` | string | Items rendered | `4` |
| `listing.listingResults.findingWidget` | string | **Part 1 addition.** Widget or flow the clicked item was found through. Closed 35-value vocabulary, Appendix A | `RESULTS_LIST` |
| `listing.listingResults.findingPage` | string | **Part 1 addition.** Page classification of the URL at click time. Reuses the `pageType` vocabulary, Appendix B | `SEARCH_RESULTS` |
| `listing.listingResults.itemListType` | string | ⚠️ **PENDING REMOVAL in Part 2** — superseded by `findingWidget`, which is more granular. Note `'You May Also Like'` mapped to **three different** new values and `'Customers Also Bought'` to two, so this is not a rename. `'Home Page - Best Sellers'` retires with no replacement — it had no live call site and never appeared on the wire. List type of the clicked item's widget | `You May Also Like` |
| `listing.listingResults.item[].itemPosition` | integer | 1-based position of the clicked item | `3` |
| `listing.listingResults.item[].productInfo.sku` | string | SKU of clicked item | `04225797` |
| `listing.listingResults.item[].productInfo.productId` | string | Unique product identifier | `04225797` |
| `listing.listingResults.item[].productInfo.brand` | string | Product brand | `SKF` |
| `listing.listingResults.item[].productInfo.inventoryStatus` | string | Inventory status enum | `in-stock-no-detail` |
| `listing.listingResults.item[].productInfo.productImage` | string | `"TRUE"`/`"FALSE"` | `TRUE` |
| `listing.listingResults.item[].productInfo.quoteRequired` | string | `"TRUE"`/`"FALSE"`| `FALSE` |
| `listing.listingResults.item[].productInfo.fullFindingMethod` | string | Concatenated `productFindingMethod|itemListType` for widget attribution| `PDP: You May Also Like|You May Also Like` |
| `listing.listingResults.item[].productInfo.promotionalPricing` | string | `"TRUE"`/`"FALSE"`| `FALSE` |
| `listing.listingResults.item[].productInfo.specialPricingInitiative` | string | Explicit fallback `FALSE`| `FALSE` |
| `listing.listingResults.item[].price.basePrice` | string | MSRP| `55.60` |
| `listing.listingResults.item[].price.sellingPrice` | string | Discounted price| `34.22` |

## Part 1 coverage change — six surfaces start firing (2026-09-24)

These product links previously navigated **silently**. Each now emits a normal Listing Clicked with
`itemPosition`, product info and the attribution pair.

| Surface | `findingWidget` |
|---|---|
| SAYT dropdown recommended products | `SEARCH_AS_YOU_TYPE` |
| Home "Buy It Again" dashboard card | `BUY_IT_AGAIN` |
| CSN dashboard table description links | `CSN_DASHBOARD_LIST` |
| Order history line-item description links | `ORDER_HISTORY` |
| Quote line-item description links | `QUOTES` |
| Substitute item cards / substitute-items dialog | `SUBSTITUTE_DIALOG_PRODUCTS` |

⚠️ **This is a coverage fix, not a behaviour change.** Historical volume for these six surfaces should
be read as **missing, not zero**. An Adobe annotation at the release date is required, or every
Listing Clicked trend reads as a step change in engagement.
