# Download Link Clicked

This event is set whenever a visitor executes a download.

---

## Javascript Code

```javascript
appEventData || [];
appEventData.push({
  "event": "Download Link Clicked",
  "linkInfo": {
    "fileName": "<fileName>",
    "linkCategory": "<linkCategory>",
    "linkContainer": "<linkContainer>",
    "linkId": "<linkId>",
    "linkRegion": "<linkRegion>"
  }
});
```

---

## Variable Definitions

| field | type | description | examples |
| :--- | :--- | :--- | :--- |
| **fileName** | string | Indicates the filename for download link tracking. | Year End 2012.pdf, Operating Instructions.doc |
| **linkCategory** | string | Indicates the Product category for a clicked link within the hierarchy [Page > Region > Container > Category > linkID] | Abrasives, Bearings, Electrical, etc. |
| **linkContainer** | string | Indicates the container for a clicked link within the hierarchy [Page > Region > Container > linkID] | Best Friends - Best Jeans, Puppy Love, Mens, Kids, Kids : Tops |
| **linkId** | string | Unique ID of a clicked link within the hierarchy [Page > Region > Container > linkID] | sign up today, sign in, jeans, sweaters, donate |
| **linkRegion** | string | Indicates the region on page for a clicked link within the hierarchy [Page > Region > Container > linkID] | Top Nav, Footer Nav, Hero, Recommended, Also Shopped, Also Bought |
