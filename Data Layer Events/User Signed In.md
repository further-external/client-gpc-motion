# User Signed In

This event is set whenever a visitor to the site logs in to their account.

---

## Javascript Code

```javascript
appEventData || [];
appEventData.push({
  "event": "User Signed In",
  "user": {
    "loginStatus": "<loginStatus>",
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
| **loginStatus** | string | Describes the login state of the user | logged in, logged out, guest |
| **custKey** | string | Unique identifier of a customer. Any ids considered PII must be hashed. | |
| **userKey** | string | Unique identifier of a user. Any ids considered PII must be hashed. | ABC1234 |
| **branchID** | string | Unique identifier of a branch/location. Any ids considered PII must be hashed. | 44556677 |
| **industry** | string | Unique identifier for the visitor industry necessary for vendor personalization | |
| **jobFunction** | string | Unique identifier for the visitor job function necessary for vendor personalization | |
