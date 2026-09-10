# Changelog

All notable changes to the Botswana ISP Tracker public demo are recorded here.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versioning
follows [Semantic Versioning](https://semver.org/) (MAJOR.MINOR.PATCH).

The version number shown here matches the `<meta name="app-version">` tag in
`index.html` and the `v{version}` badge in the page's footer.

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
