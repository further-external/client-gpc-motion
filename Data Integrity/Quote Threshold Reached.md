# Quote Threshold Reached

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
> 🔴 **THIS EVENT HAS NO DUAL-WRITE WINDOW.** It **gains** the pair and **loses**
> `thresholdLocation` in the *same* change — the changelog states there is no window where both old
> and new fields are present. Every other event in this set has a Part 1 window where old and new
> can be reconciled on live traffic. **This one does not, so it carries the whole validation load in
> a lower environment.**
>
> **The pair sits at `product[]` — top-level siblings of `threshold`, NOT nested inside it.**
> `threshold` retains `thresholdType` and nothing else.


Event should fire whenever a quantity change crosses the quote threshold: either an increase that crosses into quote-required territory, or a decrease back below it.

## Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Quote Threshold Reached",
  "product": [{
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
    },
    "findingWidget": "<findingWidget>",
    "findingPage": "<findingPage>",
    "threshold": {
      "thresholdType": "<thresholdType>",
      "thresholdLocation": "<thresholdLocation>"
    },
    "quantity": "<quantity>"
  }]
});
```

## Variable Definition

| Variable | Type | Description | Example |
|---|---|---|---|
| `product[].productInfo.sku` | string | SKU of the product | `14369084` |
| `product[].productInfo.productId` | string | Unique product identifier | `14369084` |
| `product[].productInfo.brand` | string | Product brand | `PEER CHAIN` |
| `product[].productInfo.inventoryStatus` | string | Inventory status | `not-in-stock` |
| `product[].productInfo.productImage` | string | `"TRUE"`/`"FALSE"` — product has an image | `TRUE` |
| `product[].productInfo.quoteRequired` | string | `"TRUE"`/`"FALSE"` — item requires a quote | `TRUE` |
| `product[].productInfo.promotionalPricing` | string | `"TRUE"`/`"FALSE"` — item shown at a promotional price | `FALSE` |
| `product[].productInfo.specialPricingInitiative` | string | Special pricing flag; explicit fallback `FALSE` | `FALSE` |
| `product[].price.basePrice` | string | MSRP; unformatted, no thousands separators, ≤2 decimals; `"0"` when no price is available | `3.31` |
| `product[].price.sellingPrice` | string | Discounted price; same format rules as basePrice | `1.54` |
| `product[].findingWidget` | string | **Addition — top-level sibling of `threshold`, not nested inside it.** Widget or flow where the quantity change happened. Closed 35-value vocabulary, Appendix A | `RESULTS_LIST` |
| `product[].findingPage` | string | **Addition — top-level sibling of `threshold`.** Page classification of the URL. Reuses the `pageType` vocabulary, Appendix B | `SHOPPING_CART` |
| `product[].threshold.thresholdType` | string | `quote required` (increase crossed the threshold) or `add to cart` (decrease back below it) | `quote required` |
| `product[].threshold.thresholdLocation` | string | ⚠️ **PENDING REMOVAL — same change as the additions above, no dual-write window.** Superseded by `findingWidget`/`findingPage`. Old→new: `'cart'`→`DIRECT`+`SHOPPING_CART`, `'pdp'`→`DIRECT`+`PRODUCT_DETAIL`, `'plp'`→`RESULTS_LIST`, `'saved list'`→`SAVED_LIST`, `'Buy It Again'`→`BUY_IT_AGAIN`, `'cart flyout'`→`CART_FLYOUT`, `'cart overlay'`→`CART_OVERLAY`. Location of the quantity change: `pdp`, `plp`, `cart`, `best sellers`, `recommended items` | `plp` |
| `product[].quantity` | string | Quantity at the time of the threshold cross | `5600` |

## Part 1/2 notes for this event (2026-09-24)

### Five surfaces gain coverage that previously reported no location at all

Saved-list "Add Items" search results → `SAVED_LIST` · asset-management product details →
`ASSET_PROFILE` · compare dialog and compare page → `COMPARE_PRODUCTS` · SAYT recommended-product side
buttons → `SEARCH_AS_YOU_TYPE` · any carousel-embedded stepper → *that carousel's widget*.

These fired threshold events with **no location information**. They now report normally, so expect
volume to appear where there was none.

### 🔴 A correction, not a rename: substitute item cards were mislabeled

The substitute item card **hardcoded `thresholdLocation: 'saved list'`** on the component itself. Those
cards render only in the PDP out-of-stock dialog and the quick-order substitute dialog — **never in a
saved-list flow.**

**Every historical occurrence of `'saved list'` from this surface was mislabeled and must NOT be
mapped forward to `SAVED_LIST`.** Correct attribution going forward is `SUBSTITUTE_DIALOG_PRODUCTS`.
Genuine saved-list steppers were and remain `SAVED_LIST`.

⚠️ **So historical `'saved list'` threshold volume is a blend of two unrelated surfaces and cannot be
cleanly split.** Going forward they separate; the history does not. This needs an annotation.

### Three declared values never appeared on a threshold event

`thresholdLocation` shared an enum with Listing Clicked, so `'CSN'`, `'Order History'` and `'Quotes'`
were never threshold values. They are covered by the Listing Clicked mapping.
