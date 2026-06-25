---
type: review
id: REVIEW-{{slug}}
task: TASK-{{slug}}
# spec: SPEC-…   # use INSTEAD of task: for a 1:1 review with no task — coverage then reconciles against
#                # the whole spec's ACs (ADR-0103 review-to-spec). task: takes precedence when both are set.
pr: { { pr-url — or "none yet" for a pre-PR or trunk-based review } }
reviewer: { { the review lead — never the implementer (the spec/task author may, if they didn't implement) } }
status: { { draft | pass | waived | blocked | needs-human } }
---

# Review: {{title}}

## Summary

{{2–3 sentences: what changed, what is verified, what is not.}}

## Review plan

<!-- ADR-0099 — for an orchestrated (lead) review. The lead reads the task, cited
     spec, run summary, and diff, then runs at least three independent lens
     reviewers (default: requirement correctness · verification/evidence/repro ·
     maintainability/design risk; add security, migration, performance, a11y, etc.
     as the change warrants). Each lens returns findings + evidence only; the lead
     reconciles and writes this packet. A lens reviewer never sets the status or the
     suggested decision. Omit this section for a single-reviewer review. -->

- Lenses: {{e.g. correctness · evidence/repro · maintainability — who ran each}}
- Reconciliation: {{how the lead resolved conflicts/duplicates across lenses}}

## Changed files

- `{{path}}`

## Requirement coverage

| ID     | Result     | Evidence                        | Human attention |
| ------ | ---------- | ------------------------------- | --------------- |
| AC-001 | Pass       | `{{test}}` output pasted/linked | no              |
| AC-002 | Unverified | no test output found            | yes             |

<!-- Results: Pass · Fail · Unverified · Blocked.
     A Pass needs pasted output, a CI link, or, for a manual Verify method, a
     named human's recorded observation (who judged, what they saw). An empty
     Evidence cell means Unverified, never Pass. Suite/typecheck output stays
     under the task's Verify items — the Run summary section digests it; a failed or
     missing suite routes below via the missing-test-output trigger. -->

<!-- Optional — structured evidence (ADR-0083; checked by C013): a coverage row may carry,
     directly beneath the table, a fenced code block whose info-string is
     `verify id=AC-NNN cmd="<the requirement's named Verify-with command>" result=pass|fail`.
     That info-string is the machine-checkable form `corpus check` / `corpus review` reconciles
     against the spec's named command; the block's body is the verbatim paste — for you and the
     spot-check — and is never parsed for a review result. Opt-in: a row may use only the free-form
     Evidence cell and stays a human-attention warning. The check surfaces a consistency fact
     (the recorded evidence names the requirement's own command and a pass), never a review result. -->

Spot-checked: {{which green row's evidence you re-ran yourself}}

## Change-plan coverage

<!-- Only when the task executes a change plan: one row per preservation
     guarantee / wave item, same columns as above. Delete otherwise. -->

| ID                            | Result     | Evidence     | Human attention |
| ----------------------------- | ---------- | ------------ | --------------- |
| {{SPEC-x#AC-001 (preserved)}} | {{result}} | {{evidence}} | {{yes/no}}      |

## Human attention

<!-- Route the exceptions, not the diff: unverified or failed requirements ·
     out-of-scope changes · risky files · missing test output · changed public
     interfaces · DB migrations · security-sensitive changes · new finding
     candidates · blocked questions · missing or unconvincing worker-boot
     provenance for a delegated task (no sources/guide evidence, a guide that
     silently failed to load, or a worker that left no task artifact at all) —
     investigate, don't rubber-stamp. A waived row records: who waived · which
     rows · why · expiry — the packet status becomes `waived` at merge
     (expiry semantics: the advanced lifecycle, in the Corpus repo). -->

1. {{exception — why it matters — suggested action}}

## Open decisions

<!-- Optional (ADR-0089) — include ONLY when this work closes with a decision the
     human must make. Delete the section entirely when nothing is open; it is not
     boilerplate. Frame the fork, don't bury it in bullets: the developer is
     orchestrating several agents and is context-poor right now, while you still
     hold this work's context. For each open decision:
       - the decision (one line)
       - 2–4 comparable options, each with its tradeoff — the case FOR and AGAINST
       - a recommendation + a brief why (skippable — you present, the human decides)
       - the context / impact the human may not be holding
       - what it blocks (what is gated on this decision)
     Keep the "why" short and verification-oriented (how sure · what would change it ·
     what it blocks), not a persuasion essay. Route the decision; don't rule on it. -->

1. {{the decision — options (for/against) — recommendation + why — context/impact — what it blocks}}

## Task status

<!-- At closeout, confirm the task's board row AND the task packet's own
     `status:` frontmatter are updated together — review-ready → closed (or
     blocked). A worker that boots from a stale packet inherits stale state.
     "Committed, runtime/human validation pending" = this packet `needs-human`
     + the task `review-ready`; don't invent new states. -->

{{board row + packet status updated to … }}

## Suggested decision

{{Merge / Merge with waiver (who · why · expiry) / Block until …}}
