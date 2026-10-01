# Product Added


Triggered when a user adds a product to their cart

# Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Product Added",
  "product": [{
    "productInfo": {
      "sku": "<sku>",
      "productId": "<productId>",
      "brand": "<brand>",
      "inventoryStatus": "<inventoryStatus>",
      "productImage": "<productImage>",
      "quoteRequired": "<quoteRequired>",
      "cartThreshold": "<cartThreshold>",
      "fullFindingMethod": "<productFindingMethod>|<itemListType>",
      "promotionalPricing": "<promotionalPricing>",
      "specialPricingInitiative": "<specialPricingInitiative>"
    },
    "price": {
      "basePrice": "<basePrice>",
      "sellingPrice": "<sellingPrice>"
    },
    "quantity": "<quantity>",
    "addType": "<addType>",
    "findingWidget": "<findingWidget>",
    "findingPage": "<findingPage>",
    "daysSaved": "<daysSaved>"
  }]
});
```

## Variable Definition

| Variable | Type | Description | Example |
|---|---|---|---|
| `product[].productInfo.sku` | string | SKU of added product | `10484964` |
| `product[].productInfo.productId` | string | Unique product identifier | `10484964` |
| `product[].productInfo.brand` | string | Product brand | `SUMITOMO DRIVE TECH` |
| `product[].productInfo.inventoryStatus` | string | Inventory status enum | `not-in-stock` |
| `product[].productInfo.productImage` | string | `"TRUE"`/`"FALSE"` | `TRUE` |
| `product[].productInfo.quoteRequired` | string | `"TRUE"`/`"FALSE"`  | `TRUE` |
| `product[].productInfo.fullFindingMethod` | string | `productFindingMethod|itemListType` concatenation | `Search Results|search results` |
| `product[].productInfo.productFindingVideo` | string | Video name when added from a video page | `Eaton - MiHow2 - Hydraulic Sequencing Circuit` |
| `product[].productInfo.promotionalPricing` | string | `"TRUE"`/`"FALSE"` | `FALSE` |
| `product[].productInfo.specialPricingInitiative` | string | Explicit fallback `FALSE` | `FALSE` |
| `product[].productInfo.cartThreshold` | string | when cart threshold is reached by a visitor changing the quantity of a product on PDP, PLP or the Cart.| `0`,`1`,`2` |
| `product[].price.basePrice` | string | MSRP `"0"` fallback on quote-required items | `0` |
| `product[].price.sellingPrice` | string | Discounted price | `0` |
| `product[].quantity` | string | Units added. For MOQ products added below the MOQ from a listing, reflects the actual quantity added | `1` |
| `product[].findingWidget` | string | Widget or flow the customer found the product through, one of 35 fixed values. On a PDP add, the value comes from the widget that sent the customer to the PDP. **Added 2026-09-24 (Part 1), not yet in production.** | `CUSTOMERS_ALSO_BOUGHT_PRODUCTS` |
| `product[].findingPage` | string | Page type of the URL when the event fired. Uses the existing `pageType` values. **Added 2026-09-24 (Part 1), not yet in production.** | `PRODUCT_DETAIL` |
| `product[].addType` | string | **Pending removal (Part 2).** Replaced by `findingWidget`. See Noteworthy Changes. Add context: `product detail`, `search results`, `product listing`, `related items`, `previous order`, `saved list`, `cart save for later`, etc. | `search results` |
| `product[].daysSaved` | string | Days in Save For Later before re-add; only when moved from Save For Later | `3` |

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

On this event the two fields sit on each item in `product[]` and are always present.

**`fullFindingMethod` breaks in Part 2.** It joins `productFindingMethod` and `itemListType`, and Part 2
removes `itemListType`. The SDR maps it to eVar16, so eVar16 needs a new source before Part 2 ships.

#### Old to new: `addType`

`addType` was optional and only six call sites ever set it. Every other Product Added left it out.

| Old `addType` | New `findingWidget` |
|---|---|
| `'cart save for later'` | `SAVE_FOR_LATER` |
| `'convertQuote'` | `CONVERT_QUOTE` |
| `'copyOrder'` | `COPY_ORDER` |
| `'saved list'` | `SAVED_LIST`, or `PLANT_FLOOR_SAVED_LIST` on the plant-floor panel |
| `'Search-As-You-Type'` | `SEARCH_AS_YOU_TYPE` |
| `'referred-<referrer>'` | `REFERRAL_LINK` |

The referrer name itself is not carried forward. `findingWidget` only records that the add came
through a referral link.

#### How a PDP add is attributed

When a customer clicks a product inside a widget, the widget and page are saved in `sessionStorage`,
keyed by product ID, for 30 minutes and up to 50 entries. If the customer then adds that product on
the PDP, the saved pair is used. So a PDP add is credited to the widget that sent the customer there,
not to the PDP.

#### `findingWidget` on this event

**Three `*QUANTITY_BOX` values are Product Added only.** They distinguish increments on an existing
**cart line** by the surface the stepper lives on: `QUANTITY_BOX` (cart page or line-details dialog),
`CART_FLYOUT_QUANTITY_BOX` (mini-cart), `CART_OVERLAY_QUANTITY_BOX` (add-to-cart overlay). Before this
work all three reported identically and were indistinguishable.

⚠️ **They apply only to cart-line steppers.** A stepper on a *product card* is part of an add-to-cart
form, so it reports that card's discovery widget instead. And the same interaction reports the plain
container value on a **threshold** event — bumping quantity in the mini-cart sends
`CART_FLYOUT_QUANTITY_BOX` on Product Added but `CART_FLYOUT` on a threshold crossing. Intentional:
`*QUANTITY_BOX` marks *how* the item was added, which is only meaningful here.

**Two sentinel values need reading carefully:**

- **`DIRECT`** is an *explicit* marker at the PDP add-to-cart form and the cart line-item list, **not a
  catch-all** — but it is also what you get when the click-through handoff **expires at 30 minutes**.
  A customer who browses longer than that before adding attributes to `DIRECT` rather than to the
  widget that actually sent them.
- **`NO_WIDGET_FOUND`** means placement was genuinely unknown — no marker in the ancestry, no handoff
  entry. **Read it as "unattributed", not as a widget.** Expected mainly for CMS-authored item cards.

**Report both as a share of total before quoting any widget attribution rate.** If `NO_WIDGET_FOUND`
is material, the attribution is not trustworthy yet, and that is measurable on day one.

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
