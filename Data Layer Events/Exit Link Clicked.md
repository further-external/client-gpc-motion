# Exit Link Clicked

The **Exit Link Clicked** event captures when a user clicks a link that takes them off-site (to a third-party domain). It's the destination-based version of our on-site click events (`CTA Click`, `Navigation Link Clicked`, `Ui Element clicked`), and it replaces Adobe's native exit-link tracking with something we control.

The first use case is order tracking (P44 "Last Mile Delivery"). This is the click that sends a customer to a shipment tracking page, either the new P44 page or a legacy carrier page.

---

## Event Specification

```javascript
window.appEventData = window.appEventData || [];
window.appEventData.push({
  "event": "Exit Link Clicked",
  "linkInfo": {
    "linkName": "<linkName>",
    "linkId": "<linkId>",
    "linkUrl": "<linkUrl>",
    "linkRegion": "<linkRegion>",
    "linkContainer": "<linkContainer>",
    "linkType": "<linkType>",
    "context": {
      "ocn": "<ocn>"
    }
  }
});
```

---

## Variable Definitions

| Field | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| **linkName** | string | The label of the clicked link. This is the value we count in reporting. | `Track It`, `Track All` |
| **linkId** | string | Unique ID for the clicked element (DOM id, tracking id, or CMS id). | `track-it-ship-1` |
| **linkUrl** | string | The full destination URL. For P44 this has the OCN and a unique Fulfillment ID in it. For a legacy carrier link it has the carrier tracking number. | `https://p44.example.com/track?ocn=0000345420&fid=...`, `https://wwwapps.ups.com/WebTracking/...` |
| **linkRegion** | string | The page section the link sits in. | `Body`, `Header` |
| **linkContainer** | string | The module or component the link is in. | `Shipment Card`, `Order Summary`, `Track All Modal` |
| **linkType** | string | Which experience the link is. We use this to split the new P44 experience from the legacy modal. | `Exit - P44`, `Exit - Modal` |
| **context.ocn** | string | The Motion order number (OCN) the link belongs to. It stays the same across every shipment in an order. For P44 we can pull it from the URL. For legacy it has to come from page context. | `0000345420` |
 
 **Note**: `linkInfo.context` holds the ID of business object the link is acting on (the order, in this case).

---

## Additional Attribute for tracking

Along with the spec, we want to add a data attribute to these elements for better data governance when the event fires. Adobe's automatic tracking is limited and isn't the best fit for this use case. With the attribute in place, the tag manager handles everything analytics-specific without worrying about extra hits.

1. **Flag the element.** Add `data-analytics-track-by-tag-manager="true"` to the clickable element. This works on any element, not just `<a>` (buttons or anything with a click handler are fine).
2. **Fire the event** with the payload above, using the values you have in the render context.
3. **The tag manager handles the rest.** Launch suppresses the native exit beacon for flagged elements and sends its own exit beacon instead. You don't need to touch the Adobe tracker (`s`) object.

## Example:
```html
<!-- any clickable element, not just <a> -->
<a href="https://p44.example.com/track?ocn=0000345420&fid=..."
   data-analytics-track-by-tag-manager="true">
  Track It
</a>
```

---