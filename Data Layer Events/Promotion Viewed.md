# Promotion Viewed

This event will fire when a promotion is viewed on the site (Promotions are the internal ads on the site).

---

## Javascript Code

```javascript
appEventData || [];
appEventData.push({
  "event": "Promotion Viewed", 
  "promotionViewed": {
    "promotionName": "<promotionName>", 
    "promotionId": "<promotionId>"
  }
});
```

---

## Variable Definitions

| field | type | description | examples |
| :--- | :--- | :--- | :--- |
| **promotionName** | string | The name of the promotion. | Trek bikes for kids, REI Spring Sale 2019, Viking Cruise Fall Specials |
| **promotionId** | string | Unique Identifier of a promotion | 2345, 56789, 9876 |
