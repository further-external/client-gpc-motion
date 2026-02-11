# Language Change

This event will fire when a visitor changes the site language. 

---

## Javascript Code

```javascript
appEventData || [];
appEventData.push({
  "event": "Language Change",
  "languageChange": {
    "siteLanguage": "<language>"
  }
});
```

---

## Variable Definitions

| field | type | description | examples |
| :--- | :--- | :--- | :--- |
| **siteLanguage** | string | Language selected by the visitor when changed from what was selected on the “load” of the page/SPA | english, french, spanish, etc. |
