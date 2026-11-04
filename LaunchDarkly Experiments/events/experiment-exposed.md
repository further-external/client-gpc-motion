# Experiment Exposed

**Event name:** `Experiment Exposed` · Records exposure · Phase 2 (after Page Loaded experiments)

[Back to the overview](../README.md)

## What it answers

- How many assigned visitors actually reached the feature a flag controls.
- Results for exposed visitors only, which is the fairer comparison when a feature sits deep in the
  site (for example a cart or product page change).

## When to fire it

- When the feature a flag controls is rendered for the visitor, using a **LaunchDarkly SDK hook**
  (LaunchDarkly's supported extension point) or the shared flag helper.
- **Once per flag per page view**: the same flag checked several times on one page fires once.
- Only for flags in the [allowlist](../reference/flag-allowlist.md).

## Specification

```javascript
window.appEventData = window.appEventData || [];
window.appEventData.push({
  "event": "Experiment Exposed",
  "experiment": {
    "flagKey": "<flagKey>",
    "variation": <variation>,
    "value": "<value>"
  }
});
```

| Field | Type | Description | Example |
|---|---|---|---|
| **flagKey** | string | The LaunchDarkly flag key | `redesigned-pdp` |
| **variation** | integer | Position of the served value, from 0 | `1` |
| **value** | string | The served value as text | `"false"` |

## Example

```javascript
window.appEventData.push({
  "event": "Experiment Exposed",
  "experiment": { "flagKey": "redesigned-pdp", "variation": 1, "value": "false" }
});
```
