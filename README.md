# bwispqosd

Public demo for the Botswana ISP Tracker — crowdsourced quality-of-service ratings,
live status reports and speed tests for Botswana's internet providers, sourced from
BOCRA's published sector data and operators' own results.

Sibling of [zwispqosd](https://github.com/edmundondo/zwispqosd) (Zimbabwe) and
[saispqosd](https://github.com/edmundondo/saispqosd) (South Africa) — same codebase
pattern, same shared Supabase backend (multi-tenant via a `site` column), different
country data. See `zwispqosd`'s README/SETUP docs for the full technical background
on how the backend, live feeds (IODA) and speed test work — nothing about that
plumbing is Botswana-specific.

Formatted report exports (PDF/CSV/EPUB) live on the privileged
[bwispqosp](https://github.com/edmundondo/bwispqosp) backend, not here — see its
README for details.

## What's different about this site (v1 scope)

- **English only.** The Zimbabwe site's multi-language community-translation feature
  exists in the code (so a language can be added later without a rebuild) but no
  language besides English is populated yet — this is a deliberate v1 scope cut, not
  a bug.
- **No backbone (RIPEstat/ASN) badges.** `ISP_ASN` is intentionally empty — no
  verified ASN-to-operator mapping has been compiled for Botswana yet. The badge
  simply doesn't render for any ISP without an entry, the same graceful fallback the
  Zimbabwe site already relies on for its own untracked ISPs.
- **No Cloudflare Radar national benchmark.** That feature calls a Supabase Edge
  Function that's hardcoded server-side to Zimbabwe's numbers only (and is a
  separately-tracked, not-fully-verified feature even there) — rather than build a
  second country-specific proxy sight-unseen, it's simply never invoked on this site.
- **No phone-prefix ISP detection.** `PHONE_ISP_PREFIXES` starts empty — no verified
  BOCRA numbering-plan-to-carrier mapping was available for this build.
- Provider list is intentionally small (5 tracked providers) and seed
  ratings/status/speed data is illustrative, not a real crowdsourced history.

See `CHANGELOG.md` for version history.
