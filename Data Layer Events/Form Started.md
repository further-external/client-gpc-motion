# Form Started

This event is set on the start of a form. This should be set when a visitor first interacts with and actually starts the process of completing a form. 

---

## Javascript Code

```javascript
appEventData || [];
appEventData.push({
  "event": "Form Started",
  "form": {
    "formName": "<formName>"
  }
});
```

---

## Variable Definitions

| field | type | description | examples |
| :--- | :--- | :--- | :--- |
| **formName** | string | Plain text form name. | - Contact Us<br>- Email Sign-up (can occur during account registration, account profile modification, or during checkout)<br>- Forgot Password<br>- Password Reset |
