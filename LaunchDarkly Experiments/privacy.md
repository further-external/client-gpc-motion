# Privacy

[Back to the overview](README.md)

## Never sent

- The visitor's LaunchDarkly **context** (the object LaunchDarkly uses to target, which can include a
  user or account key and attributes).
- Any flag outside the [allowlist](reference/flag-allowlist.md).
- The flag's evaluation reason or targeting rules.

## The LaunchDarkly visitor ID

The site sets a persistent visitor ID cookie that LaunchDarkly uses to keep a visitor in the same
variation. Sending it to Adobe lets us check how often visitors switch variations (a cookie reset or
consent change creates a new ID). Because it's a persistent identifier:

- send it **only when the visitor has accepted analytics cookies**;
- label it in Adobe's data governance settings as an identifier;
- never print or paste real values into documentation or tickets. Use `<VID>`.

## Consent

With analytics consent declined, nothing in this specification reaches Adobe. The data layer is the
same either way; only what the tag manager sends changes.
