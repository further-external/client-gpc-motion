
```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "User Signed In",
  "user": {
    "loginStatus": "logged in",
    "custKey": "00001401",
    "userKey": "AL98Y105",
    "branchID": "AL98",
    "emailAddress": "b1c53f9a4b8e2b6f4e1f2a3c5d7e9f0a1b2c3d4e5f60718293a4b5c6d7e8f901"
  }
});
```

| Variable | Type | Required | Description | Example |
|---|---|---|---|---|
| `user.loginStatus` | string | Yes | `logged in` | Auth service on successful sign-in |
| `user.custKey` | string | Yes | Customer surrogate key. |
| `user.userKey` | string | Yes | User surrogate key | 
| `user.branchID` | string | Yes | Branch identifier | 
| `user.emailAddress` | string | Yes | **SHA-256 hex hash** of lowercased, trimmed email. Never unhashed text values |
