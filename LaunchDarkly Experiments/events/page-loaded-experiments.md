# Page Loaded: experiments attribute

**Event name:** `Page Loaded` (existing event, new attribute) · Records assignment

[Back to the overview](../README.md)

## What it answers

- Which variation of each agreed flag the visitor was assigned on this page view.
- Combined with any Adobe metric: conversion rate, cart adds, orders, revenue by experiment and
  variation.

## When to fire it

- On every Page Loaded, including single-page app route changes, **after LaunchDarkly is ready**.
- Include **only the flags in the [allowlist](../reference/flag-allowlist.md)**.
- If LaunchDarkly isn't ready in time, send Page Loaded without `experiments`. Never block the page.

## Specification

```javascript
window.appEventData = window.appEventData || [];
window.appEventData.push({
  "event": "Page Loaded",
  "page": { /* existing page attributes, unchanged */ },
  "experiments": [
    { "flagKey": "<flagKey>", "variation": <variation>, "value": "<value>" }
  ]
});
```

| Field | Type | Description | Example |
|---|---|---|---|
| **experiments** | array | One object per allowlisted flag the visitor has a value for | |
| **flagKey** | string | The LaunchDarkly flag key, exactly as in LaunchDarkly | `page-brand-refresh` |
| **variation** | integer | Position of the served value in the flag's variations, from 0 | `0` |
| **value** | string | The served value as text. For on/off flags `"true"` or `"false"` | `"true"` |

**Not sent:** the flag version, the evaluation reason, and anything from the visitor's LaunchDarkly
context. See [Privacy](../privacy.md).

## Example

Flag keys below are illustrative until the [allowlist](../reference/flag-allowlist.md) is confirmed.

```javascript
window.appEventData.push({
  "event": "Page Loaded",
  "page": { "pageType": "PRODUCT_DETAIL", "siteLanguage": "en-us" },
  "experiments": [
    { "flagKey": "page-brand-refresh", "variation": 0, "value": "true" },
    { "flagKey": "redesigned-pdp", "variation": 1, "value": "false" }
  ]
});
```

## Where it comes from

The site already reads flags through one shared helper (`useBoolLaunchDarklyFlag`) and a few direct
`variation()` calls. The simplest build reads the allowlisted flags from the LaunchDarkly client once
it's ready and adds them to Page Loaded.
