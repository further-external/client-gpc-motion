# Suggested Term Clicked

The **Listing Clicked** event is used to capture user interaction with a suggested search term.

This event fires when a user clicks a search suggestion presented in the suggestion/autocomplete interface.

This specification intentionally excludes all product-level and listing result data.  
Only search context and suggestion interaction data are included.

---

## Event Specification

```javascript
appEventData = window.appEventData || [];
appEventData.push({
  "event": "Suggested Term Clicked",
  "listing": {
    "listingParams": {
      "searchInfo": {
        "searchMethod": "<searchMethod>",
        "searchTermEntered": "<searchTermEntered>"
      },
      "searchSuggestions": {
        "termsReturned": "<termsReturned>",
        "suggestedTerms": [
          {
            "term": "<term>",
            "position": "<position>"
          }
        ]
      }
    }
  }
});
```

___
# Variable Definition

| Field                 | Type    | Description                                                                            | Example                                   |
| --------------------- | ------- | -------------------------------------------------------------------------------------- | ----------------------------------------- |
| **searchTermEntered** | string  | The original search query entered by the user prior to suggestion click.               | `test`, `hydrualic pum`                   |
| **searchMethod**      | string  | Method used to initiate the search experience.                                         | `global`, `search within`, `autocomplete` |
| **termsReturned**     | integer | Total number of suggestions returned by the suggestion service at time of interaction. | `0`, `3`, `5`                             |
| **term**              | string  | The suggested search term that was clicked.                                            | `hydraulic pump`, `hydraulic pumps`       |
| **position**          | integer | The ranking position of the clicked suggestion (1-indexed).                            | `1`, `2`, `3`                             |
