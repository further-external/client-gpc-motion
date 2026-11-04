# Open questions

[Back to the overview](README.md)

| # | Question | Why it matters | Owner | Answer |
|---|---|---|---|---|
| 1 | Is the visitor ID cookie the key LaunchDarkly targets on, for signed-out and signed-in visitors? | Decides whether one visitor can be in two variations | Motion dev team | |
| 2 | Which flags are experiments and which are release toggles? | Only experiments go on the [allowlist](reference/flag-allowlist.md) | Motion digital team | |
| 3 | What are the exact LaunchDarkly flag keys for the allowlisted flags? | The spec sends keys, not code constants | Motion dev team | |
| 4 | Is the site refresh soft launch on 12/14 a percentage rollout on `PAGE_BRAND_REFRESH`? | If yes, this is the priority and must be live before 12/14 | Motion digital team | |
| 5 | Is there developer capacity for Page Loaded `experiments` before 12/14, and for Experiment Exposed after? | Sets the timeline | Motion dev team | |
| 6 | Is LaunchDarkly's own experimentation or data export in use? | It's the fairest reference for what LaunchDarkly counted | Motion digital team | |
| 7 | Where should results be analysed: Adobe Workspace, or exported data with significance testing? | Adobe has no built-in significance test for non-Target tests | Motion analytics | |
