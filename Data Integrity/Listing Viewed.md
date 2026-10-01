# Listing Viewed


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
| `listing.listingResults.findingWidget` | string | Always `RESULTS_LIST` on this event. **Added 2026-09-24 (Part 1), not yet in production.** | `RESULTS_LIST` |
| `listing.listingResults.findingPage` | string | Page type of the URL. Uses the existing `pageType` values. **Added 2026-09-24 (Part 1), not yet in production.** | `SEARCH_RESULTS` |
| `listing.listingResults.itemListType` | string | **Pending removal (Part 2).** Replaced by `findingWidget`. See Noteworthy Changes. Human-readable list type: `search results`, `product listing`, `product comparison`, `products demonstrated`, `related items`, `supported items``ITEM_LIST`| `search results` |
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

---

## Noteworthy Changes

### 2026-09-24

**`findingWidget` and `findingPage` added. Not in production yet.**

Source: Zack Miller's `further-adobe-changelog.md`, emailed 2026-09-17. Zack: *"None of these are in
production just yet, pending our own internal QA testing and any necessary coordination with y'all."*

The change ships in two parts. Part 1 adds the two fields. Part 2 removes the field they replace.
Part 2 has no release date yet.

- `findingWidget` is one of 35 fixed values (Appendix A of the changelog).
- `findingPage` adds no new values. It reuses the `pageType` values already sent on Page Loaded. An
  empty string means the URL matched no known page type.

On this event the two fields sit on `listing.listingResults`. `findingWidget` is always
`RESULTS_LIST`; `findingPage` carries the difference (`SEARCH_RESULTS`, `PRODUCT_CATEGORY`,
`BRAND_DETAIL`, `NO_RESULTS`).

One deliberate quirk: when search-as-you-type matches exactly one product, the customer goes straight
to the PDP and a Listing Viewed is still sent for that result. Its `findingPage` is `SEARCH_RESULTS`,
where the search started, not `PRODUCT_DETAIL`, where the customer landed. This was already the
behaviour before this change.

#### Old to new: `itemListType`

`itemListType` was hardcoded to `'ITEM_LIST'` at both places this event fires and never changed, so
removing it loses no information.

### 2026-09-16

Package 2 field renames applied. Page current for Adobe Analytics Package 2. Only the fields on this
page are listed; the repository README has the full Package 2 change set.

| From | To | Why |
|---|---|---|
| `productID` | `productId` | Package 2 rename — camelCase standardised across product fields |
| `promoPricing` | `promotionalPricing` | Package 2 rename — full word, matches the SDR friendly name |
| `"yes"/"no"`, `"true"/"false"`, `"Y"/"N"` | `"TRUE"`/`"FALSE"` | Package 2 ruled these string booleans uppercase |

### 2026-09-03

Contract validated on production beacons on 2026-09-02 and 2026-09-03: 17 event families, 0 contract
failures.
