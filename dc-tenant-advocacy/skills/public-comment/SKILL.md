---
name: public-comment
description: Track open comment periods on D.C. and federal housing rules and draft a public comment — position, section-by-section response to the proposed text, supporting facts and authority, and a requested change — ready to submit after the user approves. Use when the user says "draft a comment on [rule]", "should I comment on this", "what comment periods are open", or after reg-watch logs a proposed rule. For complaints against a specific landlord, hand off to agency-complaint-drafter instead.
argument-hint: "[--list | --decide CMT-ID | --draft CMT-ID]"
---

# /public-comment

Adapted from regulatory-legal's `comments`, extended to draft the comment itself (the upstream skill only tracks the decision).

## Tracker

`~/.claude/plugins/config/claude-for-legal/dc-tenant-advocacy/comment-tracker.yaml` — populated by `reg-watch` or `--add`:

```yaml
- id: CMT-001
  agency: "DHCD"
  title: "[rule title]"
  citation: "[D.C. Register vol/page or FR doc number]"
  docket: "[regulations.gov docket ID, if federal]"
  published: 2026-10-01
  deadline: 2026-10-31
  how_to_submit: "[email / regulations.gov / mail — from the notice]"
  decision: undecided    # filing | not-filing
  rationale: ""
```

## `--list`
Open periods sorted by deadline; ⏰ under 14 days; undecided items with deadlines under 30 days counted at the bottom.

## `--decide CMT-ID`
Record filing / not-filing and a one-line rationale. If filing, add an internal deadline 3 days before the real one under matter `advocacy` in `deadlines`.

## `--draft CMT-ID`

1. Read the notice in full (the user pastes it or it's fetched from the source). Comments respond to the actual proposed text — quote section numbers exactly.
2. Ask: who is commenting (individual tenant, tenant association, coalition)? What is the one change you most want?
3. Draft:
   - **Header:** agency, docket/citation, commenter, date.
   - **Summary:** position in two sentences.
   - **Interest:** why the commenter is affected (general — no case-specific facts unless the user chooses to include them; see gate below).
   - **Section-by-section:** for each section addressed — the proposed text (quoted), the problem, the evidence (data, lived experience, authority with provenance tags), and the requested revision as replacement language.
   - **Requested action.**
4. Keep it citable: every factual claim has a source; every legal claim is tagged.

## Gates before anything is submitted

- **Litigation-safety check** (same as `public-messaging`): a public comment is a public, permanent statement. Flag (a) any statement about a named landlord, manager, or company that isn't supported by a public record, (b) any fact from discovery material under a protective order, (c) anything inconsistent with a position taken in a pending case, (d) litigation strategy. The user must clear each flag.
- **Submit gate:** this skill never submits. It produces the final text and the submission instructions from the notice; the user submits.
