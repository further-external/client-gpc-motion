# User Detected

Each page must include the following events in this order: (1) Page Load Started, (2) User Detected, and (3) Page Load Completed. Any additional page-level events should occur before the Page Load Completed event. Any values that are not available when the event is triggered should be set to an empty string.

---

## Javascript Code

```javascript
appEventData || [];
appEventData.push({
  "event": "User Detected",
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
| **custKey** | string | Unique identifier of a customer. Any ids considered PII must be hashed. | 12345 |
| **userKey** | string | Unique identifier of a user. Any ids considered PII must be hashed. | ABC1234 |
| **branchID** | string | Unique identifier of a branch/location. Any id's considered PII must be hashed. | 44556677 |
| **industry** | string | Unique identifier for the visitor industry necessary for vendor personalization | |
| **jobFunction** | string | Unique identifier for the visitor job function necessary for vendor personalization | |
