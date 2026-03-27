# Search Suggestions Displayed

The **Search Suggestions Displayed** event captures information about suggested search terms presented to the user.

This event fires when the search suggestion service returns alternative or recommended queries, including in no-results scenarios or low-confidence result scenarios.

This specification intentionally excludes all product and listing-related variables.

---

## Event Specification

```javascript
window.appEventData = window.appEventData || [];
window.appEventData.push({
  "event": "Search Suggestions Displayed",
  "search": {
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
});

```

# Variable Definition
---

| Field                 | Type    | Description                                                                         | Example                                   |
| --------------------- | ------- | ----------------------------------------------------------------------------------- | ----------------------------------------- |
| **searchTermEntered** | string  | The original search query entered by the user prior to suggestions being displayed. | `hydrualic pum`, `test`                   |
| **searchMethod**      | string  | Method used to initiate the search experience.                                      | `global`, `autocomplete`, `search within` |
| **termsReturned**     | integer | Total number of suggestions returned by the suggestion service.                     | `0`, `3`, `5`                             |
| **term**              | string  | A suggested alternative or recommended search term displayed to the user.           | `hydraulic pump`, `hydraulic pumps`       |
| **position**          | integer | Ranking position of the suggestion within the visible suggestion list (1-indexed).  | `1`, `2`, `3`                             |
