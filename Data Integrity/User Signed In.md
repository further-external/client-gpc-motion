# User Signed In
The event should fire whenever a user successfully signs in to their account.

## Javascript Code
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "User Signed In",
  "user": {
    "loginStatus": "<loginStatus>",
    "custKey": "<custKey>",
    "userKey": "<userKey>",
    "branchID": "<branchID>",
    "emailAddress": "<emailAddress>"
  }
});
```
## Variable Definition
| Variable | Type | Required | Description | Example |
|---|---|---|---|---|
| `user.loginStatus` | string | Yes | Customer's current logged in status | `logged-in` |
| `user.custKey` | string | Yes | Customer surrogate key. |`00001401`|
| `user.userKey` | string | Yes | User surrogate key |`AL98Y105`|
| `user.branchID` | string | Yes | Branch identifier | `AL98`|
| `user.emailAddress` | string | Yes | **SHA-256 hex hash** of lowercased, trimmed email. Never unhashed text values |`b1c53f9a4b8e2b6f4e1f2a3c5d7e9f0a1b2c3d4e5f60718293a4b5c6d7e8f901` |
