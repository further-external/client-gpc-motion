# Detail Cart Toggle

This event is to be set when users toggle ON the “Detailed Cart” toggle button in the cart dashboard. 

---

## Javascript Code

```javascript
appEventData || [];
appEventData.push({
  "event": "Detail Cart Toggle",
  "cartToggle": {
    "toggleStatus": "<toggleStatus>" //on or off at time of click
  }
});
```

---

## Variable Definitions

| field | type | description | examples |
| :--- | :--- | :--- | :--- |
| **toggleStatus** | string | Indicates the toggle status for detail cart toggle | on, off |
