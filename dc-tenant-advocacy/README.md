# D.C. Tenant Advocacy Plugin

For a self-represented tenant litigating in the District of Columbia who is also doing the civic work around it: commenting on rules, testifying before the Council, and speaking publicly.

It is assembled from three plugins in this marketplace and cut down to that setting:

| From | Taken | Changed |
|---|---|---|
| `litigation-legal` | `claim-chart` (civil mode), `chronology`, `brief-section-drafter`, matter intake/update/briefing, `docket-watcher`, the shared citation guardrails | Pro se vocabulary, D.C. courts, D.C. cause-of-action templates, hand-offs to D.C. formatting skills |
| `regulatory-legal` | `reg-feed-watcher`, `policy-diff`, `comments` | Watchlist set to HUD, D.C. Register, Council LIMS; comment drafting added |
| `legal-clinic` | `deadlines` | Wired to a D.C. deadline rule table |
| New | `council-testimony`, `public-messaging`, `docket-to-deadlines` | — |

**Every output is a research draft for a self-represented party.** Every citation carries a provenance tag (`[CourtListener]` only when retrieved and read in the session; otherwise `[model knowledge — verify]`). Filing, serving, submitting, and publishing are always left to the user.

## Install

```
/plugin marketplace add wtaylor3748/claude-for-legal
/plugin install dc-tenant-advocacy@claude-for-legal
/dc-tenant-advocacy:matter-ledger --init
```

The first skill run copies `CLAUDE.md` to `~/.claude/plugins/config/claude-for-legal/dc-tenant-advocacy/CLAUDE.md`. Edit that copy. Case data (ledger, histories, chronologies, charts, deadlines) is written only under that config directory — never into this repository.

## Skills

| Command | Does |
|---|---|
| `/dc-tenant-advocacy:matter-ledger` | Case ledger: `--init`, `--add`, `--update`, `--brief`, `--status` |
| `/dc-tenant-advocacy:chronology` | Record-cited timeline; `--format=sof` statement of facts; `--format=retaliation-windows` |
| `/dc-tenant-advocacy:claim-chart` | Element-by-element proof chart and gap list; `--review` audits the landlord's motion |
| `/dc-tenant-advocacy:brief-section-drafter` | One section of a motion, opposition, or DCCA brief |
| `/dc-tenant-advocacy:deadlines` | Deadline ledger with 14/7/3/1-day warnings |
| `/dc-tenant-advocacy:docket-to-deadlines` | New docket entries → proposed deadlines and posture changes |
| `/dc-tenant-advocacy:reg-watch` | HUD / D.C. Register / Council / DCCA watch, filtered to tenant issues |
| `/dc-tenant-advocacy:public-comment` | Comment-period tracker and comment drafting |
| `/dc-tenant-advocacy:council-testimony` | Hearing tracker; timed oral and written testimony |
| `/dc-tenant-advocacy:public-messaging` | Op-eds, press, social, flyers, campaign copy with a litigation-safety check |

Agent: `docket-watcher` — scheduled, read-only version of `docket-to-deadlines`.

## References

- `references/dc-deadline-rules.yaml` — D.C. Superior Court, LTB, DCCA, statutory, and comment-period rules. Every row is tagged `verify` or `settled-<date>`.
- `references/coa-templates/` — habitability, CPPA, retaliation, constructive eviction, defective notice / licensing. Authorities checked on CourtListener on 2026-10-07 are tagged as such; everything else says `[verify]`.

Notable from the 2026-10-07 check: *Gomez v. Independence Mgmt. of Del., Inc.*, 967 A.2d 1276 (D.C. 2009), held the CPPA private action did not reach landlord-tenant relations, but D.C. Law 22-206 (2018) added D.C. Code § 28-3905(k)(6) extending it to "trade practices arising from landlord-tenant relations," as applied in *Hettinger v. Bozzuto Mgmt. Co.* (D.D.C. July 21, 2025). See `references/coa-templates/cppa.md`.

## Companion skills

Formatting, citation checking, exhibits, damages, rebuttals, agency complaints, and appellate records are handed off to the user's own skills when installed (`dc-court-filing`, `dc-citation-checker`, `exhibit-management`, `damages-calculator`, `counter-narrative`, `agency-complaint-drafter`, `appellate-record-builder`). Without them, the skill produces the content and says what formatting remains.

## Connectors

CourtListener (citation verification — strongly recommended), Google Drive, Notion. The docket skills read the JSON written by an eAccess scraper such as `claude-mem/browser-automation/dlcp-docket-checker.mjs`; this plugin holds no court credentials.
