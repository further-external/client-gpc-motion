# Page Load Completed

Page Load Completed is part of the page load sequence, including virtual page loads in the case of single page apps, and must be the last event pushed in the page load event sequence.

---

## Javascript Code

```javascript
appEventData || [];
appEventData.push({
  "event": "Page Load Completed"
});
```
