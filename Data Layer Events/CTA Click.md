# CTA Click

The **CTA Click** event captures user interaction with a call-to-action (CTA) element.

---

## Event Specification

```javascript
window.appEventData = window.appEventData || [];
window.appEventData.push({
  "event": "CTA Click",
  "linkInfo": {
    "linkName": "<linkName>",
    "linkId": "<linkId>",
    "linkUrl": "<linkUrl>",
    "linkRegion": "<linkRegion>",
    "linkContainer": "<linkContainer>",
    "linkCategory": "<linkCategory>",
    "linkPosition": "<linkPosition>",
    "ctaType": "<ctaType>",
    "ctaDetail": "<ctaDetail>"
  }
});
```
#Variable Definition:
--- 
| Field             | Type    | Description                                                                    | Example                                                           |
| ----------------- | ------- | ------------------------------------------------------------------------------ | ----------------------------------------------------------------- |
| **linkName**      | string  | Human-readable label of the clicked CTA element.                               | `Shop Now`, `Request Quote`, `View Details`                       |
| **linkId**        | string  | Unique identifier for the clicked element (DOM id, tracking id, or CMS id).    | `hero-shop-now-btn`, `cta-1234`                                   |
| **linkUrl**       | string  | Destination URL of the CTA.                                                    | `/category/hydraulics`, `/quote`, `https://external.com`          |
| **linkRegion**    | string  | High-level page section where the CTA appears.                                 | `Header`, `Hero`, `Body`, `Footer`, `Sidebar`                     |
| **linkContainer** | string  | Specific module or component containing the CTA.                               | `Promo Banner`, `Product Card`, `Search No Results Module`        |
| **linkCategory**  | string  | Functional grouping of the link.                                               | `Primary CTA`, `Secondary CTA`, `Promotional`, `Navigation`       |
| **linkPosition**  | integer | Positional index of the CTA within its container (1-indexed).                  | `1`, `2`, `3`                                                     |
| **ctaType**       | string  | Logical classification of the CTA's intent or business purpose.                | `Shop`, `Quote`, `Download`, `Learn More`, `Search Reformulation` |
| **ctaDetail**     | string  | Additional contextual detail describing the CTA placement or campaign context. | `Hero Banner`, `No Results Module`, `Product Grid Card`           |
