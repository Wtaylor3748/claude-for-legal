---
name: reg-watch
description: Check D.C. and federal housing rulemaking and legislation since the last run — D.C. Register notices (DHCD, DOB, OTA, RHC, DCHA), Council bills and hearing notices on LIMS, and HUD items in the Federal Register — filtered to what affects D.C. tenants, subsidized housing, or landlord licensing, with comment and hearing deadlines logged. Use when the user says "what's new in housing policy", "any new rules", "check the Register", "anything at the Council on housing", or pastes a notice to classify.
argument-hint: "[--since YYYY-MM-DD] [--paste]"
---

# /reg-watch

Adapted from regulatory-legal's `reg-feed-watcher` and `policy-diff`.

## Watchlist (edit in the profile copy)

| Source | How to pull | Tag |
|---|---|---|
| Federal Register — HUD | `https://www.federalregister.gov/api/v1/documents.json?conditions[agencies][]=housing-and-urban-development-department&conditions[publication_date][gte]=<since>` (free, no key) | `[Federal Register]` |
| D.C. Register | dcregs.dc.gov — search notices of proposed / final rulemaking by agency (DHCD, DOB, OTA, Rental Housing Commission, DCHA, DLCP) | `[D.C. Register]` |
| D.C. Council | lims.dccouncil.gov — bills and resolutions referred to the Committee on Housing; hearing notices | `[Council LIMS]` |
| CourtListener | new DCCA opinions mentioning "Rental Housing Act", "warranty of habitability", "28-3905" | `[CourtListener]` |

If a site blocks automated access, say so and ask the user to paste the notice (Tier 3: manual entry). Never fill the gap from model knowledge.

## Materiality filter

- **Act now:** final rule or enacted law changing eviction procedure, notice requirements, rent control, licensing/registration, habitability standards, or tenant remedies; anything that touches a pending matter's claim or defense.
- **Review:** proposed rules (NPRMs) and bills in the above areas; Council hearing notices; DCCA opinions on those statutes.
- **FYI:** guidance, press releases, commentary — tagged `[secondary — trace to primary]`.

## Steps

1. Pull each source since `--since` (default: last run date stored in `reg-watch-state.yaml`).
2. Classify by the filter. For each review/act item: what it does, who it affects, effective date or comment/hearing deadline, citation, link.
3. **Litigation cross-check:** for each item, does it change anything in a pending matter (a template element, a deadline rule, a defense)? If yes, flag `🔴 affects <slug>` and say what to update (e.g., `references/coa-templates/defective-notice-and-licensing.md`).
4. Log every comment deadline and hearing date to `comment-tracker.yaml` (used by `public-comment` and `council-testimony`) and offer to add them to `deadlines` under matter `advocacy`.
5. Save the digest to `out/reg-watch-<date>.md` and update the last-run date.

## Output

```
🏛️ Housing policy watch — [since] → [today]
🔴 Act now / affects a case    [item] — [what changes] — [effective] — [source tag + link]
🟡 Review (comment/hearing open)  [item] — deadline [date] — [source]
⚪ FYI                          [item]
Coverage: [sources reached] · [sources blocked — paste needed]
```
