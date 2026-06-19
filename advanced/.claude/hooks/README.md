# Delegation-provenance hook (ADR-0088 producer 2) — experimental, Claude Code

`swarm run --agent` records a provenance block for the workers **it** launches (ADR-0088 producer 1).
But **in-session subagents** — the ones the main agent spawns through Claude Code's own Agent tool —
never touch the CLI. This hook recipe is producer 2: it appends one trace line per subagent event to
`.swarm/work/delegations.ndjson`, so that delegation is reviewable too. A record, never a verdict
(ADR-0077 Decision 8); it always exits 0, so provenance never blocks the agent.

## Install (opt-in, copy-when-needed)

Copy `delegations.sh` into your repo's `.claude/hooks/` (and `chmod +x` it), then wire it in
`.claude/settings.json`:

```json
{
  "hooks": {
    "SubagentStart": [{ "hooks": [{ "type": "command", "command": ".claude/hooks/delegations.sh SubagentStart" }] }],
    "SubagentStop":  [{ "hooks": [{ "type": "command", "command": ".claude/hooks/delegations.sh SubagentStop" }] }]
  }
}
```

Verify the hook event names and the `settings.json` shape against your Claude Code version's docs — the
lifecycle-hook surface evolves; this is the v0 recipe.

## What it records (the ADR-0088 schema)

Each line aims at the delegation-provenance contract: `worker`, `reason`, `inputs`, `filtered`,
`tools`, `could_edit`, `evidence` (plus `ts`, `event`, and the `raw` payload). The script maps Claude
Code's hook payload onto those fields **best-effort** — adjust the `jq` expression to your version's
actual SubagentStart/Stop field names; the defaults are starting points, not guarantees.

## Status: experimental

Producer 2 is Claude-Code-first (no cross-runner hook format exists — swarm-hq #43) and lives here in
`advanced/` until the delegation-provenance build is measured (CHANGE-delegation-provenance W4). A shell
hook keyed to a stable event name is lower-staleness than agent frontmatter, but still version-specific
— verify before relying on it.
