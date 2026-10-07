---
name: deadlines
description: Track every court, agency, and comment-period deadline across all D.C. matters in one ledger with warnings at 14, 7, 3, and 1 days and overdue flags — each deadline tied to its trigger, rule, and verification status. Use when the user asks "what's due", "add a deadline", "when is my opposition due", "mark that filed", or after docket-to-deadlines proposes new entries.
argument-hint: "[--add | --done <id> | --verify <id> | --all]"
---

# /deadlines

Adapted from legal-clinic's `deadlines`, wired to `${CLAUDE_PLUGIN_ROOT}/references/dc-deadline-rules.yaml`.

## Ledger

`~/.claude/plugins/config/claude-for-legal/dc-tenant-advocacy/deadlines.yaml`:

```yaml
- id: DL-0001
  matter: ltb-2023-xxxxxx          # or "advocacy" for comment/testimony deadlines
  what: "Opposition to plaintiff's motion for summary judgment"
  due: 2026-10-21
  trigger: { event: "MSJ served by e-filing", date: 2026-10-07, source: "docket entry 52" }
  rule_id: civ-msj-opposition       # row in dc-deadline-rules.yaml, or "court-order"
  computed_by: rule | order | user
  verified: false                   # true only after the user checks the order/rule text
  status: open                      # open | done | moot
```

## Default view

```
📅 Deadlines — [today]
🔴 Overdue           [id] [matter] [what] — was due [date] ([N] days ago)
🔴 ≤ 3 days          ...
🟠 ≤ 7 days          ...
🟡 ≤ 14 days         ...
⚪ Later             ...
Unverified: [N] — listed with ⚠️
```

## `--add`

1. Ask for the triggering event, its date, and its source (docket entry / order / notice).
2. **If a court order sets the date, use the order's date** (`computed_by: order`) — orders override rules.
3. Otherwise match the trigger to a row in `dc-deadline-rules.yaml`, compute with the Civ. R. 6 counting baseline in that file (exclude trigger day; roll weekend/holiday; +3 days for mail service where applicable), and show the arithmetic.
4. If no row matches, do not guess: `confidence: low`, `needs_verification: true`, and ask the user to read the governing rule or order.
5. Carry the row's `status` (`verify` / `settled-YYYY-MM-DD`) into the entry; anything not `settled` is `verified: false`.

## `--verify <id>`
The user confirms the date against the order or rule text; set `verified: true` and add a line to `verification-log.md`.

## `--done <id>`
Mark done with the filing date and confirmation (e-filing receipt number). Append to the matter's `history.md`.

## Guardrails

- Jurisdictional deadlines (`dcca-notice-of-appeal`, `civ-alter-amend`) are always shown in 🔴 once inside 14 days.
- Never remove an overdue item silently; it stays until marked done or moot with a reason.
- This ledger is a tracker, not a calendar of record — the court's docket and orders are.
