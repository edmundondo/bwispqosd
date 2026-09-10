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

- **Language chips: English + Setswana + Kalanga + Shona + Ndebele, with four more
  present but blank.** English is Botswana's sole official language; Setswana is the
  national language; Kalanga (TjiKalanga), Kgalagadi, Shona, Mbukushu, Ndebele, Tshwa
  and !Xóõ are all recognised languages (source: "Languages of Botswana", Wikipedia,
  checked 2026-09-10 — not a constitutional list the way Zimbabwe's 16 languages are).
  Setswana, Kalanga, Shona and Ndebele ship with real best-effort-draft translations,
  because they're literally the same standard languages already drafted for the
  Zimbabwe site (Setswana/Tswana, TjiKalanga/Kalanga, ChiShona/Shona, IsiNdebele/
  Ndebele) — reused rather than re-fabricated, still unreviewed, still flagged with
  the same "🚧 need translation" badge wherever a string hasn't been checked.
  Kgalagadi, Mbukushu, Tshwa and !Xóõ have no cross-border shortcut and no verified
  source yet, so their chips exist and fall back cleanly to English rather than being
  guessed — the same "intentionally blank" pattern Zimbabwe uses for Chibarwe,
  Khoisan/Tjwao, Nambya and Ndau. Community translation via the suggest/endorse flow
  works for all nine languages today.
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
