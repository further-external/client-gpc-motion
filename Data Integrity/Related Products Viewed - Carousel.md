# Related Products Viewed - Carousel


Fires whenever a related-product recommendation module loads its product cards, including on carousel cycling. This is an umbrella event covering all related-product experiences on the site, such as Substitute Products (PDP), You May Also Like (PDP), and Recently Viewed (homepage); the specific experience is identified by `listType`.

## Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Related Products Viewed - Carousel",
  "relatedProducts": {
    "findingWidget": "<findingWidget>",
    "findingPage": "<findingPage>",
    "item": [{
      "itemPosition": <itemPosition>,
      "productInfo": {
        "sku": "<sku>",
        "productId": "<productId>",
        "brand": "<brand>",
        "listType": "<listType>",
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
});
```

## Variable Definition
| Variable | Type | Description | Example |
|---|---|---|---|
| `relatedProducts.findingWidget` | string | The carousel's widget, one of 35 fixed values. One value per carousel, next to `item[]`, not on each item. **Added 2026-09-24 (Part 1), not yet in production.** | `CUSTOMERS_ALSO_BOUGHT_PRODUCTS` |
| `relatedProducts.findingPage` | string | Page type of the URL. One value per carousel. Uses the existing `pageType` values. **Added 2026-09-24 (Part 1), not yet in production.** | `PRODUCT_DETAIL` |
| `relatedProducts.item[].itemPosition` | integer | 1-based card position. Moved from inside `productInfo` to item level for consistency | `1` |
| `relatedProducts.item[].productInfo.sku` | string | SKU | `07408161` |
| `relatedProducts.item[].productInfo.productId` | string | Unique product identifier | `07408161` |
| `relatedProducts.item[].productInfo.brand` | string | Product brand | `TIMKEN` |
| `relatedProducts.item[].productInfo.listType` | string | **Pending removal (Part 2).** Replaced by `findingWidget`. See Noteworthy Changes. Widget list type identifying the experience (e.g. `Substitute Products`, `You May Also Like`, `Recently Viewed`) | `Substitute Products` |
| `relatedProducts.item[].productInfo.inventoryStatus` | string | Inventory status enum | `in-stock-no-detail` |
| `relatedProducts.item[].productInfo.productImage` | string | `"TRUE"`/`"FALSE"` | `TRUE` |
| `relatedProducts.item[].productInfo.quoteRequired` | string | `"TRUE"`/`"FALSE"` | `FALSE` |
| `relatedProducts.item[].productInfo.promotionalPricing` | string | `"TRUE"`/`"FALSE"` | `FALSE` |
| `relatedProducts.item[].productInfo.specialPricingInitiative` | string | Explicit fallback `FALSE` | `FALSE` |
| `relatedProducts.item[].price.basePrice` | string | MSRP | `47.40` |
| `relatedProducts.item[].price.sellingPrice` | string | Discounted price | `29.17` |

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

On this event the two fields sit once on `relatedProducts`, next to `item[]`, not on each
item. One carousel view has one widget. The old `listType` was copied onto every item even though it
never varied within a carousel.

Part 1 only adds fields here. `listType` is removed in Part 2.

#### `findingWidget` is deliberately NOT a 1:1 rename of `listType`

The changelog is explicit: it is **more granular** where the same on-screen label hid different
surfaces, and **coarser** where different labels hid the same backend algorithm.

**The headline case: four carousels all displaying "You May Also Like" resolve to three different
`findingWidget` values**, because three different recommendation algorithms drive them.

| Old `listType` | Real widget | New `findingWidget` |
|---|---|---|
| `'Featured Products'` | L1 category "Featured Products" | `FEATURED_PRODUCTS` |
| `'Recommended Products'` | Home "Recommended for you" | `RECOMMENDED_PRODUCTS` |
| `'NO_RESULTS_RECOMMENDED'` | No-results recommended carousel | `RECOMMENDED_PRODUCTS` — `findingPage: NO_RESULTS` disambiguates |
| `'You May Also Like'` | Checkout-complete / punchout-complete | `RECOMMENDED_PRODUCTS` |
| `'You May Also Like'` | PDP / category listing / vertical slider | `YOU_MAY_ALSO_LIKE_PRODUCTS` |
| `'You May Also Like'` | Cart page, non-empty cart | `CUSTOMERS_ALSO_BOUGHT_PRODUCTS` |
| `'Recently Viewed'` | Home "Recently viewed" | `RECENTLY_VIEWED_PRODUCTS` |
| `'EMPTY_CART'` | Cart empty-cart carousel | `RECENTLY_VIEWED_PRODUCTS` — `findingPage: SHOPPING_CART` disambiguates |
| `'Buy It Again'` | Home "Buy It Again" carousel | `BUY_IT_AGAIN` |
| `'Substitute Products'` | PDP substitute carousel | `SUBSTITUTE_PRODUCTS` |
| `'Customers Also Bought'` | PDP "Frequently Purchased With" | `CUSTOMERS_ALSO_BOUGHT_PRODUCTS` |
| `'Customers Also Bought'` | Add-to-cart overlay nested carousel | `CART_OVERLAY_CUSTOMERS_ALSO_BOUGHT_PRODUCTS` |

⚠️ **This improves the data and breaks pre/post comparison.** Historical `listType` reporting cannot
be reconstructed from `findingWidget`. **This table is the only bridge** — any carousel performance
comparison spanning the release needs it.

⚠️ **Two values need `findingPage` to disambiguate**, marked above. Reporting on `findingWidget` alone
will merge the no-results and home "Recommended for you" carousels, and the empty-cart and home
"Recently viewed" carousels.

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
