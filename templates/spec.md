---
type: spec
id: SPEC-{{slug}}
title: {{title}}
status: draft
# lifecycle: draft → ready (contract freezes) → active (amended in place over years) → superseded
owner: {{team-or-person}}
reviewed: {{YYYY-MM-DD — refresh date for this durable record}}
# superseded_by: SPEC-…   # set ONLY when a whole feature is replaced — otherwise amend in place (ADR-0108)
# snapshot: <commit-sha>  # OPTIONAL: the code state this text was last written against. Set/refresh it
#                         # on each amendment to enable `corpus check --staleness` (diffs Affected
#                         # areas since this SHA; advisory only, ADR-0108).
sources:
  - {{ticket-id-or-intake-file — or "self" when the work originates with you}}
---

# {{title}}

## Intent

{{1–3 sentences: the behavior change and why.}}

## Non-goals

- {{what this spec deliberately does not change}}

## Requirements

<!-- One "### AC-NNN" per requirement, ordered by importance (agents weight
     earlier instructions more). Each requirement gets a "Verify with:" line —
     it is the highest-value line in this file; prefer a runnable test or
     command. Prefer stricter notation? Any spec can use SOL blocks instead:
     add "format: sol" to the frontmatter. Reference: the Corpus repo's
     `docs/reference/structured-requirements.md`.
     Living spec (ADR-0108): an AC keeps its id for life. Amend its text in place as the feature
     evolves; to retire one, mark it superseded in place — `### AC-001 — name (superseded by AC-007,
     YYYY-MM-DD)` — never delete it. Mint a new spec only when a whole feature is replaced. -->

### AC-001 — {{short name}}

When {{condition}}, {{the component}} must {{observable behavior}}.

Verify with: `{{test-name-or-command}}`

## Open questions

<!-- Frame each unresolved item as a DECISION, not a bare question — a genuine fork the spec
     can't settle on its own, not every micro-choice. For each:
     the decision in one line · 2–4 options with the case FOR/AGAINST · a recommendation +
     a brief why · what it blocks. A real "don't know yet" is a one-option decision whose
     recommendation is "find out how". An unresolved BLOCKING decision keeps the spec out of
     `status: ready`; mark "(non-blocking)" otherwise. Empty is correct when there is no fork —
     do not pad it. (ADR-0101) -->

- {{the decision — options (for/against) — recommendation + why — what it blocks}}

## Affected areas

- `{{path}}`

## Dropped from sources

<!-- Optional but recommended: what the ticket/PRD asked for that this spec
     deliberately leaves out, and why. Design rationale lives here. -->

- {{dropped item — reason}}

## Execution

<!-- Append-only, filled by the IMPLEMENTER as the work is done — for 1:1 work, when the spec was not
     split into tasks. The contract above freezes at `status: ready`; this section grows after it.
     For split work, the per-slice execution lives in each task instead. The independent review packet
     (`reviews/`) stays separate — this is the implementer's run record, not the verdict. Omit it on a
     spec that was split into tasks. (ADR-0103)

     Each change-cycle entry is a STRUCTURED change-record (ADR-0110): scope touched, the AC→evidence
     digest, and the staleness pins — the durable residue of the (ephemeral) review, so the
     requirement→evidence linkage survives the review evaporating (ADR-0104/0107). A prose entry is
     still valid; the structured form is recommended and `corpus stamp` writes the pins. -->

- **{{YYYY-MM-DD — one-line change summary}}** ({{repo}} `{{short-sha}}`).
  - Scope: {{ACs added / amended / superseded + areas actually touched}}
  - Coverage (AC→evidence): {{one line per in-scope AC → the evidence that closed it (test pass / CI
    link / named check); empty evidence reads Unverified, never Pass}}
  - Run summary: {{changed files; out-of-scope edits with reasons; blocked questions}}
  - Self-review (ADR-0056): {{what you attacked; what it surfaced + fixed; residual risk for the reviewer}}
  - reviewed-sha: {{code SHA reviewed}} · evidence-hash: {{ADR-0107 digest — written by `corpus stamp`}}
  - Finding candidates: {{slugs of durable lessons — promote each to findings/<slug>.md (corpus promote)
    or omit. `corpus check` flags a named candidate that never landed (promotion-or-die, ADR-0106).}}
