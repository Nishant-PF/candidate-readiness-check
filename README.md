# Candidate Readiness Check

A static, single-file site — `index.html` — no build step, no server, no login. Candidates open it on any device and take a ~15-minute self-assessment (communication, interests, aptitude — weighted equally). Results stay on that device until the candidate taps **Email results** or **Copy summary**; there is no shared database, so nothing needs hosting beyond static files.

## Deploy to GitHub Pages

1. Push this folder (just `index.html`, plus this README) to your repo:

   ```bash
   cd your-repo
   cp /path/to/index.html .
   git add index.html
   git commit -m "Add candidate readiness check"
   git push
   ```

2. In the repo on GitHub: **Settings → Pages → Build and deployment → Source → Deploy from a branch**, pick `main` (or whichever branch you pushed to) and `/ (root)`, then **Save**.
3. GitHub gives you a URL a minute or two later, typically `https://<your-username>.github.io/<repo-name>/`. That's the link to send candidates.

If you'd rather serve it from the repo root of a `username.github.io` repo, it becomes `https://<your-username>.github.io/` directly — same steps, just push to that special repo name.

## Before you share the link

Open `index.html` and change this one line near the top of the `<script>` block:

```js
var EMAIL_TO = "nishant@periferry.com";
```

to whichever inbox should receive results.

## How results reach you

There's no backend, so nothing is collected centrally on its own:

- **Email results** — opens the candidate's (or facilitator's) mail app with a pre-filled draft to `EMAIL_TO`. Someone still has to hit send.
- **Copy summary** — copies the same plain-text summary to the clipboard, for pasting into WhatsApp, a ticket, anything.
- **Saved on this device** — adds the result to a private, browser-local list (`localStorage`), visible under the **Saved here** tab on that same browser only. Useful when one facilitator runs several candidates back-to-back on one laptop — **Export CSV** there dumps whatever's in that list.

None of the three sync across devices. If you outgrow that (want every candidate's result to land in one shared place automatically, no one hitting send), the next step up is a small form backend — a Google Sheet behind a Apps Script Web App, or a service like Airtable/Formspree — swapped in for the `mailto:` link. Ask if you want that built.

## Editing the item bank

Everything — the eight communication items, eight interest items, eight aptitude items, the seven placement tracks, and the scoring weights — lives in plain arrays near the top of the `<script>` block (`COMM`, `INTEREST`, `APT`, `TRACKS`). Each answer option carries its own score; nothing is hardcoded elsewhere.
