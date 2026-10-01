# Listing Clicked


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
| `listing.listingResults.findingWidget` | string | Widget or flow the clicked item was found through, one of 35 fixed values. **Added 2026-09-24 (Part 1), not yet in production.** | `RESULTS_LIST` |
| `listing.listingResults.findingPage` | string | Page type of the URL when the item was clicked. Uses the existing `pageType` values. **Added 2026-09-24 (Part 1), not yet in production.** | `SEARCH_RESULTS` |
| `listing.listingResults.itemListType` | string | **Pending removal (Part 2).** Replaced by `findingWidget`. See Noteworthy Changes. List type of the clicked item's widget | `You May Also Like` |
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

On this event the two fields sit on `listing.listingResults`.

**Volume will rise in Part 1.** Listing Clicked starts firing from six places that never sent it
before (listed below). That is a coverage fix, not a change in customer behaviour.

#### Old to new: `itemListType`

This is not a straight rename. `'You May Also Like'` maps to three different new values and
`'Customers Also Bought'` to two, because different recommendation algorithms sat behind the same
label. `'Home Page - Best Sellers'` is retired with no replacement; it never appeared on the wire.

| Old `itemListType` wire value | Surface | Replacement `findingWidget` |
|---|---|---|
| `'ITEM_LIST'` | Main search / category / brand / no-results results list | `RESULTS_LIST` |
| `'ITEM_LIST'` | CSN block embedded in a results page | `CSN_LIST` |
| `'item-compare'` | Compare dialog, compare page cards, compare sticky row | `COMPARE_PRODUCTS` |
| `'Header - Best Sellers'` | Header All Products mega-menu recommendations | `ALL_PRODUCTS_MENU_RECOMMENDED_PRODUCTS` |
| `'Buy It Again'` | Order-management Buy It Again table | `BUY_IT_AGAIN` |
| `'Home Page - Recommended Products'` | Home "Recommended for you" carousel | `RECOMMENDED_PRODUCTS` |
| `'Home Page - Recently Viewed'` | Home "Recently viewed" carousel | `RECENTLY_VIEWED_PRODUCTS` |
| `'You May Also Like'` | PDP / category-listing / vertical-slider "You May Also Like" | `YOU_MAY_ALSO_LIKE_PRODUCTS` |
| `'You May Also Like'` | Checkout-complete / punchout-complete carousel | `RECOMMENDED_PRODUCTS` |
| `'You May Also Like'` | Cart page, non-empty cart | `CUSTOMERS_ALSO_BOUGHT_PRODUCTS` |
| `'Customers Also Bought'` | PDP "Frequently Purchased With" | `CUSTOMERS_ALSO_BOUGHT_PRODUCTS` |
| `'Customers Also Bought'` | Add-to-cart overlay nested carousel | `CART_OVERLAY_CUSTOMERS_ALSO_BOUGHT_PRODUCTS` |
| `'Substitute'` | PDP substitute carousel | `SUBSTITUTE_PRODUCTS` |
| `'NoResults - Recommended'` | No-results page recommended carousel | `RECOMMENDED_PRODUCTS` |
| `'EmptyCart - Frequently Purchased'` | Cart empty-cart carousel | `RECENTLY_VIEWED_PRODUCTS` |
| `'Featured Products'` | L1 category "Featured Products" | `FEATURED_PRODUCTS` |

#### Part 1 coverage change: six surfaces start firing

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
