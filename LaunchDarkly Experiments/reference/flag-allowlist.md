# Flag allowlist

[Back to the overview](../README.md)

Only these flags are sent. Adding a flag is a change to this page, agreed with the business owner of
the experiment. **All flags below are to confirm with Motion**: names are as seen in the site's code,
and the LaunchDarkly flag keys may differ.

| Priority | Flag (as seen in site code) | What it controls | Experiment or release toggle? | Owner |
|---|---|---|---|---|
| **1** | `PAGE_BRAND_REFRESH` | Site refresh (soft launch 12/14, percentage rollout) | To confirm | To confirm |
| 2 | `REDESIGNED_PDP` | Product page redesign | To confirm (A/B test?) | To confirm |
| 3 | `HEADER_REDESIGN` | Header redesign (released 10/29) | To confirm | To confirm |
| 4 | `OPTIMIZE_SAYT` | Search as you type | To confirm | To confirm |
| 5 | `BUY_IT_AGAIN_ENHANCEMENTS` | Buy It Again | To confirm | To confirm |
| 6 | `REGISTRATION_WORKFLOW_UPDATE` | Registration flow | To confirm | To confirm |

**Why the site refresh flag comes first:** if it is captured before the 12/14 soft launch, the site
refresh can be measured as refreshed vs not refreshed visitors in the same weeks, instead of a
before-and-after comparison across the holidays.

**Release toggles** (flags that turn a finished feature on for everyone) don't need to be sent once
they're fully on. Only flags that split visitors are worth capturing.
