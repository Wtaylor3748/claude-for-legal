---
name: brief-section-drafter
description: Draft one section of a D.C. Superior Court motion, opposition, or DCCA brief — statement of facts, argument heading, standard of review — built from the matter's chronology and claim chart, with every fact record-cited, every authority tagged by where it came from, and weak arguments flagged instead of dressed up. Use when the user says "draft the argument on [issue]", "write the statement of facts", "draft my opposition to [motion]", or "write the standard of review".
argument-hint: "[<slug>] [section — e.g., 'statement of facts', 'argument II', 'standard of review']"
---

# /brief-section-drafter

Adapted from litigation-legal's `brief-section-drafter`. Formatting (caption, Times New Roman, spacing, signature block, certificate of service) is not done here — hand the finished text to `dc-court-filing` / `dc-litigation-automation`, and run `dc-citation-checker` before filing.

## Load context

1. Profile, `matters/_log.yaml`, `matters/<slug>/history.md`.
2. `chronology.md` (facts) and `claim-charts/` (which elements are supported, and by what).
3. The filing being answered, if any — read it in full before drafting.

## Before drafting, ask

- Written or oral? Oral (hearing argument, DCCA argument) means 3–4 strongest points, lead with the best, drop the weak ones.
- What relief is sought, and what standard governs (e.g., Civ. R. 56 summary judgment; abuse of discretion on appeal)?

## Rules for the draft

1. **Facts come from the record.** Every factual sentence ends with a record cite from the chronology or claim chart (`[Ex. 4 at 2]`, `[Docket No. 31]`, `[Tr. 3/5/2025 at 22:4–9]`). A fact with no record cite gets `[record cite needed]` — it does not go in unsupported.
2. **Authority is tagged by provenance.** `[CourtListener]` only if retrieved and read this session; otherwise `[model knowledge — verify]`. If CourtListener is connected, retrieve each authority, read the passage, and confirm it is a holding that supports the whole proposition. Record each check in `verification-log.md`.
3. **Verbatim quotes are verbatim.** Quotation marks only with the source open. Otherwise paraphrase and flag `[verify exact quote]`.
4. **Pinpoints support the whole sentence.** Split cites when one page supports only part.
5. **Candor about weak arguments.** If authority cuts the other way, say so in a `[review — strategic call]` note: press it (with framing), concede and pivot, or drop it. Never cite a case for a proposition it doesn't hold, and disclose directly adverse controlling DCCA authority the other side hasn't cited `[model knowledge — verify obligation under D.C. R. Prof. Conduct 3.3(a)(2) as applied to pro se parties]`.
6. **Echo, don't repeat.** Reuse the matter's key framings; don't recycle sentences from earlier filings.
7. **No declarations in the user's voice.** For a declaration or affidavit, draft questions to elicit the user's own account and organize their answers — the words must be theirs.

## Output

Reviewer note → the section text → a list of every citation with its provenance tag and a count ("12 citations: 7 CourtListener-verified, 5 to verify") → decision tree (finish the next section / send to `dc-court-filing` / run `dc-citation-checker` / something else).
