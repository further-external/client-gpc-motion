# Checking a build

[Back to the overview](README.md)

A checklist for testing before release. Test on a development or staging build first, then on
production after release. Never paste real visitor IDs or flag contexts into a ticket.

## Assignment on Page Loaded

1. Open the browser console. On each page, `appEventData.filter(e => e.event === 'Page Loaded')`
   shows one Page Loaded with an `experiments` array.
2. Every flag in `experiments` is on the [allowlist](reference/flag-allowlist.md); nothing else is
   there.
3. Each object has `flagKey`, `variation` and `value`, and nothing else (no version, no context).
4. Navigate within the site (a single-page route change): Page Loaded fires again with `experiments`.
5. Hard-reload the first page of a visit: `experiments` is present on the first Page Loaded, not only
   on later pages.

## What reaches Adobe

6. In the Adobe debugger, each page view carries the assignment list variable with one
   `flagKey:variation` per flag.
7. Add a product to the cart: the cart-add hit (a link call) carries the same list variable.
8. With analytics cookies declined, no hit reaches Adobe.

## Exposure (phase 2)

9. Reach a flagged feature: one Experiment Exposed per flag per page, even if the flag is checked
   several times.
10. Pages without the feature send no Experiment Exposed.

## After launch

After one to two weeks of data, three health checks. If they look off, the issue is identity or
implementation, not the reporting tool:

- the share of Adobe visitors with more than one LaunchDarkly visitor ID;
- the share of visitors seen in more than one variation of the same flag;
- the split between variations against the split configured in LaunchDarkly.
