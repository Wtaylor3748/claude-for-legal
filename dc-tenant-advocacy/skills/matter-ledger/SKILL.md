---
name: matter-ledger
description: Set up and maintain the case ledger every other skill in this plugin reads — one entry per D.C. case (case number, court, branch, posture, side, judge, next event), with an append-only history per matter and a one-screen briefing on demand. Use when the user says "set up my cases", "add a case", "log this", "what's the status of [case]", "brief me on [case]", or before any other skill when the ledger doesn't exist yet.
argument-hint: "[--init | --add | --update <slug> | --brief <slug> | --status]"
---

# /matter-ledger

Merges litigation-legal's `matter-intake`, `matter-update`, `matter-briefing`, and `portfolio-status` into one skill sized for a self-represented party with a handful of related cases.

## Load context

1. Profile: `~/.claude/plugins/config/claude-for-legal/dc-tenant-advocacy/CLAUDE.md`. If missing, copy `${CLAUDE_PLUGIN_ROOT}/CLAUDE.md` there first and tell the user where it is.
2. Ledger: `~/.claude/plugins/config/claude-for-legal/dc-tenant-advocacy/matters/_log.yaml`.

The ledger and matter files live only on the user's machine (or in their Drive/Notion). Never write case facts into the plugin directory or any git repository.

## Modes

### `--init` (first run)

Ask for each case, one at a time (accept a pasted list):

- Case number (e.g., `2023-LTB-XXXXXX`, `2024-CAB-XXXXXX`, DCCA `24-CV-XXXX`)
- Court / branch: LTB, CAB, DCCA, OAH, RHC, other
- Caption (short form) and the user's side: defendant / plaintiff / counter-plaintiff / appellant / appellee / petitioner
- Posture: pleadings, discovery, dispositive motions, trial set, judgment, on appeal, stayed, closed
- Assigned judge (if known)
- Next known event and date
- Related cases (slugs)
- Where the documents live (Drive folder / Notion page)

Write `_log.yaml`:

```yaml
matters:
  - slug: ltb-2023-xxxxxx
    case_number: "2023-LTB-XXXXXX"
    court: super-ct-ltb
    caption: "Landlord v. Tenant"
    side: defendant
    posture: discovery
    judge: "[name]"
    next_event: { what: "status hearing", date: 2026-11-04, source: "docket entry 47" }
    related: [cab-2024-xxxxxx]
    documents: "Drive: Capitol Vista/2023-LTB"
    risk: high          # low | medium | high | critical
    last_checked_docket: null
    status: active
```

Create `matters/<slug>/history.md` with a dated opening entry for each.

### `--add`
Same questions for one new matter; append.

### `--update <slug>`
Append a dated entry to `history.md` (`YYYY-MM-DD — [event] — [source]`). Update `posture`, `next_event`, `risk` in `_log.yaml` if they changed. History is append-only: corrections are new entries, never edits.

### `--brief <slug>`
One-screen briefing read from `_log.yaml`, `history.md`, `chronology.md`, and any `claim-charts/` for the matter:

- Posture and next event (with source)
- Claims and defenses in play, with the gap count from the latest claim chart
- The 3–5 🔴 chronology events
- Open deadlines (from `deadlines`)
- Related matters and how they interact (e.g., a ruling in the CAB case that affects LTB)
- What I'd do next — decision tree

### `--status`
Table of all active matters: case number, court, posture, next event + days out, risk, last docket check. Flag any matter whose `last_checked_docket` is older than 7 days, or whose `next_event` is within 14 days.

## Guardrails

- Every `next_event` carries a `source` (docket entry, order, notice). No source → `[verify]`.
- Do not infer posture from memory of earlier conversations; ask or read the docket.
- Severity uses 🔴 critical / 🟠 high / 🟡 medium / 🟢 low and never silently drops between runs.
