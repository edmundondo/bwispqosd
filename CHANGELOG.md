# Changelog

All notable changes to the Botswana ISP Tracker public demo are recorded here.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versioning
follows [Semantic Versioning](https://semver.org/) (MAJOR.MINOR.PATCH).

The version number shown here matches the `<meta name="app-version">` tag in
`index.html` and the `v{version}` badge in the page's footer.

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
- English-only UI (community-translation code stays functional for English wording
  fixes; other languages are a future addition, not fabricated here).
- `ISP_ASN` and `PHONE_ISP_PREFIXES` both start empty — no verified data compiled
  for this build; both already degrade gracefully when empty.
- Cloudflare Radar national-benchmark feature not invoked (Zimbabwe-only edge
  function; a second, unverified proxy wasn't built sight-unseen for this release).
