# Changelog

All notable changes to `cwfqosd` are documented here, in the
[Keep a Changelog](https://keepachangelog.com/) style already used across the `*ispqos*` family.

## [1.0.0] - 2026-09-19

### Added
- Initial build: GPS / street address / city / ZIP search for free public WiFi anywhere in the USA,
  live-queried from OpenStreetMap via the Overpass API, geocoded via Nominatim (address/city) and
  Zippopotam (ZIP — see README for why Nominatim alone isn't reliable for US ZIPs).
- Per-spot crowdsourced star rating (1–5) and live-status report (Live / Partial / Down /
  Unconfirmed), CSS grid `0fr→1fr` expand panel per spot (never a fixed `max-height`, per the
  family's established lesson on that pattern).
- Local-demo-mode / Supabase-shared-mode backend toggle (`SUPABASE_CONFIG`), same convention as the
  ISP-tracker family.
- Cross-browser compatibility banner (feature-detects `fetch`/`Promise`/`localStorage`/CSS grid).
- `lite.html` no-JavaScript fallback with an honest explanation of why this app can't ship a static
  offline spot list the way the ISP trackers can, plus an email-based rating/report path.
- Brand footer referencing `matokipedo-logo.jpg` (logo file itself not included in this handoff —
  see README).
- `SITE_ID = "us"`, explicitly grep-verified against this repo before calling it done (per the
  family's hard-won lesson on `SITE_ID` mislabeling bugs).

### Scope cuts (documented explicitly, not silently omitted)
- No export/download tools on this demo tier — by design, reserved for `cwfqosp`.
- No language chips / i18n yet (the ISP trackers ship a country's real official/recognised
  languages from day one — this hasn't been researched or built for this vertical yet).
- No `AREAS`/city-picker equivalent — unnecessary here since search is live-geocoded to any
  address, not limited to a fixed tracked-city list.
- No SMS reporting number configured for this project (the ISP trackers have one per country).
