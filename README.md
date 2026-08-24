# flightmapapp.com

The public pages for **FlightMap**, a personal flight logbook for Android and iOS.

This repository is **deliberately public and deliberately separate** from the app
repository, which is private. Google Play and the Apple App Store both fetch the
privacy policy from outside the app before they will accept a listing, so these
pages have to be publicly reachable by a crawler that has no account anywhere.

Nothing secret belongs in here. There is no build step, no dependency, and no
token: it is static HTML that Cloudflare Pages serves as-is.

## What is here

| Path | |
|---|---|
| `/` | Landing page — links to the documents and to support |
| `/privacy`, `/privacy/fr`, `/privacy/ar` | Privacy policy, three languages |
| `/terms`, `/terms/fr`, `/terms/ar` | Terms of service, three languages |
| `assets/` | Stylesheet and the brand mark |
| `_headers` | Cloudflare Pages security headers |

**English is the source of truth.** The French and Arabic pages say so, and all
three are edited together — a change to the English text that does not reach the
other two is a bug, not a backlog item. This is not a nicety: GDPR Art. 12
requires the information to be intelligible to its audience, and the app ships in
all three languages.

`/privacy#deletion` is the **account-deletion URL** given to Google Play. Keep
that anchor stable; the store form points at it.

## Three things that will look like mistakes and are not

- **`WRITE_CALENDAR` is disclosed even though the app only reads.** The
  `device_calendar` library requires both permissions to be declared to grant
  read access at all. The policy explains this rather than hiding it. Do not
  "correct" the policy to drop it.
- **No webfont is loaded.** The policy discloses that the *app* fetches Inter
  from Google at runtime; serving these pages from a font CDN would hand Google
  the IP address of everyone who came here to read about that. The stylesheet
  uses a system stack on purpose.
- **The pages do not auto-redirect by browser language.** The switcher is
  visible on every page and the `hreflang` tags let a crawler find each version.
  An automatic redirect hides languages from crawlers and traps readers who want
  a different one.

## Editing

Open the file and edit it. Then check, in order:

1. The same change landed in all three languages of that document.
2. The French text keeps the house style used in the app: typographic
   apostrophes (`’`, not `'`) and a non-breaking space before `: ; ? !`.
3. The Arabic pages still carry `dir="rtl"` on `<html>`, and any Latin-script
   run inside them (an email address, a constant) still carries `dir="ltr"`.
4. The `Last updated` date at the top of every page you touched.

## Deploying

Cloudflare Pages, connected to this repository's default branch. Every push to
it deploys. Build command: none. Build output directory: `/`.

## Licence

The prose is © Zakaria Ybeggazene. The FlightMap mark in `assets/` is not free
to reuse.
