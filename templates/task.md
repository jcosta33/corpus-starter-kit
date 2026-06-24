---
type: task
id: TASK-{{slug}}
source:
  - SPEC-{{slug}}
  # - CHANGE-{{slug}}   (when the work executes a change-plan wave)
scope: [AC-001, AC-002]
status: ready
# Implementation handoff (optional — filled at review-ready; the lead or CI may fill):
# branch:        # the implementation branch
# base:          # branch it forks from
# worktree:      # path, if run in an isolated worktree
# pr:            # PR number or URL
# review_packet: # expected review path, e.g. reviews/<slug>.md
---

# Task: {{title}}

## Source

- Spec: `specs/{{feature}}/spec.md` (SPEC-{{slug}})
- {{Change plan: `change-plans/{{slug}}.md` (CHANGE-{{slug}}) — if any}}

## Scope

Implement or preserve:

- AC-001 — {{one line}}
- AC-002 — {{one line}}

## Do not change

<!-- Each entry is a backticked path to protect (`- \`src/auth/\` — rotation logic is frozen`). It is a
     PATH WALL, not prose: any backticked path in this section is protected in FULL. Two traps to avoid —
     (1) a path named only incidentally in a note (e.g. "code goes under `pastebin/`") is still read as a
     protected path and surfaced as a human-attention warning if a change touches it; (2) naming a file
     here to exempt PART of it ("the bootstrap block at the bottom of `src/server.ts`") protects the WHOLE
     file — editing any of `src/server.ts` then warns. Describe layout and partial carve-outs in prose
     elsewhere (the Scope or a note), and keep this section to whole paths that are genuinely frozen. -->

- {{areas explicitly out of bounds}}

## Affected areas

<!-- Multi-repo workspace: an entry may carry a context prefix matching a
     Commands sub-heading (`web: src/checkout/…`); one context per task. -->

- `{{path}}`

## Verify

- [ ] `{{test-or-command}}` (AC-001)
- [ ] `{{test-or-command}}` (AC-002)

## Agent instructions

1. Read the source spec (and change plan, if any) first.
2. Stay inside this task's scope. If a requirement can't be met as written,
   stop and say why instead of improvising.
3. Run every Verify item and paste the real output — a claim without output
   counts as unverified.
4. Before finishing, adversarially self-review your own diff as a skeptic
   (ADR-0056) — try to make each claim fail — and record it in `## Self-review`.
5. Fill `## Run summary` below — changed files, one line per Verify command
   citing its pasted output above, out-of-scope edits, blocked questions —
   and drop anything durable in `## Findings`.

## Findings

<!-- Anything durable discovered during the task — moved to findings/ at Close. -->

## Run summary

<!-- Filled by the implementing agent at the end of the run — the handoff
     digest the review packet reads. Cite the Verify pastes above; never
     re-paste output here. -->

- Changed files: {{paths}}
- Verify results: {{one line per command, citing its Verify item above}}
- Out-of-scope edits: {{none, or each listed with a reason}}
- Blocked questions: {{none, or each stated}}
- Provenance: {{delegated/worker-run tasks only — sources read (AGENTS.md,
  task, spec, change plan), guide(s) loaded, worker identity, isolation mode
  (worktree / shared tree / patch-only); omit for a lead-run or trivial task.
  If the worker authored no task file, the lead fills this on merge-back. }}

## Self-review

<!-- Filled by the implementing agent before handoff — the adversarial self-review
     ADR-0056 makes a mandatory completion discipline. Adopt the skeptic stance over
     your OWN output: re-run the bound proofs from a clean state, hunt the unexercised
     path (edge / error / concurrency), check for scope creep and silent semantic
     drift, treat your own confident prose as a confession — then fix what it surfaces.
     This yields fixes + a recorded critique, never a Pass/Fail verdict; the
     independent review still renders the gate (implementer ≠ reviewer). -->

- Attacked: {{which completion claims you tried to falsify, and how}}
- Surfaced + fixed: {{none, or each issue found and its fix}}
- Residual risk: {{none, or what an independent reviewer should scrutinize}}
