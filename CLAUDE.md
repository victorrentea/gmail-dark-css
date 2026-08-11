# gmail-dark-css repo instructions

## Gmail Stylus CSS

I will ask you to modify the Gmail CSS / add CSS snippets **repeatedly over time** — treat it as a recurring task. When I do (e.g. "pune acest css în gmail user css", "modifică gmail dark mode"):
1. Edit the file `gmail.user.css` (a Stylus UserCSS for `mail.google.com`; structured as `@-moz-document domain("mail.google.com")` with `@media (prefers-color-scheme: dark)` / `light` blocks).
2. If it's a dark-mode fix, add the snippet **inside the `@media (prefers-color-scheme: dark)` block** as a new **numbered section** (`/* === N. TITLE === */`), matching the file's convention (Romanian comments, `!important` on rules).
3. Bump `@version` in the `==UserStyle==` header and extend `@description` with a short summary of the new section.
   **This is mandatory, not cosmetic**: Stylus fetches over `https://` and its updater rejects a
   changed body under an unchanged version as `SAME_VERSION` (only `localhost` URLs are exempt).
   Forget the bump and the update silently does nothing.
4. Verify in Chrome via the Claude browser extension that it looks as expected (open/refresh Gmail; open a compose window if the snippet targets the formatting bar; screenshot/zoom).
   Stylus does **not** live-reload — to see a change, either inject the rules with `javascript_tool`
   as a proxy check, or push and hit **Check for update** in Stylus.
5. Always `git add` + `commit` + `push` afterwards so this CSS stays versioned:
   ```
   git add gmail.user.css && git commit -m "..." && git push
   ```
   Pushing is what publishes it — Stylus pulls from
   `https://raw.githubusercontent.com/victorrentea/gmail-dark-css/master/gmail.user.css`
   (≈5 min CDN cache) on its own 24h schedule, or immediately via **Check for update**.

## Repo context

Public on purpose — Stylus cannot send credentials, so a private repo's raw URL 404s. Keep it free
of anything sensitive; it is only Gmail class selectors and colour values.

Versions 1.0.0 → 1.15.0 were developed in the private `victorrentea/ai` repo; that history stays there.
