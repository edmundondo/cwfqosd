# cwfqosd — USA Free WiFi Tracker (public demo)

The public, shared-access half of a demo/privileged-backend pair — same model as this project's
ISP-quality trackers (`zwispqosd`/`zwispqosp` and siblings): **`cwfqosd` = demo with shared public
access, `cwfqosp` = backend connected to a privileged, analytics/export tier.**

Finds free public WiFi anywhere in the USA by GPS, street address, city, or ZIP, then lets anyone
rate a spot (1–5 stars) or report its live status (Live / Partial / Down / Unconfirmed) —
crowdsourced, same spirit as the QoS reports on the ISP trackers.

## How it's different from the ISP-tracker family, on purpose

Every `<country>d` ISP tracker ships a hardcoded `DATA` array of licensed providers — a small,
fixed list per country, researched once and updated by hand. Free WiFi has no such fixed list: what
exists near a given address changes constantly and there's no equivalent of "the country's licensed
ISPs." So instead of a `DATA` array, this app queries **live, community-maintained
[OpenStreetMap](https://www.openstreetmap.org) data** (via the free
[Overpass API](https://overpass-api.de)) every time someone searches, geocoding the address with
[Nominatim](https://nominatim.org) (city/street) and [Zippopotam](https://www.zippopotam.us) (ZIP
codes — Nominatim's own US postal-code coverage is inconsistent). This is why `lite.html` can't ship
a static offline table the way the ISP trackers' `lite.html` does — see that file for the full
explanation.

The crowdsourced layer — ratings, status reports, local-demo-mode-vs-shared-backend toggle, the
cross-browser compatibility banner, the CSS grid `0fr→1fr` expand pattern for the rating panel — all
follow the established family convention exactly.

## Running it

Open `index.html` in a browser — no build step, no server required. To publish via GitHub Pages,
push these files to a repo and enable Pages on `main`.

## Local demo mode vs. shared mode

- **Local demo mode.** Every rating and status report is saved only in your own browser via
  `localStorage`. Nothing leaves your device. (This is what happens if `SUPABASE_CONFIG` is ever
  reset to placeholder values.)
- **Shared mode — currently active.** `SUPABASE_CONFIG` is wired to the shared `zwispqosdb`
  Supabase project (same one the `*ispqos*` ISP-tracker family uses). Every visitor's ratings and
  status reports are pooled and visible to everyone, and `cwfqosp`'s admin app can read, moderate,
  and export them. See `cwfqosp/README.md` for the setup record and `cwfqosp/schema.sql` for the
  migration that was actually applied.

## No export/download tools here, by design

Same rule as every `*d` demo site in this family: exporting the underlying data is
privileged/analytics functionality, reserved for `cwfqosp`. Don't add export buttons here.

## Files

- `index.html` — the full interactive app.
- `lite.html` — no-JavaScript fallback (search isn't possible without JS here — see above — but it
  explains why and offers an email-based rating/report path).
- `README.md` — this file.
- `matokipedo-logo.jpg` — **not included in this handoff.** The `<img>` tag in both HTML files
  already references it by filename (with a graceful `onerror` fallback that just hides it if
  missing); copy the real logo in from any sibling repo to match the family's brand footer.

## Related

See `cwfqosp` (the privileged backend for this pair) and the `bpqos`/`ispqos` skills for the
reusable architecture this was built from.
