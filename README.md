# cloud-itonami-lei-2549009bksvtm7ueyt38

> **Independent third-party archive/analysis. Not affiliated with, endorsed by, or sponsored by Bright Horizons Family Solutions Inc..**

This repository archives the publicly published Terms of Use of **Bright Horizons Family Solutions Inc.**, with
source-url and retrieval-date provenance, per
[ADR-2607110300](https://github.com/com-junkawasaki/root/blob/main/90-docs/adr/2607110300-cloud-itonami-lei-corporate-tos-catalog.md)
(`cloud-itonami-lei-corporate-tos-catalog`, `com-junkawasaki/root`). It is a read-only
reference/archive repository — it does not act, propose, or execute anything on the
company's behalf, and is not a governed Advisor/Governor actor.

## Company identity

- **Legal name**: Bright Horizons Family Solutions Inc.
- **LEI (ISO 17442)**: [2549009BKSVTM7UEYT38](https://search.gleif.org/#/record/2549009BKSVTM7UEYT38) (GLEIF-verified)
- **Jurisdiction**: US-MA
- **Website**: https://www.brighthorizons.com
- **Ticker**: BFAM (NYSE)

## Contents

- `80-data/public/tos.journal.edn` — EDN quad-log of archived Terms of Use documents.
- `NOTICE` — copyright/attribution statement for the archived third-party text.
- `blueprint.edn` — machine-readable company identity record. Its `:company/jurisdiction`
  `US-MA` is where the company *sits* (GLEIF headquarters region, EDGAR business state);
  the *legal* jurisdiction is `US-DE` (GLEIF, and the 10-K cover page) — see the catalog.
- `facts/catalog.edn` — 96 verified public-register citations across 18 URLs (GLEIF entity
  record, ISIN mapping, direct-children page, both parent reporting exceptions, the
  RA000602 / XTIQ / managing-LOU registry entries, and the *separate* LEI record of the
  subsidiary named on the Terms of Use; SEC EDGAR submissions API, company-tickers file,
  XBRL companyfacts, and the FY2025 Form 10-K inline-XBRL cover page for CIK 0001437578;
  the Delaware Division of Corporations portal; the issuer's home page schema.org block
  and the exact Terms-of-Use page archived here). Every row carries `:cite/row-kind`
  (`:identity` / `:attribute` / `:definition`) so a reader does not mistake corroboration
  for identification. The header records what is deliberately *not* cited and why
  (Delaware's ICIS and Massachusetts' register are form-gated; GLEIF maps no ISIN;
  EDGAR's submissions API leaves `stateOfIncorporation` blank), and two findings a
  reader should know: the Terms of Use name **Bright Horizons Family Solutions LLC**
  (LEI `254900BHOU40CFNXWQ75`, a 1998 Delaware LLC), not the listed Inc., and GLEIF's
  LLC record still reports its parent as `NO_LEI` although the Inc. has held this LEI
  since 2025-12-10 — the parent/subsidiary edge exists only in the 10-K.
- `tools/verify_citations.cljs` — live gate over the catalog: every `:cite/url` must
  answer 2xx and carry `:cite/expect-substring`. Exit 0 = all rows verified,
  1 = at least one DRIFT (named), 2 = could not answer (parse / network / floor /
  sec.gov rows not asked). SEC EDGAR requires a User-Agent naming the requester, so
  the gate takes *your* contact address and ships none; without it the 32 sec.gov rows
  are reported `UNCHECKED` and the run exits 2, not 0.

```bash
EDGAR_CONTACT=you@example.org nbb tools/verify_citations.cljs facts/catalog.edn --min 20
# CHECKED 96 OK 96 FAIL 0 UNCHECKED 0 → PASS, exit 0        (measured 2026-08-22)
nbb tools/verify_citations.cljs facts/catalog.edn --min 20
# CHECKED 64 OK 64 ... UNCHECKED 32 → UNANSWERED, exit 2     (sec.gov not asked)
```

## Design rationale

See ADR-2607110300 in `com-junkawasaki/root` (`90-docs/adr/`).
