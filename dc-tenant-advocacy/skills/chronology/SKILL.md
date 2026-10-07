---
name: chronology
description: Build or update a dated, de-duplicated, source-cited timeline for a D.C. case from Drive/Notion folders, uploads, docket entries, agency records, and correspondence — each event tagged by significance to the tenant's theory. Use when the user says "build the timeline", "what happened when", "chron for [case]", needs a statement of facts, or needs dates for a retaliation window or habitability period.
argument-hint: "[<slug>] [--format=working|sof|retaliation-windows]"
---

# /chronology

Adapted from litigation-legal's `chronology` (`--matter` mode).

## Load context

1. Profile `~/.claude/plugins/config/claude-for-legal/dc-tenant-advocacy/CLAUDE.md`.
2. `matters/_log.yaml` and `matters/<slug>/` — run `/dc-tenant-advocacy:matter-ledger --add` first if the matter isn't there.
3. Prior `chronology.md` for the matter, if any (this run produces the next version and a diff).
4. Sources, in order: files the user gives this session → the matter's `documents` location (Drive/Notion) → docket entries → agency records (DOB inspections, OTA, RAD, OAH) → email/correspondence the user exports.

## Step 0 — Use restrictions

Ask once: "Did any of these documents come from the landlord through discovery, and is there a protective order?" If yes, note it in the header — documents under a protective order may not be usable in agency complaints, testimony, or public messaging.

## Steps

1. **Extract** one entry per dated event: `date | actor | what happened | source (file + page / docket entry / Bates)`. Undated material goes in a "Needs a date" section — never guess a date.
2. **De-dupe**: the same event in three documents is one entry with three sources.
3. **Tag provenance** on anything not from a document: `[user provided]`, `[web search — verify]`, `[model knowledge — verify]`. Every statement of law (limitations period, retaliation window, deadline) carries a tag.
4. **Tag significance** using the matter's side and theory:
   - 🔴 events that establish an element of the tenant's claim/defense or break an element of the landlord's (notice of a defect, a protected act and the landlord's response within 6 months, a missing license period, an inspection finding)
   - 🟡 supporting context
   - ⚪ background
   Reserve 🔴. When torn, tag lower and add `[review — borderline]`.
5. **Write** `matters/<slug>/chronology.md` with a header (built date, sources read, entries by tag, coverage gaps) and the table.
6. **Diff** against the prior version and show what changed.
7. Ask: "Scan the 🔴 entries — anything miscalled?"

## Formats

- `working` (default) — full table with sources.
- `sof` — statement of facts in narrative paragraphs, every sentence followed by a record cite; ⚪ entries dropped; any `[verify]` entry excluded unless the user approves it. Hand formatting to `dc-court-filing`.
- `retaliation-windows` — every protected act and every landlord action, paired, with the days between them and whether the six-month presumption of D.C. Code § 42-3505.02 applies (rule row `retaliation-presumption-window` in `references/dc-deadline-rules.yaml`).

## Guardrails

- Thin coverage for a period is reported as a gap with options (more sources / web search tagged `[web search — verify]` / stop) — not filled.
- No quotation marks unless the exact words are in the source open in this session.
