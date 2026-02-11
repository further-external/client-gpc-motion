# CTA Listing Viewed

The ctaListing viewed event will be used to gather information about the impressions of CTAs on a page, including:
Autopilot Buttons

This should be fired between the page load started and completed events.

---

## Javascript Code

```javascript
appEventData || [];
appEventData.push({
  "event": "CTA Listing Viewed",
  "ctaClick": {
    "ctaType": "<ctaType>",
    "ctaDetail": "<ctaDetail>",
    "itemListType": "<itemListType>", 
    "itemPosition": "<itemPosition>"
  }
});
```

---

## Variable Definitions

| field | type | description | examples |
| :--- | :--- | :--- | :--- |
| **ctaDetail** | `string` | Detailed description of the CTA link | Autopilot example:<br>ati tools<br>cutting tools<br>SMC Example:<br>Sign up<br>Start Building<br>Request Quote<br>Add to Cart<br>Aventics Example:<br>Sign up<br>Start Building<br>Add to Cart for Quote<br>Start Over<br>CTA button Example:<br>Shop Now - hero image<br>Shop Product |
| **ctaType** | `string` | Indicates the type of CTA clicked. In this scenario of SMC vs Aventics, capturing the different types of CTA for the configurators. | SMC Configurator, Aventics Configurator, CTA button, Recommended Products, Explore Our Offers, Shop Trusted Brands |
| **itemListType** | `string` | Indicates the type of CTA listing. | List types could include:<br>autopilot<br>homepage feature<br>recommended products |
| **itemPosition** | `integer` | Integer position of a property within a sorted result. The first returned is position 1. For map results, this value can be the rank by distance from POI. | 1,2,3,4,5 |
