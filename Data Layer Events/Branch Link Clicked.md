# Branch Link Clicked

This event is designed to measure custom clicks on branch links throughout the site. By capturing these specific data points, you can gain a granular understanding of how users are interacting with branch-specific contact methods.

---

## Use Cases
You can use this event to track various interactions, including but not limited to:
* **My Branch** – Contact Branch
  * **Email Branch**
  * **Phone**
* **My Branch** – Account Rep
  * **Email Rep**

---

## JavaScript Code
Implement the following snippet within your event listener to push the data to the `appEventData` array:

```javascript
window.appEventData = window.appEventData || [];
window.appEventData.push({
  "event": "Branch Link Clicked",
  "branchLink": {
    "linkType": "<linkType>",
    "linkText": "<linkText>",
    "contactInfo": "<contactInfo>"
  }
});
```

---

## Variable Definitions

| Field | Type | Description | Examples |
| :--- | :--- | :--- | :--- |
| **linkType** | `string` | Indicates the specific category of link clicked. | Email, Phone Number |
| **linkText** | `string` | The actual text or label displayed on the link. | Email Branch, Email Rep, tel: |
| **contactInfo** | `string` | The hashed phone number or email address associated with the link. | (123)-456-7890, email123@email.com |

