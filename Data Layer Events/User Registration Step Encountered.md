# User Registration Step Encountered

This event occurs and determines where a user is in the registration process after clicking the register CTA, and should only trigger after an action has occurred in a given step.

---

## Javascript Code

```javascript
window.appEventData = window.appEventData || [];
appEventData.push({
  "event": "User Registration Stated",
  "registration": {
    "linkName": "linkName",
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
