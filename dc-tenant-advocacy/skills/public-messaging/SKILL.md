---
name: public-messaging
description: Draft public-facing material — op-eds, press statements, social posts, tenant-organizing flyers, campaign talking points, candidate Q&A answers — in plain language, then run a mandatory litigation-safety check before anything goes public (privileged strategy, statements about named parties without record support, protective-order material, contradictions with court filings, campaign-finance and disclaimer requirements). Use when the user says "write an op-ed", "press statement", "post about", "flyer for the tenant meeting", "talking points", or "campaign message".
argument-hint: "[op-ed | press | social | flyer | talking-points | campaign] [topic]"
---

# /public-messaging

New skill, built on commercial-legal's `stakeholder-summary` plain-language pattern plus the shared guardrails' destination check. Public is the one destination that can never be pulled back.

## Step 1 — Brief

Ask: audience, format and length, the one thing the reader should do or believe afterward, who it's from (individual, tenant association, campaign committee), and whether it mentions any pending case or named party.

## Step 2 — Draft

- Plain language (8th-grade target unless the outlet calls for more), active voice, concrete details, one ask.
- Format norms: op-ed 600–800 words with a news hook in the first paragraph; press statement with headline, dateline, quote, contact; social post within platform limits; flyer with what/when/where/why/how to join.
- Every factual claim gets an inline source note in the draft (stripped from the final copy): `[public record: DOB inspection 2024-03-14]`, `[court filing: Docket No. 31]`, `[user's own experience]`, `[web search — verify]`.

## Step 3 — Litigation-safety check (mandatory, before any final copy)

Produce a table, one row per flagged line:

| # | Line | Risk | Why | Fix |
|---|---|---|---|---|

Check for:

1. **Litigation strategy or work product** — planned motions, weaknesses, settlement positions, what the user intends to prove. Remove.
2. **Statements of fact about a named person or company** (landlord, manager, owner, judge, official) — each must be backed by a public record (court filing, inspection report, agency finding, published article) or framed as the user's own experience or opinion. Unsupported factual accusations create defamation exposure; statements made in court are privileged but repeating them outside court may not be `[model knowledge — verify]`. Flag every one.
3. **Protective-order or discovery material** — anything learned only through discovery. Remove unless the user confirms it's public.
4. **Inconsistency with filings** — anything that contradicts a position in a pending case (check `matters/` chronology and claim charts). The other side will read it.
5. **Statements about a judge in a pending case** — criticism of a judge presiding over the user's case can hurt the case. Flag `[review]` every time.
6. **Campaign material** (if from a candidate or committee): "Paid for by" disclaimer and D.C. Office of Campaign Finance requirements `[verify — OCF rules]`; no use of government resources; coordinated-communication rules if a PAC is involved `[verify]`.
7. **Third-party privacy** — neighbors' names, unit numbers, health details. Remove unless consented.

## Step 4 — Final copy

Clean text with source notes removed, plus the cleared flag table. If any 🔴 flag is uncleared, the skill delivers the draft marked `NOT CLEARED FOR PUBLICATION` and lists what must be resolved.

## Never

- Publishes, posts, emails, or sends to a reporter. The user does.
- Invents quotes. A quote attributed to the user is drafted for the user to approve; quotes from anyone else must come from a source open in this session.
