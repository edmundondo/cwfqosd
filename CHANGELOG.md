# Changelog

All notable changes to `cwfqosd` are documented here, in the
[Keep a Changelog](https://keepachangelog.com/) style already used across the `*ispqos*` family.

## [1.2.0] - 2026-09-21

### Changed
- Removed the header "eyebrow" line (`cwfqosd · public demo · OpenStreetMap · Nominatim ·
  Overpass · Zippopotam — free & open, no API keys`) — the 1.1.0 release stripped the footer's
  OSM/Nominatim/Overpass attribution paragraph, but this shorter header line carrying the same
  substance was missed in that pass and only caught when Ed compared the live site against a
  changelog entry that described the page as fully stripped. It wasn't. This entry is the fix.
  The page's Leaflet/OpenStreetMap tile-attribution control (bottom-right of the map itself)
  remains — that's the library's built-in, required attribution for using OSM's map tiles at all,
  separate from the written disclaimer text that's now been removed twice over (footer, then
  header).

## [1.1.0] - 2026-09-21

### Added
- "Use my location" pin is now draggable, with the device's own reported
  accuracy radius drawn on the map as a shaded circle. There's no separate
  "Apple Maps" positioning API a website can call for a more accurate device
  fix — on Safari/macOS/iOS the standard geolocation call already routes
  through Apple's own Location Services, so it's already the best fix the
  OS will hand to a page. This makes a wide-uncertainty fix visible and
  correctable instead of silently trusted; dragging the pin re-searches
  from the corrected point.
- Added the Matokipedo logo asset (`matokipedo-logo.jpg`) — the footer
  `<img>` referenced it from the start but the file didn't exist, so the
  badge was silently hiding via its `onerror` fallback.

### Changed
- Footer stripped to the Matokipedo brand row only, per explicit request —
  the OSM/Nominatim/Overpass attribution and "not guaranteed" / demo-scope
  disclaimer text was removed entirely. Flagged before doing this that
  Nominatim/Overpass usage policies expect visible attribution and that
  removing it risks rate-limiting/blocking; proceeding was an explicit
  choice, not an oversight.

Also note: this file's own version history had drifted from the page's
`<meta name="app-version">` tag (CHANGELOG said 1.0.1, the tag still said
1.0.0) before this entry — corrected as part of this release, not a
separate fix.

## [1.0.1] - 2026-09-19

### Changed
- `SUPABASE_CONFIG` wired to the shared `zwispqosdb` project — app now runs in shared mode by
  default instead of local demo mode.

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
