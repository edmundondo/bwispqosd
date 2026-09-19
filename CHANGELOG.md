# Changelog

All notable changes to the Botswana ISP Tracker public demo are recorded here.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versioning
follows [Semantic Versioning](https://semver.org/) (MAJOR.MINOR.PATCH).

The version number shown here matches the `<meta name="app-version">` tag in
`index.html` and the `v{version}` badge in the page's footer.

## [1.2.1] — 2026-09-18

### Fixed
- **Critical: every report submitted through this site was being silently recorded under
  Zimbabwe's data (`site: "zw"`), not Botswana's own (`site: "bw"`)** — `SITE_ID` was left over
  from the file this repo was originally templated from and was never updated. Every QoS rating,
  live-status report, speed test, conversion, translation suggestion and referral click submitted
  here since this site launched (2026-09-10) went into the shared database tagged as Zimbabwean
  data, invisible to Botswana's own admin panel. Checked the live database directly: nothing real
  was actually miscategorized by this (the only `site: "zw"` rows found are genuinely
  Zimbabwe-specific — Harare/Chegutu, Zimbabwean ISPs — so no real Botswana submissions have been
  lost or need re-attribution), but the bug was live in production and would have silently
  swallowed the first real tester submission. Fixed: `SITE_ID` now correctly reads `"bw"`.

## [1.2.0] — 2026-09-17

### Fixed
- **The expanded provider row (star rating, live-status report, speed test) used a fixed
  `max-height:1200px` cap to animate opening/closing, with `overflow:hidden` on the box the whole
  time — any provider whose expanded content ran taller than that had everything past ~1200px of
  content silently clipped away and unreachable by any amount of scrolling, including the comment
  box and "Submit rating" button on the QoS form. Same bug, same fix as `zwispqosd` v1.3.1:
  replaced the fixed-pixel animation with a CSS grid `0fr → 1fr` expand (no JS, no fixed cap) that
  always sizes to the row's actual content on any device.

### Added
- **Real area/suburb picker on every rating/report form** (QoS rating, live-status report, speed
  test, switch/signup) — ported from `zwispqosd` v1.3.0. A new `<select>` next to the existing
  city picker, populated from a researched, sourced list of real Botswana suburbs/areas per
  tracked city (`AREAS` in `index.html`). Picking a city populates that city's real areas; "Use my
  location" still only ever resolves to a tracked city (never an area) and clears the area choice
  when it fires. Coverage is honestly uneven: Gaborone and the other larger towns have dozens of
  sourced areas; smaller towns only have a handful because that's genuinely all that could be
  traced to a real source (Wikipedia, council/planning documents, established news outlets) —
  "Whole city / not sure" is always available and the honest default. Sourcing notes for each city
  are documented inline in `index.html` next to the `AREAS` object.

### Notes
- Same additive, nullable `area` column already in place on the shared Supabase project (added
  for `zwispqosd` v1.3.0) — no new migration needed for this repo.
- Companion to `bwispqosp` v0.4.0's provider-analytics drill-down, which is what surfaces this
  field (City → Area → ISP → individual reports).

## [1.1.0] — 2026-09-10

### Added
- **Real official/recognised language chips**, replacing the v1.0.0 English-only
  scope cut: English, Setswana, Kalanga, Kgalagadi, Shona, Mbukushu, Ndebele, Tshwa
  and !Xóõ (source: "Languages of Botswana", Wikipedia, checked 2026-09-10).
  Setswana, Kalanga, Shona and Ndebele reuse zwispqosd's existing best-effort-draft
  translations for the same standard languages (Setswana/Tswana, TjiKalanga/Kalanga,
  ChiShona/Shona, IsiNdebele/Ndebele are shared across the border, not distinct
  languages) — legitimate reuse, not fabrication, still marked unreviewed. Kgalagadi,
  Mbukushu, Tshwa and !Xóõ have no cross-border shortcut and no verified source yet,
  so they ship as chips with empty translation content, falling back to English with
  the standard "🚧 need translation" badge — the same "intentionally blank rather
  than guessed" treatment Zimbabwe uses for its own untranslated languages. The
  suggest/endorse community-translation flow now covers all nine languages.
- These blocks were sitting dormant in this repo's own `index.html` since the
  v1.0.0 build (inherited unused from the zwispqosd template) — this release wires
  them up rather than fabricating anything new for the shared languages.

### Fixed
- Corrected the README/CHANGELOG "English only" v1 scope note, which undersold what
  "replicate the same pattern as Zimbabwe" was always meant to include — Zimbabwe's
  own site treats its official/constitutional languages as core, not optional.

## [1.0.0] — 2026-09-10

### Added
- First build, replicating the zwispqosd (Zimbabwe) demo/backend split pattern for
  Botswana from day one — no export options here (see `bwispqosp` for those),
  brand footer/logo matching zwispqosd, versioning in place.
- Provider list (`DATA`): Orange Botswana, Mascom Wireless, BTC Mobile (BeMobile),
  Starlink, and a grouped "Independent ISPs" placeholder — sourced from BOCRA's
  2024 Annual Report (period to March 2024) and operators' own results, with
  published-vs-derived figures clearly distinguished in each entry's `note`/`source`.
- 11 real Botswana cities for GPS/nearest-city matching (Gaborone, Francistown,
  Maun, Kasane, Palapye, Serowe, Molepolole, Selebi-Phikwe, Mahalapye, Lobatse,
  Ghanzi) and small, clearly-illustrative seed QoS/status/speed data across them.
- Botswana-correct phone number handling (`+267`, 8-digit numbers, no leading
  trunk zero) in `normalizePhone`/`isValidPhone`.

### Notes — deliberate v1 scope cuts (see README.md for the full list)
- English-only UI at launch — superseded in v1.1.0, see above.
- `ISP_ASN` and `PHONE_ISP_PREFIXES` both start empty — no verified data compiled
  for this build; both already degrade gracefully when empty.
- Cloudflare Radar national-benchmark feature not invoked (Zimbabwe-only edge
  function; a second, unverified proxy wasn't built sight-unseen for this release).
