# Gmail dark mode CSS

A [Stylus](https://add0n.com/stylus.html) UserCSS that makes Gmail genuinely dark — the parts
Google's own dark theme leaves white or unreadable: compose/reply panes, recipient chips,
autocomplete dropdowns, formatting toolbars, attachment cards, calendar-invite panels, and a
long tail of inline colours that arrive inside HTML mail.

Lives in its own public repo purely so Stylus can fetch it over `https://` and self-update.

## Install

Open this URL in a browser with Stylus installed — Stylus intercepts it and shows an installer page:

```
https://raw.githubusercontent.com/victorrentea/gmail-dark-css/master/gmail.user.css
```

Then click **Install style**.

## Updating

Stylus re-checks the URL on its own schedule (default: every 24h), or immediately via
**Check for update** in the Stylus manage page.

Stylus only accepts an update when `@version` is **higher** than the installed one — a changed
body with an unchanged version is rejected as `SAME_VERSION`. So every edit must bump `@version`
in the `==UserStyle==` header.

## Structure

`@-moz-document domain("mail.google.com")` wrapping three blocks:

- `@media (prefers-color-scheme: dark)` — the bulk of it, as numbered sections (`/* === N. TITLE === */`)
- `@media (prefers-color-scheme: light)` — a few light-mode contrast fixes
- a global block — keyboard-shortcut hints, right-pane hiding

Rules lean on `!important` throughout, because Gmail ships its own inline styles and CSS
custom properties that would otherwise win.

## Why so many sections

Gmail's class names are obfuscated and change; each section records one specific visual bug and
the selector that fixed it, with a comment explaining what Gmail was doing wrong. That history is
the point — it's what makes the file maintainable when a selector eventually breaks.
