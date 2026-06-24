---
name: split-work
type: agent-guide
description: >-
  Split a spec or change plan into task packets agents can run without colliding:
  every requirement lands in exactly one task, tasks that write the same files are
  sequenced not parallelized, and the dependency order is written down. Use when the
  work is too big for one run or several agents will work at once. Never invent new
  requirements while splitting, and never cut a task from a requirement with an open
  blocking question. Skip when one task packet covers the whole job — most do.
---

# Splitting work into tasks

Most work is one spec → one implementer — **no task packet**; the implementer fills the spec's
`## Execution` section. Cut tasks only when the work is too big for one agent run, or when several
agents will work in parallel and a collision would be expensive. The output is N task packets (template at
`templates/task.md`), each self-contained, plus a few lines
recording the order they run in.

## Cut along requirements, cover them all

Cut task boundaries along the spec's requirement IDs (or the change plan's waves and guarantee
IDs — a plan splits by wave, see the plan's Task split table). Then check coverage both ways:

- **Nothing uncovered.** Every requirement appears in some task's Scope — or is explicitly
  recorded as deferred. A requirement no task owns is the one that silently doesn't get built.
- **Nothing owned twice.** No requirement appears in two tasks' Scopes. Two agents each
  "owning" AC-003 produce two implementations and one merge fight.

While splitting you will spot gaps — behavior the spec never decided. Don't quietly write the
missing requirement into a task packet: route it back to the spec (or its Open questions). A
requirement that exists only in a task was never reviewed as part of the spec. And a
requirement with an open **blocking** question isn't ready to become a task at all — splitting
it commits a guess.

## Keep each task small, single-concern, and untangled

Coverage decides _what_ goes in a task; size and tangle decide whether it can be reviewed. Small,
single-concern changes are the best-replicated result in code review — review effectiveness is best
on a small change and the proportion of useful review comments drops as a change spreads across more
files. So when you cut:

- **One concern per task.** Prefer more, smaller tasks over one that bundles unrelated requirements.
- **Refactor in its own task, ahead of the behavior change.** A rename, a move, or a signature
  change that other work builds on is its own task and commit — separate from the feature or fix it
  enables. Mixing a refactor with a behavior change is the most common way a diff becomes
  unreviewable; the interface-defining task already goes first (see _Run order_ below), so this falls
  out naturally. A trivial cleanup (a local rename) may ride along.
- **Split out the connective tissue.** When new code wires into existing code, make the high-diffusion
  wiring — the edits touching many existing files — its own task, so the reviewer judges the new logic
  and its integration separately rather than as one tangled blob.

This buys _cleaner_ reviews — fewer false positives at the same defect yield — not more bugs caught;
that is reason enough. It is a convention; nothing sizes a task for you. (Grounding + the optional
oversized-packet heuristic: [Corpus ADR-0094](https://github.com/jcosta33/corpus/blob/main/docs/adrs/0094-decomposition-and-risk-weighted-review.md).)

## Tasks that share files are not independent

The collision that matters is **writes**. Before declaring two tasks parallel, list the files
and directories each will touch (each packet's Affected areas) and compare. Same file in two
lists → they are one sequence, not two parallel tasks: pick an order and record it.

```text
Two tasks may run in parallel only if ALL of these hold:
  1. neither depends on the other — directly or through a chain;
  2. they write no file or directory in common;
  3. neither reads files the other writes;
  4. they don't both touch a shared surface — a public interface,
     a schema or migration, generated code, CI or build config.

When in doubt, run them one after the other. Unknown scope counts
as conflicting with everything.
```

The two defaults in that box do the real work. **Unknown serializes:** a task that can't say
what it writes is assumed to collide with everything — sequence it. **Shared serializes:** a
schema migration or a public interface is a hidden meeting point even when the feature work
looks disjoint. Parallelism is the opt-in, earned by demonstrated disjointness; sequencing is
the default. All of this is a convention checked by hand against the listed paths — splitting
work is judgment work, and no Corpus tooling does it for you.

## Write the dependency order down

A few lines next to the packets (in the change plan's Task split, the spec's folder, or the
board) — plain language:

```markdown
## Run order — SPEC-payment-retry

1. TASK-retry-interface — defines the retry interface (first; others build on it)
2. TASK-retry-core — AC-001..AC-003 (after 1)
3. TASK-retry-metrics — AC-004 (after 1; parallel with 2 —
   no shared files, checked 2026-06-11)
```

Interface-defining work goes first: when one task fixes a contract others call, sequencing it
ahead is cheaper than reconciling three guesses about it afterwards. If you find a cycle —
task A waits on B waits on A — the boundary is wrong; merge them or re-cut.

## Each packet stands alone

The agent running a packet sees the packet, not your splitting reasons. Each one carries its
own source links, Scope ("implement or preserve" the listed IDs), **Do not change** (which for
a parallel task includes the files its siblings own), Affected areas, and a Verify line per
requirement. A packet that needs the other packets explained to it isn't disjoint yet — and
"the other agent will handle it" is not a sentence that belongs inside one.

One context carve-out (platform or repo): a spec shipping the same behavior on N platforms —
or a requirement independently verifiable in each of N repos, the contract-test shape (an API
honored on both sides) — may scope the same requirement id to N context tasks, write-disjoint
by platform directory or repo. At spec level the requirement reads green only when every
context task's packet shows Pass; per-context results never substitute for each other. The
entry condition is strict: a behavior that only exists when both repos meet decomposes into
per-repo requirements instead — the carve-out never covers a requirement no single task
verifies.

## Spec-external mode: snapshot the slice

When a dedicated workspace governs a separate code repo, keep the implementer single-root.
Snapshot the requirement slice each task covers **into** the task packet — stamped with the
spec id and the version/commit it was cut against — and place the task in the code repo's
gitignored `.corpus/`. The implementer then reads the pinned snapshot, not a cross-repo path,
and the spec cannot drift mid-task. Re-cut the task if the canonical spec changes materially.
The external workspace stays canonical; the in-code copy is a marked execution snapshot, not
authoritative. (Grounding: [Corpus ADR-0100](https://github.com/jcosta33/corpus/blob/main/docs/adrs/0100-spec-external-ops-local-mode.md).)

## Before you finish

- [ ] Every requirement (or guarantee/wave item) is in exactly one task's Scope — none
      uncovered, none duplicated (context carve-out — platform or repo: N context tasks may share one id, each
      verifying it whole in its own context).
- [ ] No new requirement was invented inside a packet; gaps went back to the spec.
- [ ] No task was cut from a requirement with an open blocking question.
- [ ] Every parallel pair passed all four conditions in the box — including the file-overlap
      comparison, done against listed paths, not from memory.
- [ ] The run order is written down where the next person will look.
- [ ] Each packet reads as self-contained: source, scope, do-not-change, verify.
- [ ] Spec-external mode: each task carries a pinned spec-slice snapshot and lands in the code
      repo's gitignored `.corpus/`.
