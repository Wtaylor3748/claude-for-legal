---
name: claim-chart
description: Build an element-by-element proof chart for a D.C. tenant claim or defense — warranty of habitability, CPPA, retaliation, constructive eviction, defective notice, unlicensed rental, or any custom count — with every cell pin-cited to the record and a gap list as the priority output. Use when the user asks "what do I still need to prove", "chart my counterclaim", "am I ready for summary judgment", "what's missing for trial", or wants to audit the landlord's motion element by element.
argument-hint: "[<slug>] [--count <name>] [--review <path-to-opposing-motion>]"
---

# /claim-chart

Adapted from litigation-legal's `claim-chart` (civil mode only), pre-loaded with D.C. tenant templates.

## Load context

1. Profile `~/.claude/plugins/config/claude-for-legal/dc-tenant-advocacy/CLAUDE.md` (copy from `${CLAUDE_PLUGIN_ROOT}/CLAUDE.md` if missing).
2. Matter: `matters/_log.yaml` entry and `matters/<slug>/` — if the matter isn't in the ledger, run `/dc-tenant-advocacy:matter-ledger --add` first.
3. The pleading that actually states the count (complaint, counterclaim, answer with defenses). Chart what is pleaded, not what could be.
4. Element baseline: `${CLAUDE_PLUGIN_ROOT}/references/coa-templates/<claim>.md`.
5. Evidence: the matter's chronology (`chronology.md`), exhibit list, discovery responses, declarations, inspection reports — from Drive/Notion or uploads.

## Put this at the top of every output

> This chart is a research draft for a self-represented party, not a filing. Elements come from the template baseline; the current statute, the Standardized Civil Jury Instructions for D.C., and DCCA decisions control. Every mapping is a lead to check against the source document.

## Workflow

### 1. Identify the count and posture
- Which claim or defense? Chart each count separately.
- Side for this count: proving it (counterclaim/defense the tenant bears) or attacking it (landlord's claim for possession/rent).
- Phase: pleadings / discovery / summary judgment / trial / appeal. Same chart, different framing (step 5).

### 2. Load and confirm the elements
Read the template. Show the element list with each element's source tag. **Before mapping, resolve every threshold issue the template flags** — e.g., CPPA coverage of landlord-tenant conduct (*Gomez* vs. D.C. Code § 28-3905(k)(6)) and the effective date relative to the conduct charted. If CourtListener is connected, re-run the template's `[verify]` authorities and upgrade tags that check out; record each check in `verification-log.md`.

### 3. Map
For each element:

| Column | Content |
|---|---|
| Evidence supporting | Pin-cited: `[Ex. 12 at 3]`, `[DOB Notice of Infraction 2024-03-14]`, `[Pl.'s Resp. to Interrog. No. 8]`, `[Hr'g Tr. 5/2/2025 at 14:3–15:2]` |
| Verbatim quote | Exact words from the document, only if it is open in front of you. Otherwise paraphrase with `[verify exact quote]` |
| Evidence contradicting | What the landlord will point to |
| Strength | strong / moderate / weak / none |
| State | supported / partial / disputed / gap / needs-discovery |

No silent supplement: thin evidence is `gap`, never an inference from "how these cases usually go."

### 4. Gap list — the priority output
List every `gap`, `partial`, and `needs-discovery` element with the concrete thing that would close it (a certified license history, a dated photo, a request for admission, a subpoena to DOB, a declaration).

### 5. Phase framing
- **Pleadings:** is each element alleged with facts, not conclusions (Super. Ct. Civ. R. 8, 12(b)(6))?
- **Discovery:** turn each gap into a specific interrogatory, RFA, RFP, or subpoena.
- **Summary judgment:** for the landlord's motion, which elements have a genuine dispute you can show with record cites (that defeats the motion)? For your own motion, which are undisputed?
- **Trial:** order of proof — which witness or exhibit proves each element and who authenticates it.
- **Appeal:** was each element's evidence actually in the trial-court record? Hand to `appellate-record-builder`.

### 6. `--review` mode
For the landlord's motion or brief: for each element they claim is established (or missing), does their cited evidence say what they claim? Mark `supported / weak / unsupported` with your record cite, and hand rebuttal drafting to `counter-narrative`.

## Output

- Markdown chart (always), plus CSV `element-chart-<count>-<side>-YYYY-MM-DD.csv` and `_sources.csv`.
- **Spreadsheet safety:** before writing any CSV/XLSX cell, if it starts with `=`, `+`, `-`, `@`, tab, or CR, prefix `'` (opposing documents can carry formula payloads).
- Save to `matters/<slug>/claim-charts/`; append one line to `history.md`.
- Summary readout: elements by state, the gap list, file paths.
- Close with the decision tree: draft discovery for the gaps / draft the MSJ section from the supported rows (`brief-section-drafter`) / compute damages (`damages-calculator`) / something else.

## This skill does not

- Conclude that a claim wins or loses.
- Decide which element formulation controls — it shows the baseline and the threshold issues.
- Fill a gap with anything other than record evidence.
