---
type: spec
id: SPEC-{{slug}}
title: {{title}}
status: draft
owner: {{team-or-person}}
reviewed: {{YYYY-MM-DD — refresh date for this durable record}}
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
     add "format: sol" to the frontmatter. See `advanced/sol-reference.md` in your workspace
     (full reference: the Corpus repo's docs/reference/structured-requirements.md). -->

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
     spec that was split into tasks. (ADR-0103) -->

- Affected areas: {{paths actually touched}}
- Verify results: {{one line per AC's `Verify with:` command, citing the pasted output}}
- Run summary: {{changed files; out-of-scope edits with reasons; blocked questions}}
- Self-review (ADR-0056): {{what you attacked; what it surfaced + fixed; residual risk for the reviewer}}
