# Form Submission Succeeded

This event is set when a form is successfully completed. 

---

## Javascript Code

```javascript
appEventData || [];
appEventData.push({
  "event": "Form Submission Succeeded",
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
