# User Registered

This event is set whenever a visitor to the site registers for a new account. This may be a direct registration or also as a part of the purchase/checkout process if user registration is required at that time.

---

## Javascript Code

```javascript
appEventData || [];
appEventData.push({
  "event": "User Registered",
  "user": {
    "accountType": "<accountType>",
    "custKey": "<custKey>",
    "userKey": "<userKey>",
    "branchID": "<branchID>",
    "industry": "<industry>",
    "jobFunction": "<jobFunction>"
  }
});
```

---

## Variable Definitions

| field | type | description | examples |
| :--- | :--- | :--- | :--- |
| **accountType** | string | Determines the type of account a user selects for registration this will be empty on the Step Name: "Account type" step | Personal, business |
| **custKey** | string | Unique identifier of a customer. Any ids considered PII must be hashed. | |
| **userKey** | string | Unique identifier of a user. Any ids considered PII must be hashed. | ABC1234 |
| **branchID** | string | Unique identifier of a branch/location. Any ids considered PII must be hashed. | 44556677 |
| **industry** | string | Unique identifier for the visitor industry necessary for vendor personalization | |
| **jobFunction** | string | Unique identifier for the visitor job function necessary for vendor personalization | |
