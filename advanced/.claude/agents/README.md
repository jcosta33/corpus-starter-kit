# Experimental: Claude Code agents (the swarm-agents probe)

Runner-specific worker definitions for Claude Code, incubating here per swarm-hq #43 —
copy-when-needed, not active in the kit itself. Claude Code discovers agents from a project's
`.claude/agents/` directory; copy a file from here into your repo's `.claude/agents/` to use it.

## `swarm-reviewer`

An independent reviewer for a finished Swarm task. Shipping it as a Claude Code *agent* (rather than
only a skill) lets the `tools:` allowlist — `Read, Grep, Glob, Bash`, with no Edit/Write — **narrow the
edit surface** the reviewer reaches for. It is *not* full enforcement: `Bash` is granted (the reviewer
re-runs the task's Verify checks) and a shell can still write, so "does not edit source" remains a
convention the body carries (ADR-0063 — "enforced" is reserved for a tool that actually enforces).
Real enforcement would need a `PreToolUse` hook that blocks write-ish Bash — a future step. The probe
re-runs the Verify checks itself, drafts the kit's `templates/review.md` packet, and never issues a
verdict (the human owns Pass/Fail; ADR-0077). It is the runner projection of the catalog's
`persona-skeptic` + `review-output` discipline.

## Status: experimental

Claude-Code-first by design — no cross-runner agent-definition format exists (swarm-hq #43). No model
id is pinned (it inherits the session model) so the definition does not rot per release. Measure it
before relying on it: does the read-only scoping measurably change reviewer behavior versus the
prose-only baseline? Until that is shown across more than one role, this stays a probe in `advanced/`,
not a founded `swarm-agents` repo.
