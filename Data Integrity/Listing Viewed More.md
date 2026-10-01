# Listing Viewed More


Event should fire whenever additional listing results load (pagination or "load more"). The `item[]` array contains only the newly shown items.

## Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Listing Viewed More",
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
| `listing.listingParams.pageNum` | integer | Result page number; increments as additional results load | `2` |
| `listing.listingParams.searchInfo.searchTermEntered` | string | Keyword exactly as entered; `""` for browse contexts | `quotes` |
| `listing.listingParams.searchInfo.searchMethod` | string | `global`, `category:[name]`, `search within results`, `retailer`, `direct product` | `global` |
| `listing.listingParams.refinements[]` | array | One object per applied refinement; `[]` when none applied | — |
| `listing.listingParams.refinements[].refinementType` | string | Facet name | `inStockOnly` |
| `listing.listingParams.refinements[].refinementValue` | string | Applied facet value | `allDc` |
| `listing.listingParams.sorts.sortSequence` | integer | Sort dominance when multiple sorts are applied (conditional) | `1` |
| `listing.listingParams.sorts.sortView` | string | Presentation view | `Grid` |
| `listing.listingResults.resultsCount` | integer | Total matching items | `40` |
| `listing.listingResults.resultsShown` | integer | Items rendered in this load | `24` |
| `listing.listingResults.findingWidget` | string | Always `RESULTS_LIST` on this event. **Added 2026-09-24 (Part 1), not yet in production.** | `RESULTS_LIST` |
| `listing.listingResults.findingPage` | string | Page type of the URL. Uses the existing `pageType` values. **Added 2026-09-24 (Part 1), not yet in production.** | `PRODUCT_CATEGORY` |
| `listing.listingResults.itemListType` | string | **Pending removal (Part 2).** Replaced by `findingWidget`. See Noteworthy Changes. List type: `search results`, `product listing`, `product comparison`, `products demonstrated`, `related items`, `supported items` | `search results` |
| `listing.listingResults.item[].itemPosition` | integer | 1-based position within the newly shown items | `1` |
| `listing.listingResults.item[].productInfo.sku` | string | SKU | `11864702` |
| `listing.listingResults.item[].productInfo.productId` | string | Unique product identifier | `11864702` |
| `listing.listingResults.item[].productInfo.brand` | string | Product brand | `TOPWORX` |
| `listing.listingResults.item[].productInfo.inventoryStatus` | string | Inventory status | `not-in-stock` |
| `listing.listingResults.item[].productInfo.productImage` | string | `"TRUE"`/`"FALSE"` — product has an image | `TRUE` |
| `listing.listingResults.item[].productInfo.quoteRequired` | string | `"TRUE"`/`"FALSE"` — item requires a quote | `FALSE` |
| `listing.listingResults.item[].productInfo.promotionalPricing` | string | `"TRUE"`/`"FALSE"` — item shown at a promotional price | `FALSE` |
| `listing.listingResults.item[].productInfo.specialPricingInitiative` | string | Special pricing flag; explicit fallback `FALSE` | `FALSE` |
| `listing.listingResults.item[].price.basePrice` | string | MSRP; unformatted, no thousands separators, ≤2 decimals; `"0"` when no price is available (never an empty string) | `1541.26` |
| `listing.listingResults.item[].price.sellingPrice` | string | Discounted price; same format rules as basePrice; `"0"` for quote-required items | `934.10` |

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

On this event the two fields sit on `listing.listingResults`. It fires when more results
load in a list, so the values match Listing Viewed: `findingWidget` is always `RESULTS_LIST` and
`findingPage` comes from the URL.

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
