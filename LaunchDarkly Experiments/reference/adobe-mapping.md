# Adobe mapping

[Back to the overview](../README.md) · For the analytics team

| Data | Adobe variable | Value format | Expiry / allocation | Notes |
|---|---|---|---|---|
| Assignments (Page Loaded `experiments`) | **list variable 2** (to confirm free) | `flagKey:variation`, one value per flag | Hit; set on every hit | list1 is already used (Refinements); only two list variables remain |
| Exposure (Experiment Exposed) | **list prop** (number to assign) + **counter event** (number to assign) | `flagKey:variation` | Hit | Keeps the last list variable free |
| Variation label | **Classification** of `flagKey:variation` | e.g. `Site refresh: new` | n/a | Static labels only (experiment name, variation label, owner). Classifications apply to all history, so they can't hold dates |
| LaunchDarkly visitor ID | eVar + prop (numbers to assign) | as sent | eVar: visit | Only with analytics consent. See [Privacy](../privacy.md) |

## Rules for the tag manager

1. **No flag version in the value.** It goes up every time someone edits the flag's targeting and
   would split one variation into many rows.
2. **Set the assignment variable on every hit, including link calls.** Cart adds, orders and other
   interactions go out as link calls, which send only the variables each rule lists. If the
   assignment variable isn't listed in a rule, conversions from that rule aren't credited to any
   variation.
3. **Hit expiry for assignments.** A visitor reassigned mid-visit is not credited to both variations.
4. **Deduplicate exposure** per flag per page view in the rule as well as on the site.
5. **Don't read LaunchDarkly's browser storage in production rules.** It's an internal format that
   holds the visitor's context. It's fine for a development-only proof of concept.

## Reading results

Adobe Analytics has no built-in significance testing for tests that don't run in Adobe Target. Lift
can be computed with calculated metrics, or, more robustly, outside Adobe on exported data.
