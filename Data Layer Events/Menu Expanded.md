# Menu Expanded
This event fires when a user clicks on a top-level navigation category tab (e.g., Products, Services, or Resources) to expand a multi-column dropdown menu. It is designed to capture user engagement and intent to browse category content before a final link selection or redirect occurs.

## Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "Menu Expanded",
  "linkInfo": {
    "linkContainer": "<linkContainer>",
    "linkRegion": "<linkRegion>",
    "linkId": "<linkId>",
    "linkType": "<linkType>"
  }
});
```

## Variable Definitions
| Path | Type | Description | Example | Pattern | Min Length | Max Length | Minimum | Maximum | Multiple Of |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| linkInfo.linkContainer | string | Identifies the primary overarching structural container housing the menu links. | header-nav, footer-nav, Search Bar, Language Bar | | | | | | |
| linkInfo.linkRegion | string | Captures the specific dropdown menu context or grouping lane within the header block. | header, footer | | | | | | |
| linkInfo.linkId | string | Programmatic key or text identifier matching the specific user selection triggering the expansion. | products, services, resources | | | | | | |
| linkInfo.linkType | string | Describes the behavior or visual type of interactive element deployed. | menu-expand, tab, CTA | | | | | | |
