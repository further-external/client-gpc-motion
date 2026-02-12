# User Registration Started

This event occurs when a user starts a registration (i.e. clicks “Register” Call-to-Action).

---

## Javascript Code

```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "User Registration Started",
  "registration": {
    "linkName":"linkName",
    "accountType": "<accountType>",
  }
});
```

---

## Variable Definitions

| field | type | description | examples |
| :--- | :--- | :--- | :--- |
| **linkName** | String | Capture of the name of the CTA that triggered the user registration | Register, Create a personal account |
| **accountType** | string | Determines the type of account a user selects for registration this will be empty on the Step Name: "Account type" step | Personal, business |
