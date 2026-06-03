# Navigation Link Clicked

This event can be used to measure the click of any navigation link on the site in a custom manner. 

The different values within this event can be used as needed. Using the data here along with pageType will enable you to understand the details of the link clicked as well as the page where such a link was clicked. Examples of link clicks or events that could be measured with this function include (but are not limited to):
- Track Orders
- View/Upload Tax Documents/Certificates
- Navigation menu clicks

For the Header redesign this will apply to most elements found in the following menus:
- Services
- Resources
- Account Menu

---

## Javascript Code

```javascript
window.appEventData = window.appEventData || [];
window.appEventData.push({
  "event": "Navigation Link Clicked",
  "linkInfo": {
    "linkCategory": "<linkCategory>",
    "linkContainer": "<linkContainer>",
    "linkId": "<linkId>",
    "linkRegion": "<linkRegion>",
    "linkUrl": "<linkUrl>"
  }
});
```

---

## Variable Definitions

| field | type | description | examples |
| :--- | :--- | :--- | :--- |
| **linkRegion** | string | Indicates the region on page for a clicked link within the hierarchy [Page > Region > Container > linkID] | Top Nav, Footer Nav, Hero, Recommended, Also Shopped, Also Bought |
| **linkContainer** | string | Indicates the container for a clicked link within the hierarchy [Page > Region > Container > linkID] | Best Friends - Best Jeans, Puppy Love, Mens, Kids, Kids : Tops |
| **linkCategory** | string | Indicates the Product category for a clicked link within the hierarchy [Page > Region > Container > Category > linkID] | Abrasives, Bearings, Electrical, etc. |
| **linkId** | string | Unique ID of a clicked link within the hierarchy [Page > Region > Container > linkID] | sign up today, sign in, jeans, sweaters, donate |
| **linkUrl**| string  | Destination URL of a clicked element.| `/category/hydraulics`, `/quote`, `https://external.com`|
