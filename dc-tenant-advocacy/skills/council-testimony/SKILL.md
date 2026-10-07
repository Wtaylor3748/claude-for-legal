---
name: council-testimony
description: Prepare testimony for a D.C. Council hearing or roundtable — track the hearing and sign-up/record-close dates, then draft a timed oral version (3 or 5 minutes) and a fuller written statement for the record, built on the bill text and the user's own experience, with every claim sourced. Use when the user says "I want to testify", "draft my testimony on Bill [number]", "Council hearing on [topic]", or after reg-watch logs a hearing notice.
argument-hint: "[--track <hearing> | --draft <bill-or-hearing> [--minutes 3|5]]"
---

# /council-testimony

New skill, built on regulatory-legal's comment-tracking pattern and commercial-legal's plain-language stakeholder-summary pattern.

## `--track`

Record in `comment-tracker.yaml` (type `hearing`): committee, bill/PR number, hearing date and time, witness sign-up deadline and method, written-testimony record-close date, and submission address — all taken from the hearing notice, each with `[Council LIMS]` or `[user provided]` tags. Rules for witness sign-up and time limits vary by committee and hearing; read them from the notice, don't assume `[verify]`. Offer to add the sign-up and record-close dates to `deadlines` under matter `advocacy`.

## `--draft`

1. **Read the bill text** (LIMS) and the committee's hearing notice. Identify the sections that matter to the user.
2. **Interview** (short): What's your position — support, oppose, support with amendments? What happened to you that shows why? What one change or outcome do you want? Are you speaking for yourself or a group?
3. **Oral version** (word budget ≈ 130 words per minute):
   - Name, ward, who you are (1 sentence)
   - Position on the bill (1 sentence)
   - Your story — concrete, dated, specific, in your own words (the user's account, organized; not invented)
   - What the bill does or fails to do about it, citing the section
   - The ask — the specific amendment or vote
   - Thank the chair
4. **Written statement** for the record: the oral version expanded with data, citations (tagged), and proposed amendment language in legislative style ("On page X, line Y, strike '…' and insert '…'").
5. **Q&A prep:** 3–5 questions Councilmembers are likely to ask and short, truthful answers.

## Gates

- **Litigation-safety check** (as in `public-messaging`): testimony is public and transcribed. Pending-case facts should be stated only as they appear in public filings, with no strategy and nothing from protective-order material; statements about named parties must be supported by a public record. Ask before including the user's own case at all — a pending case can be described generally ("I am currently in litigation with my housing provider over conditions") without details.
- **The user delivers and submits.** This skill never sends testimony.
