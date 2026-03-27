# CTA Click

When a CTA item is clicked, specific data points are pushed to the data layer. The implementation varies depending on whether the click occurs on a listed item or a standalone action.

---

## JavaScript Code

```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "CTA Click",
  "ctaClick": {
    "ctaType": "<ctaType>",
    "ctaDetail": "<ctaDetail>",
    "itemListType": "<itemListType>", 
    "itemPosition": "<itemPosition>"
  }
});
```

Note: For CTA clicks such as “Where is my order,” that is not a click on a list item, the only variables of the above specification that would need to be added are, “ctaType” and “ctaDetail.” Below is an example of such a CTA:

```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "CTA Click",
  "ctaClick": {
    "ctaType": "<ctaType>",
    "ctaDetail": "<ctaDetail>"
  }
});
```

---

## Variable Definitions

| Field | Type | Description | Examples |
| :--- | :--- | :--- | :--- |
| **ctaDetail** | `string` | Detailed description of the CTA link. | `ati tools`, `Sign up`, `Add to Cart`, `Shop Now - hero image` |
| **ctaType** | `string` | Indicates the type of CTA clicked. Captures context like configurators or specific button types. | `SMC Configurator`, `Aventics Configurator`, `Recommended Products`, `Shop Trusted Brands` |
| **itemListType** | `string` | Indicates the type of CTA listing. | `autopilot`, `homepage feature`, `recommended products` |
| **itemPosition** | `integer` | Integer position of a property within a sorted result. The first returned is position 1. | `1`, `2`, `3`, `4`, `5` |
