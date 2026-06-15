# Gate templates — wire `swarm check` into your repo

Two ways to run the checks contract automatically. They are templates (not active just by sitting
here) because git hooks must be installed and CI workflows must live under `.github/workflows/`.

| File | Where it runs | Posture |
|---|---|---|
| `pre-commit` | each committer's machine, on `git commit` | **fail-open** convenience — skips if swarm-cli isn't installed, never blocks a teammate |
| `swarm-check.yml` | GitHub Actions, on PR + push to main | **authoritative** — installs swarm-cli and gates the merge |

The split is deliberate: the hook is a fast local nudge that must never get in the way (so it
fail-opens and is easy to `--no-verify`); CI is the line that actually holds, because it controls
its own environment. Exit codes are the same in both: `2` blocks, `1` warns, `0` passes.

## Install the pre-commit hook

```sh
cp hooks/pre-commit .git/hooks/pre-commit && chmod +x .git/hooks/pre-commit
```

It runs `swarm check` on the staged files under `specs/`, `reviews/`, and `tasks/`. It only does
anything if `swarm` is on your PATH — swarm-cli is not yet on npm, so install it from source first
(<https://github.com/jcosta33/swarm-cli>). With no `swarm` on PATH it prints a hint and exits clean.

To override a blocking result for one commit: `git commit --no-verify` (CI will still gate the merge).

**Co-located workspace?** If you copied the kit into a subfolder of a code repo (e.g.
`your-repo/workspace/`), the staged paths are `workspace/specs/…`, not `specs/…` — edit the
`grep -E` prefix in `pre-commit` (and run `swarm check workspace/` in the CI step) to match where
your specs actually live.

## Install the CI workflow

```sh
mkdir -p .github/workflows && cp hooks/swarm-check.yml .github/workflows/swarm-check.yml
```

Then make **swarm check** a required status check in your branch-protection settings so a failing
check blocks the merge. The workflow installs swarm-cli from source on each run; when swarm-cli
ships to npm, swap the install step for `npm i -g <published-name>`.
